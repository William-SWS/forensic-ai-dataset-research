# 01 Ambiente de análise (uv, bibliotecas, Spark via Docker)

**Status:** parcial. A parte Python está feita; **Spark via Docker está pendente.**
**Retroativo:** este ticket foi escrito depois do trabalho (decisão 22). Os itens marcados foram verificados; nada foi marcado por suposição.
**Depende de:** nada

## Por que

Todas as EDAs e o benchmark de ferramentas da base grande precisam de um ambiente reproduzível. O projeto compara pandas, DuckDB, Polars e Spark local, e a máquina tem 16 GB de RAM (~4 GB livres), sem Java instalado.

## Escopo

- Projeto `uv` na raiz com as bibliotecas de análise e Jupyter.
- `.gitignore` que mantém dados e ambiente fora do git.
- Spark local via Docker, já que não há JDK no host (decisão 12b, confirmada na 15).

## Fora do escopo

- Qualquer análise de dados (tickets 05 e 06).
- Instalar Java no sistema.

## Critérios de aceite

- [x] `uv sync`/`uv run` funciona e `pyproject.toml` declara: pandas, DuckDB, Polars, pyarrow, scikit-learn, matplotlib, seaborn, pillow, Jupyter, nbconvert, ipykernel, nbformat. Versões resolvidas hoje: Python 3.13.15, pandas 3.0.6, DuckDB 1.5.6, Polars 2.0.0, scikit-learn 1.9.1.
- [x] `uv run jupyter nbconvert --to notebook --execute` executa o notebook `01_eda_loghub.ipynb` sem erro (0 células com erro na saída).
- [x] `.gitignore` contém `data/raw/`, `data/interim/`, `.venv/`, `__pycache__/` e `.ipynb_checkpoints/`.
- [ ] **Pendente:** um contêiner Docker com Spark executa `spark.range(10).count()` e devolve 10. O Docker está disponível (servidor 29.8.2); a imagem ainda não foi escolhida nem testada.
- [ ] **Pendente:** o comando para subir o contêiner e para abrir o PySpark está documentado em `AGENTS.md` na seção de comandos que funcionam.

## Notas

- **Correção:** a decisão 18 diz "Python 3.12". O ambiente criado usa **Python 3.13.15**: `uv init --python 3.12` fixou `requires-python = ">=3.12"`, e o `uv` resolveu 3.13. Não existe `.python-version`. Correção registrada na decisão 23.
- `AGENTS.md` ainda diz "Não existe código, ambiente Python nem dados" e que o `.gitignore` é "a criar": está desatualizado e precisa de revisão.
