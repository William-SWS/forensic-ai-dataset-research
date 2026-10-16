# 03 CIC-IoT2023: download da base grande e medição de tamanho

**Status:** parcial e **bloqueado por decisão do usuário** (qual pasta baixar e tamanho total).
**Retroativo:** escrito depois do trabalho (decisão 22).
**Depende de:** 01 (ambiente)
**Bloqueia:** o roteiro da base grande (conversão para Parquet e benchmark de ferramentas)

## Por que

A **base grande** é a razão de existir o estudo de processamento distribuído. Antes de qualquer benchmark é preciso saber qual versão dos CSVs é a certa, quanto pesa e se cabe no disco (89 GB livres; regra do projeto: se passar de ~40 GB, perguntar ao usuário).

## Escopo

- Receber do usuário os arquivos baixados (a página exige formulário de cadastro).
- Entender a estrutura: `CSV/CSV/<ataque>/` versus `MERGED_CSV`.
- Medir o tamanho total e aplicar a regra dos 40 GB.

## Fora do escopo

- Os PCAP (decisão 9).
- A conversão para Parquet e o benchmark (tickets futuros).

## Critérios de aceite

- [x] 4 CSVs por ataque recebidos em `data/raw/cic-iot2023/`: `DoS-HTTP_Flood.pcap.csv` (40.686 linhas), `DoS-HTTP_Flood1.pcap.csv` (31.175), `DDoS-HTTP_Flood-.pcap.csv` (28.790) e `DictionaryBruteForce.pcap.csv` (13.064), mais o `README_CSV.pdf`.
- [x] Esquema verificado: 39 colunas idênticas nos 4 arquivos, **sem coluna `label`** (a página oficial lista 46 features). Registrado em `docs/cic-iot2023-arquivos-csv.md` e na decisão 19.
- [x] Sobreposição entre `DoS-HTTP_Flood` e `DoS-HTTP_Flood1` medida: 42 linhas idênticas (de 40.662 e 30.869 linhas únicas).
- [ ] **Pendente (usuário):** decidir e baixar o `MERGED_CSV` (ou parte dele). O `README_CSV.pdf` descreve um conjunto "combined and shuffled" com `label`, o que provavelmente é o MERGED; isso não está confirmado. O PDF traz dois números sobrepostos de arquivos (309 e 169).
- [ ] **Pendente:** o tamanho total em GB do CSV completo (das pastas `CSV` e `MERGED_CSV`) está **não verificado**. A listagem da página não mostra tamanhos.
- [ ] **Pendente:** número total de linhas medido, para comparar com os 46.686.579 declarados na planilha.
- [ ] **Pendente:** se o total passar de ~40 GB, decisão do usuário sobre usar um subconjunto de arquivos.

## Notas

- Uma pesquisa pública não achou documentação do `MERGED_CSV`, e dois números de artigos (449 milhões de amostras com 39 features, 46,7 milhões) não concordam entre si; nenhum foi adotado.
- Os zips (`CSV.zip`, `MERGED_CSV.zip`) exigem o dobro de espaço durante a extração.
