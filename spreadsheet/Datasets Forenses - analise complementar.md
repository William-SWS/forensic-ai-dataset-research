# Datasets Forenses — análise complementar

**Documento derivado de:** `Datasets Forenses.xlsx` (abas `datasets_forense_digital.csv`, `Síntese`, `Meotodologia`)
**Data da verificação:** 2026-09-23
**Registros analisados:** 37 (linhas 2 a 38 da aba principal)
**A planilha não foi alterada.** Este documento é o único artefato novo; o xlsx permanece intacto para edição manual.

Este documento responde a três perguntas:

1. Quais bases são de 2020 para trás (relação "bases de dados antigas").
2. Os links da planilha apontam para as versões mais recentes; onde não apontam, qual é o link atualizado.
3. Quais registros são de fato datasets e quais são repositórios, portais ou coleções.

---

## 0. Como os anos foram determinados

Nenhum ano foi atribuído por estimativa. A ordem de precedência usada foi:

1. **Artigo fundador da base**, verificado por DOI na Crossref (evidência mais forte).
2. **Ano declarado na própria planilha** (coluna D, "Construção", ou coluna Q).
3. **Página oficial da base** ou metadados do repositório (ex.: data de criação do repositório na API do GitHub).
4. **Nome da base**, quando ele carrega o ano (ex.: `2018 Lone Wolf`, `NPS-2009-domexusers`).
5. Sem evidência obtível → registrado como **não determinado**, nunca inferido.

A coluna "fonte do ano" em cada tabela diz exatamente de onde o ano veio.

---

## 1. Bases de dados antigas (2020 para trás)

**31 dos 37 registros são de 2020 ou antes.** Ordenados por ano.

