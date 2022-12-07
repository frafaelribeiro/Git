# Anotações de comandos Git

## Como remover arquivos enviados anteriormente por commit a partir de um novo Gitignore

Para remover um único arquivo, ou seja, para parar de rastrear o arquivo, mas não excluir esse arquivo do sistema, use:

`git rm --cached filename`

Para parar de rastrear todos os arquivos no *.gitignore*:

Primeiro, faça o commit de quaisquer alterações no código que estejam faltando. Depois, execute o comando:

`git rm -r --cached`  

> Ex: `git rm -r --cached ./nginx_com_node/node/node_modules`

Isso removerá todos os arquivos alterados do índice (área de staging). Logo depois, execute:

`git add .`

Faça o commit:

`git commit -m ".gitignore agora está funcionando"`

Para desfazer o *git rm --cached filename*, use *git add filename*  

## Praticando git-flow

`╰─❯ mkdir praticando_gitflow`  
`╰─❯ cd praticando_gitflow`  

- Iniciando o repositório do git

```bash
╰─❯ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Repositório vazio Git inicializado em  /mnt/f/Projetos/curso_fullcycle/Git/praticando_gitflow/.git/
```
- Opções do git-flow

```bash
╰─❯ git flow
usage: git flow <subcommand>

Available subcommands are:
   init      Initialize a new git repo with support for the branching model.
   feature   Manage your feature branches.
   bugfix    Manage your bugfix branches.
   release   Manage your release branches.
   hotfix    Manage your hotfix branches.
   support   Manage your support branches.
   version   Shows version information.
   config    Manage your git-flow configuration.
   log       Show log deviating from base branch.

Try 'git flow <subcommand> help' for details.
```
- iniciando o git flow e informando os parâmetros

```bash
╭─   ~/Projetos/curso_fullcycle/Git/praticando_gitflow on   master ········································································  base at  22:25:57
╰─❯ git flow init   
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master] main
Branch name for "next release" development: [develop] 

How to name your supporting branch prefixes?
Feature branches? [feature/] 
Bugfix branches? [bugfix/] 
Release branches? [release/] 
Hotfix branches? [hotfix/] 
Support branches? [support/] 
Version tag prefix? [] 
Hooks and filters directory? [/home/rafael/Projetos/curso_fullcycle/Git/praticando_gitflow/.git/hooks] 

╭─   ~/Projetos/curso_fullcycle/Git/praticando_gitflow on   develop ·························································· took  2m 2s  base at  22:29:41
╰─❯
```
Vemos que o git flow inicia na branch develop.  
- Criando uma feature nova

```bash
╭─   ~/P/curso_f/Git/praticando_gitflow on   develop ········  base at  22:30:59
╰─❯ git flow feature
No feature branches exist.

You can start a new feature branch:

    git flow feature start <name> [<base>]


╭─   ~/P/curso_f/Git/praticando_gitflow on   develop ········  base at  22:32:35
╰─❯ git flow feature start welcome
Switched to a new branch 'feature/welcome'

Summary of actions:
- A new branch 'feature/welcome' was created, based on 'develop'
- You are now on branch 'feature/welcome'

Now, start committing on your feature. When done, use:

     git flow feature finish welcome


╭─   ~/P/curso_f/G/praticando_gitflow on   feature/welcome ··  base at  22:33:21
╰─❯
```
Criamos um novo arquivo  

```bash
╰─❯ cat index.html       
<h1>Olá mundo</h1>
```

```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   feature/welcome ?1 
╰─❯ ls       
index.html

╭─   ~/P/curso_f/G/praticando_gitflow on   feature/welcome ?1 
╰─❯ git status                    
No ramo feature/welcome
Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)
        index.html

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)

╭─   ~/P/curso_f/G/praticando_gitflow on   feature/welcome ?1 
╰─❯ git add .                                

╭─   ~/P/curso_f/G/praticando_gitflow on   feature/welcome +1 
╰─❯ git commit -m 'Add index'
[feature/welcome f7e5004] Add index
 1 file changed, 1 insertion(+)
 create mode 100644 index.html

╭─   ~/P/curso_f/G/praticando_gitflow on   feature/welcome ··  base at  22:37:19
╰─❯ git log



commit f7e500471f63ea5236fc8c5ab82b8d091f388539 (HEAD -> feature/welcome)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:37:19 2022 -0300

    Add index

commit 11cc85a05076e0ed82b6c7b80332413dd40d5217 (main, develop)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:28:18 2022 -0300

    Initial commit
(END)
```
- terminado a feature

