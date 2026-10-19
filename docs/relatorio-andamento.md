# O que foi feito até agora: escolha e análise exploratória de bases forenses

**Data:** 2026-10-15
**Fontes deste texto:** os notebooks `01_eda_loghub.ipynb`, `02_eda_comofod.ipynb` e `03_eda_cic_iot2023_ddos_http_flood.ipynb`, os tickets em `docs/issues/` e o log `docs/decisions.md`. Todo número abaixo aparece na saída de um notebook ou no resultado de um ticket. Quando algo é hipótese, o texto diz.

Este documento conta o trabalho em ordem e explica o raciocínio de cada passo. Os notebooks trazem os detalhes técnicos; aqui o foco é entender **o que foi perguntado, o que foi medido e o que isso significa**.

---

## 1. A pergunta do projeto

Existem dezenas de bases de dados públicas para forense digital. A pergunta é prática: **dá para construir modelos de IA úteis sobre elas?** E, para uma base grande demais para a memória desta máquina, **qual é a melhor forma de trabalhar com ela?**

O projeto parte de um levantamento já feito no repositório: uma planilha com 37 bases (`spreadsheet/Datasets Forenses.xlsx`), uma revisão de literatura de 89 trabalhos e uma síntese por nicho (`bases-dados-forense-digital-sintese.md`). A partir disso, os entregáveis são três:

1. A descrição padronizada (**datasheet**) das 4 bases escolhidas.
2. A **análise exploratória** (EDA) das 3 bases de porte "ok".
3. O **roteiro** de como trabalhar a base grande (Parquet, pandas x DuckDB x Polars x Spark local, comparação de nuvens).

Até agora o trabalho cobriu boa parte do item 2 e o primeiro contato com a base grande. Os itens 1 e 3 ainda não começaram (seção 11).

---

## 2. Conceitos que aparecem no texto

Alguns termos se repetem em todas as bases. Vale fixá-los antes.

**Viabilidade de IA.** Não é "o modelo acertou muito". É o julgamento de se a base sustenta um modelo útil, olhando cinco coisas: se os rótulos existem e são confiáveis, se as classes estão balanceadas, se há duplicatas, se há risco de vazamento e quanto um modelo simples consegue com uma avaliação honesta.

**Baseline.** Um modelo propositalmente simples (aqui, random forest e regressão logística do scikit-learn, sem ajuste fino) que serve só como régua. Se até ele vai bem, a base tem sinal. Se ele fica no acaso, ou a tarefa é difícil, ou as características escolhidas não capturam o fenômeno.

**Divisão treino/teste.** O modelo aprende numa parte dos dados (treino) e é avaliado em outra que ele nunca viu (teste). A nota do teste estima como o modelo se sairia com dados novos.

**Vazamento.** Acontece quando o teste não é de fato "novo": a mesma informação aparece dos dois lados. É como um aluno que recebe na prova as mesmas questões da lista de exercícios. Ele tira nota alta, mas a nota mede memória, não aprendizado. **Este é o achado central do estudo** (seção 9): nas três bases analisadas, a forma de dividir os dados mudou o veredito.

**Unidade independente.** Para evitar vazamento, a divisão tem que separar unidades que realmente não compartilham informação. Às vezes é a linha; muitas vezes não. No CoMoFoD a unidade certa é a fotografia; no HDFS, o padrão de eventos; na CIC-IoT2023, o segmento ou o arquivo.

**Métricas usadas:**

| Métrica | O que mede | Como ler |
|---|---|---|
| **AUC** (área sob a curva ROC) | A chance de o modelo dar nota maior a um exemplo positivo do que a um negativo | 0,5 = acaso (cara ou coroa); 1,0 = perfeito |
| **Precisão** | Dos que o modelo marcou como positivos, quantos eram de fato | Alta = poucos alarmes falsos |
| **Recall** (revocação) | Dos positivos reais, quantos o modelo encontrou | Alto = poucos casos perdidos |
| **F1** | Média harmônica de precisão e recall | Só fica alto se as duas forem altas |
| **PR-AUC** | Área sob a curva precisão x recall | Mais exigente que a AUC quando a classe positiva é rara |

