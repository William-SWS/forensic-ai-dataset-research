# CIC-IoT2023: por que há vários CSVs por ataque (ex.: `DoS-HTTP_Flood.pcap.csv` e `DoS-HTTP_Flood1.pcap.csv`)

**Data:** 2026-10-15 · **Status:** parte verificada na página oficial, parte inferida. Cada afirmação diz de qual tipo é.

## Resposta curta

Os dois arquivos são, **muito provavelmente, dois pedaços da mesma captura do ataque `DoS-HTTP_Flood`**. Têm as mesmas colunas e o mesmo tipo de ataque, e cada um traz linhas diferentes. O sufixo `1` indica o segundo pedaço, e o arquivo sem número indica o primeiro. Para o estudo, devem ser tratados como **uma única classe** (`DoS-HTTP_Flood`), concatenados.

Isso **não está escrito em lugar nenhum que eu tenha conseguido ler**. É uma inferência a partir das evidências abaixo e deve ser confirmada depois do download (ver "Como confirmar").

## O que é verificado (fonte: página oficial do dataset no CIC/UNB)

Página: <https://www.unb.ca/cic/datasets/iotdataset-2023.html>

- O diretório principal tem quatro subdiretórios: `PCAP`, `CSV`, `Example` e `Supplementary Materials`.
- `PCAP` guarda o tráfego original capturado durante os ataques.
- `CSV` guarda as **features extraídas dos arquivos originais**, para uso em aprendizado de máquina.
- `Example` é um **notebook Jupyter** que mostra como treinar e avaliar modelos de detecção e classificação de ataques.
- `Supplementary Materials` tem o código-fonte e a descrição das ferramentas usadas na coleta e no tratamento: **Mergecap** para juntar vários `.pcap`, **PySpark** para tratar os dados, **TCPDump** para **dividir os `.pcap` em vários arquivos menores** e **DPKT** para extrair as features.
- A tabela de features da página lista **46 features** (inclui `flow_duration`, `Duration`, `Srate`, `Drate`, `urg_count`, `Radius`, `Covariance`, `Weight`). **Os CSVs por ataque que foram baixados não têm essas 46: têm 39 colunas** (ver "Verificado nos arquivos baixados" abaixo).
- Há 33 ataques em 7 categorias: DDoS, DoS, Recon, Web-based, Brute Force, Spoofing e Mirai.

## O que é inferido (não confirmado)

1. **A divisão em pedaços.** A página diz que o TCPDump foi usado para dividir os `.pcap` em arquivos menores, e que o DPKT extraiu as features dos arquivos resultantes. Pelo nome `X.pcap.csv`, cada CSV corresponde a **um** arquivo `.pcap` de entrada. Se o `.pcap` do ataque foi dividido, o resultado são `X.pcap`, `X1.pcap`, etc., e daí `X.pcap.csv`, `X1.pcap.csv`. É coerente com os dois nomes que você viu, mas a página **não descreve a convenção de numeração**.
2. ~~Mesmo esquema nos dois.~~ **Verificado** nos arquivos baixados: cabeçalhos idênticos (ver abaixo).
3. **Linhas diferentes (sem sobreposição) entre os dois.** Esperado se foram cortados em sequência. Não verificado. Se o corte não for limpo, podem existir fluxos duplicados ou cortados ao meio na fronteira.
4. ~~Coluna de rótulo.~~ **Verificado:** os CSVs por ataque **não têm coluna de rótulo**; a classe só está no nome do arquivo (ver abaixo).

## Verificado nos arquivos baixados (2026-10-15)

Foram baixados 4 CSVs em `data/raw/cic-iot2023/` (pasta `CSV/CSV/<ataque>/`) e o `README_CSV.pdf`:

| Arquivo | Linhas de dados | Tamanho |
|---|---|---|
| `DoS-HTTP_Flood.pcap.csv` | 40.686 | 8,6 MB |
| `DoS-HTTP_Flood1.pcap.csv` | 31.175 | 6,6 MB |
| `DDoS-HTTP_Flood-.pcap.csv` | 28.790 | 6,2 MB |
| `DictionaryBruteForce.pcap.csv` | 13.064 | 2,6 MB |