```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   feature/welcome 
╰─❯ git flow feature finish welcome
Switched to branch 'develop'
Updating 11cc85a..f7e5004
Fast-forward
 index.html | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
Deleted branch feature/welcome (was f7e5004).

Summary of actions:
- The feature branch 'feature/welcome' was merged into 'develop'
- Feature branch 'feature/welcome' has been locally deleted
- You are now on branch 'develop'


╭─   ~/P/curso_f/Git/praticando_gitflow on   develop ········  base at  22:39:41
╰─❯
```
- Grando um release

```bash
╭─   ~/P/curso_f/Git/praticando_gitflow on   develop ········  base at  22:39:41
╰─❯ git flow release start 0.1.0   
Switched to a new branch 'release/0.1.0'

Summary of actions:
- A new branch 'release/0.1.0' was created, based on 'develop'
- You are now on branch 'release/0.1.0'

Follow-up actions:
- Bump the version number now!
- Start committing last-minute fixes in preparing your release
- When done, run:

     git flow release finish '0.1.0'


╭─   ~/P/curso_f/Git/praticando_gitflow on   release/0.1.0 ··  base at  22:41:52
╰─❯
```
  - Paralelo ao release iniciamos uma nova feature

```bash
╭─   ~/P/curso_f/Git/praticando_gitflow on   release/0.1.0 ··  base at  22:41:52
╰─❯ git flow feature start contact 
Switched to a new branch 'feature/contact'

Summary of actions:
- A new branch 'feature/contact' was created, based on 'develop'
- You are now on branch 'feature/contact'

Now, start committing on your feature. When done, use:

     git flow feature finish contact


╭─   ~/P/curso_f/G/praticando_gitflow on   feature/contact ··  base at  22:44:54
╰─❯ git branch



  develop
* feature/contact
  main
  release/0.1.0
(END)
```
  - criando um novo arquivo na feature contact

```bash
╰─❯ cat contact.html 
<h1>Contact</h1>
```

```bash
╰─❯ git add . 
╰─❯ git commit -m 'Add contact'
[feature/contact 5ac0090] Add contact
 1 file changed, 1 insertion(+)
 create mode 100644 contact.html
```
  - finalizando a feature contact

```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   feature/contact ··  base at  22:49:55
╰─❯ git flow feature finish contact
Switched to branch 'develop'
Updating f7e5004..5ac0090
Fast-forward
 contact.html | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 contact.html
Deleted branch feature/contact (was 5ac0090).

Summary of actions:
- The feature branch 'feature/contact' was merged into 'develop'
- Feature branch 'feature/contact' has been locally deleted
- You are now on branch 'develop'


╭─   ~/P/curso_f/Git/praticando_gitflow on   develop ········  base at  22:50:34
╰─❯
```
- vemos no git log as alterações que estão na develop inclui o Add contact

```bash
╰─❯ git log 


commit 5ac0090026d5014946c2fae69c13f57e9673fcf6 (HEAD -> develop)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:49:21 2022 -0300

    Add contact

commit f7e500471f63ea5236fc8c5ab82b8d091f388539 (release/0.1.0)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:37:19 2022 -0300

    Add index

commit 11cc85a05076e0ed82b6c7b80332413dd40d5217 (main)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:28:18 2022 -0300

    Initial commit
(END)
```
- fazendo o checkout release/0.1.0 não encontramos o Add contact

```bash
╭─   ~/P/curso_f/Git/praticando_gitflow on   develop ········  base at  22:53:02
╰─❯ git checkout release/0.1.0            
Switched to branch 'release/0.1.0'

╭─   ~/P/curso_f/Git/praticando_gitflow on   release/0.1.0 ··  base at  22:54:36
╰─❯ git log



commit f7e500471f63ea5236fc8c5ab82b8d091f388539 (HEAD -> release/0.1.0)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:37:19 2022 -0300

    Add index

commit 11cc85a05076e0ed82b6c7b80332413dd40d5217 (main)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:28:18 2022 -0300

    Initial commit
(END)
```
- Vamos fazer um ajuste de ultima hora no release/0.1.0
```bash
╰─❯ cat index.html  
<h1>Olá mundo!</h1>
```
```bash
╰─❯ git add .
╰─❯ git commit -m 'Add !'      
[release/0.1.0 5d79215] Add !
 1 file changed, 1 insertion(+), 1 deletion(-)
╰─❯ git status           
No ramo release/0.1.0
nothing to commit, working tree clean
```

