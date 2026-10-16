# Bases de dados mais relevantes para forense digital com IA

**Síntese de pesquisa** — material de apoio para a construção de uma apresentação sobre quais bases de dados escolher para trabalhar em forense digital.

**Data da consolidação:** 2026-09-23

---

## 1. O que foi pesquisado

O levantamento partiu de dois conjuntos e os cruzou:

1. **A planilha `Datasets Forenses.xlsx`**: 37 bases catalogadas por nicho (rede, IoT, malware, móvel, imagem/multimídia, disco/memória, texto/e-mail), com descrição, origem e onde baixar.
2. **A revisão de literatura** (`literature_review.md`, 89 trabalhos): extração de quais bases cada artigo efetivamente usa, com leitura de texto completo quando disponível e do resumo quando não.

O cruzamento revelou **68 bases únicas** no total, sendo 37 da planilha e 39 identificadas nos artigos, das quais **apenas 8 se sobrepõem**. Ou seja: a planilha e a literatura recente de IA aplicada conversam pouco.

**Fontes de dado e verificação:**

- **Citações:** Crossref (`is-referenced-by-count`) como fonte primária; OpenAlex apenas quando não existe registro na Crossref (ex.: EMBER no arXiv, IoT-23 no Zenodo, CoMoFoD sem DOI).
- **Auditoria de citações:** a OpenAlex apresentou falha grave no artigo do Bot-IoT (94 citações contra 1.759 na Crossref e 1.777 no Semantic Scholar). Por isso a Crossref é a fonte primária, e toda contagem foi conferida em pelo menos duas fontes quando possível.
- **Evidência de uso:** nome do dataset localizado no texto completo (PDF convertido) ou no resumo recuperado por API. Nenhum número foi inferido.

---

## 2. Critério de relevância

Uma base é relevante para trabalho em forense digital quando atende a três critérios combinados:

| Critério | Como foi medido |
|---|---|
| **Importância estrutural** | É o padrão de fato do subcampo (todo artigo reporta resultado nela) |
| **Volume de citações** | Crossref `is-referenced-by-count`, medido em 2026-09-23 |
| **Uso atual** | Presença nos artigos revisados, com viés para 2023-2026 |

A métrica que sintetiza volume e atualidade é **citações por ano** (citações ÷ idade da base). Ela evita premiar bases antigas só por serem antigas, e é o que ordena as recomendações.

---

## 3. Recomendação por nicho

Cada nicho tem **duas bases recomendadas** (uma "clássica" e uma "moderna" quando possível), com a justificativa e o veredito de infraestrutura.

### 3.1 Rede/Tráfego

**Recomendadas: CIC-IDS2017 e CSE-CIC-IDS2018**

| Base | Ano | Citações | Citações/ano | Uso recente |
|---|---|---|---|---|
| CIC-IDS2017 | 2017 | 3.808 | 423 | IoV-BERT-IDS (2025) |
| CSE-CIC-IDS2018 | 2018 | sem DOI | — | RAPIER (NDSS 2024), TCG-IDS (TIFS 2025) |

Por quê: são a mesma linhagem do CIC/UNB e permitem comparar duas gerações; são as bases de rede com uso mais forte em 2024-2026. **UNSW-NB15** (3.382 citações, 307/ano) é a alternativa se for preciso um DOI citável. **NSL-KDD**, apesar das 3.843 citações, deve ser evitada: tráfego de 1998, crítica de obsolescência já padronizada.

**Spark:** CIC-IDS2017 → não para as tabelas (2,8 milhões de fluxos); só se for reprocessar o PCAP bruto (~48,8 GB). CSE-CIC-IDS2018 → no limite (16,2 milhões de instâncias); DuckDB resolve antes do Spark.

### 3.2 IoT

**Recomendadas: CIC-IoT2023 e Bot-IoT**

| Base | Ano | Citações | Citações/ano | Uso recente |
|---|---|---|---|---|
| CIC-IoT2023 | 2023 | 980 | 327 | MIETT (AAAI 2025) |
| Bot-IoT | 2019 | 1.759 | 251 | FedCAD (2025) |

Por quê: CIC-IoT2023 tem a maior velocidade de citação de todo o levantamento e é a aposta de novidade; Bot-IoT tem o maior volume absoluto entre as bases específicas de IoT. **TON_IoT** (854 citações) é a alternativa mais rica para forense, por ser heterogênea (telemetria + logs de SO + rede).

**Spark: sim para os dois.** 46,6 milhões (CIC-IoT2023) e mais de 72 milhões (Bot-IoT) de registros. É o nicho onde o processamento distribuído se justifica de fato. Cuidado com o desbalanceamento extremo do Bot-IoT (classe normal ≈ 0,007%).

### 3.3 Malware

**Recomendadas: EMBER2024 e Drebin**