| # | Base | Categoria | Ano | Fonte do ano |
|---|---|---|---|---|
| 25 | NIST NSRL / RDS | Disco/Memória | 2000 (origem) | Página do NIST lista 2000; a planilha declara RDSv3 desde 2023 |
| 34 | Enron Email Corpus | Texto/E-mail | 2001 | Planilha (liberação FERC em 2001); corpus republicado pela CMU |
| 27 | DFRWS Forensic Challenges | Disco/Memória | série desde 2005 | Página do DFRWS lista edições de 2005 a 2026 |
| 2 | NSL-KDD | Rede/Tráfego | 2009 | Artigo fundador: DOI [10.1109/cisda.2009.5356528](https://doi.org/10.1109/cisda.2009.5356528) |
| 26 | Digital Corpora — M57-Patents | Disco/Memória | 2009 | Digital Corpora ("2009 M57-Patents Scenario") + paper DFRWS 2009, DOI [10.1016/j.diin.2009.06.016](https://doi.org/10.1016/j.diin.2009.06.016). **A planilha diz ADFSL 2011; ver §4** |
| 28 | Govdocs1 | Disco/Memória | 2009 | Página do Digital Corpora cita Garfinkel et al., DFRWS 2009 |
| 29 | Real Data Corpus | Disco/Memória | 2009 a 2011 | Paper 2009 (DOI acima) + página oficial: "As of February 21, 2011" |
| 30 | NPS-2009-domexusers | Disco/Memória | 2009 | Nome da base + corpus NPS do Digital Corpora |
| 21 | Dresden Image Database | Imagem/Multimídia | 2010 | Artigo fundador: DOI [10.1145/1774088.1774427](https://doi.org/10.1145/1774088.1774427) |
| 6 | CTU-13 | Rede/Tráfego | 2011 (captura) | Planilha; artigo de referência 2014, DOI [10.1016/j.cose.2014.05.011](https://doi.org/10.1016/j.cose.2014.05.011) |
| 16 | Malimg | Malware | 2011 | Artigo fundador: DOI [10.1145/2016904.2016908](https://doi.org/10.1145/2016904.2016908) |
| 19 | CASIA (Image Tampering) | Imagem/Multimídia | 2013 | Artigo fundador: DOI [10.1109/chinasip.2013.6625374](https://doi.org/10.1109/chinasip.2013.6625374) |
| 23 | CoMoFoD | Imagem/Multimídia | 2013 | Tralić et al., ELMAR 2013. **Sem DOI localizado na Crossref**; citação sem DOI |
| 15 | Drebin | Malware | 2014 | Artigo fundador: DOI [10.14722/ndss.2014.23247](https://doi.org/10.14722/ndss.2014.23247) (amostras de 2010 a 2012) |
| 3 | UNSW-NB15 | Rede/Tráfego | 2015 | Artigo fundador: DOI [10.1109/milcis.2015.7348942](https://doi.org/10.1109/milcis.2015.7348942) |
| 20 | RAISE | Imagem/Multimídia | 2015 | Artigo fundador: DOI [10.1145/2713168.2713194](https://doi.org/10.1145/2713168.2713194) |
| 4 | CIC-IDS2017 | Rede/Tráfego | 2017 (captura) | Planilha (jul/2017); artigo 2018, DOI [10.5220/0006639801080116](https://doi.org/10.5220/0006639801080116) |
| 18 | CIC-AndMal2017 | Móvel | 2017 | Nome da base; artigo 2018, DOI [10.1109/ccst.2018.8585560](https://doi.org/10.1109/ccst.2018.8585560) |
| 5 | CSE-CIC-IDS2018 | Rede/Tráfego | 2018 | Planilha (fev-mar/2018) + página oficial do CIC |
| 14 | EMBER | Malware | 2018 | Anderson & Roth, arXiv [1804.04637](https://arxiv.org/abs/1804.04637) |
| 31 | 2018 Lone Wolf Scenario | Disco/Memória | 2018 | Nome da base + página oficial do Digital Corpora |
| 32 | OTRF / Mordor (Security-Datasets) | Disco/Memória | 2018 | API do GitHub: repositório criado em 2018-05-31 |
| 38 | DARPA Transparent Computing | (sem categoria) | 2018 a 2020 | API do GitHub: repositório do programa criado em 2018-06-04, último push em 2020-04-29 |
| 8 | Bot-IoT | IoT | 2019 | Artigo fundador: DOI [10.1016/j.future.2019.05.041](https://doi.org/10.1016/j.future.2019.05.041) |
| 9 | TON_IoT | IoT | 2020 | Artigo fundador: DOI [10.1109/access.2020.3022862](https://doi.org/10.1109/access.2020.3022862) |
| 10 | IoT-23 (Aposemat) | IoT | 2020 | Zenodo, DOI [10.5281/zenodo.4743746](https://doi.org/10.5281/zenodo.4743746) (planilha registra capturas de 2018-2019) |
| 11 | MQTT-IoT-IDS2020 | IoT | 2020 | Nome da base + depósito no IEEE DataPort |
| 12 | MedBIoT | IoT | 2020 | Artigo fundador: DOI [10.5220/0009187802070218](https://doi.org/10.5220/0009187802070218) |
| 13 | IoT-Flock (gerador) | IoT | 2020 | API do GitHub: repositório criado em 2020-03-04; preprint DOI [10.21203/rs.3.rs-20786/v1](https://doi.org/10.21203/rs.3.rs-20786/v1) |
| 36 | CIC-Darknet2020 | Rede/Tráfego | 2020 | Nome da base + página oficial do CIC |

### 1.1 Bases de 2021 em diante (4 registros)

| # | Base | Categoria | Ano | Fonte do ano |
|---|---|---|---|---|
| 17 | CIC-MalMem-2022 | Disco/Memória | 2022 | Artigo fundador: DOI [10.5220/0010908200003120](https://doi.org/10.5220/0010908200003120) |
| 7 | CIC-IoT2023 | IoT | 2023 | Artigo fundador: DOI [10.3390/s23135941](https://doi.org/10.3390/s23135941) |
| 33 | CIRCL Forensics Exercises | Disco/Memória | 2023 | Post oficial do Digital Corpora, datado de 2023-05-05 |
| 37 | ADFIR forensic dataset | (sem categoria) | 2026 | Mendeley Data: publicado em 2026-01-02, DOI [10.17632/65g9gm8zrd.1](https://doi.org/10.17632/65g9gm8zrd.1) |

### 1.2 Ano não determinado (2 registros)

| # | Base | Motivo |
|---|---|---|
| 24 | NIST CFReDS | É portal, não uma base única: agrega datasets de anos diferentes. Não existe "ano do CFReDS" |
| 35 | IoT-CAD Dataset | Página do CFReDS protegida por desafio Cloudflare; a data de depósito não aparece no HTML acessível |

**Leitura prática.** A planilha é majoritariamente um retrato da geração 2009-2020 de bases forenses. Apenas 4 registros são posteriores a 2020, e dois deles (CIC-IoT2023 e CIC-MalMem-2022) vêm do CIC/UNB, laboratório que também responde por 5 dos registros antigos (NSL-KDD, CIC-IDS2017, CSE-CIC-IDS2018, CIC-AndMal2017 e CIC-Darknet2020). O laboratório aparece, portanto, em 7 dos 37 registros, concentração que a aba `Síntese` registra apenas em parte.

---

## 2. Links: estado atual e versões mais recentes

### 2.1 Links da planilha que respondem (32 de 37)

Todos retornaram HTTP 200 na verificação de 2026-09-23. Os 37 links foram testados individualmente.

### 2.2 Links quebrados e substitutos

| # | Base | Link na planilha | Status | Substituto verificado |
|---|---|---|---|---|
| 15 | Drebin | `sec.cs.tu-bs.de/~danarp/drebin/` | inacessível (sem resposta) | DOI do artigo fundador: [10.14722/ndss.2014.23247](https://doi.org/10.14722/ndss.2014.23247). O dataset em si é de acesso por solicitação |
| 19 | CASIA | `forensics.idealtest.org` | inacessível (sem resposta) | Ground truth do CASIA v2.0: [github.com/namtpham/casia2groundtruth](https://github.com/namtpham/casia2groundtruth) |
| 21 | Dresden Image Database | `forensics.inf.tu-dresden.de/ddimgdb` | inacessível (o domínio inteiro não responde) | Não há espelho equivalente. Alternativa mais recente para o mesmo problema: Forchheim Image Database (2021), DOI [10.1007/978-3-030-68780-9_40](https://doi.org/10.1007/978-3-030-68780-9_40) |
| 16 | Malimg | link do Kaggle | não verificável (ver §2.4) | DOI do artigo fundador: [10.1145/2016904.2016908](https://doi.org/10.1145/2016904.2016908) |
| 36 | CIC-Darknet2020 | link do Kaggle | não verificável (ver §2.4) | Página oficial do CIC: [unb.ca/cic/datasets/darknet2020.html](https://www.unb.ca/cic/datasets/darknet2020.html) |

### 2.3 Links que funcionam mas apontam para o lugar errado

| # | Base | Link na planilha | Link correto |
|---|---|---|---|
| 33 | CIRCL Forensics Exercises | `digitalcorpora.org/?p=overview` (página genérica) | [digitalcorpora.org/2023/05/05/circl-forensics-exercises/](https://digitalcorpora.org/2023/05/05/circl-forensics-exercises/) |
| 26 | Digital Corpora — M57-Patents | `digitalcorpora.org` (raiz do portal) | [digitalcorpora.org/corpora/scenarios/m57-patents-scenario](https://digitalcorpora.org/corpora/scenarios/m57-patents-scenario) |
| 30 | NPS-2009-domexusers | página agregadora de imagens de disco | Não localizei página dedicada; o agregador [digitalcorpora.org/corpora/disk-images/](https://digitalcorpora.org/corpora/disk-images/) é o link mais específico disponível |

### 2.4 Ressalva importante sobre os links do Kaggle

O Kaggle responde **HTTP 200 até para endereço inexistente** (serve uma página de verificação reCAPTCHA). Testei um slug inventado e ele também retornou 200. Consequência direta: **não é possível confirmar nem refutar por HTTP** se os links de Kaggle da planilha (Malimg e CIC-Darknet2020) estão válidos. Uma checagem por HEAD sugeriu 404 para ambos, mas o método é inconsistente para esse domínio. Os dois precisam de conferência manual no navegador.

### 2.5 Bases com versão mais recente disponível

| # | Base na planilha | Versão mais recente | Link | Evidência |
|---|---|---|---|---|
| 14 | EMBER (2018) | **EMBER2024** | [github.com/FutureComputing4AI/EMBER2024](https://github.com/FutureComputing4AI/EMBER2024) | Artigo KDD 2025, DOI [10.1145/3711896.3737431](https://doi.org/10.1145/3711896.3737431), autoria Joyce, Miller, Roth, Zak, Zaresky-Williams, Anderson, Raff, Holt |
| 18 | CIC-AndMal2017 | **AndMal 2020** e **MalDroid 2020** | [andmal2020.html](https://www.unb.ca/cic/datasets/andmal2020.html) · [maldroid-2020.html](https://www.unb.ca/cic/datasets/maldroid-2020.html) | Títulos das páginas oficiais do CIC/UNB verificados |
| 7 | CIC-IoT2023 | Geração 2024-2025 do mesmo lab: **IIoT 2024**, **IIoT 2025**, **IoMT 2024**, **IoV 2024**, **IoT-DIAD 2024**, **EVSE 2024**, **Tabular IoT Attack 2024**, **SBAN 2025**, **CIC-DGG 2025** | [iiot-dataset-2025](https://www.unb.ca/cic/datasets/iiot-dataset-2025.html) · [iomt-dataset-2024](https://www.unb.ca/cic/datasets/iomt-dataset-2024.html) · [iov-dataset-2024](https://www.unb.ca/cic/datasets/iov-dataset-2024.html) · [iot-diad-2024](https://www.unb.ca/cic/datasets/iot-diad-2024.html) · [evse-dataset-2024](https://www.unb.ca/cic/datasets/evse-dataset-2024.html) · [tabular-iot-attack-2024](https://www.unb.ca/cic/datasets/tabular-iot-attack-2024.html) · [sban-dataset-2025](https://www.unb.ca/cic/datasets/sban-dataset-2025.html) · [cic-dgg-2025](https://www.unb.ca/cic/datasets/cic-dgg-2025.html) | Índice oficial de datasets do CIC/UNB e títulos das páginas |
| 3 | UNSW-NB15 | **UNSW-NB15 Augmented Dataset** (do CIC) e **Enriched Dataset** | [cic-unsw-nb15.html](https://www.unb.ca/cic/datasets/cic-unsw-nb15.html) · [enricheddataset.html](https://www.unb.ca/cic/datasets/enricheddataset.html) | Títulos das páginas oficiais do CIC/UNB |
| 10 | IoT-23 | Cópia com DOI citável (a planilha só traz a página do laboratório) | DOI [10.5281/zenodo.4743746](https://doi.org/10.5281/zenodo.4743746) | Registro no Zenodo, 2020, autores García, Parmisano e Erquiaga |
| 21 | Dresden Image Database | **Forchheim Image Database** (2021), do mesmo grupo de Dresden | DOI [10.1007/978-3-030-68780-9_40](https://doi.org/10.1007/978-3-030-68780-9_40) | Hadwiger & Rieß, LNCS 2021. Página do dataset no domínio de Dresden está fora do ar daqui |
| 38 | DARPA Transparent Computing | Repositório oficial do programa + cópia processada do engagement E3 | [github.com/darpa-i2o/Transparent-Computing](https://github.com/darpa-i2o/Transparent-Computing) · DOI [10.5281/zenodo.18391065](https://doi.org/10.5281/zenodo.18391065) | Repositório GitHub verificado; cópia Zenodo dos logs E3 (Cadets, Fivedirections, Theia, Trace) |
| 19 | CASIA | Versões mais recentes para o mesmo problema | **DEFACTO** (2019, já na planilha) e **IMD2020** (2020) | IMD2020: Novozamsky, Mahdian e Saic, 2020. **Link oficial do IMD2020 não respondeu daqui**, portanto tratar como não verificado |
| 2 | NSL-KDD | Bases que substituem o NSL-KDD na prática | **CIC-IDS2017** e **CSE-CIC-IDS2018** (ambas já na planilha) | A aba `Síntese` já registra que o NSL-KDD deriva de capturas de 1998 |

**Observação de contexto que a planilha não tem:** o repositório `elastic/ember` está marcado como **arquivado** no GitHub, com último push em 2024-11-22. Isso é consistente com a migração da linha EMBER para o repositório do EMBER2024 e vale como sinal para quem for usar a base.

---

## 3. Natureza de cada registro

Nem todos os 37 registros são datasets. A distinção importa para citação e para reprodutibilidade.

| Natureza | Quantidade | Registros |
|---|---|---|
| Dataset primário (uma base, autocontida) | 24 | 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 28, 30, 36 |
| Corpus ou cenário composto (dataset multi-fonte) | 4 | 26 (M57-Patents), 29 (Real Data Corpus), 31 (Lone Wolf), 37 (ADFIR) |
| Portais e agregadores (não são dataset) | 3 | 24 (NIST CFReDS), 27 (DFRWS Forensic Challenges), 35 (IoT-CAD, hospedado no CFReDS) |
| Repositório de datasets (coleção) | 2 | 32 (OTRF/Mordor), 38 (DARPA Transparent Computing) |
| Ferramenta ou gerador (não é dataset) | 1 | 13 (IoT-Flock) |
| Material didático (não é dataset de pesquisa) | 1 | 33 (CIRCL Forensics Exercises) |
| Conjunto de referência (dataset de hashes) | 1 | 25 (NIST NSRL/RDS) |
| Corpus de texto (dataset de outra área) | 1 | 34 (Enron) |

### 3.1 Detalhamento dos casos ambíguos

**NIST CFReDS (24).** É portal. A descrição na própria planilha já diz "portal-gateway". O registro certo não é "um dataset" e sim "o repositório onde datasets como o IoT-CAD ficam hospedados". Isso cria uma duplicação estrutural com o registro 35, que É um dataset mas mora no CFReDS.

**DFRWS Forensic Challenges (27).** É uma série anual de desafios, um por edição, com tema diferente a cada ano (memória, mobile, IoT, ICS/PLC). Não é um dataset. Quem cita "o desafio do DFRWS" precisa dizer o ano.

**OTRF/Mordor (32).** É um repositório que reúne vários datasets pré-gravados de logs de ataque em JSON/PCAP, mapeados ao MITRE ATT&CK. Funciona como fonte de vários datasets, não como um dataset.

**DARPA Transparent Computing (38).** É o programa, e o que se usa em pesquisa são os pacotes de engagement (Cadets, Fivedirections, Theia, Trace). A planilha aponta para uma pasta do Google Drive; o repositório oficial do programa é a referência mais estável.

**IoT-CAD (35).** É dataset, mas está classificado na planilha sob o guarda-chuva do CFReDS. A categoria "IoT" está correta; o link é que aponta para dentro do portal.

**NIST NSRL/RDS (25).** É dataset, mas de natureza diferente: uma coleção de hashes de software conhecido, para filtrar arquivos *known good/bad*. Não serve para classificação supervisionada, e sim para redução de dados. A aba `Síntese` já faz essa ressalva corretamente.

**Enron (34).** É dataset, e a própria aba `Síntese` registra que a maior parte da literatura que o cita é de PLN geral, não de forense. Vale manter a ressalva.

**Real Data Corpus (29).** É corpus, com sub-corpora (Non-US, US Persons, Releasable, Realistic) e acesso condicionado a aprovação de IRB. Isso o distingue dos datasets de download livre.

**CIC-Darknet2020 (36).** É dataset primário: uma captura de tráfego de darknet com rótulos de classe. Está corretamente categorizado em Rede/Tráfego. O único ponto de atenção é o nome, que remete à família de capturas do CIC e pode ser confundido com uma versão de outro dataset.

---

## 4. Inconsistências na planilha, para edição manual

Não alterei nada. Estas são as divergências que encontrei entre o que a planilha afirma e o que as fontes primárias mostram.

| # | Registro | O que a planilha diz | O que a fonte primária mostra |
|---|---|---|---|
| 26 | Digital Corpora — M57-Patents | "Autores: Woods, Lee, Garfinkel, Dittrich et al. (ADFSL 2011)" | A página oficial data o cenário como "2009 M57-Patents Scenario"; o paper de referência das corpora é Garfinkel et al., DFRWS 2009, DOI [10.1016/j.diin.2009.06.016](https://doi.org/10.1016/j.diin.2009.06.016) |
| 33 | CIRCL Forensics Exercises | Link `digitalcorpora.org/?p=overview` | O post real é de 2023-05-05 e tem URL própria (ver §2.3) |
| 19 | CASIA | Link `forensics.idealtest.org` | Endereço fora do ar; falta um link alternativo na planilha |
| 21 | Dresden Image Database | Link `forensics.inf.tu-dresden.de/ddimgdb` | Endereço fora do ar; falta alternativa |
| 15 | Drebin | Link `sec.cs.tu-bs.de/~danarp/drebin/` | Endereço fora do ar; a planilha já registra que o acesso é restrito, mas o link não funciona |
| 24 e 35 | NIST CFReDS e IoT-CAD | Ambos tratados como bases distintas | CFReDS é portal e IoT-CAD é dataset hospedado nele; convém marcar a relação para não parecerem duplicatas nem pares |
| 3, 18 | UNSW-NB15 e CIC-AndMal2017 | Sem menção a versões posteriores | Existem UNSW-NB15 Augmented, AndMal 2020 e MalDroid 2020 (ver §2.5) |
| 14 | EMBER | Link para `elastic/ember` | Repositório arquivado desde 2024-11-22; a linha ativa é o EMBER2024 |
| 11, 15, 16, 23 | MQTT-IoT-IDS2020, Drebin, Malimg, CoMoFoD | Sem DOI | Tenho DOI para Drebin e Malimg; **não localizei DOI para CoMoFoD** na Crossref, e não preenchi por suposição |
| 7 | CIC-IoT2023 | "Artigo: Neto et al., Sensors 2023" | Confirmado: DOI [10.3390/s23135941](https://doi.org/10.3390/s23135941). Pode ser acrescentado ao lado do link |
| 24 | NIST NSRL / RDS | "desde 2023 em SQLite (RDSv3)" | Não consegui confirmar a data exata do RDSv3 na página do NIST, que lista 2000, 2016, 2017 e 2026. Tratar 2023 como afirmação da planilha, não como fato verificado |

### 4.1 Registros sem categoria

Os registros **37 (ADFIR)** e **38 (DARPA Transparent Computing)** estão com a coluna "Categoria" vazia, e a aba `Síntese` já os agrupa como "sem categoria na planilha original". Sugestão de classificação com base no conteúdo:

- **ADFIR (37):** Disco/Memória — o conteúdo é simulação de técnicas de ataque mais artefatos de NTFS extraídos de imagens de disco.
- **DARPA TC (38):** Rede/Disco híbrido — são logs de proveniência de sistema, usados tanto para detecção de APT quanto para investigação de host.

---

## 5. Metodologia e limitações

### 5.1 O que foi feito

- Leitura integral das três abas da planilha (37 registros, colunas A a Q, incluindo os hyperlinks das colunas N, O e P).
- Teste individual de HTTP dos 37 links da coluna E.
- Verificação de DOI e ano de fundação das bases na Crossref e na OpenAlex, por busca de título.
- Verificação de datas de criação e última atualização de repositórios pela API oficial do GitHub.
- Leitura de páginas oficiais (CIC/UNB, NIST, Digital Corpora, DFRWS, Mendeley, Zenodo) para extrair nomes e datas.
- Busca de versões posteriores para as bases com linhagem conhecida.

### 5.2 Limitações declaradas

1. **Kaggle não é verificável por HTTP.** Ver §2.4. Os dois links de Kaggle da planilha ficaram como não verificados, não como quebrados.
2. **Três domínios estavam inacessíveis deste ambiente**: `sec.cs.tu-bs.de` (Drebin), `forensics.idealtest.org` (CASIA) e `forensics.inf.tu-dresden.de` (Dresden, incluindo o Forchheim). Não sei distinguir entre host desativado e bloqueio de rede local. Recomendo conferir no navegador antes de remover esses links da planilha.
3. **O CFReDS está atrás de proteção Cloudflare**, o que impediu ler a data de depósito do IoT-CAD.
4. **Não consegui DOI para CoMoFoD** (ELMAR 2013) nem para CSE-CIC-IDS2018 nem para M57-Patents, Real Data Corpus e Govdocs1 isoladamente. Nesses casos a evidência usada é o paper-pai (Garfinkel et al. 2009) ou a página oficial.
5. **Verificação de ano, não de conteúdo.** Não abri imagens de disco, PCAPs ou corpora. Os números de volume citados na planilha (ex.: 46.686.579 amostras do CIC-IoT2023) não foram conferidos.
6. **Não verifiquei a coluna L** (contagem de repositórios no GitHub) nem as estimativas das colunas K e M. A aba `Meotodologia` já documenta que K e M são faixas estimadas e que L tem inflação por siglas ambíguas.
7. **A classificação da seção 3 é minha**, derivada das descrições da planilha e do conteúdo real das páginas. Onde é julgamento e não fato, isso está dito no texto.

---

## 6. Fontes primárias citadas

Todos os DOIs abaixo foram resolvidos na Crossref ou na OpenAlex em 2026-09-23.

| Uso | Referência | DOI |
|---|---|---|
| NSL-KDD, ano | Tavallaee et al., CISDA 2009 | [10.1109/cisda.2009.5356528](https://doi.org/10.1109/cisda.2009.5356528) |
| UNSW-NB15, ano | Moustafa & Slay, MilCIS 2015 | [10.1109/milcis.2015.7348942](https://doi.org/10.1109/milcis.2015.7348942) |
| CIC-IDS2017, ano | Sharafaldin et al., ICISSP 2018 | [10.5220/0006639801080116](https://doi.org/10.5220/0006639801080116) |
| CTU-13, ano | García et al., Computers & Security 2014 | [10.1016/j.cose.2014.05.011](https://doi.org/10.1016/j.cose.2014.05.011) |
| CIC-IoT2023, ano | Neto et al., Sensors 2023 | [10.3390/s23135941](https://doi.org/10.3390/s23135941) |
| Bot-IoT, ano | Koroniotis et al., FGCS 2019 | [10.1016/j.future.2019.05.041](https://doi.org/10.1016/j.future.2019.05.041) |
| TON_IoT, ano | Moustafa et al., IEEE Access 2020 | [10.1109/access.2020.3022862](https://doi.org/10.1109/access.2020.3022862) |
| IoT-23, ano | García, Parmisano, Erquiaga, Zenodo 2020 | [10.5281/zenodo.4743746](https://doi.org/10.5281/zenodo.4743746) |
| MedBIoT, ano | Guerra-Manzanares et al., ICISSP 2020 | [10.5220/0009187802070218](https://doi.org/10.5220/0009187802070218) |
| IoT-Flock, ano | Repositório GitHub criado em 2020-03-04 | [10.21203/rs.3.rs-20786/v1](https://doi.org/10.21203/rs.3.rs-20786/v1) |
| EMBER, ano | Anderson & Roth, 2018 | [arXiv:1804.04637](https://arxiv.org/abs/1804.04637) |
| EMBER2024 | Joyce et al., KDD 2025 | [10.1145/3711896.3737431](https://doi.org/10.1145/3711896.3737431) |
| Drebin, ano | Arp et al., NDSS 2014 | [10.14722/ndss.2014.23247](https://doi.org/10.14722/ndss.2014.23247) |
| Malimg, ano | Nataraj et al., VizSec 2011 | [10.1145/2016904.2016908](https://doi.org/10.1145/2016904.2016908) |
| CIC-AndMal2017, ano | Lashkari et al., ICCST 2018 | [10.1109/ccst.2018.8585560](https://doi.org/10.1109/ccst.2018.8585560) |
| CASIA, ano | Dong, Wang, Tan, ChinaSIP 2013 | [10.1109/chinasip.2013.6625374](https://doi.org/10.1109/chinasip.2013.6625374) |
| RAISE, ano | Dang-Nguyen et al., MMSys 2015 | [10.1145/2713168.2713194](https://doi.org/10.1145/2713168.2713194) |
| Dresden, ano | Gloe & Böhme, ACM SAC 2010 | [10.1145/1774088.1774427](https://doi.org/10.1145/1774088.1774427) |
| Forchheim, versão mais recente | Hadwiger & Rieß, LNCS 2021 | [10.1007/978-3-030-68780-9_40](https://doi.org/10.1007/978-3-030-68780-9_40) |
| DEFACTO, ano | Mahfoudi et al., EUSIPCO 2019 | [10.23919/eusipco.2019.8903181](https://doi.org/10.23919/eusipco.2019.8903181) |
| CIC-MalMem-2022, ano | Carrier et al., ICISSP 2022 | [10.5220/0010908200003120](https://doi.org/10.5220/0010908200003120) |
| Corpora forenses (M57-Patents, Real Data Corpus, Govdocs1) | Garfinkel et al., DFRWS 2009 | [10.1016/j.diin.2009.06.016](https://doi.org/10.1016/j.diin.2009.06.016) |
| ADFIR, ano | Mendeley Data, 2026-01-02 | [10.17632/65g9gm8zrd.1](https://doi.org/10.17632/65g9gm8zrd.1) |
| DARPA TC E3, cópia processada | Zenodo | [10.5281/zenodo.18391065](https://doi.org/10.5281/zenodo.18391065) |

**Sem DOI localizado:** CoMoFoD (Tralić, Zupancic, Grgić, Grgić, ELMAR 2013) e CSE-CIC-IDS2018. Não preenchi DOI por suposição em nenhum dos dois.