**Autocorrelação de lag 1.** Mede o quanto cada linha se parece com a seguinte. Perto de 0 = linhas embaralhadas; perto de 1 = linhas em sequência, quase iguais às vizinhas.

---

## 3. As bases escolhidas e por quê

A regra foi ter **nichos diferentes**: uma base grande e três de porte "ok", cada uma de um nicho, e nenhuma das menores no mesmo nicho da grande (Rede/IoT).

| Papel | Base | Nicho | Por que ela |
|---|---|---|---|
| Base grande | **CIC-IoT2023** | IoT/Rede | 46,7 M de registros (declarado na planilha); a mais citada por ano no levantamento (327 citações/ano) |
| Porte "ok" | **CIC-MalMem-2022** | Memória | Dumps de memória com malware; 58.596 registros documentados, 50/50 |
| Porte "ok" | **Loghub** (HDFS_v1 e BGL) | Logs de sistema | Referência clássica em detecção de anomalias em logs; licença aberta |
| Porte "ok" | **CoMoFoD Small** | Imagem | Falsificação por copiar-e-colar (copy-move), com máscaras e variantes degradadas |

O trio de porte "ok" foi escolhido pelo usuário (decisão 7). Foram combinadas bases reserva: Dumpware10 (memória), DEFACTO ou CASIA v2 (imagem) e outro sistema do Loghub (logs).

---

## 4. Como o trabalho foi organizado

Cada etapa vira um **ticket** em `docs/issues/`, com critérios de aceite verificáveis (o que precisa estar medido e impresso para a etapa contar como feita). A análise fica nos **notebooks** em `notebooks/`, que rodam do zero sem erro. As decisões e os achados importantes entram, em ordem, no log `docs/decisions.md`, que nunca é reescrito: correções são entradas novas.

Uma correção de processo ocorreu no caminho: os notebooks 01 e 02 começaram sem tickets. O erro foi apontado, e os tickets foram escritos (alguns retroativos, marcados como tal). Desde então, ticket antes de notebook (o ticket 10 já seguiu essa ordem).

| Ticket | Assunto | Estado |
|---|---|---|
| 01 | Ambiente (uv, bibliotecas, Spark via Docker) | Parcial: falta o Spark |
| 02 | Download das bases de porte "ok" | Parcial: falta o arquivo principal do MalMem |
| 03 | Download da CIC-IoT2023 | Parcial: bloqueado por decisão do usuário |
| 05 | EDA do Loghub | Concluído |
| 06-01 a 06-06 | EDA do CoMoFoD (inventário, máscaras, PSNR, baseline, fotografias, veredito) | Concluídos |
| 10 | EDA de um arquivo da CIC-IoT2023 | Concluído |
| 07-01 | Datasheet do CoMoFoD | Concluído (`docs/datasheets/comofod.md`) |
| 04, 07-02 a 07-04, 08, 09 | EDA do MalMem, datasheets das outras bases, roteiro da base grande | Ainda não escritos |

---

## 5. Preparação: ambiente e downloads (tickets 01, 02 e 03)

### Ambiente

Projeto Python gerenciado com `uv`, com Python 3.13.15, pandas 3.0.6, DuckDB 1.5.6, Polars 2.0.0, scikit-learn 1.9.1, além de pyarrow, matplotlib, seaborn, pillow e Jupyter. A máquina tem 16 GB de RAM (cerca de 4 GB livres), 12 núcleos e uma RTX 4050 de 6 GB. O Spark local via Docker ainda não foi montado.

Os dados ficam fora do git: os arquivos baixados, intactos, em `data/raw/<base>/`, e os extraídos em `data/interim/`.

### Downloads e integridade

Baixar não basta: é preciso conferir que o arquivo chegou inteiro. Para isso se compara o **hash** (uma "impressão digital" do arquivo) com o valor publicado pela fonte.

