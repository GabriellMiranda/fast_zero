## Ambiente e ferramentas necessárias

Para começar a desenvolver com este projeto, você precisará configurar algumas ferramentas essenciais. Veja abaixo uma explicação dos principais itens e etapas:

- **Python 3.10+**: Linguagem de programação usada no projeto. Certifique-se de ter uma versão igual ou superior à 3.10 instalada.
- **Git**: Sistema de controle de versão para gerenciar o código-fonte e colaborar com outros desenvolvedores.
- **Docker**: (Opcional) Plataforma para criar ambientes isolados e portáveis para rodar aplicações.
- **gh**: (Opcional) Ferramenta de linha de comando para interagir com o GitHub.
- **pipx**: Utilitário para instalar e executar aplicativos Python globalmente, mas de forma isolada, evitando conflitos de dependências.
- **Poetry**: Gerenciador de dependências e ambientes virtuais para projetos Python. Facilita a instalação de pacotes e o controle de versões.
- **poetry-plugin-shell**: Plugin do Poetry que facilita o uso do ambiente virtual diretamente pelo terminal.
- **FastAPI**: Framework web moderno e rápido para construir APIs com Python.
- **pytest**: Ferramenta para escrever e rodar testes automatizados.
- **ruff**: Ferramenta para análise de código (lint) e formatação automática, garantindo boas práticas.
- **taskipy**: Permite definir comandos customizados (tasks) no arquivo `pyproject.toml` e executá-los facilmente.

### Passos recomendados para configurar o ambiente

1. **Escolha e instale um editor de texto** e um terminal de sua preferência.
2. **Instale o Python 3.10+** e o **Git** no seu sistema.
3. **Instale o pipx** para gerenciar ferramentas Python globalmente:
    ```bash
    python3 -m pip install --user pipx
    pipx ensurepath
    ```
4. **Instale o Poetry via pipx**:
    ```bash
    pipx install poetry
    ```
5. **Instale o plugin poetry-plugin-shell** para facilitar o uso do ambiente virtual:
    ```bash
    poetry self add poetry-plugin-shell
    ```
6. **(Opcional) Gerencie versões do Python com o Poetry**:
    ```bash
    poetry env use 3.11
    ```
    > Substitua `3.11` pela versão desejada.
7. **Crie um novo projeto**:
    ```bash
    poetry new --flat fast_zero
    ```
    > O parâmetro `--flat` cria a estrutura de pastas sem subdiretórios extras.
8. **Adicione o FastAPI**:
    ```bash
    poetry add 'fastapi[standard]'
    ```
9. **Ative o ambiente virtual** e rode o servidor:
    ```bash
    poetry shell
    fastapi dev fast_zero/app.py
    ```
10. **Adicione ferramentas de desenvolvimento**:
     ```bash
     poetry add --group dev pytest pytest-cov taskipy ruff
     ```
11. **Configure o ruff, pytest e taskipy** no arquivo `pyproject.toml` conforme as necessidades do projeto.
12. **Use o Taskipy** para simplificar a execução de comandos do projeto, como testes, lint e formatação.

Essas etapas garantem um ambiente de desenvolvimento organizado, isolado e produtivo, facilitando a colaboração e a manutenção do projeto.

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


Next: Introdução ao desenvolvimento web:
https://fastapidozero.dunossauro.com/estavel/02/