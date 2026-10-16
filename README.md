# Seleção e análise exploratória de bases de dados forenses

Este projeto estuda se dá para construir modelos de IA úteis sobre bases públicas de forense digital. Ele escolhe quatro bases de nichos diferentes, faz a análise exploratória de cada uma e prepara um roteiro para trabalhar com uma base grande demais para a memória da máquina.

O ponto de partida é um levantamento que já está neste repositório: uma planilha com 37 bases forenses, uma revisão de literatura com 89 trabalhos e uma síntese de recomendações por nicho.

## Objetivos

- Escolher três bases de porte "ok", que cabem na memória, para avaliar a viabilidade de IA em forense digital.
- Usar uma base grande para comparar formas de processar dados fora da memória: pandas, DuckDB, Polars e Spark local, além de comparar em custo e esforço Databricks Free Edition, GCP e AWS.

### Entregáveis

1. Datasheet de cada uma das quatro bases: origem, volume, rótulos, licença, acesso e riscos.
2. Análise exploratória das três bases de porte "ok".
3. Roteiro de trabalho para a base grande.

## As bases

| Papel | Base | Nicho | Quem criou | O que registra | Formato |
|---|---|---|---|---|---|
| Base grande | CIC-IoT2023 | IoT e rede | CIC, University of New Brunswick (Neto et al., 2023) | Tráfego de 105 dispositivos IoT sob 33 ataques | PCAP e CSV |
| Porte "ok" | CIC-MalMem-2022 | Memória | CIC, University of New Brunswick (Carrier et al., 2022) | Atributos de dumps de RAM de máquinas Windows com e sem malware | CSV |
| Porte "ok" | Loghub (HDFS_v1 e BGL) | Logs de sistema | Projeto LogPAI, com logs de Xu et al. (2009) e do LLNL | Logs do Hadoop HDFS e do supercomputador BlueGene/L | Texto e CSV |
| Porte "ok" | CoMoFoD Small | Imagem | Universidade de Zagreb (Tralić et al., 2013) | Fotos adulteradas por cópia e colagem, com máscaras e versões degradadas | PNG e JPEG |

Bases reserva, caso alguma das escolhidas não sirva: Dumpware10 (memória), DEFACTO ou CASIA v2 (imagem) e outro sistema do Loghub (logs).

## Estado atual

| Base | Situação | Onde |
|---|---|---|
| Loghub | Análise concluída | `notebooks/01_eda_loghub.ipynb` |
| CoMoFoD | Análise concluída | `notebooks/02_eda_comofod.ipynb` |
| CIC-IoT2023 | Um arquivo analisado (`DDoS-HTTP_Flood-.pcap.csv`, 28.790 linhas) | `notebooks/03_eda_cic_iot2023_ddos_http_flood.ipynb` |
| CIC-MalMem-2022 | Bloqueada: só chegaram 850 linhas de uma família de spyware; falta o arquivo principal de 58.596 registros | ainda sem notebook |

Ainda não foram feitos os datasheets, o roteiro da base grande nem o Spark local via Docker.

## Principais resultados até agora

- **Loghub HDFS_v1:** 575.061 traces e 2,93% de anomalias, mas só 589 combinações distintas de eventos. A divisão aleatória dá F1 de 0,999; testando só com combinações nunca vistas, o F1 fica em 0,968.
- **Loghub BGL:** 4.747.963 linhas e 7,34% de alertas. 44% dos alertas do período final têm um molde de mensagem que nunca tinha aparecido. Treinando no passado e testando no futuro, o F1 é 0,72.
- **CoMoFoD:** 10.400 imagens em 200 cenas, que vêm de apenas 41 fotografias. Um modelo simples tem AUC de 0,984 quando a mesma foto aparece no treino e no teste, e 0,495 (acaso) quando a separação é por fotografia.
- **CIC-IoT2023:** os CSV por ataque têm 39 colunas e nenhuma coluna de rótulo. As linhas estão em sequência (autocorrelação até 0,967) e formam 61 segmentos. Por extrapolação, a base inteira ocuparia cerca de 10,5 GB em CSV e 14,6 GB no pandas, mais que a memória livre.

O ponto comum às três bases analisadas é que a forma de separar treino e teste muda o resultado. Os detalhes estão em `docs/relatorio-andamento.md` e na seção de veredito de cada notebook.

## Como reproduzir

### Ambiente

