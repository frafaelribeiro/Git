# Assinar seus commits automaticamente

Para verificar se já existe alguma chave criada executamos o comando:

```bash
╭─   ~/P/curso_fullcycle/Git ······  base at  22:04:16
╰─❯ gpg --list-secret-keys --keyid-format long

```
Para criar uma nova chave executamos:


```bash
╭─   ~/P/curso_fullcycle/Git ······  base at  22:04:16
╰─❯ gpg --full-gen-key
gpg (GnuPG) 2.2.27; Copyright (C) 2021 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Por favor selecione o tipo de chave desejado:
   (1) RSA e RSA (padrão)
   (2) DSA e Elgamal
   (3) DSA (apenas assinatura)
   (4) RSA (apenas assinar)
  (14) Existing key from card
Sua opção? 1
RSA chaves podem ter o seu comprimento entre 1024 e 4096 bits.
Que tamanho de chave você quer? (3072) 4096
O tamanho de chave pedido é 4096 bits
Por favor especifique por quanto tempo a chave deve ser válida.
         0 = chave não expira
      <n>  = chave expira em n dias
      <n>w = chave expira em n semanas
      <n>m = chave expira em n meses
      <n>y = chave expira em n anos
A chave é valida por? (0) 5y
A chave expira em ter 30 nov 2027 22:08:31 -03
Está correto (s/N)? s

GnuPG precisa construir uma ID de usuário para identificar sua chave.

Nome completo: Rafael Ribeiro
Endereço de correio eletrônico: f.rafaelribeiro@gmail.com
Comentário: 
Você selecionou este identificador de usuário:
    "Rafael Ribeiro <f.rafaelribeiro@gmail.com>"

Muda (N)ome, (C)omentário, (E)ndereço ou (O)k/(S)air? O
Precisamos gerar muitos bytes aleatórios. É uma boa idéia realizar outra
atividade (digitar no teclado, mover o mouse, usar os discos) durante a
geração dos números primos; isso dá ao gerador de números aleatórios
uma chance melhor de conseguir entropia suficiente.
Precisamos gerar muitos bytes aleatórios. É uma boa idéia realizar outra
atividade (digitar no teclado, mover o mouse, usar os discos) durante a
geração dos números primos; isso dá ao gerador de números aleatórios
uma chance melhor de conseguir entropia suficiente.
gpg: chave XXXXXXXXXXXXXXX marcada como plenamente confiável
gpg: directory '/home/rafael/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/rafael/.gnupg/openpgp-revocs.d/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX.rev'
chaves pública e privada criadas e assinadas.

pub   rsa4096 2022-12-02 [SC] [expira: 2027-12-01]
      XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
uid                      Rafael Ribeiro <f.rafaelribeiro@gmail.com>
sub   rsa4096 2022-12-02 [E] [expira: 2027-12-01]

```

Verificando a chave gerada:

```bash
╭─   ~/Projetos/curso_fullcycle/Git ············  base at  22:21:16
╰─❯ gpg --list-secret-keys --keyid-format long
/home/rafael/.gnupg/pubring.kbx
-------------------------------
sec   rsa4096/XXXXXXXXXXXXXXX 2022-12-02 [SC] [expira: 2027-12-01]
      XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
uid                 [final] Rafael Ribeiro <f.rafaelribeiro@gmail.com>
ssb   rsa4096/XXXXXXXXXXXXXXX 2022-12-02 [E] [expira: 2027-12-01]
```
Capturando a chave publica através do Id

```bash
╭─   ~/Projetos/curso_fullcycle/Git ············  base at  22:21:26
╰─❯ gpg --armor --export XXXXXXXXXXXXXXX
-----BEGIN PGP PUBLIC KEY BLOCK-----
...

-----END PGP PUBLIC KEY BLOCK-----
```

Copiamos a chave publica e adicionamos no github

No GitHub ir na foto do seu login (canto superior direito) -> settings -> SSH an GPG Keys -> New GPG Key.  

A a partir deste momento o github vai compar a assinatura dos commits com esta chave publica.  