| Base | Arquivo | Tamanho medido | Conferência |
|---|---|---|---|
| Loghub HDFS_v1 | `HDFS_v1.zip` | 186.645.559 B | MD5 igual ao do Zenodo; `unzip -t` sem erro |
| Loghub BGL | `BGL.zip` | 57.489.019 B | MD5 igual ao do Zenodo; `unzip -t` sem erro |
| CoMoFoD Small | `comofod_small.rar` | 3.213.318.957 B (~3,0 GiB) | Tamanho igual ao do servidor; SHA256 registrado |
| CIC-IoT2023 | 4 CSVs por ataque + `README_CSV.pdf` | 6 a 9 MB cada | Recebidos do usuário (formulário) |
| CIC-MalMem-2022 | 3 CSVs | 850 linhas no total | **Incompleto** (seção 8) |

As bases do CIC exigem um formulário de cadastro com dados pessoais. Por regra do projeto, o agente não preenche esse formulário: o usuário baixa e coloca os arquivos em `data/raw/`.

---

## 6. Loghub: logs de sistema (notebook 01, ticket 05)

### O que é

O Loghub reúne logs reais de sistemas. Foram usadas duas partes, com rótulos de natureza diferente:

- **HDFS_v1**: logs do sistema de arquivos distribuído do Hadoop, 11.175.629 linhas (1,58 GB descompactado). O rótulo (normal ou anomalia) vale para um **trace**, isto é, todas as linhas de um mesmo bloco de dados (`BlockId`).
- **BGL**: logs do supercomputador BlueGene/L, 4.747.963 linhas (0,74 GB). O rótulo vale para **cada linha**: ou é um alerta de uma categoria, ou não é alerta.

O notebook usa o DuckDB para ler os logs brutos sem carregá-los inteiros na memória. Roda do zero em cerca de 1,5 minuto.

### HDFS_v1: o que foi medido

**Rótulos e balanceamento.** São 575.061 traces, e 2,93% são anomalias: 33,2 traces normais para cada anômalo. O rótulo do arquivo `anomaly_label.csv` e o da matriz de eventos coincidem em 100% dos traces, então o rótulo é consistente entre as fontes.

**Redundância extrema.** Cada trace é descrito por quantas vezes cada um dos 29 tipos de evento (E1 a E29) aparece nele. Ao contar quantos desses vetores são diferentes, só sobram **589 vetores distintos** (0,10% dos traces). Um único vetor cobre **52,2%** de todos os traces. Ou seja, a base parece ter meio milhão de exemplos, mas a maior parte é repetição. Nove vetores aparecem com rótulos conflitantes (o mesmo vetor ora normal, ora anômalo) e cobrem 550 traces.

**Baseline em dois cenários.** Aqui está a lição do HDFS:

- **(a) Divisão aleatória:** F1 0,979 (regressão logística) e 0,999 (random forest). Parece excelente, mas **100% dos vetores do teste já estavam no treino**. O modelo só precisa reconhecer o que já viu.
- **(b) Padrões novos:** os vetores frequentes ficam no treino e os raros são divididos de modo que nenhum vetor do teste apareça no treino. Média de 5 sorteios: F1 0,952 (regressão logística) e **0,968** (random forest).

O resultado (b) ainda é bom, então o HDFS **tem sinal**. Mas o 0,999 do cenário (a) não mede generalização. Ressalva: o teste do cenário (b) tem só 2.263 a 2.704 traces, com cerca de metade de anomalias, e não reproduz a proporção real das classes.

**Risco de circularidade (hipótese, não testada).** Segundo o README, o rótulo do HDFS foi produzido por regras manuais, e 12 dos 29 eventos só aparecem em traces anômalos. Parte do desempenho pode ser o modelo reaprendendo as regras que geraram o rótulo, e não detectando falhas de verdade.

### BGL: o que foi medido

**Rótulos.** São 348.460 alertas (7,34% das linhas), em 41 categorias, de 2005-06-03 a 2006-01-04. Os totais batem com a documentação. O parse tem 34.786 linhas irregulares (0,73%).

