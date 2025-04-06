# ASSINANDO COMMITS NO GIT COM VÁRIAS CONTAS: O GUIA COMPLETO (WINDOWS, LINUX e MACOS)

![Banner](./images/banner.png)

- [Ver no Medium](https://tanabebruno.medium.com/assinando-commits-no-git-com-várias-contas-o-guia-completo-windows-linux-e-macos-ea2232212015)
- [Ver em ingles](README.md)

Se você já passou pelo desafio de configurar múltiplas chaves SSH e agora quer dar um passo além na segurança e confiabilidade dos seus commits, chegou ao lugar certo! Neste guia, vamos continuar exatamente de onde paramos no [tutorial anterior](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13), só que agora falando de chaves GPG para assinar seus commits. Assim, você ganha aquele selo de “Verified” (mais estiloso que qualquer check do Twitter) e garante que todo mundo saiba que quem fez o commit foi realmente você! 🤩

Sabe aquelas empresas que exigem commits assinados, ou aquele momento em que você quer mostrar que o código é genuinamente seu (sem clonagem ou invasão)? Pois é aí que entra o GPG como seu melhor aliado, garantindo integridade e autenticidade. E, claro, vamos manter o clima leve de sempre: dá pra se divertir enquanto aprende a configurar duas ou mais chaves GPG sem complicação. 🚀

Bora deixar tudo rodando suave e assinado? Vamos lá! ✋

**IMPORTANTE**: Esse tutorial é a segunda parte de uma série. Se você ainda não leu o primeiro, recomendo dar uma olhada no tutorial de [Como configurar duas ou mais chaves SSH para ter diversas contas Git no mesmo computador? (Windows, Linux e MacOs)](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13) antes de continuar aqui, porque vou continuar esse tutorial de onde o último parou e você precisa fazer algumas coonfigurações que foram feitas e explicadas lá. Além disso, você vai entender melhor como tudo se conecta e fica mais fácil de acompanhar. 😉

---

## Sumário 📌

**Bora ver o que você vai ver nesse guia?** 🔍

- [ASSINANDO COMMITS NO GIT COM VÁRIAS CONTAS: O GUIA COMPLETO (WINDOWS, LINUX e MACOS)](#assinando-commits-no-git-com-várias-contas-o-guia-completo-windows-linux-e-macos)
  - [Sumário 📌](#sumário-)
  - [1. O que são chaves GPG? 🤔](#1-o-que-são-chaves-gpg-)
  - [2. Por que configurar mais de uma chave GPG? 🔒](#2-por-que-configurar-mais-de-uma-chave-gpg-)
  - [3. Pré-requisitos: assegurando que o GPG está instalado 🔧](#3-pré-requisitos-assegurando-que-o-gpg-está-instalado-)
    - [Windows](#windows)
    - [Linux](#linux)
    - [MacOS](#macos)
  - [4. Gerando as novas chaves GPG 🔑](#4-gerando-as-novas-chaves-gpg-)
    - [Windows, Linux e MacOS](#windows-linux-e-macos)
    - [IMPORTANTE](#importante)
  - [5. Configurando o Git para usar as chaves GPG corretas 🔧](#5-configurando-o-git-para-usar-as-chaves-gpg-corretas-)
    - [Windows, Linux e MacOS (parte comum)](#windows-linux-e-macos-parte-comum)
    - [Windows](#windows-1)
    - [Linux e MacOS](#linux-e-macos)
  - [6. Cópia das chaves GPG para colocá-las nos serviços ☁️](#6-cópia-das-chaves-gpg-para-colocá-las-nos-serviços-️)
    - [Windows, Linux e MacOS](#windows-linux-e-macos-1)
  - [7. Adicionando as chaves GPG nos serviços (GitHub, GitLab, Bitbucket, etc) ☁️](#7-adicionando-as-chaves-gpg-nos-serviços-github-gitlab-bitbucket-etc-️)
    - [GitHub](#github)
    - [GitLab](#gitlab)
    - [BitBucket](#bitbucket)
  - [8. Como assinar os commits? ✍️](#8-como-assinar-os-commits-️)
    - [Assinando os commits automaticamente](#assinando-os-commits-automaticamente)
    - [Assinando os commits manualmente](#assinando-os-commits-manualmente)
  - [9. Conclusão 🎉](#9-conclusão-)
  - [Quem é Bruno Tanabe?](#quem-é-bruno-tanabe)

---

## 1. O que são chaves GPG? 🤔

Pensa no **GPG (GNU Privacy Guard)** como um super-herói da criptografia que não só protege a identidade de quem está fazendo o commit, mas também garante a integridade do que está sendo enviado. Em vez de só provar “quem é” você, ele mostra que foi **exatamente** você quem assinou aquele commit — sem chance de fraude ou invasão de hackers de plantão. 🕵️‍♂️

Quando você assina um commit com GPG, recebe aquele **selo de autenticidade** (o “Verified”) que deixa tudo com cara de profissional. É tipo colocar um **cadeado poderoso** nos seus commits, mostrando pra todo mundo que eles são legítimos e foram gerados por você mesmo.

E por que isso é tão legal? Porque, além de aumentar a confiança no histórico do projeto, você evita aquela bagunça de alguém se passando por você — e ainda pode separar o que é pessoal do que é trabalho só **trocando de chave**! Imagina um esquema tipo “Clark Kent” (seu login de trabalho) e “Superman” (sua conta pessoal), cada um com sua própria assinatura. ⚡️

Resumindo: GPG é aquele toque extra de segurança e credibilidade. Quer deixar seus commits com uma carinha de “isso aqui é sério e foi feito por mim mesmo”? Então bora adotar as chaves GPG nesse seu rolê Git e sair voando de capa em busca de commits mais seguros! ✨

---

## 2. Por que configurar mais de uma chave GPG? 🔒

Se você já teve que lidar com múltiplas contas Git (seja pra projetos pessoais, trabalho ou clientes), provavelmente já entendeu que a **organização** é o segredo pra não perder a cabeça. Agora, quando falamos em **chaves GPG**, a conversa sobe mais um degrau: você não quer só provar que é você nos commits, mas sim provar de **quais** contas vem cada commit, né?  

Imagine o cenário:  

- 💼 Sua **conta de trabalho** precisa daquela assinatura verificada, mostrando que os commits vieram “oficialmente” do seu time ou empresa.  
- 🏠 Sua **conta pessoal**, em paralelo, assina cada commit com sua própria chave, adicionando mais segurança e autenticidade aos seus projetos.  

Ter várias chaves GPG diferentes pra cada uma dessas contas é a maneira mais prática de **separar** (e assinar) o que é pessoal do que é de trabalho. E o melhor? Sem confundir o Git, sem precisar ficar lembrando de trocar configurações toda hora e, claro, com aquele selo de “Verified” que deixa tudo com uma cara de “profissa”.  

Em vez de “brincar” de copiar/colar chaves, você configura cada uma delas direitinho e pronto: na hora de assinar, o Git sabe exatamente qual usar. Assim, no seu repositório de trabalho, fica claro que foram seus commits “oficiais”, e nos seus projetos pessoais, a assinatura vem de outro “você” (mas ainda assim, é tudo você, só que organizando a bagunça).  

E bora combinar que, quando o assunto é **segurança**, nunca é demais ter cada “ambiente” isolado pra não dar chance ao azar. Então, se você curtiu a ideia de garantir que ninguém vai se passar por você (mesmo que seja só pra uma zoeira no seu repositório), vambora ver como configurar essas chaves GPG e deixar tudo fluindo tranquilo… e **assinado**! ✍️✨

---

## 3. Pré-requisitos: assegurando que o GPG está instalado 🔧

Antes de sair criando suas chaves e dando aquela assinatura top nos commits, precisamos garantir que o **GPG** já está na sua máquina, prontinho pra entrar em ação. Afinal, sem essa ferramenta do nosso super-herói da criptografia, não tem como rolar o show das assinaturas verificadas. 🎉

A boa notícia é que o processo de instalação é supertranquilo:

### Windows

[Acesse o site oficial do **Gpg4win** na página de downloads](https://gpg4win.org/get-gpg4win.html).

Depois de baixar, clique no arquivo `.exe` e execute como **Administrador**.

Vai abrir aquele instalador clássico cheio de “Next”. Quando aparecer a opção com os recursos que você quer instalar, escolha apenas o GnuPG. Ele é o que vai fazer a mágica acontecer, apenas ele é necessário pra gente. O Kleopatra e o GpgOL são legais, mas não são obrigatórios pra nossa missão de assinar commits. Então, desmarque eles e siga em frente. 🚀

Quando terminar, abra o terminal (**Prompt de Comando ou PowerShell**) e digite:

```bash
   gpg --version
```

Se aparecer o número da versão do GPG, sucesso! Você já pode voar de capa por aí assinando commits. 🚀

### Linux

Abra o terminal e tente:

```bash
   gpg --version
```

Se rolar a versão do GPG, maravilha — tá pronto. Se não, basta instalar:

```bash
   sudo apt-get install gnupg
```

(Ou o gerenciador de pacotes da sua distro, tipo `yum`, `dnf`, etc.) Cinco minutinhos e… já era. 🔧

### MacOS

Abra o Terminal e digite:

```bash
   gpg --version
```

Se vier a versão, ótimo. Caso contrário, você pode instalar via [Homebrew](https://brew.sh/):

```bash
   brew install gnupg
```

Em poucos instantes, já tá tudo no jeito. 🍏

Pronto! Com o GPG **oficialmente** liberado pra dar aquela força na segurança, a festa dos commits verificados pode continuar. Agora é só partir pro próximo passo e começar a configurar de verdade suas chaves GPG. Partiu? ✨

---

## 4. Gerando as novas chaves GPG 🔑

Agora que já temos o GPG instalado e pronto pra ação, é hora de criar as chaves GPG que vão dar aquele toque especial nos seus commits. E não se preocupe, o processo é bem tranquilo e rápido! Vamos lá? 🚀

Como vocês viram no [tutorial anterior](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13) com as chaves **SSH**, eu gosto de isolar as chaves em uma pasta específica na raiz do meu usuário. Isso ajuda a manter tudo organizado e facilita na hora de encontrar as chaves que você precisa. Então, vamos criar uma pasta chamada `gpg` dentro do diretório `.ssh` que já criamos antes. Se você não fez isso, não tem problema, mas recomendo fortemente que faça! 😉

### Windows, Linux e MacOS

Vamos ao passo-a-passo. Funciona igual no Windows, Linux e MacOs então aqui não tem diferença de sistema:

Abra o terminal da sua máquina e garanta que você está na raiz do seu usuário. Você pode fazer isso com o comando:

```bash
    cd ~
```

Agora, vamos criar a pasta `.gpg` na raiz do seu usuário:

```bash
    mkdir .gpg
```

**Pasta criada!** Agora, vamos entrar nela:

```bash
    cd .gpg
```

Agora vem a parte importante: **gerar as chaves GPG**. Assim como no [tutorial anterior](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13), eu vou criar duas chaves GPG, uma para cada uma das minhas contas, uma ´pessoal´ e outra do ´trabalho´. Caso você tenha mais de duas contas, basta criar uma chave para cada uma delas, o processo é o mesmo.

```bash
    gpg --full-generate-key
```

Nesse momento, o GPG vai te fazer uma série de perguntas. E basta você escolher as opções que mais fazem sentido pra você. Aqui estão as opções que eu escolhi:

- **Tipo de chave**: (9) ECC (de assinar e cifrar) *pré-definição*
- **Curva Elliptica**: (1) Curve 25519 *pré-definição*
- **Expiração**: (0) Nunca expira *pré-definição* (Se você escolher uma data de expiração, você vai precisar gerar uma nova chave quando ela expirar.)

### IMPORTANTE

As três últimas opções são as mais importantes, então preste atenção:

- **Nome**: Aqui você vai colocar o nome que você quer que apareça nos commits. Eu recomendo que você coloque o mesmo nome que você colocou na sua conta do GitHub, GitLab, Bitbucket ou o que você estiver usando. Isso vai ajudar a identificar os commits mais facilmente.
- **Email**: Aqui você **OBRIGATÓRIAMENTE*** vai colocar o email que você usou na sua conta do GitHub, GitLab, Bitbucket ou o que você estiver usando. Se você não colocar o email correto, o GPG não vai conseguir verificar os commits e você vai ficar sem aquele selo de “Verified”. Então, preste atenção nessa parte! 😉
- **Comentário**: Esse campo é opcional e não é tão importante, ele está classificado como importante apenas para manter ordem do tutorial. Você pode deixar em branco ou colocar algo que faça sentido pra você.

Agora vou repetir o processo para a segunda chave, que vai ser a chave da minha conta de trabalho. O processo é o mesmo, mas você vai colocar o **nome** e o **email** da sua outra conta.

```bash
    gpg --full-generate-key
```

Sobre as opções, você pode escolher as mesmas que escolhemos antes, mas lembre-se de colocar o nome e o email da sua conta de trabalho.

*Repita o processo quantas vezes forem necessárias para criar as chaves que você precisa.*

---

## 5. Configurando o Git para usar as chaves GPG corretas 🔧

Você já tem suas chaves GPG prontinhas e agora é hora de fazer o Git reconhecer essas belezuras. E não se preocupe, o processo é bem simples! Vamos lá? 🚀

Se lembra que no último [tutorial](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13) criamos um arquivo `.gitconfig` para cada uma das contas? Então, agora vamos adicionar as chaves GPG nesse arquivo. O processo é o mesmo, só que agora vamos adicionar a chave GPG ao invés da chave SSH.

Aqui está o passo-a-passo:

### Windows, Linux e MacOS (parte comum)

Primeiro, você precisa descobrir o ID da chave GPG que você acabou de criar. Para isso, basta rodar o seguinte comando:

```bash
    gpg --list-secret-keys --keyid-format LONG
```

Esse comando vai listar todas as chaves GPG que você tem na sua máquina. Você vai ver algo parecido com isso:

```bash
   sec   ed25519/8AEDA33EA0CA3AF6 2024-10-24 [SC] [expires: 2025-10-24]
         8F2F8C1E26E0069BC7FE7E258AEDA33EA0CA3AF6
   uid                 [ultimate] Bruno Tanabe (My Personal Key) <brunotanabe@personal.com>
   ssb   cv25519/458RRDCC83ER4528 2024-10-24 [E] [expires: 2025-10-24]

   sec  ed25519/5A3F4B2D7E8C9A88 2024-10-24 [SC] [expires: 2025-10-24]
        A8AYTC1E26AFE7E2585A3F4B2D7E8C9ADADFC9A
   uid                 [ultimate] Bruno Tanabe (My Work Key) brunotanabe@work.com>
   ssb   cv25519/87A3F4B283ER49A 2024-10-24 [E] [expires: 2025-10-24]
```

Você vai ter uma chave para cada uma das contas que você tem. O que você precisa fazer agora é copiar o ID de cada uma das chaves. O ID da chave é a parte que está entre a barra `/` e o espaço, no caso do exemplo acima, o ID da chave pessoal é `8AEDA33EA0CA3AF6` e o ID da chave de trabalho é `5A3F4B2D7E8C9A88`.

Lembra do último [tutorial](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13), onde criamos um arquivo `.gitconfig` para cada uma das contas? Então, agora vamos adicionar a chave GPG nesse arquivo. O processo é o mesmo, só que agora vamos adicionar a chave GPG ao invés da chave SSH.

No terminal, vamos acessar o arquivo `.gitconfig` da conta que você quer adicionar a chave GPG. No meu caso, os arquivos `.gitconfig` de cada uma das contas estão na pasta `.git` na raiz do meu usuário (como criamos no último tutorial). Então, o próximo passo é acessar os arquivos `.gitconfig` de cada uma das contas. Para isso, basta rodar o seguinte comando:

```bash
    cd ~/.git
```

Agora vamos editar o arquivo `.gitconfig` da conta que você quer adicionar a chave GPG. E por isso, o tutorial será diferente para cada sistema operacional. Vamos lá:

### Windows

Abra o arquivo com o **Notepad** (ou qualquer editor que preferir):

   ```bash
   notepad .gitconfig-personal
   ```

Dentro do arquivo, você vai adicionar a seguinte linha `signingkey = 8AEDA33EA0CA3AF6`, modificada com o ID da chave dessa conta. O arquivo vai parecido com:

```ini
   [user]
      name = Bruno Tanabe Personal
      email = brunotanabe@personal.com
      signingkey = 8AEDA33EA0CA3AF6
   [core]
      sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
```

**Mas Tanabe, como vou saber qual ID pertence a cada conta?**
Simples! Quando você criou a chave, você colocou o nome e o email da conta que você queria. Então, basta olhar o ID da chave e ver qual é o nome e o email que você colocou. Assim, você vai saber qual ID pertence a cada conta. Mas e se as contas tiverem o mesmo nome e email? Nesse caso, não tem diferença, você pode usar o mesmo ID para as duas contas ou selecionar qualquer uma das duas chaves. O importante é que você saiba qual ID pertence a cada conta.

Perfeito! Agora, vamos fazer a mesma coisa para a conta de trabalho. O processo é o mesmo, só que agora você vai adicionar a chave GPG da conta de trabalho. Então, abra o arquivo `.gitconfig` da conta de trabalho:

```bash
   notepad .gitconfig-work
```

O arquivo ficará parecido com:

```ini
   [user]
      name = Bruno Tanabe Work
      email = brunotanabe@work.com
      signingkey = 5A3F4B2D7E8C9A88
   [core]
      sshCommand = "ssh -i ~/.ssh/work_ssh_key"
```

Basta repetir o processo para cada uma das contas que você tem. E pronto! Agora você já tem suas chaves GPG configuradas e prontas pra dar aquele toque especial nos seus commits. 🚀

### Linux e MacOS

Abra o arquivo com o **nano** (ou qualquer editor que preferir):

```bash
   nano .gitconfig-personal
```

Dentro do arquivo, você vai adicionar a seguinte linha `signingkey = 8AEDA33EA0CA3AF6`, modificada com o ID da chave dessa conta. O arquivo vai parecido com:

```ini
   [user]
      name = Bruno Tanabe Personal
      email = brunotanabe@personal.com
      signingkey = 8AEDA33EA0CA3AF6
   [core]
      sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
```

**Mas Tanabe, como vou saber qual ID pertence a cada conta?**  
Simples! Quando você criou a chave, você colocou o nome e o email da conta que você queria. Então, basta olhar o ID da chave e ver qual é o nome e o email que você colocou. Assim, você vai saber qual ID pertence a cada conta. Mas e se as contas tiverem o mesmo nome e email? Nesse caso, não tem diferença, você pode usar o mesmo ID para as duas contas ou selecionar qualquer uma das duas chaves. O importante é que você saiba qual ID pertence a cada conta.

Perfeito! Agora, vamos fazer a mesma coisa para a conta de trabalho. O processo é o mesmo, só que agora você vai adicionar a chave GPG da conta de trabalho. Então, abra o arquivo `.gitconfig` da conta de trabalho:

```bash
   nano .gitconfig-work
```

O arquivo ficará parecido com:

```ini
   [user]
      name = Bruno Tanabe Work
      email = brunotanabe@work.com
      signingkey = 5A3F4B2D7E8C9A88
   [core]
      sshCommand = "ssh -i ~/.ssh/work_ssh_key"
```

Basta repetir o processo para cada uma das contas que você tem. E pronto! Agora você já tem suas chaves GPG configuradas e prontas pra dar aquele toque especial nos seus commits. 🚀

---

## 6. Cópia das chaves GPG para colocá-las nos serviços ☁️

Agora que você já tem suas chaves GPG configuradas, é hora de copiá-las para colar nos serviços que você usa (GitHub, GitLab, Bitbucket, etc.). É bem simples: esses serviços só precisam da **chave pública** pra verificar seus commits. Então, basta copiar essa parte da chave GPG e inserir na plataforma que você preferir ― rapidinho você garante aquele selo de “Verified”! 🚀

### Windows, Linux e MacOS

Novamente, você vai precisar do seguite comando para listar as informações de cada uma das suas chaves GPG:

```bash
    gpg --list-secret-keys --keyid-format LONG
```

Esse comando vai listar todas as chaves GPG que você tem na sua máquina. Você vai ver algo parecido com isso:

```bash
   sec   ed25519/8AEDA33EA0CA3AF6 2024-10-24 [SC] [expires: 2025-10-24]
         8F2F8C1E26E0069BC7FE7E258AEDA33EA0CA3AF6
   uid                 [ultimate] Bruno Tanabe (My Personal Key) <brunotanabe@personal.com>
   ssb   cv25519/458RRDCC83ER4528 2024-10-24 [E] [expires: 2025-10-24]

   sec  ed25519/5A3F4B2D7E8C9A88 2024-10-24 [SC] [expires: 2025-10-24]
        A8AYTC1E26AFE7E2585A3F4B2D7E8C9ADADFC9A
   uid                 [ultimate] Bruno Tanabe (My Work Key) brunotanabe@work.com>
   ssb   cv25519/87A3F4B283ER49A 2024-10-24 [E] [expires: 2025-10-24]
```

Agora, ao invés de anotar o ID da chave para utilizar, você deve anotar a impressão digital `fingerprint` da chave, que é a sequência de números e letras que aparece logo abaixo do ID da chave. No caso do exemplo acima, a impressão digital da chave pessoal é `8F2F8C1E26E0069BC7FE7E258AEDA33EA0CA3AF6` e a impressão digital da chave de trabalho é `A8AYTC1E26AFE7E2585A3F4B2D7E8C9ADADFC9A`.

Feito isso, é hora de usá-lo pra copiar a chave pública. O comando é o mesmo em todos os sistemas operacionais, basta substituir a impressão digital da chave pela da chave que você quer copiar. Por exemplo, se for a conta pessoal a impressão digital é `8F2F8C1E26E0069BC7FE7E258AEDA33EA0CA3AF6` e o comando vai ficar assim:

```bash
   gpg --armor --export 8F2F8C1E26E0069BC7FE7E258AEDA33EA0CA3AF6
```

Esse comando vai gerar uma chave pública que você pode copiar e colar na plataforma que você quiser. O resultado vai ser algo parecido com isso:

```bash
   -----BEGIN PGP PUBLIC KEY BLOCK-----

   4bOkOJy0eUJydW5vIFRhbmFiZSAoRmVpdG8gY29tIGFtb3I/IE7ilJzDum8sIGZl
   d2p8u1j/Arg4BGfrUlcSCisGAQQBl1UBBQEBB0BYYWYdzHtrGMIPo/Dk1cgc0JPo
   b3IuIGNvbSBkZWRpY2HilJzCuuKUnMO6by4gUG9yIEJydW5vIFRhbmFiZSEpIDxi
   ruSgH33JThIPRlDurrzjPSIIeSHAP47x6f29Lrm7w0ksdYfxVQ1fo/e/+V2mtNPb
   QJn61JXAhsMAAoJEOXVOzy94AH7VjIBALW9dBGGjjM1GWRMcCEECvHV57IJgoBuG
   brVfpcaPCs/1IAMBCAeIeAQYFgoAIBYhBC8CfJ+0aWPB5M2J2uXVOzy94AH7BQJn
   94AH7BQJn61JXAhsDBQsJCAcCAiICBhUKCQgLAgQWAgMBAh4HAheAAAoJEOXVOzy9
   W9dBGGjjM1GWRMcCEECvHV57IJgoBuGGbT942xT4SbAP441tlp5bLy7EobHSOHmk
   Z+tSVxYJKwYBBAHaRw8BAQdARcc22jcKOHSJjLYQCga9nG0nnLqWvDhaPfWz
   nLqWvDhaPfWzZ+tSVxYJKwYBBAHaRw8BAQdARcc22jcKOHSJjLYQCga9nG0
   CF8xYhBC8CfJ+0aWPB5M2J2uXVOzy94AH7BQJn61JXAhsMAAoJEOXVOzy94AH7Vj
   McCEECvHV57IJgoBuGGbT942xT4SbAP441tlp5bLy7EobHSOHmkeqiiDbfRhnlJl
   Tf0bkK+GAw==W9dBGGjjM1GWRMc
   -----END PGP PUBLIC KEY BLOCK-----
```

Você deve copiar de `-----BEGIN PGP PUBLIC KEY BLOCK-----` até `-----END PGP PUBLIC KEY BLOCK-----`. E pronto! Agora é só colar na plataforma que você quiser e garantir aquele selo de “Verified” nos seus commits. 🚀

Caso você tenha mais de uma chave, basta repetir o processo para cada uma delas. E não se preocupe, o processo é o mesmo, só muda o ID da chave. Então, se você tem duas chaves, basta rodar o comando duas vezes, uma para cada chave. Se eu fosse rodar o comando para a chave de trabalho, ficaria assim:

```bash
   gpg --armor --export E6BF4F45C3ADD6950420C1D4F94F3E72C3DD5962
```

Eu recomendo que você vá copiando cada chave e adicionando ela a cada serviço correspondente, então fique alternando entre os passos 7 e 8. 🔄

---

## 7. Adicionando as chaves GPG nos serviços (GitHub, GitLab, Bitbucket, etc) ☁️

Boa notícia: toda a configuração no seu computador já tá pronta! Agora falta só um detalhe pra tudo funcionar redondinho — avisar pros serviços de controle de versão (GitHub, GitLab, Bitbucket ou qualquer outro) que você tem uma chave GPG e que eles podem assinar os commits com ela. Isso é super simples e rápido, só precisa colar a chave pública que você copiou no passo anterior. 🖥️✨

Agora que você já copiou as chaves, bora colar no seu serviço favorito:

Aqui você verá como adicionar as chaves nos principais serviços de versionamento de código, mas caso use outro basta achar uma sessão semelhante e adicionar as chaves.

### GitHub

1. Acesse: [https://github.com/settings/keys](https://github.com/settings/keys)
2. Clique em **New GPG key**.
3. Dê um nome pra chave (ex: **Personal** ou **Work**).
4. Cole o conteúdo da chave pública no campo **Key**.
5. Clique em **Add GPG key**. Pronto! ✅

### GitLab

1. Acesse: [https://gitlab.com/-/profile/gpg_keys](https://gitlab.com/-/profile/gpg_keys)
2. No campo **Key**, cole sua chave pública.
3. Dê um título pra identificar (ex: **Pessoal** ou **Trabalho**).
4. Clique em **Add key**. 🔑

### BitBucket

1. Acesse: [https://bitbucket.org/account/settings/gpg-keys/](https://bitbucket.org/account/settings/gpg-keys/)
2. Clique em **Add key**.
3. No campo **Label**, dê um nome pra sua chave.
4. No campo **Key**, cole sua chave pública.
5. Salve. 💾

E pronto! Agora você já tem suas chaves GPG adicionadas nos serviços e pode começar a assinar seus commits com elas. 🚀

---

## 8. Como assinar os commits? ✍️

Agora que você já tem suas chaves GPG configuradas e adicionadas nos serviços, é hora de aprender a assinar os commits. E não se preocupe, o processo é bem simples! Vamos lá? 🚀

Você pode assinar os commits de duas formas: **automaticamente** ou **manualmente**. Vou te mostrar como fazer os dois, assim você escolhe o que mais combina com você. 😉

### Assinando os commits automaticamente

Para assinar os commits automaticamente, basta dar o seguinte comando no terminal:

```bash
   git config --global commit.gpgSign true
```

Esse comando basicamente vai adicionar a seguinte linha no seu arquivo `.gitconfig`:

```ini
   [commit]
      gpgSign = true
```

Dessa forma, todos os commits que você fizer vão ser assinados automaticamente com a chave GPG que você configurou. E o melhor: não precisa fazer nada diferente do que você já faz! É só fazer o commit normalmente e pronto. 🚀

### Assinando os commits manualmente

Caso você não queira assinar todos os commits, você pode assinar os commits manualmente (não consigo imaginar nenhum motivo para você não querer assinar todos os seus commits, mas alguns desenvolvedores são estranhos). Para isso, basta adicionar a flag `-S` no comando de commit:

```bash
   git commit -S -m "Mensagem do commit"
```

Esse comando vai assinar o commit com a chave GPG que você configurou. E o melhor: você pode usar esse comando em qualquer repositório, não precisa fazer nada diferente do que você já faz! É só fazer o commit normalmente e pronto. 🚀

---

## 9. Conclusão 🎉

Olha só até onde você chegou! Já sabe gerar chaves, configurar o Git pra usar cada uma delas e ainda colar tudo direitinho nos serviços que você usa. Nada mal, hein? 🚀  

Com as chaves GPG, cada commit passa a ser **seu cartão de visita** (com direito a selo de “Verified” e tudo), mostrando que a segurança é levada a sério no seu workflow. Além disso, ter chaves diferentes pra cada conta (pessoal, trabalho, frila...) deixa tudo organizado e evita confusão quando você estiver no ritmo frenético de commits.  

Agora é só partir pro abraço: aproveite a sensação de ter seus commits assinados e devidamente “verificados” em qualquer repo por aí. E se der vontade de criar novas chaves pra outros projetos ou contas, você já sabe bem o caminho. Então, bora continuar explorando as infinitas possibilidades do Git e do GPG — seu histórico de commits agradece! ✨

---

## Quem é Bruno Tanabe?

Se você chegou até aqui e ainda não se perguntou “quem diabos é esse cara que me fez configurar tudo isso?”, parabéns pela paciência! Mas, caso tenha ficado curioso, deixa eu me apresentar rapidinho. 👋

Sou **Bruno Tanabe**, desenvolvedor focado em backend e inteligência artificial, sempre criando soluções escaláveis e inovadoras (ou pelo menos tentando). Se curtiu o tutorial e quiser trocar uma ideia, aqui estão meus contatos:

Me encontra aqui:

- [LinkedIn](https://www.linkedin.com/in/tanabebruno/)
- [GitHub](https://github.com/BrunoTanabe)
- [Email](mailto:tanabebruno@gmail.com)
- [Medium](https://medium.com/@tanabebruno)

Agora sim, missão cumprida! 🎯

---