Informar ao git a chave com o qual ele deve assinar os commits.  

```bash
╭─   ~/Projetos/curso_fullcycle/Git ············  base at  22:30:49
╰─❯ git config --global user.signingkey XXXXXXXXXXXXXXX
```
Adicionar a variável de ambiente GPG_TTY no shell (bash_profile, zshrc, etc..)  

```bash
╭─   ~/Projetos/curso_fullcycle/Git ············  base at  22:32:23
╰─❯ vim ~/.zshrc  
...

# GPG 
export GPG_TTY=$(tty)
#
```
Configurando o git para assinar por padrão todos os repositórios e tags

```bash
╭─   ~/Projetos/curso_fullcycle/Git ············  base at  22:40:43
╰─❯ git config --global commit.gpgsign true 

╭─   ~/Projetos/curso_fullcycle/Git ············  base at  22:41:08
╰─❯ git config --global tag.gpgSign true
```
Fazendo teste  

```bash
╭─   ~/Projetos/curso_fullcycle/Git ············  base at  22:42:31
╰─❯ mkdir praticando_assinatura     

╭─   ~/Projetos/curso_fullcycle/Git ············  base at  22:43:33
╰─❯ cd praticando_assinatura

╭─   ~/P/curso_f/G/praticando_assinatura on   master ?1 
╰─❯ cat index.html          
<h1>Teste assinatura</h1>
```


```bash
╭─   ~/P/curso_f/G/praticando_assinatura on   master ?1 
╰─❯ git status
No ramo master

No commits yet

Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)
        index.html

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)

╭─   ~/P/curso_f/G/praticando_assinatura on   master ?1 
╰─❯ git add .

```


```bash
╭─   ~/P/curso_f/G/praticando_assinatura on   master +1 
╰─❯ git status
No ramo master

No commits yet

Mudanças a serem submetidas:
  (utilize "git rm --cached <arquivo>..." para não apresentar)
        new file:   index.html


╭─   ~/P/curso_f/G/praticando_assinatura on   master +1 
╰─❯ git commit -m 'First commit'        
[master (root-commit) 5f5ad55] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 index.html

```
Vai pedir para informar a Frase secreta na primeira utilização.  

Se não tiver usando a configuração de assinatura global pode assinar sobre demanda usando  :  
`git commit -S -m 'First commit'`  

Como verificar se o commit esta assinado  

```bash
╭─   ~/P/curso_f/G/praticando_assinatura on   master 
╰─❯ git log --show-signature -1 

commit 5f5ad55fe7a12e9a22fc2f870329416882c0ccc5 (HEAD -> master)
gpg: Assinatura feita qui 01 dez 2022 22:48:09 -03
gpg:                usando RSA chave XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
gpg: Assinatura correta de "Rafael Ribeiro <f.rafaelribeiro@gmail.com>" [final]
Author: Rafael Ribeiro <f.rafaelribeiro@gmail.com>
Date:   Thu Dec 1 22:48:09 2022 -0300

    First commit
(END)
```
Agora quando realizar um push para o GitHub os commit terão a informação que está verificado.  

Adicionando gpg.conf para utilizar o agent para guarda a Frase secreta.  

```bash
╰─❯ vim ~/.gnupg/gpg.conf  

╰─❯ cat ~/.gnupg/gpg.conf 
use-agent

╰─❯ gpgconf --launch gpg-agent
```

## Adicionando outro email na chave

Listando nossa chave

```bash
╭─   ~/P/curso_f/Git/praticando_assinatura on   master ······  base at  21:40:45
╰─❯ gpg --list-secret-keys --keyid-format long
/home/rafael/.gnupg/pubring.kbx
-------------------------------
sec   rsa4096/21740521A5D4EED9 2022-12-02 [SC] [expira: 2027-12-01]
      XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
uid                 [final] Rafael Ribeiro <f.rafaelribeiro@gmail.com>
ssb   rsa4096/XXXXXXXXXXXXXXX 2022-12-02 [E] [expira: 2027-12-01]
```
Caso a variável GPG_TTY não esteja exportada:  