**Atalhos fáceis.** Todos os alertas estão em linhas de nível FATAL. A regra "nível = FATAL" acha 99,98% dos alertas (recall), mas só 40,76% das linhas FATAL são alertas (precisão). Dentro do próprio conjunto, o texto da mensagem quase determina o rótulo.

**Mas o passado não prevê o futuro.** O teste mais revelador: guardar os "moldes" de mensagem (templates, com números trocados por `<N>`) que foram alerta nos primeiros 70% do log e ver quantos alertas dos 30% finais eles reconhecem. Resultado: **55,9%** (48.060 de 86.033), com 1 falso alarme. Ou seja, **44% dos alertas futuros vêm de templates que nunca tinham aparecido**. O sistema muda com o tempo.

**Baseline por janela.** O log foi cortado em janelas de 100 linhas consecutivas; cada janela é descrita pela contagem dos 300 templates mais frequentes no período de treino, e o alvo é "a janela contém algum alerta". A divisão é **cronológica** (70% iniciais para treino, 30% finais para teste), que é como um sistema real seria usado. Resultado: random forest com **F1 0,72** (precisão 0,94, recall 0,58, PR-AUC 0,67); regressão logística com F1 0,66.

### Veredito do Loghub

- **BGL com divisão cronológica é o melhor ponto de partida**: tem mudança ao longo do tempo e o baseline está longe do teto, então há espaço real para métodos melhores.
- **HDFS serve para comparar métodos**, desde que a avaliação seja em padrões não vistos.
- Nas duas, o rótulo vem de regras ou de categorias da própria fonte. Os resultados dizem quão bem um modelo reproduz esse rótulo, não necessariamente quão bem detecta incidentes reais.

---

## 7. CoMoFoD: imagens com copiar-e-colar (notebook 02, tickets 06-01 a 06-06)

### O que é

O CoMoFoD (Universidade de Zagreb) traz imagens em que um pedaço da própria imagem foi copiado e colado em outro lugar, às vezes girado, redimensionado ou distorcido. A versão Small tem imagens de 512x512 organizadas em 200 **cenas**. Cada cena tem 52 arquivos:

- 4 imagens-base: `O` (original), `F` (falsificada), `B` (máscara binária) e `M` (máscara colorida);
- para `O` e para `F`, 24 variantes degradadas: 3 níveis de cada um de 5 pós-processamentos (brilho, contraste, redução de cor, desfoque, ruído) e 9 níveis de compressão JPEG.

O notebook só **lê** as imagens, por causa do acordo de uso (seção 10). Roda do zero em 2 min 33 s.

### 06-01: inventário e integridade

Antes de analisar, conferir se a base está inteira. Resultado: 10.400 arquivos de imagem, 200 cenas, 0 nomes fora do padrão, 3,21 GB. **Todas as cenas têm exatamente os 52 arquivos esperados** (um `assert` no notebook falha se isso mudar). Pelo `readme.txt`, as cenas se dividem em combinação (41), translação (40), rotação (40), escala (40) e distorção (39). A região copiada vai de 360 a 37.542 pixels (mediana 3.369), de um total de 262.144.

### 06-02: o que as máscaras marcam

Uma base para localizar falsificações depende de máscaras corretas, e o significado delas não está documentado.

- As imagens têm todas 512x512, mas o **modo de cor é misto** (parte RGB, parte RGBA), então o notebook converte tudo antes de comparar.
- A máscara `B` marca regiões pequenas: mediana de **2,6%** da imagem (de 0,3% a 29%). Para um futuro modelo de localização, isso significa forte desbalanceamento de pixels. A área de `B` acompanha a área declarada no `readme.txt` (correlação em log de 0,976).
- Comparando os pixels em que `O` e `F` diferem com a máscara: nas 163 cenas com diferença localizada, `B` cobre 100% dessa diferença (mediana), com IoU mediano de 0,50. A leitura compatível com os números é que **`B` marca a região de origem e a região colada**, enquanto a diferença `O≠F` só "vê" a colada. Isso não está documentado pelos autores.
- **Achado inesperado:** em **35 cenas** (18 de rotação e 17 de escala; nenhuma das outras categorias), `O` e `F` diferem em mais de 50% dos pixels, não só na região copiada. A causa não está documentada. Para um detector, é um possível atalho: aprender o processamento global em vez da adulteração.

