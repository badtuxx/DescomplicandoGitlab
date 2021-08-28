## Conteúdo

### Git Config

Para adicionar o seu nome, ou seja, o nome que irá aparecer como o autor de seus commits.

```bash
    git config --global user.name "Nome do usuário"
```    

Para adicionar o email do autor, faça:

```bash
    git config --global user.email "jeferson@linuxtips.com.br"
```    

Para configurar qual será o seu editor de texto padrão, execute o seguinte comando:

```bash
    git config --sysytem editor vim
```    


Para editar o arquivo de configuração do git:

```bash
    git config --global --edit
```    

O arquivo de configuração GLOBAL do Git:

```bash
    vim $HOME/.gitconfig
```    

O arquivo de configuração SYSTEM do Git:

```bash
    vim /etc/gitconfig
```

O arquivo de configuração LOCAL do Git:

```bash
    vim SEU_REPO/.git/config
```    

Para listar as configurações do Git:

```bash
    git config --global --list
    git config --system --list
    git config --local --list
```    

Onde:

```bash
    --global --list => Lista as configurações contida no arquivo $HOME/.gitconfig
    --system --list => Lista as configurações contida no arquivo /etc/gitconfig
    --local --list => Lista as configurações contida no arquivo SEU_REPO/.git/config
```  

### Iniciando no Git

Para clonar um repositório remoto

```bash
    git clone ENDEREÇO_DO_REPO # lembre-se de copiar o endereço completo

```  

Para adicionar um arquivo no INDEX

```bash
    git add NOME_DO_ARQUIVO # Adiciona o arquivo ao INDEX
    git add. # Adiciona todos os arquivos desse diretório
```  

Para adicionar um arquivo no HEAD

```bash
    git commit -am "mensagem descritiva do commit" # adiciona todos os arquivos do INDEX para o HEAD
    git commit -m "mensagem descritiva do commit" NOME_DO_ARQUIVO # adiciona o arquivo ao HEAD
```

Para adicionar as suas mudanças para o repositório Git remoto

```bash
    git push
    git push orgin MINHA_BRANCH # adiciona ao servidor remoto na branch especificada
```

Para verificar o status do repositório local

```bash
    git status
```

Para verificar os logs dos nossos commits

```bash
    git log
    git log -p
    git log -2 # para visualizar os dois ultimos commits
    git log --oneline
    git log --raw
    git log --pretty=full
    git log --graph
    git log -- README.md
    git log --stat
    git log --author=Jeferson
```

```bash

```
