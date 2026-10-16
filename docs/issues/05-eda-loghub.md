# 05 EDA do Loghub (HDFS_v1 e BGL)

**Status:** concluído, com ressalvas listadas nas notas.
**Retroativo:** escrito depois do trabalho (decisão 22). O notebook `notebooks/01_eda_loghub.ipynb` foi mantido.
**Depende de:** 01 (ambiente) e 02 (download do Loghub)

## Por que

O Loghub é a base de porte "ok" do nicho de logs de sistema. A **viabilidade de IA** depende de rótulos confiáveis, balanceamento, duplicatas, vazamento e de um **baseline** com divisão correta.

## Escopo

- HDFS_v1: rótulo por trace; BGL: rótulo por mensagem.
- Perfil dos logs brutos sem carregá-los inteiros na RAM (DuckDB).
- Baseline com scikit-learn e veredito.

## Fora do escopo

- Parser de logs de alta qualidade (Drain); ajuste de hiperparâmetros; modelos profundos.

## Critérios de aceite

- [x] O notebook roda do zero sem erro (`jupyter nbconvert --execute`, 0 células com erro), em cerca de 1,5 min.
- [x] HDFS: 575.061 traces, 2,93% de anomalias (33,2:1); rótulo da matriz de eventos e de `anomaly_label.csv` coincidem em 100% dos traces.
- [x] HDFS: 589 vetores distintos (0,10%); um vetor cobre 52,2% dos traces; 9 vetores com rótulos conflitantes cobrem 550 traces. O notebook confere o hash com `drop_duplicates` (`assert`).
- [x] HDFS: baseline com dois cenários. Divisão aleatória (a): F1 0,979 (regressão logística) e 0,999 (random forest), com 100% dos vetores do teste vistos no treino. Padrões novos (b): F1 médio 0,952 e 0,968, em 5 sorteios, com teste de 2.263 a 2.704 traces.
- [x] BGL: 4.747.963 linhas e 348.460 alertas (7,34%) em 41 categorias, de 2005-06-03 a 2006-01-04, iguais aos números da documentação.
- [x] BGL: parse irregular quantificado (34.786 linhas, 0,73%); templates aproximados por troca de dígitos.
- [x] BGL: lookup cronológico de templates alerta pega 55,86% dos alertas dos 30% finais (48.060 de 86.033); a regra `nível = FATAL` tem recall 99,98% e precisão 40,76%.
- [x] BGL: baseline por janela de 100 linhas, divisão cronológica 70/30: random forest com F1 0,72 e PR-AUC 0,67; regressão logística com F1 0,66.
- [x] O veredito de viabilidade está na seção 3 do notebook, com números das saídas e hipóteses marcadas como tal.
- [ ] O resultado entrou no datasheet do Loghub (ticket 07, ainda não escrito).

## Notas

- **Revisão durante o trabalho:** a primeira versão do notebook tinha um baseline por janela fraco (F1 0,39 a 0,57) por usar só 40 templates, e um cenário (b) instável. Foram corrigidos antes do veredito (300 templates escolhidos só no período de treino; padrões raros divididos por grupo). O notebook final reflete a versão corrigida.
- **Risco de circularidade (hipótese, não testada):** o rótulo do HDFS vem de regras manuais (README) e 12 dos 29 eventos só aparecem em anomalias.
- **Memória:** o pico de RAM não foi medido. O notebook limita o DuckDB a 3 GB.
- O notebook gera `data/interim/loghub/loghub.duckdb` (ignorado pelo git).
- **Tamanhos em `data/interim/loghub/`:** HDFS.log 1,58 GB, BGL.log 0,74 GB.
