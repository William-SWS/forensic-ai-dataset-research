# 02 Download e integridade das bases de porte "ok"

**Status:** parcial. Loghub e CoMoFoD feitos e verificados; **CIC-MalMem-2022 pendente** (arquivos recebidos incompletos).
**Retroativo:** escrito depois do trabalho (decisão 22).
**Depende de:** 01 (ambiente) para as verificações em Python; os downloads em si não dependem.

## Por que

Cada EDA precisa de uma **base bruta** íntegra em `data/raw/<base>/`, com tamanho e hash medidos. As bases do projeto têm acesso diferente: Loghub e CoMoFoD têm download direto; CIC-MalMem-2022 exige formulário de cadastro, então vale o **fallback de acesso**: o usuário baixa.

## Escopo

- Baixar (ou receber do usuário) as três bases e conferir tamanho e hash publicado, quando houver.
- Registrar o tamanho medido, no lugar das estimativas "NÃO VERIFICADO".

## Fora do escopo

- Extração e análise (tickets 05, 06, 04).
- Baixar a base grande (ticket 03).

## Critérios de aceite

- [x] **Loghub HDFS_v1:** `data/raw/loghub/HDFS_v1.zip` com 186.645.559 bytes e MD5 `76a24b4d9a6164d543fb275f89773260`, igual ao publicado no Zenodo (10.5281/zenodo.8196385); `unzip -t` sem erros.
- [x] **Loghub BGL:** `data/raw/loghub/BGL.zip` com 57.489.019 bytes e MD5 `4452953c470f2d95fcb32d5f6e733f7a`, igual ao publicado; `unzip -t` sem erros.
- [x] **CoMoFoD Small:** `data/raw/comofod/comofod_small.rar` com 3.213.318.957 bytes, igual ao tamanho informado pelo servidor; SHA256 `6ea6a5e9788f02838f5992cb192b9404f5c64e1980551c31985f4afd87d401e9`. A listagem do `unrar l` mostra 10.403 entradas e a extração para `data/interim/comofod/` produziu 10.402 arquivos. O *release agreement* foi lido e aceito pelo usuário (decisão 16).
- [ ] **CIC-MalMem-2022:** o arquivo principal (a base completa, 58.596 registros) está ausente. A pasta `data/raw/cic-malmen-2022/` tem 3 arquivos (`Output1.csv`, `output2.csv`, `output3.csv`) com 850 linhas no total, todas `Spyware-TIBS`, 56 colunas (`Filename` mais 55 features), sem benignos e sem coluna de rótulo. O usuário precisa baixar o arquivo principal em `http://cicresearch.ca/CICDataset/CICMalMem2022/` (formulário). Quando chegar: medir tamanho, contar linhas e confirmar 58.596.
- [ ] Renomear ou mover a pasta `cic-malmen-2022` (typo de "MalMem") ou documentar o nome como está. Decisão do usuário.
- [x] `data/raw/` não é versionado (`.gitignore`).

## Notas

- A página do CIC pede nome, e-mail, organização e país. O agente não preenche o formulário com dados pessoais do usuário.
- A tentativa de leitura do HDFS_v1 caiu uma vez no meio do download (curl 56) e foi retomada com `-C -`; o MD5 final conferiu.
