# Projeto Django com Poetry e Docker

Este guia resume os comandos necessários para configurar o ambiente, gerenciar a aplicação Django e rodar o projeto via Docker, baseado no histórico de execução.

1. Configuração do Ambiente (Python & Poetry)
   Prepare o ambiente utilizando o pyenv para garantir a versão correta do Python e o pipx para o Poetry.# Instalar Python 3.12.1 e definir como global

```powershell
pyenv install 3.12.1
pyenv global 3.12.1
```

## Instalar Poetry via pipx

```powershell
pip install --user
pipx pipx ensurepath
pipx install poetry 
```

1. Inicialização do Projeto

   Comandos para criar a estrutura inicial do projeto e instalar as dependências base.# Criar repositório e adicionar Django

```powershell
poetry new djangocourse
cd djangocourse
poetry add django
```

1. Iniciar projeto e app Django

```powershell
poetry run django-admin startproject djangocourse .
poetry run python manage.py startapp app
```

1. Comandos de Gerenciamento (Django)Agrupamento de comandos comuns de desenvolvimento executados via Poetry.

### Banco de Dados: Migrações e Superusuário

```powershell
poetry run python manage.py makemigrations
poetry run python manage.py migrate
poetry run python manage.py createsuperuser
```

### Servidor e Estáticos

```powershell
poetry run python manage.py runserver
poetry run python manage.py collectstatic
```

### Internacionalização (Traduções)

```powershell
poetry run python manage.py makemessages --locale=pt_BR
poetry run python manage.py compilemessages
```

1. Containerização com DockerComandos para construir a imagem e gerenciar a execução do container.Build e Execução# Build da imagem
docker build -t djangocourse .

### Rodar container com mapeamento de porta e volume (Hot Reload)

```powershell
docker run -p 8000:8000 --name djangocourse -v "${pwd}:/code" djangocourse
```

### Comandos Administrativos no Container

Utilize o exec para rodar comandos sem precisar parar o container:

```powershell
docker exec djangocourse poetry run python manage.py migrate
docker exec djangocourse poetry run python manage.py compilemessages
```

1. Limpeza e Manutenção# Parar e remover container
docker stop djangocourse
docker rm djangocourse

### Desativar ambiente virtual (se estiver ativo)

```powershell
deactivate
```

Nota: Para usuários Windows, se houver erro de permissão ao ativar o ambiente,

```powershell
execute:Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
```