| Base | Ano | Citações | Citações/ano |
|---|---|---|---|
| EMBER2024 | 2025 | 26 | 26 |
| Drebin | 2014 | 1.651 | 138 |

Por quê: EMBER é o padrão industrial para malware PE com ML, e a linha foi renovada em 2025 (publicação no KDD). Drebin é a base mais citada do nicho e a referência de Android, com acesso por solicitação formal. **Malimg** (1.067 citações) serve como linha de base rápida, sem barreira de acesso, mas é base pequena.

**Spark:** EMBER → no limite (o vetor de features fica em 10-20 GB; DuckDB resolve). Drebin → não.

### 3.4 Móvel

**Recomendadas: CIC-AndMal2017 e CIC-InvesAndMal2019**

| Base | Ano | Citações | Citações/ano | Uso recente |
|---|---|---|---|---|
| CIC-AndMal2017 | 2017 | 292 | 32 | — |
| CIC-InvesAndMal2019 | 2020 | 250 | 42 | RAPIER (NDSS 2024) |

Ressalva: é o nicho mais fraco do levantamento. A planilha original tinha uma única linha (CIC-AndMal2017); a segunda recomendação veio dos artigos. **CICMalDroid2020** é a geração mais recente, mas sem contagem de citações medida.

**Spark:** não. A extração de features dos PCAPs roda com Zeek em paralelo numa máquina só.

### 3.5 Imagem/Multimídia

**Recomendadas: FaceForensics++ e CASIA v2**

| Base | Ano | Citações | Citações/ano | Uso recente |
|---|---|---|---|---|
| FaceForensics++ | 2019 | 2.683 | 383 | dois trabalhos da revisão (2023, 2025) |
| CASIA v2 | 2013 | 696 | 54 | MGQFormer (AAAI 2024) |

Por quê: FF++ é o padrão de fato em deepfake e vídeo, com a maior velocidade de citação do nicho; CASIA v2 é o padrão de fato em localização de falsificação de imagem. Alternativas por ângulo: **DEFACTO** (126 citações, 200 mil+ imagens, quatro categorias), **IMD2020** (223, manipulação realista) e **DF40** (42, benchmark mais novo).

**Spark: não — e aqui a recomendação é firme.** O gargalo em imagem/vídeo é GPU e decodificação, não volume tabular. PyTorch + DataLoader em GPU; para pré-processamento em massa, ffmpeg em paralelo ou Ray/DALI. Spark só ajudaria em tabelas de features já extraídas.

### 3.6 Disco/Memória

**Recomendadas: CIC-MalMem-2022 e Govdocs1**

| Base | Ano | Citações | Citações/ano | Uso recente |
|---|---|---|---|---|
| CIC-MalMem-2022 | 2022 | 147 | 37 | três trabalhos (2025, 2026) |
| Govdocs1 | 2009 | 284 | 17 | carving e sector hashing |

Por quê: CIC-MalMem-2022 é a única base de memória já tabular e rotulada, e a mais usada em trabalhos recentes. Govdocs1 (~1 milhão de arquivos redistribuíveis, conforme a página oficial) é a referência para carving e classificação de fragmentos. Alternativas: **M57-Patents** (~1 TB, multi-modal), **Loghub** (257 citações, logs) e **Dumpware10** (129 citações, segunda opção de memória).

**Spark:** CIC-MalMem-2022 → não (58.596 registros). Govdocs1 → sim, o caso mais claro de paralelização depois do IoT (hashing/carving sobre ~1 milhão de arquivos).

### 3.7 Texto/E-mail

**Recomendada: Enron Email Corpus** (620 citações, ~500 mil e-mails).

Não há segunda base neste nicho. O diagnóstico da própria planilha é que a maior parte da literatura que cita o Enron é de processamento de linguagem em geral, não de forense. Se for preciso um segundo conjunto, teria de vir dos logs (Loghub ou DARPA TC, ambos em Disco/Memória).

**Spark:** não (~1 GB).

### 3.8 Sem categoria (ADFIR e DARPA TC)

Se algum entrar na apresentação, o **DARPA TC** é o mais interessante: logs de proveniência em domínio público, com três projetos no GitHub. O **ADFIR** é de janeiro de 2026, licença CC BY 4.0, ainda sem literatura.

**Spark:** DARPA TC → provavelmente sim, porque o README oficial descreve um repositório muito grande; tamanho não verificado. ADFIR → não.

---

## 4. Quadro consolidado

| Nicho | Recomendada 1 | Recomendada 2 | Critério dominante |
|---|---|---|---|
| Rede/Tráfego | CIC-IDS2017 | CSE-CIC-IDS2018 | citações + uso 2024-2026 |
| IoT | CIC-IoT2023 | Bot-IoT | velocidade de citação + volume |
| Malware | EMBER2024 | Drebin | padrão industrial + citações |
| Móvel | CIC-AndMal2017 | CIC-InvesAndMal2019 | único disponível |
| Imagem/Multimídia | FaceForensics++ | CASIA v2 | padrão de fato do subcampo |
| Disco/Memória | CIC-MalMem-2022 | Govdocs1 | prontidão para ML + escala |
| Texto/E-mail | Enron | — | único disponível |

