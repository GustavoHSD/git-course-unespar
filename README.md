# Git
Mini curso de git para a semana da computação da UNESPAR - Apucarana

# Sumário

1. [Introdução](#introdução)
2. [Controle de Versão](#controle-de-versão)
   1. [Surgimento do Git](#surgimento-do-git)
   2. [Instalação e Setup](#instalação-e-setup)
3. [Fundamentos do Git](#fundamentos-do-git)
   1. [Inicializando Repositório](#inicializando-repositório)
   2. [Salvando Mudanças no Repositório](#salvando-mudanças-no-repositório)
   3. [Commits](#commits)
   4. [Repositórios Remotos](#repositórios-remotos)
4. [Git Branching](#git-branching)
   1. [O que é Branch](#o-que-é-branch)
   2. [Branch e Merge](#branch-e-merge)
   3. [Gerenciamento de Branch](#gerenciamento-de-branch)
5. [Exemplos de Uso](#exemplos-de-uso)

# Introdução<a name="introdução"/>

## Controle de Versão

O controle de versão é um sistema fundamental que registra e gerencia as alterações em arquivos, permitindo a recuperação de versões específicas. 

O método de controle de versão de muitas pessoas é fazer cópias de arquivos para outra pasta. É um modo simples, porém muito suscetível a erros.

Para resolver isso foram desenvolvidos os VCSs (Version Control System) locais, que têm um simples banco de dados que mantém todas as mudanças nos arquivos, como ilustrado na imagem a seguir: 

<p align="center">
  <img src="https://git-scm.com/book/en/v2/images/local.png" alt="Controle de versão local">
</p>

##### Figura 1. Controle de versão local


### Surgimento do Git<a name="surgimento-do-git"/>

Por volta de 2002, o kernel do Linux adotou a ferramenta de controle de versão proprietária chamada BitKeeper. Contudo, a parceria chegou ao fim em 2005, resultando na revogação do acesso gratuito à ferramenta. Diante dessa situação, a comunidade Linux sentiu a necessidade de criar sua própria solução de controle de versão, guiada por objetivos específicos:

- **Eficiência**: Desenvolver uma ferramenta ágil para gerenciar o versionamento de código de maneira eficaz.
- **Simplicidade**: Manter uma abordagem intuitiva e de fácil utilização, sem adicionar complexidades desnecessárias.
- **Suporte para Desenvolvimento Não-Linear (Branches)**: Permitir a criação e gestão eficiente de ramificações no desenvolvimento de software.
- **Completamente Descentralizado**: Adotar uma arquitetura descentralizada para promover autonomia e colaboração entre os desenvolvedores, eliminando a dependência de um ponto centralizado.
- **Capacidade de Gerenciar Projetos de Grande Escala**: Possuir recursos robustos para gerenciar efetivamente projetos extensos, assegurando escalabilidade e desempenho.

Esses princípios nortearam a criação de uma nova ferramenta de controle de versão, culminando no desenvolvimento do Git, que não apenas atendeu às demandas da comunidade Linux, mas também se tornou uma base sólida para a evolução contínua do controle de versão.

### Instalação e Setup<a name="instalação-e-setup"/>

#### Instalação
O Git é multiplataforma, o que significa que pode ser instalado em varios sistemas, como linux, windows e macOS.

O processo de instalação é muito simples, no linux normalmente é possivel instalar pelo package manager da distribuição:

Para sistemas baseados em debian:

```
sudo apt install git-all
```

Para Windows é só fazer o download do instalador <a href="https://git-scm.com/download/win">aqui</a>.

Para verificar a instalação é só digitar `git` ou `git --version` no terminal.

#### Setup

Agora que o Git está instalado é necessario fazer algumas configurações.

Git vem com uma ferramenta chamada `git config` que permite setar variaveis que o Git usa para operar corretamente. Essas variaveis são armazenadas em 3 lugares diferentes:
   
   1. `[path]/etc/gitconfig` ficam salvas variaveis para todos usuarios do sistema, para salvar ou ler desse arquivo é utilizado o comando `git config` com a flag `--system`.

   2. `~/.gitconfig` ou `~/.config/git/config` estão as variaveis especificas ao usuario. Para salvar e ler desse arquivo é utilizada a flag `--global`.

   3. `.git/config` estara dentro do repositório que está em uso, as variaveis armazenadas aqui são especificas do repositório. Para acessa-lo a flag `--local` é utilizada.

Você pode ver todas configurações salvas com o comando:
```
git config --list --show-origin
```
A primeira coisa a ser feita após a instalação é setar o nome e email.
Essas informações são usadas por todas commits do Git.

Para configurar username e email utiliza-se os seguintes comandos:

```
git config --global user.name "User Name"
git config --global user.email "user.name@exemple.com"
```

## Fundamentos do Git<a name="fundamentos-do-git"/>

### Inicializando Repositório<a name="inicializando-repositório"/>

Existem duas formas de ter um repositorio:

   1. Inicializar o repositorio em uma pasta qualquer do seu computador.

   2. Clonar um repositório de algum outro lugar, como o Github por exemplo.

#### 1. Inicializando Repositório localmente

Navegue até a pasta que deseja inicializar o repositorio:

Linux:
```
cd /home/user/my_project
```
Windows:
```
cd C:/Users/user/my_project
```

Agora digite:
```
git init
```
Esse comando criara um pasta chamada `.git`, que tem todos arquivos necessarios para o Git.

Para começar a controlar versões de arquivos existentes é necessário rastrear esses arquivos e fazer um commit inicial. Podemos fazer isso com alguns comandos.

`git add` que especifica os arquivos que você deseja rastrear
`git commit` para fazer o commit inicial:

É uma pratica comum ter um README que tem algumas informações do repositório, vamos usar ele como exemplo para primeira commit.

Criar README.md no Linux ou macOS:
```
touch README.md
echo "Curso de git" >> README.md
```

No windows:
```
echo. > README.md
echo Curso de git >> README.md
```

```
git add README.md
git commit -m "Commit inicial: adiocnar README ao projeto" 
```

#### 2. Clonando repositório

Quando clonando um repositório não é só uma copia dos arquivos do projeto, o Git faz o download de quase todos os dados do repositório incluido todas versões de todos arquivos.

Um repositório é clonado com o comando `git clone <url>`.

Use o comando a baixo para clonar esse repositorio:
```
git clone https://github.com/GustavoHSD/Git-Course_Unespar.git
```

### Salvando Mudanças no Repositório<a name="salvando-mudanças-no-repositório"/>

Agora com um repositório Git criado é só fazer alterações nos arquivos do projeto e adicionar commits dessas alterações a cada vez que chegar em um estado que você deseja salvar.

Cada arquivo do repositório pode estar em um de 2 estados: rastreado e não-rastreado. Em resumo arquivos rastreados são arquivos que o Git conhece.

Arquivos não rastreados são quaisquer arquivos que não foram incluidos no último **snaptshot**(versão) e não estão na área de stage.

<p align="center">
  <img src="https://git-scm.com/book/en/v2/images/lifecycle.png" alt="Ciclo de vida dos status de seus arquivos">
</p>

##### Figura 2. Ciclo de vida dos status de seus arquivos

É possível verificar o status dos arquivos usando o comadno `git status`.

Agora execute o comando `git status`. O output deveria ser algo parecido com isso:
```
On branch master
nothing to commit, working tree clean
```

Isso significa que nenhum dos arquivos rastreado foi modificado desde a ultima **snapshot**.

Crie um novo arquivo CONTRIBUTING.md:

```
touch CONTRIBUTING.md
```

Agora execute o comando `git status` novamente, o output deve ser semelhante ao seguinte:
```
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        CONTRIBUTING.md

nothing added to commit but untracked files present (use "git add" to track)
```

Use o `git add` para para começar a rastrear o novo arquivo.
```
git add CONTRIBUTING.md
```

Verificando o status mais uma vez o output deveria ser algo assim:
```
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   CONTRIBUTING.md
```

Vamos modificar um arquivo que estava sendo rastreado e executar o `git status`
```
echo 'alguma coisa' >> README.md
```

o output deveria ser algo como:

```
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md
```
Use o comando `git add` para preparar o arquivo para commit e em seguida use `git status` novamente.

Você deveria ver algo como:
```
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md
```

### Commits<a name="commits"/>

Agora que o novo CONTRIBUTING.md e README.md estão preparados para commit podemos usar o comando `git commit`.

Agora o editor padrão será aberto e é só digitar a mensagem do commit(este exemplo é a tela do Nano)
```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
#       new file:   CONTRIBUTING.md
#       modified:   README.md
#

```

Quando sair do editor o Git criara sua **commit** com a mensagem digitada.

Também é possivel usar a flag `-m` para digitar a mensagem da commit junto com o comando:
```
git commit -m "Mensagem da commit"
```

O output seria algo assim:
```
[master 3150898] Mensagem da commit
 2 files changed, 2 insertions(+)
 create mode 100644 CONTRIBUTING.md
```

### Repositórios Remotos<a name="repositórios-remotos"/>

Para colaborar com outras pessoas em um projeto Git é necessário gerenciar seus repositórios remotos. Trabalhar com esses repositórios envolve fazer **pushing** e **pulling** dos dados do projeto.

#### Exibindo seus repositórios remotos

Para ver os repositorios remotos que você configurou é utilizado o comando `git remote -v`. 

Vá para na pasta do repositório clonado anteriormente e execute o comando sitado, você deve ver **origin**, que é o nome padrão dado pelo Git ao servidor clonado.

Utilizando a flag `-v` com o `git remote` é possível ver as URLs do repositório remoto.
```
origin  https://github.com/GustavoHSD/Git-Course_Unespar.git (fetch)
origin  https://github.com/GustavoHSD/Git-Course_Unespar.git (push)
```

#### Pushing

Quando você quer enviar seu progresso para o servidor remoto o comando a ser utlizado é `git push [remote-name] [branch-name]`.

Então para enviar suas commits ao servidor o comando seria:
```
git push orign main
```

Esse comando funcionara somente em um servidor que você tem permissão de escrita e se outra pessoa não fez um **push** nesse meio tempo, nesse caso você precisaria atualizar localmente para depois fazer o **push**.

## Git Branching

### O que é Branch<a name="o-que-é-branch"/>

No git uma branch é uma nova ramificação do repositório principal. Branches permitem trabalhar em diferentes partes do projeto sem afetar a branch principal. Você pode fazer o merge dessas diferentes branches na main/master.

### Branch e Merge<a name="branch-e-merge"/>

#### Criando nova Branch

Vamos adicionar um hello world em python ao nosso projeto.

Para isso criaremos a branch hello-world-python usando o comando `git branch <branch name>`
```
git branch hello-world-python
```

Use o comando `git branch` para ver todas branches do projeto, o output deveria ser algo como:
```
  hello-world-python
* main
```

Agora use o comando `git checkout <branch name>` para trocar de branch.

```
Switched to branch 'hello-world-python'
```

Crie um arquivo chamado helloworld.py na nova branch e digite print("Hello world").

Execute o comando `git commit -a -m "Hello world in python"`

Note que a flag `-a` permite pular o staging e faz a commit direto.

### Gerenciamento de Branch<a name="gerenciamento-de-branch"/>

## Exemplos de Uso<a name="exemplos-de-uso"/>