- **39 colunas, iguais nos 4 arquivos**, todas numéricas: `Header_Length`, `Protocol Type`, `Time_To_Live`, `Rate`, flags TCP, contagens de flags, indicadores de protocolo (`HTTP`, `HTTPS`, `DNS`, ..., `IGMP`, `IPv`, `LLC`), `Tot sum`, `Min`, `Max`, `AVG`, `Std`, `Tot size`, `IAT`, `Number`, `Variance`.
- **Não existe coluna `label`.** A classe de ataque só aparece no nome do arquivo (e da pasta). Para modelar, o rótulo precisa ser criado a partir do nome.
- Os valores têm cara de **agregação por janela** (por exemplo `Number` = 100, flags como fração), não de um fluxo individual. Isso é uma leitura do conteúdo, não confirmada por documentação.
- O arquivo `DoS-HTTP_Flood1.pcap.csv` tem o mesmo esquema do `DoS-HTTP_Flood.pcap.csv` e linhas diferentes, o que é compatível com a hipótese de dois pedaços da mesma captura. A numeração em si continua sem documentação.
- **Divergência com a página oficial:** a página lista 46 features (com `flow_duration`, `Duration`, `Srate`, `Drate`, `urg_count`, `Radius`, `Covariance`, `Weight`) e não lista `Time_To_Live` nem `IGMP`, que existem nos arquivos. Ou a tabela da página descreve outra versão, ou outro conjunto (por exemplo o MERGED). Não resolvido.

### O que o `README_CSV.pdf` diz
Texto do PDF (a camada de texto tem duas versões sobrepostas, uma dizendo **309** e outra **169** arquivos):

> This folder shows the features extracted from .pcap files as multiple .csv files (using the scripts present in the supplementary materials). All 309 [169] .csv files refer to a combined and shuffled dataset including all attacks. The attacks are identified by the 'label' feature.

Isso descreve um conjunto **combinado e embaralhado, com coluna `label`**, que **não é** o que está nos arquivos por ataque. A leitura mais coerente é que o README descreve a pasta `MERGED_CSV`, e que `CSV/CSV/<ataque>/` contém os pedaços por ataque sem rótulo. **Não está confirmado**: o README fica na pasta pai das duas. A contagem 309 vs 169 também fica sem resolução.

## Cuidado com nomes parecidos

`DoS-HTTP_Flood` (esta pasta) e `DDoS-HTTP_Flood` são **classes diferentes**: DoS parte de um atacante, DDoS de vários. A página lista `HTTP flood` nas duas categorias. Não misturar.

## Como confirmar depois do download

Com os dois arquivos em `data/raw/cic-iot2023/`:

```bash
cd data/raw/cic-iot2023/CSV/CSV/DoS-HTTP_Flood   # ajuste o caminho
wc -l DoS-HTTP_Flood.pcap.csv DoS-HTTP_Flood1.pcap.csv        # linhas por arquivo
head -1 DoS-HTTP_Flood.pcap.csv | md5sum; head -1 DoS-HTTP_Flood1.pcap.csv | md5sum   # cabeçalho igual?
head -1 DoS-HTTP_Flood.pcap.csv | tr ',' '\n' | wc -l          # número de colunas (verificado: 39, sem rótulo)
tail -n +2 DoS-HTTP_Flood.pcap.csv | sort -u > /tmp/a; tail -n +2 DoS-HTTP_Flood1.pcap.csv | sort -u > /tmp/b; comm -12 /tmp/a /tmp/b | wc -l   # linhas idênticas nos dois
```

Os comandos acima já foram aplicados aos 4 arquivos baixados (resultados na seção "Verificado"). Sobreposição entre `DoS-HTTP_Flood` e `DoS-HTTP_Flood1`: **42 linhas idênticas** (de 40.662 e 30.869 linhas únicas), ou seja, praticamente disjuntos. Há também duplicatas dentro de cada arquivo (24 e 306 linhas repetidas), o que a EDA da base grande deve tratar.

## Consequências para a análise (hipóteses, a validar no ticket de EDA)

- Tratar a pasta `DoS-HTTP_Flood` como **uma classe**, concatenando os arquivos.
- Como os CSVs são pedaços sequenciais de uma captura, **sorteio aleatório de linhas** entre treino e teste tende a colocar fluxos vizinhos no treino e no teste e inflar as métricas. Dividir **por arquivo** é uma alternativa a considerar. Isso é hipótese de modelagem, não fato do dataset.
- Para o benchmark de Spark, a grande quantidade de arquivos CSV pequenos é um bom caso de leitura distribuída, e a conversão para Parquet resolve a fragmentação.

## Fontes

- Página oficial do dataset (consultada em 2026-10-15): <https://www.unb.ca/cic/datasets/iotdataset-2023.html>
- Artigo: Neto et al., "CICIoT2023: A real-time dataset and benchmark for large-scale attacks in IoT environment", Sensors 2023, DOI [10.3390/s23135941](https://doi.org/10.3390/s23135941). **Não consegui ler o texto do artigo** (o site da MDPI bloqueou o acesso automático), então não há nele evidência usada aqui.
- O `README.pdf` do dataset, que fica atrás do formulário, pode explicar a convenção de nomes. Vale lê-lo ao baixar.