```bash
╭─   ~/Projetos/curso_fullcycle/Git ·········· took  1m 13s  base at  22:48:56
╰─❯ export GPG_TTY=$(tty)           

╭─   ~/Projetos/curso_fullcycle/Git ························  base at  22:47:21
╰─❯ echo $GPG_TTY        
/dev/pts/4
```

```bash
╭─   ~/Projetos/curso_fullcycle/Git ························  base at  22:47:26
╰─❯ gpg --edit-key XXXXXXXXXXXXXXX 
gpg (GnuPG) 2.2.27; Copyright (C) 2021 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Chave secreta disponível.

sec  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: SC  
     confiança: final         validade: final
ssb  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: E   
[final] (1). Rafael Ribeiro <f.rafaelribeiro@gmail.com>

gpg> adduid 
Nome completo: Rafael Ribeiro
Endereço de correio eletrônico: f.rafaelribeiro@live.com
Comentário: 
Você selecionou este identificador de usuário:
    "Rafael Ribeiro <f.rafaelribeiro@live.com>"

Muda (N)ome, (C)omentário, (E)ndereço ou (O)k/(S)air? O

sec  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: SC  
     confiança: final         validade: final
ssb  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: E   
[final] (1)  Rafael Ribeiro <f.rafaelribeiro@gmail.com>
[ desconhecida] (2). Rafael Ribeiro <f.rafaelribeiro@live.com>

gpg> list

sec  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: SC  
     confiança: final         validade: final
ssb  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: E   
[final] (1)  Rafael Ribeiro <f.rafaelribeiro@gmail.com>
[ desconhecida] (2). Rafael Ribeiro <f.rafaelribeiro@live.com>

gpg> uid 2

sec  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: SC  
     confiança: final         validade: final
ssb  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: E   
[final] (1). Rafael Ribeiro <f.rafaelribeiro@live.com>
[desconhecida] (2)* Rafael Ribeiro <f.rafaelribeiro@gmail.com>

gpg> trust 
sec  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: SC  
     confiança: final         validade: final
ssb  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: E   
[final] (1). Rafael Ribeiro <f.rafaelribeiro@live.com>
[desconhecida] (2)* Rafael Ribeiro <f.rafaelribeiro@gmail.com>

Por favor decida quanto você confia neste usuário para
verificar corretamente as chaves de outros usuários
(olhando em passaportes, checando impressões digitais
de outras fontes...)

  1 = Eu não sei ou nem direi
  2 = Eu NÃO confio
  3 = Eu tenho pouca confiança
  4 = Eu confio totalmente
  5 = Eu confio ao extremo
  m = voltar ao menu principal

Sua decisão? 5
Você quer realmente definir esta chave à confiança final? s

sec  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: SC  
     confiança: final         validade: final
ssb  rsa4096/XXXXXXXXXXXXXXX
     criado: 2022-12-02  expira: 2027-12-01  uso: E   
[final] (1). Rafael Ribeiro <f.rafaelribeiro@live.com>
[desconhecida] (2)* Rafael Ribeiro <f.rafaelribeiro@gmail.com>

gpg> save

```

```bash
╭─   ~/Projetos/curso_fullcycle ·············· took  1m 39s  base at  22:59:54
╰─❯ gpg --list-secret-keys --keyid-format=long
gpg: checando o trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: profundidade: 0 válidas:   1 assinadas:   0 confiança: 0-, 0q, 0n, 0m, 0f, 1u
gpg: próxima checagem de banco de dados de confiabilidade em 2027-12-01
/home/rafael/.gnupg/pubring.kbx
-------------------------------
sec   rsa4096/XXXXXXXXXXXXXXX 2022-12-02 [SC] [expira: 2027-12-01]
      XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
uid                 [final] Rafael Ribeiro <f.rafaelribeiro@live.com>
uid                 [final] Rafael Ribeiro <f.rafaelribeiro@gmail.com>
ssb   rsa4096/XXXXXXXXXXXXXXX 2022-12-02 [E] [expira: 2027-12-01]
```
