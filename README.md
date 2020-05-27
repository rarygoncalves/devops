# DevOps Learning ![GitHub License](https://img.shields.io/github/license/rarygoncalves/devops-learning?label=License) ![GitHub Release (latest SemVer Stable Release)](https://img.shields.io/github/v/release/rarygoncalves/devops-learning?label=Stable%20Release&sort=semver) ![GitHub Release (latest SemVer Latest Release)](https://img.shields.io/github/v/release/rarygoncalves/devops-learning?include_prereleases&label=Latest%20Release&sort=semver)

[![Linkedin](https://img.shields.io/static/v1?label=Linkedin&message=Rary%20Gonçalves&logo=linkedin&style=social)](https://www.linkedin.com/in/rarygoncalves/)

## Continuous Integration ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/rarygoncalves/devops-learning/Django?label=Integration&logo=django)

Para a integração contínua, as atividades de `build` e `test` são realizadas com um workflow baseado na linguagem Python e o framework Django, onde o script é executado na própria plataforma de forma nativa via GitHub Actions, utilizando o template para Django Project fornecido oficialmente.

### Regras de Integração

O script de `build` e `test` possui algumas configurações e condições de inicialização, que vão desde períodos de tempo e modificações no projeto:

#### Condições

1. O workflow será iniciado na versão da branch *master* sempre que um **Push** ou **Pull Request** for identificado na branch;

2. O workflow também será iniciado na versão da branch *master* periodicamente **às 07:00 a.m. (10:00 UTC)** toda **segunda-feira**, independentemente de alterações via *Push* ou *Pull Request*.

#### Configurações

1. O workflow irá utilizar a *versão mais recente* do **Ubuntu** como ambiente de execução;

2. O workflow também irá utilizar a versão do **Python 3.6** para *executar os comandos*.

### Script

Para iniciar as atividades pré-estabelecidas de CI com todas as condições e configurações acima mencionadas, o script `django.yml` é interpretado pelo GitHub Actions como um workflow deste repositório e executado.

```yaml
name: Django

on:
  push:
    branches:
      - master
  pull_request:
    branches:
      - master
  schedule:
    - cron: "0 10 * * 1"

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      max-parallel: 1
      matrix:
        python-version: [3.6]

    steps:
    - uses: actions/checkout@v2

    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v1
      with:
        python-version: ${{ matrix.python-version }}

    - name: Install Dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Run Tests
      run: |
        python manage.py test
```

> `/.github/workflows/django.yml`


### Execução

- [X] O ambiente do workflow é iniciado
- [X] O ambiente é configurado pelo GitHub Actions para `build` e `test`
- [X] A versão do Python a ser utilizada é configurada no ambiente
- [X] O gerenciador de pacotes PyPI é atualizado, o arquivo `requirements.txt` é identificado e as dependências são instaladas
- [x] O projeto é testado e a saída do teste é apresentada
- [X] O workflow retorna o resultado da Action
- [X] O workflow é encerrado

> Assumindo que todas as etapas foram concluídas com sucesso de execução, o workflow de CI é finalizado de forma positiva e a Action é validada.


## Continuous Delivery ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/rarygoncalves/devops-learning/Heroku?label=Delivery&logo=heroku)

Para a entrega contínua, a atividade de `deploy` é realizada com um workflow baseado no serviço de hospedagem em nuvem Heroku, onde o script é executado na própria plataforma de forma nativa via GitHub Actions, utilizando o template para Heroku Deployment fornecido por AkhileshNS em Marketplace > Actions.

[![Linkedin](https://img.shields.io/static/v1?label=Actions&message=heroku-deploy&logo=github&style=social)](https://www.linkedin.com/in/rarygoncalves/)

### Regras de Entrega

O script de `deploy` possui algumas configurações e condições de inicialização:

#### Condições

1. O workflow será iniciado na versão da branch *master* sempre que um **Push** for identificado na branch;

#### Configurações

1. O workflow irá utilizar a *versão mais recente* do **Ubuntu** como ambiente de execução;

### Script

Para iniciar as atividades pré-estabelecidas de CD com todas as condições e configurações acima mencionadas, o script `heroku.yml` é interpretado pelo GitHub Actions como um workflow deste repositório e executado.

```yaml
name: Heroku

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest
  
    steps:
      - uses: actions/checkout@v2

      - name: Deploy on Heroku
        uses: akhileshns/heroku-deploy@v3.0.4 # This is the action
        with:
          heroku_api_key: ${{secrets.HEROKU_API_KEY}}
          heroku_app_name: "${{secrets.HEROKU_APP_NAME}}" #Must be unique in Heroku
          heroku_email: "${{secrets.HEROKU_EMAIL}}"`
```

> `/.github/workflows/heroku.yml`

### Execução

- [X] O ambiente do workflow é iniciado
- [X] O ambiente é configurado pelo GitHub Actions para `deploy`
- [X] O script de `deploy` do Heroku é iniciado
- [X] O workflow retorna o resultado da Action
- [X] O workflow é encerrado

> Assumindo que todas as etapas foram concluídas com sucesso de execução, o workflow de CD é finalizado de forma positiva, a Action é validada e o conteúdo do projeto já está em produção no App Heroku configurado para `deploy`.