### 06-03: pós-processamentos e PSNR

O PSNR mede o quanto uma imagem degradada se afasta da original (mais dB = menos degradação). O arquivo `psnr.txt` tem 600 linhas e cobre **só o ruído sobre as originais**: 6,25% das 9.600 variantes pós-processadas. Brilho, contraste, redução de cor, desfoque, JPEG e todas as variantes de `F` ficam sem PSNR. Medianas do ruído: 20,7 dB, 23,1 dB e 33,0 dB nos níveis 1, 2 e 3.

### 06-04 e 06-06: o baseline e as fotografias reaproveitadas

Esta é a parte mais instrutiva do estudo.

**O plano.** Classificar cada imagem como original ou falsificada usando 12 características globais simples (médias e desvios por canal de cor, nitidez, energia de bordas, proporção de altas frequências). Como cada cena gera 50 imagens parecidas, o plano já previa **dividir por cena**: nenhuma cena nos dois lados.

**O sinal de alerta.** Com divisão por cena, o random forest chegou a AUC perto de 0,97, enquanto a regressão logística e cada característica isolada ficavam em 0,5. Um modelo que vai bem quando nenhuma peça sozinha tem sinal é suspeito. Além disso, o `readme.txt` repetia as mesmas áreas de região copiada em categorias diferentes.

**A investigação (ticket emergente 06-06).** As 200 imagens originais foram reduzidas a miniaturas 32x32 em tons de cinza e comparadas por correlação. Resultado: **as 200 cenas vêm de apenas 41 fotografias distintas**, igual em três limiares (0,90, 0,95 e 0,98). Uma fotografia aparece em até 13 cenas (mediana 4); 37 das 41 são usadas em mais de uma cena, e 8 aparecem nas 5 categorias de manipulação.

**O baseline refeito, em três divisões** (média de 5 sorteios):

| Divisão | Random forest (AUC) | Regressão logística (AUC) |
|---|---|---|
| Por imagem (variantes da mesma cena misturadas) | 0,984 | 0,502 |
| Por cena | 0,967 | 0,521 |
| **Por fotografia** | **0,495** | 0,510 |

Quando a mesma fotografia aparece no treino e no teste, o random forest aprende "a cara" de cada foto e a pequena diferença entre `O` e `F` dentro dela. Quando a divisão é por fotografia, ele cai no acaso. Esse mecanismo é a explicação compatível com os números, mas não foi testado diretamente. Com só as 400 imagens-base, por fotografia, a AUC também é 0,50.

Limitação: o agrupamento por miniaturas é simples e não foi validado por inspeção manual dos grupos.

### 06-05: veredito do CoMoFoD

- **Classificar original x falsificada com características globais não é viável**: com a divisão correta, o resultado é acaso.
- **Treinar um modelo do zero também não**: 41 fotografias é pouco.
- **Uso realista (hipótese):** benchmark de robustez, aproveitando as variantes degradadas, e teste de transferência de um detector treinado em outra base.
- **Não avaliado:** localização em nível de pixel, detectores copy-move clássicos e redes convolucionais.

---

## 8. CIC-IoT2023 e CIC-MalMem-2022

### CIC-IoT2023: um pedaço da base grande (notebook 03, ticket 10)

**O que chegou.** Quatro CSVs por ataque (`DoS-HTTP_Flood`, `DoS-HTTP_Flood1`, `DDoS-HTTP_Flood-` e `DictionaryBruteForce`), com 13 mil a 41 mil linhas cada. Duas surpresas, registradas em `docs/cic-iot2023-arquivos-csv.md`:

