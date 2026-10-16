# 06-04 CoMoFoD: baseline com divisão por cena e controle de vazamento

**Status:** concluído (com emenda: ver 06-06)
**Notebook:** `notebooks/02_eda_comofod.ipynb`, seção 4
**Depende de:** 06-01

## Por que

A base tem 10.400 arquivos e 200 cenas (a premissa original era que as cenas fossem independentes; **isso se mostrou falso**, ver 06-06 e o Resultado): cada cena gera 50 imagens classificáveis (a original, a falsificada e 24 variantes de cada). Uma divisão aleatória por imagem põe variantes da mesma cena em treino e teste e infla qualquer métrica. O **baseline** deste ticket dá um número de referência honesto para a **viabilidade de IA**, medido com a divisão correta e comparado com a divisão ingênua.

## O que fazer

- Montar o conjunto classificável: imagens `O` e `F` (base mais 24 variantes de cada), com **rótulo** autêntica ou falsificada. As máscaras `B` e `M` não entram.
- Extrair 12 características globais simples por imagem: média e desvio por canal RGB, variância do laplaciano, energia de gradiente em x e em y, razão de alta frequência (FFT), média e desvio em tons de cinza.
- Treinar RandomForest e regressão logística com `GroupKFold` de 5 dobras **agrupando por cena**.
- Rodar dois controles: (i) só as 400 imagens-base, sem variantes; (ii) divisão aleatória por imagem (`StratifiedKFold`), para mostrar o tamanho do vazamento.

## Fora do escopo

- Localização em nível de pixel, redes convolucionais, ELA, detectores copy-move clássicos. Isso exige GPU e outro desenho; fica registrado como próximo passo.
- Ajuste de hiperparâmetros.

## Critérios de aceite

- [x] O notebook imprime o número de imagens classificáveis por rótulo e o número de cenas independentes (esperado: 10.000 imagens, 5.000 por rótulo, 200 cenas; confirmar com a medição).
- [x] Há uma verificação visível (`assert`) de que, em cada dobra do `GroupKFold`, nenhuma cena aparece ao mesmo tempo em treino e teste.
- [x] A saída traz AUC e acurácia para: divisão por cena (RandomForest e regressão logística), só imagens-base, e divisão aleatória por imagem.
- [x] O resultado é reportado **como saiu**, inclusive se ficar próximo do acaso (AUC perto de 0,5). Não se ajusta o desenho para melhorar o número.
- [x] Um parágrafo interpreta a diferença entre divisão por cena e aleatória (tamanho do vazamento) e diz o que o resultado implica para a viabilidade.

## Notas

- **Hipótese a testar, não resultado:** como `F` é a mesma cena que `O` com uma região copiada, características globais provavelmente não separam as classes, e a divisão aleatória por imagem pode parecer boa por vazamento. Só vale como conclusão depois da medição.
- ~~Correção pendente no rascunho~~ **Feita:** o texto diz 12 características e o `print` sem função foi trocado por `(imagens, características)`.
- Memória: 10.000 imagens de 512x512 não cabem em RAM de uma vez se forem todas carregadas; o rascunho calcula as características uma imagem por vez.

## Resultado (2026-10-15)

- 10.000 imagens classificáveis (5.000 por rótulo), 200 cenas, 12 características. O `assert` de que nenhum grupo cai em treino e teste ao mesmo tempo está ativo.
- **O desenho "por cena" não bastava**: as 200 cenas vêm de 41 fotografias (ticket 06-06). O baseline foi então medido em três divisões, média de 5 sorteios:

| Divisão | RandomForest (AUC) | Regressão logística (AUC) |
|---|---|---|
| por imagem | 0,984 | 0,502 |
| por cena | 0,967 | 0,521 |
| por fotografia | 0,495 | 0,510 |

- Nenhuma característica sozinha separa as classes (AUC de 0,49 a 0,51). Com as 400 imagens-base, por fotografia: AUC 0,50.
- A hipótese de partida ("perto do acaso") estava certa só para a divisão correta; com divisão por cena o resultado parece bom (0,967) por memorização das fotografias. O mecanismo é a explicação compatível com os dados, não foi testado diretamente.
