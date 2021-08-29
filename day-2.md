## Day-2

Durante o Day-2 do treinamento Descomplicando o Gitlab, você vai aprender como sobreviver utilizando o git.

Nós vamos aprender:

- [Day-2](#day-2)
    - [Git Config](#git-config)
    - [Iniciando no Git](#iniciando-no-git)
    - [Verificando os Logs](#verificando-os-logs)
    - [Revert e Reset](#revert-e-reset)
    - [Branches](#branches)
    - [Branching e Merge](#branching-e-merge)
  - [Exemplo de fluxo do Git](#exemplo-de-fluxo-do-git)


#### Git Config

Antes de começar a brincar com os nossos repositórios, primeiro nós precisamos configurar e personalizar o git de acordo com as nossas preferências e necessidades.

Abaixo vamos conhecer algumas opções, lembrando que durante o treinamento nós acabamos vendo mais opções e detalhes do que temos hoje no livro, isso se da por conta da dinâmica do treinamento ajudar. Porém a ideia é ter cada vez mais opções e detalhes para que você possa seguir e aprender muito, mesmo sem ter feito o treinamento.

Bem, bora lá!


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

#### Iniciando no Git

Para iniciar os nossos trabalhos, nós podemos criar um novo repositório, ou ainda clonar um repositório já existente.

Para criar um repositório novo, execute o seguinte comando:


```bash
    git init
```

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

#### Verificando os Logs

Para que possamos gerenciar bem nossos repositórios, precisamos saber e entender como buscar maiores informações sobre determinado commit. Inclusive é fundamental saber como buscar essas informações, por exemplo em casos de reset, revert, etc.

Bora conhecer como ter acesso aos logs do git.


Abaixo irei adicionar diferentes formas de ter acesso aos logs. É muito importante que você teste e entenda como funciona cada uma delas.

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

Para ter um visualização da árvore de branches e commites de forma gráfica. 

OBS: Esse tipo de visualização pode ajudar a entender como se deram os merges em um ambiente onde utiliza-se o [git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) , e em ambientes de [*trunk based*](https://trunkbaseddevelopment.com/) pode ajudar a visualizar se o fluxo de merges de *short live branches* esta sendo seguido e com isso ajudar no *debug*.

```bash
    git log --oneline --graph --decorete --all
```

#### Revert e Reset 

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

Com isso, nosso repositorio voltou para o commit b7ca89d e o arquivo README.md e cheatsheet_git.md foram removidos da Staging Area.

Podemos ainda utilizar o comando git reset --hard para voltar o nosso repositório para o commit específico.


```bash
    git reset --hard b7ca89d
HEAD is now at b7ca89d Update README.md
```

Com o comando acima, o nosso repositório voltou para o commit b7ca89d e os arquivos README.md e cheatsheet_git.md foram removidos do repositório.


Outra opção para voltar o nosso repositório para um commit específico é o comando git revert.


```bash
    git revert b7ca89d
On branch main
Your branch is behind 'origin/main' by 4 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md
	modified:   cheatsheet_git.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Agora, o nosso repositório voltou para o commit b7ca89d, mas o arquivo README.md e cheatsheet_git.md não foram removidos do repositório.

Simples, não?


Agora vamos imaginar que o problema não foi no conteúdo do arquivo, mas na mensagem do commit.
Podemos alterar a mensagem do commit através do comando git commit --amend.


```bash
    git commit --amend
```

Com isso, abrirá o editor de texto, para que possamos alterar a mensagem do commit.

Caso queira, pode-se utilizar o comando git commit --amend com o parametro -m e a "mensagem" para alterar a mensagem do commit.


```bash
    git commit --amend -m "adicionando o reset, revert e o amend"
```


Pronto, acredito que já sabemos como utilizar o git para reverter alguma cagada, ou melhor, algum errinho bobo. :)


#### Branches

Durante o processo de desenvolvimento, podemos criar várias branches, para trabalhar em diferentes partes do nosso projeto. Com isso, podemos ter diversas pessoas trabalhando simultaneamente no mesmo projeto, e sem interferir na branch principal.

Imagina que temos o codigo de nossa aplicação, e temos que realizar alguma alteração no codigo, e queremos que ela seja testada, e depois que ela estiver testada, podemos colocar ela em produção.

O que isso significa?

Precisamos criar uma branch, realizar todas as mudanças que precisamos, testar o código, e depois realizar o merge com a branch principal, colando essas mudanças para a branch principal, para que ela seja aplicada na produção.

Ficou claro?

Se ainda não, não se preocupe, pois iremos ainda brincar com branches por diversas vezes, como por exemplo durante a aula sobre git flow.

Para criar uma nova branch, basta utilizar o comando git checkout com o parametro -b.


```bash
    git checkout -b branch_giropops
Switched to a new branch 'branch_giropops'
```

Com isso, criamos uma nova branch, e o HEAD foi movido para a branch criada. Ou seja, nesse momento todas as mudanças que fizermos, não serão aplicadas na branch principal, e sim na branch criada, a branch branch_giropops.

Para visualizar as branches existentes, basta utilizar o comando git branch.


```bash
    git branch
* branch_giropops
  main
```

Para voltar para a branch principal, basta utilizar o comando git checkout.

```bash
    git checkout main
Switched to branch 'main'
```

Para remover uma branch, basta utilizar o comando git branch -d.


```bash
    git branch -d branch_giropops
Deleted branch branch_giropops (was 1d8f8f0).
```


#### Branching e Merge


O merge, nada mais é do que a junção de duas branches, ou seja, a junção de dois códigos. É o momento onde você adiciona o conteúdo de uma branch para outra branch.
Normalmente fazemos o merge de uma branch com a branch principal, mas podemos também fazer o merge de duas branches, ou seja, adicionar o conteúdo de duas branches para uma terceira. Sim, eu sei que parece confuso, mas vai ficar mais fácil de entender conforme formos avançando.

Vamos criar uma nova branch novamente, para que possamos fazer algumas alterações e depois realizar o merge com a branch principal.


```bash
    git checkout -b branch_giropops
Switched to a new branch 'branch_giropops'
```


Agora, vamos fazer algumas mudanças no nosso código.


```bash
    git add .
    git commit -m "adicionando arquivos novos para aprender sobre o merge"
```


Agora, vamos realizar o merge com a branch principal.
Para isso, precisamos primeiro voltar para a branch principal.

```bash
    git checkout main
Switched to branch 'main'
```

Agora, vamos fazer o merge.


```bash
    git merge branch_giropops
```

Agora, o nosso codigo está em produção, e o conteúdo da branch branch_giropops foi adicionado ao conteúdo da branch principal.

Nós ainda vamos brincar muito mais com branches, merges e ainda precisamos conhecer o rebase, mas isso vai ficar para mais para frente, agora nós precisamos práticar tudo que aprendemos durante o Day-2.


Abaixo temos alguns exemplos de como funciona a dinamica durante o dia a dia utilizando o git.
Muito obrigado ao @felipefrocha por criar o fluxo abaixo para que possamos praticar. :)

Inclusive gostaria de salientar a importância da colaboração de todos, para que tenhamos um livro bastante completo sobre a utilização do Gitlab. 

Lembrando que esse livro é parte do treinamento [Descomplicando o Gitlab da LINUXtips.](https://linuxtips.io)


Agora bora praticar um pouquinho!

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