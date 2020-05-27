# DevOps ![GitHub License](https://img.shields.io/github/license/rarygoncalves/devops?label=License)

![GitHub Release (latest SemVer Stable Release)](https://img.shields.io/github/v/release/rarygoncalves/devops?label=Stable%20Release&sort=semver)
![GitHub Release (latest SemVer Latest Release)](https://img.shields.io/github/v/release/rarygoncalves/devops?include_prereleases&label=Latest%20Release&sort=semver)

[![Linkedin](https://img.shields.io/static/v1?label=Linkedin&message=Rary%20Gonçalves&logo=linkedin&style=social)](https://www.linkedin.com/in/rarygoncalves/)

## Continuous Integration ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/rarygoncalves/devops/Django?label=Integration&logo=django)

Para a integração contínua, as atividades de `build` e `test` são realizadas com um workflow baseado na linguagem Python e o framework Django, onde o script é executado na própria plataforma de forma nativa via GitHub Actions, utilizando o template para Django Project fornecido oficialmente.

### Regras de Integração

O script de build e test possui algumas configurações e condições de inicialização, que vão desde períodos de tempo e modificações no projeto:

#### Condições

1. O workflow será iniciado na versão da branch *master* sempre que um **Push** ou **Pull Request** for identificado na branch;

2. O workflow também será iniciado na versão da branch *master* periodicamente **às 07:00 a.m. (10:00 UTC)** toda **segunda-feira**, independentemente de alterações via *Push* ou *Pull Request*.

#### Configurações

1. O workflow irá utilizar a *versão mais recente* do **Ubuntu** como ambiente de execução;

2. O workflow também irá utilizar a versão do **Python 3.6** para *executar os comandos*.

### Execução

1. O ambiente do workflow é iniciado:

```
Current runner version: '2.262.1'
Operating System
  Ubuntu
  18.04.4
  LTS
Virtual Environment
  Environment: ubuntu-18.04
  Version: 20200518.1
  Included Software: https://github.com/actions/virtual-environments/blob/ubuntu18/20200518.1/images/linux/Ubuntu1804-README.md
Prepare workflow directory
Prepare all required actions
Download action repository 'actions/checkout@v2'
Download action repository 'actions/setup-python@v1'
```

> Repare que estamos aqui utilizando apenas uma máquina Ubuntu 18.04 LTS, mas outras máquinas também podem ser incrementadas para testes mais precisos em variações de sistemas operacionais como Windows 10, Mac OS etc.

2. O ambiente é configurado pelo GitHub Actions para build e test da versão da branch master:

```
Run actions/checkout@v2
Syncing repository: rarygoncalves/devops
Getting Git version info
Deleting the contents of '/home/runner/work/devops/devops'
Initializing the repository
Disabling automatic garbage collection
Setting up auth
Fetching the repository
Determining the checkout info
Checking out the ref
/usr/bin/git log -1
commit 0b915c648d5325570983300fa0d2635e5e09261d
Author: Rary Gonçalves <40248598+rarygoncalves@users.noreply.github.com>
Date:   Mon May 25 11:52:03 2020 -0300

    Atualizando ordem de shield de releases
```

3. A versão do Python a ser utilizada é configurada no ambiente:

```
Run actions/setup-python@v1
Successfully setup CPython (3.6.10)
```

4. O gerenciador de pacotes PyPI é atualizado, o arquivo `requirements.txt` é identificado e as dependências são instaladas:

```
Run python -m pip install --upgrade pip
Collecting pip
  Downloading pip-20.1.1-py2.py3-none-any.whl (1.5 MB)
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 20.1
    Uninstalling pip-20.1:
      Successfully uninstalled pip-20.1
Successfully installed pip-20.1.1
Collecting asgiref==3.2.3
  Downloading asgiref-3.2.3-py2.py3-none-any.whl (18 kB)
Collecting certifi==2019.11.28
  Downloading certifi-2019.11.28-py2.py3-none-any.whl (156 kB)
Collecting Django==3.0.3
  Downloading Django-3.0.3-py3-none-any.whl (7.5 MB)
Collecting pytz==2019.3
  Downloading pytz-2019.3-py2.py3-none-any.whl (509 kB)
Collecting sqlparse==0.3.0
  Downloading sqlparse-0.3.0-py2.py3-none-any.whl (39 kB)
Installing collected packages: asgiref, certifi, pytz, sqlparse, Django
Successfully installed Django-3.0.3 asgiref-3.2.3 certifi-2019.11.28 pytz-2019.3 sqlparse-0.3.0
```

5. O projeto é testado e a saída do teste é apresentada:

```
Run python manage.py test

System check identified no issues (0 silenced).
----------------------------------------------------------------------
Ran 0 tests in 0.000s

OK
```

> No momento, nenhum caso de teste unitário foi implementado neste projeto, portanto o único teste a ser rodado é o de `build` da aplicação Django, onde verifica se não há erros de sintaxe.

6. Finalização do worflow de integração:

```
Post job cleanup.
/usr/bin/git version
git version 2.26.2
/usr/bin/git config --local --name-only --get-regexp core\.sshCommand
/usr/bin/git submodule foreach --recursive git config --local --name-only --get-regexp 'core\.sshCommand' && git config --local --unset-all 'core.sshCommand' || :
/usr/bin/git config --local --name-only --get-regexp http\.https\:\/\/github\.com\/\.extraheader
http.https://github.com/.extraheader
/usr/bin/git config --local --unset-all http.https://github.com/.extraheader
/usr/bin/git submodule foreach --recursive git config --local --name-only --get-regexp 'http\.https\:\/\/github\.com\/\.extraheader' && git config --local --unset-all 'http.https://github.com/.extraheader' || :
```
```
Cleaning up orphan processes
```

> Assumindo que todas as etapas foram concluídas com sucesso de execução, o workflow de CI é finalizado de forma positiva e a integração é validada.


## Continuous Delivery ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/rarygoncalves/devops/Heroku?label=Delivery&logo=heroku)

> (em breve)