- os arquivos têm **39 colunas**, e a página oficial lista 46 features (com nomes diferentes em parte);
- **não há coluna de rótulo**: a classe só aparece no nome do arquivo. O `README_CSV.pdf` descreve um conjunto "combinado e embaralhado" com `label`, provavelmente a pasta `MERGED_CSV`, que ainda não foi baixada.

**O que foi analisado.** Só o arquivo `DDoS-HTTP_Flood-.pcap.csv`: 28.790 linhas, 39 colunas, 6,45 MB. Sem rótulo e com uma única classe, não há baseline possível. O objetivo foi entender o esquema, a qualidade, as armadilhas e o custo por registro. Roda em cerca de 5 segundos.

**Qualidade.** 0 nulos, 0 duplicadas, 0 infinitos. Três colunas constantes (`Telnet`, `SMTP`, `IRC`).

**Coerência interna.** Várias relações entre colunas, lidas nas primeiras linhas, foram testadas em vez de assumidas. Valem em 100% das linhas: `Variance = Std²`, `Tot size = AVG`, `Tot sum = AVG × Number`, `IPv = LLC`, `ARP = 1 − IPv` e as frações de flags iguais à contagem dividida por `Number`. Já `Rate = 1/IAT` vale só aproximadamente (dentro de 1% em 87,2% das linhas). Na prática: pelo menos 5 das 39 colunas podem sair sem perder informação (as 3 constantes e 2 cópias exatas), e há 11 pares de colunas com correlação acima de 0,95.

**Ordem e segmentos.** As linhas **não estão embaralhadas**: a autocorrelação de lag 1 chega a 0,967 (`HTTP`), e 33 de 36 colunas ficam acima do ruído. Um controle com as linhas embaralhadas dá no máximo 0,011. Além disso, a coluna `Number` vale 100 em 99,79% das linhas, e as 61 exceções ficam espalhadas pelo arquivo. A hipótese testada: cada exceção fecha um **segmento** de captura. Resultado: 61 segmentos de 68 a 1.146 linhas (mediana 297), internamente homogêneos. O segmento explica 89% da variância de `HTTP`, contra 0,2% com segmentos sorteados ao acaso.

**Heterogeneidade.** 78,7% das linhas são tráfego TCP com HTTP dominante. Mas 4.634 linhas (16,1%) quase não têm HTTP, e 92% delas estão em **6 segmentos inteiros**. Sem rótulo, não dá para saber se são outra fase do ataque ou outro tráfego.

**Escala.** Medido: 224 bytes por registro no CSV e 312 bytes na memória do pandas (`float64`). **Extrapolando** para 46,7 M de registros (supondo a mesma largura de linha, não verificado): ~10,5 GB em CSV, ~14,6 GB em `float64` e ~7,3 GB em `float32`. Numa máquina de 16 GB com cerca de 4 GB livres, a base inteira não cabe na memória, e isso justifica o roteiro com Parquet e ferramentas fora de memória.

**Consequências para depois.** Nunca dividir por linha (linhas vizinhas são quase iguais); dividir por segmento ou por arquivo. Remover colunas constantes e cópias. Usar `float32` ou leitura fora de memória.

### CIC-MalMem-2022: bloqueada

Os três arquivos recebidos (`Output1.csv`, `output2.csv`, `output3.csv`) somam 850 linhas, todas da família `Spyware-TIBS`, com 56 colunas, sem benignos e sem coluna de rótulo. A base documentada tem 58.596 linhas balanceadas. Sem o arquivo principal, a EDA não pode começar (ticket 04, ainda não escrito). A pasta se chama `cic-malmen-2022`, com erro de digitação; renomear ou não é decisão do usuário.

---

## 9. A lição que atravessa as bases

Nas três bases analisadas, **a forma de dividir os dados decidiu o resultado**:

| Base | Divisão ingênua | Divisão correta | Unidade independente |
|---|---|---|---|
| CoMoFoD | AUC 0,984 (por imagem) | AUC 0,495 (por fotografia) | Fotografia |
| HDFS_v1 | F1 0,999 (aleatória) | F1 0,968 (padrões novos) | Vetor de eventos |
| BGL | Templates quase determinam o rótulo | F1 0,72 (cronológica) | Tempo |
| CIC-IoT2023 | (sem rótulo ainda) | Linhas vizinhas com autocorrelação 0,967 | Segmento ou arquivo |