```bash
╰─❯ git log 

commit 5d7921595db56ea51358f33a9d1dac482823d961 (HEAD -> release/0.1.0)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:57:10 2022 -0300

    Add !

commit f7e500471f63ea5236fc8c5ab82b8d091f388539
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:37:19 2022 -0300

    Add index

commit 11cc85a05076e0ed82b6c7b80332413dd40d5217 (main)
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:28:18 2022 -0300

    Initial commit
(END)
```
 Neste momento temos nosso release com o ajuste de ultima hora, mas sem a feature de contato.

- Vamos colocar a release em produção, adicionamos as mensagens, isto irá fazer o merge no main, gerar uma tag e um merge no developer

```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   release/0.1.0 
╰─❯ git flow release finish 0.1.0

     /mnt/f/Projetos/curso_fullcycle/Git/praticando_gitflow/.git/MERGE_MSG             
Merge branch 'release/0.1.0'
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.











                                  [ 6 linhas lidas ]
^G Ajuda      ^O Gravar     ^W Onde está? ^K Recortar   ^T Executar   ^C Local
^X Sair       ^R Ler o arq  ^\ Substituir ^U Colar      ^J Justificar ^/ Ir p/ linha
```

```bash
/mnt/f/Projetos/curso_fullcycle/Git/praticando_gitflow/.git/TAG_MSG             
Tagging 0.1.0
# 
# Write a message for tag:
#    0.1.0
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
```

```bash
/mnt/f/Projetos/curso_fullcycle/Git/praticando_gitflow/.git/MERGE_MSG             
Merge tag '0.1.0' into develop

Tagging 0.1.0
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.










^G Ajuda      ^O Gravar     ^W Onde está? ^K Recortar   ^T Executar   ^C Local
^X Sair       ^R Ler o arq  ^\ Substituir ^U Colar      ^J Justificar ^/ Ir p/ linha
```


```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   release/0.1.0 
╰─❯ git flow release finish 0.1.0  
Switched to branch 'main'
Merge made by the 'ort' strategy.
 index.html | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
Already on 'main'
Switched to branch 'develop'
Merge made by the 'ort' strategy.
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
Deleted branch release/0.1.0 (was 5d79215).

Summary of actions:
- Release branch 'release/0.1.0' has been merged into 'main'
- The release was tagged '0.1.0'
- Release tag '0.1.0' has been back-merged into 'develop'
- Release branch 'release/0.1.0' has been locally deleted
- You are now on branch 'develop'


╭─   ~/P/curso_f/G/praticando_gitflow on   develop 
╰─❯
```

```bash
╰─❯ git branch 


* develop
  main
(END)
```
- No log vemos o merge feito

```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   develop 
╰─❯ git log   

commit 475573d9a93b0837f52d39f94b37e3eb260d508b (HEAD -> develop)
Merge: 5ac0090 6715273
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 23:05:04 2022 -0300

    Merge tag '0.1.0' into develop
    
    Tagging 0.1.0

commit 6715273a1c39b75352d757315637217b6d36f87b (tag: 0.1.0, main)
Merge: 11cc85a 5d79215
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 23:01:31 2022 -0300

    Merge branch 'release/0.1.0'

commit 5d7921595db56ea51358f33a9d1dac482823d961
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:57:10 2022 -0300

    Add !

commit 5ac0090026d5014946c2fae69c13f57e9673fcf6
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:49:21 2022 -0300

:
```
- Na main vemos o merge 

```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   develop 
╰─❯ git checkout main          
Switched to branch 'main'

╭─   ~/P/curso_fullcycle/Git/praticando_gitflow on   main ···  base at  23:20:48
╰─❯ git log  
commit 6715273a1c39b75352d757315637217b6d36f87b (HEAD -> main, tag: 0.1.0)
Merge: 11cc85a 5d79215
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 23:01:31 2022 -0300

    Merge branch 'release/0.1.0'

commit 5d7921595db56ea51358f33a9d1dac482823d961
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:57:10 2022 -0300

    Add !

commit f7e500471f63ea5236fc8c5ab82b8d091f388539
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Tue Nov 29 22:37:19 2022 -0300

    Add index

commit 11cc85a05076e0ed82b6c7b80332413dd40d5217
:
```
- visualizando a tag