**As cinco mais relevantes do levantamento, em uma linha:**

1. **CIC-IDS2017** — tráfego de intrusão, 3.808 citações, o ponto de partida de qualquer NIDS com ML.
2. **FaceForensics++** — deepfake em imagem e vídeo, 2.683 citações, o padrão do subcampo.
3. **Bot-IoT** — 1.759 citações, 72 milhões de registros, a base de IoT com maior massa crítica.
4. **Drebin** — malware Android, 1.651 citações, referência histórica que ainda não foi substituída.
5. **CIC-IoT2023** — a base de IoT com maior velocidade de adoção (980 citações em 3 anos), a escolha de quem quer novidade.

---

## 5. Quando usar Spark/PySpark

Regra de decisão usada em todo o levantamento:

| Faixa | Recomendação |
|---|---|
| < 10 milhões de linhas ou < 10 GB | **Não usar Spark.** DuckDB ou Polars numa máquina só, com menos setup e melhor desempenho |
| 10-100 milhões de linhas ou dezenas de GB | **No limite.** DuckDB com 32 GB resolve; Spark se houver joins distribuídos |
| > 100 GB, PCAP em nível de pacote, ou corpus de ~1 milhão de arquivos | **Spark justificado** |
| Imagem/vídeo com deep learning | **Nunca Spark.** GPU + DataLoader |

Veredito por base recomendada:

| Base | Spark? |
|---|---|
| CIC-IDS2017 | Não (sim só no PCAP bruto) |
| CSE-CIC-IDS2018 | No limite |
| CIC-IoT2023 | **Sim** |
| Bot-IoT | **Sim** |
| EMBER2024 | No limite |
| Drebin | Não |
| CIC-AndMal2017 | Não |
| CIC-InvesAndMal2019 | Não |
| FaceForensics++ | Não (GPU) |
| CASIA v2 | Não (GPU) |
| CIC-MalMem-2022 | Não |
| Govdocs1 | **Sim** |
| Enron | Não |

---

## 6. Lacunas e pontos de atenção

1. **A planilha e a literatura se desencontram.** Dos 39 datasets identificados nos artigos, 31 não têm linha na planilha. A planilha é forte em bases clássicas de disco/memória (M57-Patents, Govdocs1, NSRL, Real Data Corpus) que quase não aparecem na literatura recente de IA, e fraca exatamente nas bases que a IA usa: FaceForensics++, Celeb-DF, DFDC, DeeperForensics, WildDeepfake, VISION, DF40, IMD2020, NIST16, Columbia e Loghub estão todos ausentes.

2. **Bases sem DOI de referência.** CSE-CIC-IDS2018, NIST CFReDS, NIST NSRL/RDS, DFRWS Challenges, NPS-2009, 2018 Lone Wolf, OTRF/Mordor, CIRCL, IoT-CAD e DARPA TC não têm artigo fundador citável. Nelas, a citação precisa ser feita pela página oficial.

3. **Referências canônicas ainda pendentes.** CrossPlatform (Android/iOS), CIC-DoHBrw-2020, MaleVis, FFT-75, FRGC e ALASKA2 ficaram sem referência de origem verificada. DFDC tem apenas relatório em arXiv, não publicado em veículo revisado por pares.

4. **Karggle não é auditável por HTTP.** A plataforma devolve HTTP 200 até para endereço inexistente, então os links de Kaggle da planilha dependem de conferência manual.

5. **Tamanhos herdados da planilha, não medidos.** Os volumes citados (CIC-IDS2017 ~48,8 GB, CIC-IoT2023 46,6 milhões, Bot-IoT 72 milhões) vêm das descrições da própria planilha e não foram conferidos byte a byte.

---

## 7. Conclusão para a apresentação

- A escolha de base para forense digital com IA deve partir de **quatro blocos**: tráfego de rede (CIC-IDS2017/2018), IoT (CIC-IoT2023/Bot-IoT), imagem e vídeo (FaceForensics++/CASIA) e memória (CIC-MalMem-2022), com Govdocs1 como a opção de escala para disco.
- **Só dois nichos exigem processamento distribuído de verdade:** IoT (dezenas de milhões de registros) e Govdocs1 (cerca de 1 milhão de arquivos). Todo o resto se resolve em uma máquina, com GPU para imagem/vídeo.
- A decisão deve ser defendida com **citações por ano** (atualidade) e com **uso em trabalhos de 2024-2026**, não só com o total acumulado, que premia bases antigas.
- Há uma **oportunidade de trabalho** em preencher as 31 bases ausentes da planilha e em resolver as seis referências canônicas pendentes, o que fecha o mapa antes de qualquer projeto novo.