O tamanho declarado de uma base engana: 10.400 imagens viram 41 fotografias; 575 mil traces viram 589 padrões. Antes de confiar em qualquer métrica, é preciso descobrir **quantas unidades realmente independentes a base tem** e dividir por elas.

---

## 10. Limitações

### Limitações de uso (licença e acesso)

| Base | Condições |
|---|---|
| **CoMoFoD** | *Release agreement*: só pesquisa acadêmica, sem uso comercial, sem redistribuir nem modificar as imagens baixadas, citando Tralić et al., ELMAR 2013. A base não tem garantia dos autores, e eles podem mudar os termos a qualquer momento. Nenhuma imagem da base vai para o git, para documentos ou para apresentações. Texto completo e regras práticas em [`datasheets/comofod.md`](datasheets/comofod.md#termos-de-uso). |
| **Loghub** | CC-BY-4.0 (Zenodo, DOI 10.5281/zenodo.8196385): uso livre com atribuição. |
| **CIC-IoT2023 e CIC-MalMem-2022** | Download só após formulário de cadastro em `cicresearch.ca`. Os termos de licença dessas duas ainda não foram lidos nem registrados no projeto. |
| **CoMoFoD Large** | Só por contato com os autores; fora do estudo. |

### Limitações do próprio estudo

- **Baselines simples, sem ajuste**, de uma execução (com média de sorteios onde indicado). Eles servem de régua, não de teto.
- **Hipóteses não testadas**, marcadas como tal: circularidade do rótulo do HDFS; o mecanismo de memorização no CoMoFoD; o significado da máscara `B`, de `Number` e dos segmentos da CIC-IoT2023.
- **Templates aproximados no BGL** (números trocados por `<N>`); um parser como o Drain daria templates mais fiéis.
- **Agrupamento por fotografia** feito com miniaturas, sem validação manual.
- **CIC-IoT2023 representada por um único arquivo**: nada se afirma sobre separabilidade nem sobre a base inteira. Os tamanhos são extrapolação.
- **Picos de memória não medidos** nos notebooks (o DuckDB foi limitado a 3 GB no Loghub).

---

## 11. O que falta

1. **CIC-MalMem-2022:** o usuário baixar o arquivo principal; depois, escrever o ticket 04 e rodar a EDA.
2. **CIC-IoT2023:** decidir e baixar o `MERGED_CSV` (ou parte dele), medir o tamanho real e o total de linhas e aplicar a regra dos ~40 GB.
3. **Ambiente:** subir o Spark local via Docker e documentar os comandos.
4. **Roteiro da base grande** (tickets 08 e 09): conversão para Parquet, comparação medida de pandas, DuckDB, Polars e Spark local, e comparação em custo e esforço de Databricks Free Edition, GCP e AWS.
5. **Datasheets** das 4 bases (ticket 07), reunindo origem, volume, rótulos, licença, acesso e riscos.
6. **Spec `0000`** e tickets pendentes, que dependem de o usuário rodar `/to-spec` e `/to-tickets`.

---

## 12. Onde está cada coisa

| O quê | Onde |
|---|---|
| Glossário | `CONTEXT.md` |
| Log de decisões | `docs/decisions.md` |
| Tickets | `docs/issues/` |
| Notas sobre os CSVs da CIC-IoT2023 | `docs/cic-iot2023-arquivos-csv.md` |
| EDA do Loghub | `notebooks/01_eda_loghub.ipynb` (veredito na seção 3) |
| EDA do CoMoFoD | `notebooks/02_eda_comofod.ipynb` (veredito na seção 5) |
| EDA de um arquivo da CIC-IoT2023 | `notebooks/03_eda_cic_iot2023_ddos_http_flood.ipynb` (seção 7) |
| Dados brutos e extraídos (fora do git) | `data/raw/<base>/` e `data/interim/<base>/` |