```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   main ·· took  38s  base at  23:21:47
╰─❯ git tag 

0.1.0
(END)
```
- Agora temos tudo em produção, porem apareceu um problema e temos que fazer um hotfix

```bash
╭─   ~/P/curso_fullcycle/Git/praticando_gitflow on   main ···  base at  23:24:54
╰─❯ git flow hotfix start index  
Switched to a new branch 'hotfix/index'

Summary of actions:
- A new branch 'hotfix/index' was created, based on 'main'
- You are now on branch 'hotfix/index'

Follow-up actions:
- Start committing your hot fixes
- Bump the version number now!
- When done, run:

     git flow hotfix finish 'index'


╭─   ~/P/curso_f/Git/praticando_gitflow on   hotfix/index ···  base at  23:25:35
╰─❯
```
  - aplicando o fix

```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   hotfix/index !1 ··  base at  23:26:56
╰─❯ cat index.html 
<h1>Olá mundo!!!</h1>

╭─   ~/P/curso_f/G/praticando_gitflow on   hotfix/index !1 ··  base at  23:27:01
╰─❯ git add .                  

╭─   ~/P/curso_f/G/praticando_gitflow on   hotfix/index +1 ··  base at  23:27:55
╰─❯ git commit -m 'Fix !!!'
[hotfix/index 47d2649] Fix !!!
 1 file changed, 1 insertion(+), 1 deletion(-)

╭─   ~/P/curso_f/Git/praticando_gitflow on   hotfix/index ···  base at  23:28:15
╰─❯ 
```
  - agora finalizamo o fix

```bash
╭─   ~/P/curso_f/Git/praticando_gitflow on   hotfix/index ···  base at  23:28:15
╰─❯ git flow hotfix finish index

     /mnt/f/Projetos/curso_fullcycle/Git/praticando_gitflow/.git/MERGE_MSG             
Merge branch 'hotfix/index'
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.











                                  [ 6 linhas lidas ]
^G Ajuda      ^O Gravar     ^W Onde está? ^K Recortar   ^T Executar   ^C Local
^X Sair       ^R Ler o arq  ^\ Substituir ^U Colar      ^J Justificar ^/ Ir p/ linha
```

```bash
/mnt/f/Projetos/curso_fullcycle/Git/praticando_gitflow/.git/TAG_EDITMSG *          
0.1.1
#
# Write a message for tag:
#   index
# Lines starting with '#' will be ignored.












                                  [ 5 linhas lidas ]
^G Ajuda      ^O Gravar     ^W Onde está? ^K Recortar   ^T Executar   ^C Local
^X Sair       ^R Ler o arq  ^\ Substituir ^U Colar      ^J Justificar ^/ Ir p/ linha
```

```bash
/mnt/f/Projetos/curso_fullcycle/Git/praticando_gitflow/.git/MERGE_MSG             
Merge tag 'index' into develop

0.1.1
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.









                                  [ 8 linhas lidas ]
^G Ajuda      ^O Gravar     ^W Onde está? ^K Recortar   ^T Executar   ^C Local
^X Sair       ^R Ler o arq  ^\ Substituir ^U Colar      ^J Justificar ^/ Ir p/ linha
```

```bash
╭─   ~/P/curso_f/Git/praticando_gitflow on   hotfix/index ···  base at  23:28:15
╰─❯ git flow hotfix finish index
Switched to branch 'main'
Merge made by the 'ort' strategy.
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
Switched to branch 'develop'
Merge made by the 'ort' strategy.
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
Deleted branch hotfix/index (was 47d2649).

Summary of actions:
- Hotfix branch 'hotfix/index' has been merged into 'main'
- The hotfix was tagged 'index'
- Hotfix tag 'index' has been back-merged into 'develop'
- Hotfix branch 'hotfix/index' has been locally deleted
- You are now on branch 'develop'


╭─   ~/P/curso_f/G/praticando_gitflow on   develop 
╰─❯
```
- vemos que temos as tags
```bash
╭─   ~/P/curso_f/G/praticando_gitflow on   develop 
╰─❯ git tag 

0.1.0
index
(END)
```

[iniciando gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)  
