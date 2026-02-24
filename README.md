# Tools used to developed this solution

## [pyenvy](https://github.com/pyenv-win/pyenv-win)

Is a simple python version management tool. It lets the user easily switch between multiple versions of Python. Also, it follows the UNIX tradition of single-purpose tools that do one thing well.

### How to install pyenv

- In a powershell, run the command line bellow:

```powershell
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"

```

If you are getting any UnauthorizedAccess error as below then start Windows PowerShell with the "Run as administrator" option and run

 ```powershell
 Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
 ```

now re-run the above installation command.

```powershell

& : File C:\Users\kirankotari\install-pyenv-win.ps1 cannot be loaded because running scripts is disabled on this system. For
more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:173
+ ... n.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
+ ~~~~~~~~~~~~~~~~~~~~~~~~~ 
 + CategoryInfo          : SecurityError: (:) [], PSSecurityException 
 + FullyQualifiedErrorId : UnauthorizedAccess
```

- Next, we need to set a global default python version, in this case we choosed 3.12.1

```powershell
pyenv global 3.12.1
```

## [pipx](https://pipx.pypa.io/stable/)

pipx is a tool that help the user install and run end-user application written in Python. It is roughly similar to macOS's brew, JavaScript's npx, and Linux's apt.

It's closely related to pip. In fact, it uses pip, but is focused on installing and managing Python packages that can be run from the command line directly as applications.

### How to install it

- In a terminal, run the command bellow, using pyenvy:

```powershell
 pyenv exec pip install --user pipx
```

- Next, we need to add the pipx to the path so we can invoke its functionalities.

```powershell
pyenv exec pip install --user pipx
pyenv exec pipx ensurepath
```

## [poetry](https://python-poetry.org/docs/)

Poetry is a tool for dependency management and packaging in Python. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you. Poetry offers a lockfile to ensure repeatable installs, and can build your project for distribution.

### How to install poetry

First, we must already installed pyenv and pipx. Then, in a powershell console type the command:

```powershell
pip install poetry

```

## [Django](https://docs.djangoproject.com/en/6.0/)

With poetry installed, we can install Django. This tool it is a python web framework to develop web applications which was designed to make common web development tasks fast and easy.

### How to install Django

We can install pip in using any terminal console. In our case, we used powershell, and also have installed pyenvy, pipx and poetry. After this, we run the command bellow:

```powershell
poetry add django
```

## How to run the project

```powershell
docker run -p 8005:8000 --name djangocourse djangocourse
docker exec djangocourse poetry run python manage.py migrate
```