O projeto usa [uv](https://docs.astral.sh/uv/) com Python 3.13 (`requires-python >= 3.12`). As dependências estão em `pyproject.toml`: pandas, DuckDB, Polars, pyarrow, scikit-learn, matplotlib, seaborn, pillow e Jupyter.

```bash
uv sync
uv run jupyter lab
```

### Dados

Os dados não estão no git (`.gitignore`). Os arquivos baixados ficam intactos em `data/raw/<base>/`, e os extraídos vão para `data/interim/<base>/`.

| Base | Como obter | Onde colocar |
|---|---|---|
| Loghub | Download direto no Zenodo (DOI 10.5281/zenodo.8196385): `HDFS_v1.zip` e `BGL.zip` | `data/raw/loghub/` |
| CoMoFoD Small | Download direto em https://www.vcl.fer.hr/comofod/ (`comofod_small.rar`, 3,0 GiB), depois de ler o acordo de uso | `data/raw/comofod/` |
| CIC-IoT2023 | Formulário de cadastro em https://www.unb.ca/cic/datasets/iotdataset-2023.html | `data/raw/cic-iot2023/` |
| CIC-MalMem-2022 | Formulário de cadastro em https://www.unb.ca/cic/datasets/malmem-2022.html | `data/raw/cic-malmen-2022/` |

Os formulários do CIC pedem dados pessoais, então cada pesquisador faz o próprio cadastro e baixa os arquivos.

Antes de rodar os notebooks 01 e 02, extraia os arquivos:

```bash
unzip -q data/raw/loghub/HDFS_v1.zip -d data/interim/loghub/hdfs
unzip -q data/raw/loghub/BGL.zip -d data/interim/loghub/bgl
mkdir -p data/interim/comofod && unrar x data/raw/comofod/comofod_small.rar data/interim/comofod/
```

O notebook 03 lê o CSV direto de `data/raw/cic-iot2023/`.

### Executar os notebooks do zero

```bash
uv run jupyter nbconvert --to notebook --execute --inplace notebooks/01_eda_loghub.ipynb
```

Tempos medidos: cerca de 1,5 min (Loghub), 2 min 33 s (CoMoFoD) e 5 s (CIC-IoT2023). O notebook do Loghub limita o DuckDB a 3 GB de RAM.

## Condições de uso das bases

- **Loghub:** licença CC-BY-4.0. O uso é livre, desde que a fonte seja citada.
- **CoMoFoD:** o [acordo de uso](https://www.vcl.fer.hr/comofod/release_agreemen.html) permite só pesquisa acadêmica ou científica, sem nenhum uso comercial. A base não pode ser redistribuída, publicada, copiada nem disseminada, nem mesmo para colegas da mesma instituição. As imagens baixadas não podem ser modificadas, mas imagens novas podem ser criadas a partir delas. Todo trabalho que usar a base deve citar Tralić et al., "CoMoFoD - New Database for Copy-Move Forgery Detection", ELMAR-2013, pp. 49-54. Por isso nenhuma imagem da base entra no repositório, e a figura de exemplo do notebook 02 fica desligada por padrão.
- **CIC-IoT2023 e CIC-MalMem-2022:** o download exige cadastro. Os termos de licença ainda não foram lidos nem registrados.

## Ambiente de trabalho

16 GB de RAM (cerca de 4 GB livres), 89 GB de disco livre, RTX 4050 Laptop com 6 GB de VRAM, 12 núcleos, Linux. Todo o processamento roda localmente; as nuvens entram só na comparação de custo e esforço.

## Estrutura do repositório

```
.
├── README.md
├── CONTEXT.md                  glossário do projeto
├── AGENTS.md                   instruções para agentes de IA
├── pyproject.toml, uv.lock     ambiente Python
├── notebooks/                  análise exploratória, um notebook por base
├── docs/
│   ├── decisions.md            log cronológico de decisões (só se acrescenta)
│   ├── relatorio-andamento.md  explicação didática do que foi feito
│   ├── cic-iot2023-arquivos-csv.md
│   ├── issues/                 tickets de cada etapa
│   └── presentations/          apresentação das bases (.pptx)
├── spreadsheet/                catálogo de 37 bases e sua verificação
├── bases-dados-forense-digital-sintese.md
├── literature_review.md
├── lit-review_ia_forense_digital.md
└── data/                       fora do git: raw/ (baixado) e interim/ (extraído)
```

## Próximos passos

1. Receber o arquivo principal da CIC-MalMem-2022 e fazer a análise exploratória.
2. Baixar a versão rotulada da CIC-IoT2023 (`MERGED_CSV`) e medir o tamanho real.
3. Subir o Spark local via Docker.
4. Converter a CIC-IoT2023 para Parquet e comparar pandas, DuckDB, Polars e Spark.
5. Escrever os datasheets das quatro bases e o roteiro da base grande.
