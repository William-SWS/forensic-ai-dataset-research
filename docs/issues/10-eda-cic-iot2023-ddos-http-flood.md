# 10 EDA do `DDoS-HTTP_Flood-.pcap.csv` (um pedaço da CIC-IoT2023)

**Status:** concluído
**Notebook:** `notebooks/03_eda_cic_iot2023_ddos_http_flood.ipynb`
**Depende de:** 01 (ambiente) e 03 (o arquivo já foi recebido em `data/raw/cic-iot2023/`)
**Numeração:** 10 para não colidir com os tickets 04, 07, 08 e 09 previstos na proposta do project-builder.

## Por que

Este é um dos 4 CSVs por ataque que o usuário baixou da **base grande**. Não representa a base inteira, mas é o primeiro contato com o esquema real da CIC-IoT2023 e permite: (1) entender o que cada coluna significa e se os dados são coerentes; (2) medir custo por registro (disco e memória), insumo para o roteiro da base grande; (3) descobrir armadilhas (colunas constantes, redundância, ordem das linhas, heterogeneidade) antes do trabalho em escala.

## Escopo

- EDA de **um único arquivo**: `data/raw/cic-iot2023/DDoS-HTTP_Flood-.pcap.csv` (28.790 linhas e 39 colunas numéricas, 6,45 MB (6,2 MiB)).
- Qualidade, coerência interna, distribuições, redundância, ordem das linhas, heterogeneidade e custo por registro.

## Fora do escopo

- **Qualquer modelo ou baseline supervisionado.** O arquivo não tem coluna de **rótulo**: a classe só aparece no nome do arquivo, então só há uma classe. Não dá para medir separabilidade.
- Comparar com os outros 3 CSVs recebidos (`DoS-HTTP_Flood`, `DoS-HTTP_Flood1`, `DictionaryBruteForce`).
- Conversão para Parquet e o **benchmark de ferramentas** (tickets futuros).
- Tirar conclusões sobre a base grande além do que um pedaço permite.

## Critérios de aceite

- [x] O notebook roda do zero sem erro (`jupyter nbconvert --execute`) e o tempo de execução é registrado.
- [x] **Esquema e qualidade:** número de linhas e colunas, tipos, nulos, linhas duplicadas, colunas constantes e colunas com poucos valores distintos, todos medidos e impressos.
- [x] **Coerência interna** conferida por verificações que imprimem a porcentagem de linhas que cumprem cada regra, e **falham visivelmente** (`assert`) só nas regras estruturais óbvias: frações em [0, 1]; `Min <= AVG <= Max`; `Variance` coerente com `Std`². Hipóteses a testar (não assumir): as colunas `*_flag_number` são `*_count / Number`; `Tot size` é igual a `AVG`; `IPv` e `LLC` são idênticas.
- [x] **Distribuições:** resumo estatístico e gráficos das variáveis principais, com atenção às caudas pesadas (`Rate`, `IAT`, `Tot sum`, `Variance`); a distribuição de `Number` e quantas linhas não têm o valor típico.
- [x] **Redundância:** matriz de correlação e lista dos pares com |r| > 0,95 e das colunas idênticas.
- [x] **Ordem das linhas:** autocorrelação de lag 1 das variáveis numéricas para indicar se as linhas são sequenciais ou embaralhadas, e uma frase sobre a implicação para divisão treino/teste.
- [x] **Heterogeneidade:** quanto do arquivo é de fato tráfego HTTP/TCP (frações de `HTTP`, `TCP`, `ARP`, `DNS`, `UDP`, `ICMP`) e quantas linhas fogem do padrão dominante; uma projeção 2D (PCA) para ver a estrutura. Nenhuma afirmação sobre rótulos.
- [x] **Escala:** bytes por registro no CSV e na memória do pandas (medidos) e **extrapolação explícita** para 46.686.579 registros, identificada como extrapolação a partir de um pedaço (supõe largura de linha semelhante, não verificado).
- [x] Uma seção final separa o que **sabemos** sobre este arquivo do que **não sabemos** (rótulo, representatividade, relação com o restante da base).
- [x] Os resultados entram na seção "Resultado" deste ticket e numa nova entrada de `docs/decisions.md`.

## Notas

- Observações do esquema já conhecidas (de `docs/cic-iot2023-arquivos-csv.md`): 39 colunas, sem `label`, valores com cara de agregação por janela. Nenhuma está confirmada pela documentação oficial; a página lista 46 features e não as mesmas.
- O nome do arquivo termina em `-.pcap.csv` (hífen antes do ponto), diferente dos outros. Não há explicação documentada.
- Pela estrutura, `Number` parece ser o número de pacotes por janela (100 na maioria das linhas); é hipótese.

## Resultado (2026-10-15)

Notebook `notebooks/03_eda_cic_iot2023_ddos_http_flood.ipynb`: roda do zero sem erro, em cerca de 5 segundos (4 figuras).

- **Forma:** 28.790 linhas, 39 colunas (30 `float64`, 9 `int64`), 6,45 MB; 0 nulos, 0 duplicadas, 0 infinitos; constantes: `Telnet`, `SMTP`, `IRC`. Sem coluna de rótulo.
- **Hipóteses do ticket, testadas:** valem em 100% das linhas `Tot size == AVG`, `IPv == LLC`, `*_flag_number == *_count / Number` (a 0,01), `Variance == Std²`, `Tot sum == AVG × Number`, `ARP == 1 − IPv` e contagem de flag ≤ `Number`. `Rate × IAT ≈ 1` vale dentro de 1% em 87,2% das linhas e de 10% em 97,0%, mas só em 6,85% com tolerância de 1e-6: a hipótese `Rate = 1/IAT` está **só aproximadamente** certa.
- **Redundância:** 11 pares com |r| > 0,95; 2 pares de colunas idênticas (`IPv`/`LLC` e `AVG`/`Tot size`).
- **Ordem:** sequencial; autocorrelação de lag 1 até 0,967 (`HTTP`), 33 de 36 colunas acima do ruído (±0,012); controle embaralhado: no máximo 0,011.
- **Caudas:** `Rate` máximo 699.051 (862 vezes a mediana); `IAT` com 8 linhas acima de 1 s e uma de 46.665 s (~13 h).
- **Heterogeneidade:** 78,7% das linhas são TCP ≥ 0,9 com HTTP ≥ 0,5; 4.634 linhas (16,1%) têm HTTP < 0,1, 92% delas em 6 segmentos inteiros.
- **Escala:** 224 B/registro no CSV, 312 B no pandas (`float64`), 156 B (`float32`); **extrapolado** para 46,7M registros: ~10,5 GB, ~14,6 GB e ~7,3 GB.

### Escopo que surgiu durante a execução (seção 4.1 do notebook)

Os 61 valores de `Number < 100` aparecem espalhados pelo arquivo. A hipótese de que cada um fecha um segmento foi testada: são 61 segmentos de 68 a 1.146 linhas (mediana 297), e o segmento explica 89% da variância de `HTTP` e 24% da variância mediana das colunas (ao acaso: ~0,2%). Isso não estava previsto no ticket e muda a recomendação de divisão treino/teste (por segmento, nunca por linha). A interpretação dos segmentos continua sendo hipótese.

### Pendências e limites

- Sem rótulo, nada se afirma sobre separabilidade ou sobre os 6 segmentos sem HTTP (outra fase do ataque ou outro tráfego?).
- A extrapolação de tamanho supõe a mesma largura de linha nos demais arquivos; o tamanho real continua **não verificado** (ticket 03).
