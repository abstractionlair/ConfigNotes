### Step 1: Install Dependencies

First, ensure you have the necessary dependencies installed:

```sh
sudo dnf update
sudo dnf install -y git curl gcc make zlib-devel bzip2 bzip2-devel readline-devel \
sqlite-devel openssl-devel xz xz-devel libffi-devel tk-devel
```

### Step 2: Install `pyenv` and `pyenv-virtualenv`

1. **Install `pyenv`:**

```sh
curl https://pyenv.run | bash
```

2. **Add `pyenv` to your shell configuration:**

```sh
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
source ~/.bashrc
```

3. **Install `pyenv-virtualenv`:**

```sh
git clone https://github.com/pyenv/pyenv-virtualenv.git "$(pyenv root)"/plugins/pyenv-virtualenv
```

### Step 3: Install `poetry`

```sh
curl -sSL https://install.python-poetry.org | python3 -
```

Add `poetry` to your PATH:

```sh
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### Step 4: Install `direnv`

1. **Install `direnv`:**

```sh
sudo dnf install direnv
```

2. **Add `direnv` to your shell configuration:**

```sh
echo 'eval "$(direnv hook bash)"' >> ~/.bashrc
source ~/.bashrc
```

### Step 5: Setting Up a Project

1. **Create a project directory:**

```sh
mkdir my_project
cd my_project
```

2. **Initialize `poetry` in the project:**

```sh
poetry init
```

3. **Create a `.envrc` file for `direnv`:**

```sh
echo 'layout poetry' > .envrc
direnv allow
```

4. **Install Python version using `pyenv`:**

```sh
pyenv install 3.9.7
pyenv virtualenv 3.9.7 my_project
```

5. **Set the local Python version:**

```sh
pyenv local my_project
```

6. **Install dependencies using `poetry`:**

```sh
poetry add <dependency>
```

### Step 6: Maintaining Environments

1. **Activate the virtual environment:**

```sh
pyenv activate my_project
```

2. **Deactivate the virtual environment:**

```sh
pyenv deactivate
```

3. **Update dependencies:**

```sh
poetry update
```

4. **Add new dependencies:**

```sh
poetry add <new_dependency>
```

5. **Remove dependencies:**

```sh
poetry remove <dependency>
```

### Step 7: Switching Between Projects

1. **Navigate to another project directory:**

```sh
cd another_project
```

2. **`direnv` will automatically switch to the correct environment based on the `.envrc` file.**

### Step 8: Cleaning Up

1. **Remove a virtual environment:**

```sh
pyenv uninstall my_project
```

2. **Remove a Python version:**

```sh
pyenv uninstall 3.9.7
```
