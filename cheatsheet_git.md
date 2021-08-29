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



### Logs

Para verificar os logs dos nossos commits:

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


Visualização da árvore de branches e commites de forma gráfica. 

OBS: Esse tipo de visualização pode ajudar a entender como se deram os merges em um ambiente onde utiliza-se o [git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) , e em ambientes de [*trunk based*](https://trunkbaseddevelopment.com/) pode ajudar a visualizar se o fluxo de merges de *short live branches* esta sendo seguido e com isso ajudar no *debug*.

```bash
    git log --oneline --graph --decorete --all
```


### Revert e Reset 

Quem nunca commitou algo que não era para committar?
Nesses momentos você precisa conhecer o Revert e o Reset, eles serão seus amigos em momentos dificeis como o de um commit errado.

Vamos imaginar a situação onde você acabou de adicionar todos os seus arquivos para a Staging Area.


```bash
    git add .
    git status

On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   arq1
	new file:   arq2
	new file:   arq21
	new file:   arq22
	new file:   arq222
	new file:   arq24
	new file:   arq25
	new file:   minhas_senhas.txt

```

Como podemos ver, acabamos adicionando o arquivo minhas_senhas.txt! E agora?
Bem, nesses momentos dificeis você pode contar com o git reset!

Para retirar esse arquivo da Staging Area, faça:

```bash
    git reset minhas_senhas.txt
```

Perceba, o arquivo é removido da Staging Area, mas não é removido do repositório. 

```bash
    git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   arq1
	new file:   arq2
	new file:   arq21
	new file:   arq22
	new file:   arq222
	new file:   arq24
	new file:   arq25

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	minhas_senhas.txt
```

Para remover o arquivo do repositório, faça:

```bash
    rm minhas_senhas.txt
```

Ou caso queira utilizar o comando do git, faça:

```bash
    git clean -n
Would remove minhas_senhas.txt
```

No comando acima, somente é exibido quais arquivos poderiam ser removidos. O comando acima não remove os arquivos.

Para remover os arquivos do repositório, faça:

```bash
    git clean -f
Removing minhas_senhas.txt
```

Existe ainda a opção do git reset --hard, que remove o arquivo do repositório e o arquivo da Staging Area. Utilize esse cara com moderação, pois ele pode apagar arquivos importantes do seu repositório.


Vamos adicionar os arquivos novamente, e realizar mais um teste, agora utilizando a opção do git reset --hard.


```bash
    git add .                                                       
    git status                                                      
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   arq1
	new file:   arq2
	new file:   arq21
	new file:   arq22
	new file:   arq222
	new file:   arq24
	new file:   arq25
	new file:   minhas_senhas.txt
```

Após adicionar o arquivo minhas_senhas.txt, faça:


```bash
    git reset --hard
HEAD is now at 23b2ac1 Merge pull request #1 from badtuxx/main
```

Com isso, os arquivos sao removidos do repositório e da Staging Area, e o HEAD é resetado para o commit anterior.

Ainda utilizando o comando git reset, é possível passar um commit específico para o HEAD, ou seja, voltar o seu repositório para um commit específico.


```bash
    git log --oneline
23b2ac1 (HEAD -> main, origin/main, origin/HEAD) Merge pull request #1 from badtuxx/main
4b58c01 Update README.md
b7ca89d Update README.md
b567836 Update cheatsheet_git.md
4f0259b adicionando parte do Day2
011cfef Initial commit
```

Vamos escolher o commit cbe499d para resetar o nosso repositório.


```bash
    git reset b7ca89d 
Unstaged changes after reset:
M	README.md
M	cheatsheet_git.md
```

### Exemplo de fluxo do Git
Apenas para aprecisação dos comando aprendidos até o momento é legal realizar uma pequena prova de conceito, para fixar a idiea de alguns comandos, veja abaixo uma sugestão de sequência de comandos que poderiam ser utilizados no dia a dia:
```bash
    git init
    touch testes
    git commit -m "Initial commit"
    git log                                                                 # visualizamos um único commit
    git checkout -b feature/teste                                           # Cria uma branch e muda para ela
    touch menos
    git add menos
    git commit -m "Criar arquivo menos"
    touch mais
    git add mais
    git commit -m "Criar arquivo mais"
    touch mais_menos menos_mais                                             # criamos mais dois arquivos
    echo "Esse é o arquivo menos" >> menos                                  # Alteramos um arquivo 
    echo "Esse é o arquivo mais" >> mais                                    # Alteramos outro arquivo
    git add .                                                               # Adicione todos os arquivos alterados e/ou criados na pasta corrente
    git commit -m "Criar arquivos e Alteração de arquivos"
    git log                                                                 # visualizar commites até o momento
    git commit --amend                                                      # Altere a mensagem do seu ultimo commit
    git log
    git rebase -i HEAD~3 #Alterar os ultimos 3 commites
    # Troque o valor de pick por squash nas ultimas 3 linhas 
    # referentes aos commites
    git log
    git branch                                                              # visualiza qual a branch atual
    git branch feature/teste                                                # cria uma nova branch com o nome "feature/teste"
    git checkout feature/teste                                              # muda para a branch criada "feature/teste"
    touch a 
    git add a                                                               # adiciona apenas o arquivo "a" e/ou suas alterações
    git commit -m "Criar arquivo a" 
    touch b
    git add b                                                               # adiciona apenas o arquivo "b" e/ou suas alterações
    git commit -m "Criar arquivo b"
    touch c d
    git add c
    git add d
    git commit -m "Criar arquivo c e d"
    ls -l                                                                   # lista os arquivos na pasta
    git log
    git checkout main                                                       # retorna para a branch "main"
    ls -l                                                                   # note que os arquivos da outra branch não estao presentes mais
    git log --decorate --oneline --graph --all                              # visualização de todos os commites e em quais branches  em ordem cronologica
    git merge feature/teste                                                 # merge das duas branchs
    ls -l                                                                   # Veja que todos os arquivos aparecem nesse momento
    # vamos adicionar mais arquivos e commita-los em branches 
    # diferentes e ver como fica
    touch e f g
    git add .
    git commit -am "Criar arquivos e f g"
    touch h i j
    git add h
    git commit -m "Criar arquivo h"
    git add i 
    git commit -m "Criar arquivo i"
    git add j
    git commit -m "Criar arquivo j"
    git checkout feature/teste
    touch k
    git add k
    git commit -m "Criar arquivo k"
    git log --decorate --oneline --graph --all                               # para ajudar a decorar: "git dog all"
    # vamos criar mais uma branch e adicionar arquivos
    git checkout -b feature/mais_teste
    touch l
    git add l
    git commit -m "Criar arquivo l"
    git checkout main
    git log --decorate --oneline --graph --all
    git merge feature/teste
    git log --decorate --oneline --graph --all
    git merge feature/mais_teste
    git log --decorate --oneline --graph --all
```
