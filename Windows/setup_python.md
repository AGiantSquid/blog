# setup python

1. install `pyenv` to manage python versions
    - install dependencies: 
      ```shell
      sudo apt-get install -y make build-essential libssl-dev zlib1g-dev \
      libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
      libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl
      ```
    - install `pyenv`
      ```shell
      curl https://pyenv.run | bash
      ```
    - figure out which version you want:
    ```shell
    pyenv install --list | grep " 3\."
    ```
    - install the version you want:
    ```shell
    pyenv install -v 3.7.2
    ```
    - check versions installed:
    ```shell
    pyenv versions
    ```
    - use version:
    ```shell
    pyenv global 3.7.2
    ```
    ```shell
    pyenv local 3.7.2
    ```
    
2. Create virtual env in project
    ```shell
    python -m venv .venv
    source .venv/bin/activate
    ```
    
