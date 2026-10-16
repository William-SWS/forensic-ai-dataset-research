# 06-06 CoMoFoD: fotografias reaproveitadas entre cenas e vazamento por fotografia

**Status:** concluído
**Notebook:** `notebooks/02_eda_comofod.ipynb`, seção 4.1
**Depende de:** 06-01
**Origem:** ticket **emergente**, criado durante a execução do 06-04, quando um random forest com divisão por cena chegou a AUC 0,95 enquanto a regressão logística e cada característica isolada ficavam em 0,5. O `readme.txt` repete as mesmas áreas de região copiada em categorias diferentes.

## Por que

A unidade de divisão treino/teste precisa ser a **unidade independente** da base. O `readme.txt` e a estrutura de arquivos sugerem 200 cenas, mas se a mesma fotografia for reaproveitada em várias cenas, dividir por cena ainda vaza e infla qualquer métrica.

## O que fazer

- Comparar as 200 imagens originais (`O`) por correlação de miniaturas 32x32 em tons de cinza e agrupar as que são a mesma fotografia.
- Testar a sensibilidade ao limiar de agrupamento.
- Repetir o baseline agrupando por fotografia.

## Fora do escopo

- Identificar a origem das fotografias ou confirmar com os autores.
- Um método de deduplicação mais sofisticado (hashes perceptuais, features de rede).

## Critérios de aceite

- [x] O notebook informa o número de fotografias distintas e o tamanho dos grupos, com sensibilidade a pelo menos 3 limiares.
- [x] O baseline por fotografia está na tabela da seção 4.2, ao lado das divisões por imagem e por cena, com `assert` de que nenhuma fotografia aparece em treino e teste.
- [x] O veredito (06-05) usa a fotografia, não a cena, como unidade independente.

## Resultado (2026-10-15)

- **41 fotografias distintas** nos limiares 0,90, 0,95 e 0,98 (resultado igual). Cenas por fotografia: mínimo 1, mediana 4, máximo 13; 37 das 41 usadas em mais de uma cena; 8 aparecem nas 5 categorias de manipulação.
- Baseline com random forest: AUC 0,984 por imagem, 0,967 por cena e **0,495 por fotografia**.
- Limitação: o agrupamento por miniaturas é simples; não foi validado por inspeção manual dos grupos nem contra uma verdade conhecida.
