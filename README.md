# fast_zero

Projeto FastAPI com boas práticas de desenvolvimento, testes e cobertura de código.

## Comandos disponíveis

Os comandos abaixo podem ser definidos no seu `pyproject.toml` usando o [taskipy](https://github.com/taskipy/taskipy):

```toml
[tool.taskipy.tasks]
lint = 'ruff check'
pre_format = 'ruff check --fix'
format = 'ruff format'
run = 'fastapi dev fast_zero/app.py'
pre_test = 'task lint'
test = 'pytest -s -x --cov=fast_zero -vv'
post_test = 'coverage html'
```

| Comando     | O que faz                                                                 |
|-------------|---------------------------------------------------------------------------|
| lint        | Checa boas práticas do código Python com ruff                             |
| pre_format  | Corrige automaticamente problemas de lint com ruff                        |
| format      | Formata o código conforme convenções de estilo                            |
| run         | Executa o servidor de desenvolvimento do FastAPI                          |
| pre_test    | Executa o lint antes dos testes                                           |
| test        | Roda os testes com pytest de forma verbosa e gera relatório de cobertura  |
| post_test   | Gera o relatório HTML de cobertura após os testes                         |

## Como rodar os comandos

Para executar qualquer comando, basta usar:

```bash
task <comando>
```

Exemplo para rodar os testes:

```bash
task test
```

## Como abrir o relatório de cobertura no navegador

Se estiver usando WSL, execute o comando abaixo para abrir o relatório de cobertura no navegador do Windows:

```bash
wslview htmlcov/index.html
```

Se estiver em um ambiente Linux puro, você pode usar:

```bash
xdg-open htmlcov/index.html
```

---

Sinta-se à vontade para adaptar os comandos conforme sua necessidade!