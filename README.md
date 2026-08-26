<div align="center">

  <h1>
    <img
      src="https://git-scm.com/images/logo@2x.png"
      width="100"
      alt="Git"
    />
    Guide to Work
  </h1>

  <p>
    📚 Guia prático de Git para desenvolvimento, versionamento e colaboração
  </p>

</div>

---

## 📖 Sobre este guia

Este guia foi criado para servir como uma **referência prática de Git**, desde os conceitos fundamentais até recursos mais avançados utilizados no desenvolvimento de software.

O conteúdo aborda o fluxo completo de trabalho com Git:

```text
📁 Trabalhar nos arquivos
       ↓
🔍 Verificar alterações
       ↓
📦 Preparar alterações
       ↓
💾 Criar commit
       ↓
🌿 Trabalhar com branches
       ↓
🔄 Integrar alterações
       ↓
🌐 Sincronizar com o repositório remoto
````

O objetivo é ajudar desenvolvedores a compreender **não apenas quais comandos executar, mas também quando e por que utilizá-los**.

> 💡 Este guia é baseado nos conceitos apresentados no livro **Pro Git** e em práticas comuns de desenvolvimento com Git.

---

# 📚 Sumário

* 🏁 [1. Começando com Git](#-1-começando-com-git)

  * ⚙️ [1.1 Instalação e configuração](#️-11-instalação-e-configuração)
  * 🆕 [1.2 Inicializando um repositório](#-12-inicializando-um-repositório)
  * 📂 [1.3 Clonando um repositório](#-13-clonando-um-repositório)
* 🔄 [2. Fluxo básico de trabalho](#-2-fluxo-básico-de-trabalho)

  * 🔍 [2.1 Verificando o status](#-21-verificando-o-status)
  * ➕ [2.2 Adicionando alterações](#-22-adicionando-alterações)
  * 👀 [2.3 Visualizando alterações](#-23-visualizando-alterações)
  * 💾 [2.4 Criando commits](#-24-criando-commits)
  * ✏️ [2.5 Alterando o último commit](#️-25-alterando-o-último-commit)
  * 📜 [2.6 Visualizando o histórico](#-26-visualizando-o-histórico)
  * ↩️ [2.7 Desfazendo alterações](#️-27-desfazendo-alterações)
* 🌿 [3. Branches](#-3-branches)

  * 📋 [3.1 Gerenciando branches](#-31-gerenciando-branches)
  * 🔀 [3.2 Mesclando branches](#-32-mesclando-branches)
  * 📊 [3.3 Verificando branches](#-33-verificando-branches)
* 🌐 [4. Repositórios remotos](#-4-repositórios-remotos)

  * 🔗 [4.1 Gerenciando remotes](#-41-gerenciando-remotes)
  * 🔄 [4.2 Sincronizando alterações](#-42-sincronizando-alterações)
* 🚀 [5. Recursos avançados](#-5-recursos-avançados)

  * 📦 [5.1 Stash](#-51-stash)
  * 🎯 [5.2 Staging interativo](#-52-staging-interativo)
  * 🗜️ [5.3 Squash de commits](#️-53-squash-de-commits)
  * 🆘 [5.4 Recuperando alterações com reflog](#-54-recuperando-alterações-com-reflog)
  * 🪝 [5.5 Git Hooks](#-55-git-hooks)
* 📋 [6. Tabela de comandos essenciais](#-6-tabela-de-comandos-essenciais)
* 💡 [7. Boas práticas](#-7-boas-práticas)

---

# 🏁 1. Começando com Git

## ⚙️ 1.1 Instalação e configuração

Antes de utilizar o Git, é necessário instalá-lo e configurar sua identidade.

As informações configuradas aqui são associadas aos commits realizados por você.

### 📥 Instalação

Baixe o Git através do site oficial:

👉🏻 [git-scm.com](https://git-scm.com/)

Depois da instalação, verifique se o Git está disponível:

```bash
git --version
```

Exemplo:

```text
git version 2.x.x
```

### 👤 Configurando seu nome

```bash
git config --global user.name "Seu Nome"
```

### 📧 Configurando seu e-mail

```bash
git config --global user.email "seu.email@example.com"
```

### 🔍 Verificando as configurações

```bash
git config --global --list
```

### ✏️ Configurando o editor padrão

Caso utilize o Visual Studio Code:

```bash
git config --global core.editor "code --wait"
```

> 💡 A configuração `--global` aplica as informações a todos os repositórios do usuário.

---

# 🆕 1.2 Inicializando um repositório

Para começar a versionar um projeto existente, utilize:

```bash
git init
```

Esse comando cria uma pasta oculta chamada:

```text
.git/
```

Essa pasta contém as informações internas necessárias para o Git controlar o histórico do projeto.

Exemplo:

```text
meu-projeto/
├── src/
├── index.html
├── package.json
└── .git/
```

> ⚠️ Nunca altere ou exclua manualmente a pasta `.git` sem saber exatamente o que está fazendo. Ela contém o histórico e as configurações do repositório.

---

# 📂 1.3 Clonando um repositório

Quando um projeto já existe em um servidor remoto, como GitHub ou GitLab, normalmente utilizamos `git clone`.

```bash
git clone https://github.com/usuario/repositorio.git
```

O comando:

* 📥 Baixa os arquivos
* 📜 Baixa o histórico
* 🌿 Baixa as branches
* 🔗 Configura o repositório remoto
* 📁 Cria uma cópia local do projeto

Depois:

```bash
cd repositorio
```

---

# 🔄 2. Fluxo básico de trabalho

Um dos conceitos mais importantes do Git é entender os diferentes estados pelos quais uma alteração passa.

## 📦 Os três principais estados

```text
┌──────────────────────┐
│   📁 Working Tree    │
│  Arquivos modificados│
└──────────┬───────────┘
           │ git add
           ↓
┌──────────────────────┐
│   📦 Staging Area     │
│ Alterações preparadas │
└──────────┬───────────┘
           │ git commit
           ↓
┌──────────────────────┐
│   💾 Repository       │
│ Histórico versionado  │
└──────────────────────┘
```

### 📁 Working Tree

É o diretório onde você trabalha e modifica seus arquivos.

### 📦 Staging Area

É a área onde você seleciona quais alterações farão parte do próximo commit.

### 💾 Repository

É onde o Git armazena os commits e o histórico do projeto.

---

# 🔍 2.1 Verificando o status

O comando mais importante para acompanhar o estado do seu projeto é:

```bash
git status
```

Ele mostra:

* 📝 Arquivos modificados
* 🆕 Arquivos novos
* 📦 Arquivos adicionados ao staging
* ❌ Arquivos não rastreados
* 🌿 Branch atual

> 💡 É uma boa prática executar `git status` frequentemente durante o desenvolvimento.

---

# ➕ 2.2 Adicionando alterações

Para adicionar um arquivo específico:

```bash
git add arquivo.js
```

Para adicionar vários arquivos:

```bash
git add arquivo.js styles.css
```

Para adicionar todas as alterações:

```bash
git add .
```

Ou:

```bash
git add -A
```

### 🎯 Adicionar apenas partes de um arquivo

```bash
git add -p
```

Esse comando permite selecionar individualmente quais blocos de alteração devem ser adicionados ao staging.

---

# 👀 2.3 Visualizando alterações

Antes de criar um commit, é importante revisar o que foi alterado.

### 🔍 Alterações ainda não adicionadas

```bash
git diff
```

### 📦 Alterações que já estão no staging

```bash
git diff --staged
```

Isso ajuda a evitar commits contendo alterações acidentais.

---

# 💾 2.4 Criando commits

Depois de adicionar as alterações ao staging:

```bash
git commit -m "Adiciona página de login"
```

Um commit representa um **snapshot do projeto em determinado momento**.

Um bom commit deve ser:

* 🎯 Pequeno
* 🧩 Focado em uma alteração
* 📝 Fácil de entender
* 🔍 Fácil de revisar

### ❌ Evite

```bash
git commit -m "alterações"
```

### ✅ Prefira

```bash
git commit -m "Adiciona validação do formulário de login"
```

---

# ✏️ 2.5 Alterando o último commit

Se você esqueceu de adicionar um arquivo ao último commit:

```bash
git add arquivo.js
git commit --amend --no-edit
```

Para alterar a mensagem:

```bash
git commit --amend -m "Nova mensagem do commit"
```

> ⚠️ Evite alterar commits que já foram enviados para um repositório compartilhado, principalmente se outras pessoas já trabalham sobre eles.

---

# 📜 2.6 Visualizando o histórico

Para visualizar o histórico completo:

```bash
git log
```

Uma versão mais compacta:

```bash
git log --oneline
```

Uma visualização gráfica bastante útil:

```bash
git log --oneline --graph --decorate --all
```

Exemplo:

```text
* a1b2c3d (HEAD -> main) Adiciona página inicial
* d4e5f6g Corrige estilos do formulário
* h7i8j9k Cria estrutura inicial
```

---

# ↩️ 2.7 Desfazendo alterações

O Git oferece diferentes formas de desfazer alterações.

É importante entender **em qual estado a alteração está** antes de executar um comando.

---

## 📦 Remover arquivo do staging

Com `git restore`:

```bash
git restore --staged arquivo.js
```

O arquivo continua modificado, mas deixa de estar no staging.

Alternativamente:

```bash
git reset HEAD arquivo.js
```

---

## 🗑️ Descartar alterações locais

Para restaurar um arquivo para o estado do último commit:

```bash
git restore arquivo.js
```

> ⚠️ As alterações locais serão perdidas.

---

## ↩️ Desfazer um commit com `revert`

Para desfazer um commit que já foi compartilhado:

```bash
git revert <hash-do-commit>
```

O Git cria um **novo commit** que desfaz as alterações do commit anterior.

✅ É uma opção segura para históricos compartilhados.

---

## ⏪ Reset

Para mover o `HEAD` para outro commit:

```bash
git reset <commit>
```

Existem diferentes níveis:

```bash
git reset --soft <commit>
git reset --mixed <commit>
git reset --hard <commit>
```

### 🟢 `--soft`

Mantém as alterações no staging.

### 🟡 `--mixed`

Mantém as alterações nos arquivos, mas remove do staging.

### 🔴 `--hard`

Remove as alterações posteriores ao commit.

> 🚨 **Cuidado com `git reset --hard`.** Alterações não salvas podem ser perdidas permanentemente.

---

# 🌿 3. Branches

Branches permitem desenvolver funcionalidades de forma isolada sem alterar diretamente a branch principal.

Um fluxo comum:

```text
main
 │
 ├── feature/login
 │
 ├── feature/dashboard
 │
 └── fix/header
```

Isso facilita:

* ✨ Desenvolvimento de funcionalidades
* 🐛 Correção de bugs
* 🧪 Experimentos
* 👥 Trabalho em equipe
* 🔀 Integração controlada

---

# 📋 3.1 Gerenciando branches

### 🔍 Listar branches

```bash
git branch
```

### 🌱 Criar uma branch

```bash
git branch feature/login
```

### 🔀 Trocar de branch

Com o comando moderno:

```bash
git switch feature/login
```

Alternativamente:

```bash
git checkout feature/login
```

### 🌱 Criar e trocar para uma nova branch

```bash
git switch -c feature/login
```

Ou:

```bash
git checkout -b feature/login
```

> 💡 `git switch` foi criado especificamente para operações relacionadas a branches e torna a intenção do comando mais clara.

---

## 🗑️ Excluir uma branch

```bash
git branch -d feature/login
```

Para forçar a exclusão:

```bash
git branch -D feature/login
```

> ⚠️ `-D` pode excluir uma branch contendo alterações que ainda não foram mescladas.

---

# 🔀 3.2 Mesclando branches

Para integrar uma branch à branch atual:

```bash
git merge feature/login
```

Exemplo:

```bash
git switch main
git merge feature/login
```

Fluxo:

```text
feature/login
      │
      │
      ↓
    merge
      │
      ↓
     main
```

### ⚠️ Conflitos

Quando duas branches modificam a mesma parte de um arquivo, pode ocorrer um **merge conflict**.

Nesse caso:

1. 🔍 Identifique os conflitos.
2. ✏️ Edite os arquivos.
3. 📦 Adicione os arquivos corrigidos.
4. 💾 Crie o commit do merge.

```bash
git add .
git commit
```

---

# 📊 3.3 Verificando branches

### ✅ Branches já mescladas

```bash
git branch --merged
```

### ❌ Branches ainda não mescladas

```bash
git branch --no-merged
```

### 🌐 Branches remotas

```bash
git branch -r
```

### 🌍 Todas as branches

```bash
git branch -a
```

---

# 🌐 4. Repositórios remotos

Um repositório remoto é uma versão do seu projeto armazenada em outro local, normalmente em serviços como:

* 🐙 GitHub
* 🦊 GitLab
* 🪣 Bitbucket

Ele permite compartilhar e sincronizar o código com outras pessoas.

---

# 🔗 4.1 Gerenciando remotes

### ➕ Adicionar um remote

```bash
git remote add origin https://github.com/usuario/repositorio.git
```

`origin` é o nome convencional utilizado para o repositório remoto principal.

### 📋 Listar remotes

```bash
git remote -v
```

### 🔍 Visualizar detalhes

```bash
git remote show origin
```

---

# 🔄 4.2 Sincronizando alterações

## ⬆️ Push

Envia commits locais para o repositório remoto:

```bash
git push origin main
```

Para configurar a branch upstream na primeira vez:

```bash
git push -u origin main
```

Depois disso, normalmente:

```bash
git push
```

---

## ⬇️ Pull

Baixa alterações do remoto e integra com a branch atual:

```bash
git pull origin main
```

Conceitualmente:

```text
git pull
   =
git fetch
   +
git merge
```

---

## 📥 Fetch

Para baixar informações do remoto sem realizar o merge:

```bash
git fetch
```

Isso atualiza as referências remotas, mas não altera seus arquivos de trabalho.

> 💡 `git fetch` é útil quando você deseja verificar o que mudou no remoto antes de integrar as alterações.

---

# 🚀 5. Recursos avançados

## 📦 5.1 Stash

O `git stash` permite guardar temporariamente alterações que ainda não estão prontas para um commit.

Isso é útil quando você precisa trocar de branch rapidamente.

```bash
git stash
```

Depois, para recuperar:

```bash
git stash pop
```

### 📋 Listar stashes

```bash
git stash list
```

### 👀 Visualizar um stash

```bash
git stash show
```

### 🗑️ Remover um stash

```bash
git stash drop
```

Fluxo:

```text
📝 Trabalho atual
      ↓
📦 git stash
      ↓
🌿 Trocar de branch
      ↓
🔧 Resolver outra tarefa
      ↓
↩️ git stash pop
      ↓
📝 Continuar trabalho
```

---

# 🎯 5.2 Staging interativo

Quando você deseja criar commits pequenos e organizados:

```bash
git add -p
```

O Git apresenta cada bloco de alteração e pergunta o que fazer.

Algumas opções:

```text
y → adicionar
n → não adicionar
s → dividir
q → sair
```

Isso permite separar diferentes alterações que foram feitas no mesmo arquivo.

---

# 🗜️ 5.3 Squash de commits

Durante o desenvolvimento, é comum criar vários commits pequenos:

```text
feat: cria formulário
fix: corrige botão
fix: corrige validação
style: ajusta espaçamento
```

Antes de integrar a branch, esses commits podem ser combinados.

```bash
git rebase -i HEAD~4
```

No editor interativo:

```text
pick   a1b2c3d cria formulário
squash d4e5f6g corrige botão
squash h7i8j9k corrige validação
squash m1n2o3p ajusta espaçamento
```

O resultado pode ser um histórico mais limpo:

```text
feat: adiciona formulário de login
```

> ⚠️ Evite reescrever o histórico de branches compartilhadas sem alinhar com a equipe.

---

# 🆘 5.4 Recuperando alterações com reflog

O `reflog` registra movimentações do `HEAD` e de referências locais.

```bash
git reflog
```

Ele pode ajudar a recuperar estados que aparentemente foram perdidos após comandos como:

* `git reset`
* `git rebase`
* `git checkout`
* `git merge`

Exemplo:

```text
a1b2c3d HEAD@{0}: reset: moving to HEAD~1
d4e5f6g HEAD@{1}: commit: Adiciona nova funcionalidade
```

Se você precisar retornar para determinado estado:

```bash
git reset --hard d4e5f6g
```

> 🛟 O `reflog` é uma das ferramentas mais importantes para recuperação de trabalho perdido em um repositório local.

---

# 🪝 5.5 Git Hooks

Git Hooks são scripts executados automaticamente em determinados momentos do fluxo do Git.

Eles podem ser utilizados para:

* 🧪 Executar testes
* 🔍 Rodar linters
* 🎨 Verificar formatação
* 📝 Validar mensagens de commit
* 🛡️ Impedir commits inválidos

### 💻 Hooks locais

Executados na máquina do desenvolvedor.

Exemplos:

```text
pre-commit
commit-msg
pre-push
```

### 🖥️ Hooks no servidor

Executados no lado do servidor.

Exemplos:

```text
pre-receive
update
post-receive
```

Um `pre-commit`, por exemplo, pode executar um linter antes de permitir o commit.

---

# 📋 6. Tabela de comandos essenciais

| Comando       | Finalidade                         | Emoji |
| :------------ | :--------------------------------- | :---: |
| `git init`    | Criar um novo repositório          |   🆕  |
| `git clone`   | Clonar um repositório              |   📂  |
| `git status`  | Verificar o estado atual           |   🔍  |
| `git add`     | Adicionar alterações ao staging    |   ➕   |
| `git diff`    | Visualizar alterações              |   👀  |
| `git commit`  | Criar um snapshot                  |   💾  |
| `git log`     | Visualizar histórico               |   📜  |
| `git branch`  | Gerenciar branches                 |   🌿  |
| `git switch`  | Trocar de branch                   |   🔀  |
| `git merge`   | Mesclar branches                   |   🔗  |
| `git remote`  | Gerenciar repositórios remotos     |   🌐  |
| `git fetch`   | Buscar alterações remotas          |   📥  |
| `git pull`    | Buscar e integrar alterações       |   🔄  |
| `git push`    | Enviar commits para o remoto       |   ⬆️  |
| `git stash`   | Guardar alterações temporariamente |   📦  |
| `git restore` | Restaurar alterações               |   ↩️  |
| `git reset`   | Mover o estado do repositório      |   ⏪   |
| `git revert`  | Criar commit que desfaz outro      |   ↩️  |
| `git rebase`  | Reorganizar histórico              |  🗜️  |
| `git reflog`  | Recuperar estados anteriores       |   🆘  |

---

# 💡 7. Boas práticas

## 💾 Faça commits pequenos

Prefira vários commits focados em alterações específicas em vez de um único commit gigante.

### ❌ Evite

```text
feat: fiz várias coisas
```

### ✅ Prefira

```text
feat: adiciona formulário de login
fix: corrige validação de email
style: ajusta espaçamento do formulário
```

---

## ✍️ Escreva boas mensagens de commit

Uma boa mensagem deve explicar claramente **o que foi alterado**.

Prefira verbos no imperativo:

```text
Adiciona autenticação
Corrige validação
Remove componente obsoleto
Atualiza dependências
```

---

## 🌿 Utilize branches

Evite desenvolver todas as funcionalidades diretamente na `main`.

Um fluxo simples:

```text
main
 │
 ├── feature/login
 ├── feature/dashboard
 └── fix/header
```

---

## 🔍 Revise antes de commitar

Antes de criar um commit:

```bash
git status
git diff
git diff --staged
```

Isso reduz a possibilidade de enviar alterações acidentais.

---

## 🧹 Mantenha o histórico organizado

Commits pequenos e bem definidos tornam o projeto:

* 🔍 Mais fácil de revisar
* 🐛 Mais fácil de depurar
* ↩️ Mais fácil de reverter
* 👥 Mais fácil de trabalhar em equipe
* 📜 Mais fácil de compreender no futuro

---

## ⚠️ Tenha cuidado com comandos destrutivos

Comandos como:

```bash
git reset --hard
```

podem remover alterações locais.

Antes de executar comandos destrutivos, confirme:

```bash
git status
git diff
```

E, quando necessário, utilize:

```bash
git stash
```

para preservar seu trabalho.

---

# 🧭 Fluxo recomendado para o dia a dia

Um fluxo simples e seguro para desenvolvimento:

```text
🌿 Criar uma branch
       ↓
git switch -c feature/minha-feature
       ↓
💻 Desenvolver
       ↓
🔍 git status
       ↓
👀 git diff
       ↓
📦 git add
       ↓
💾 git commit
       ↓
🔄 git pull
       ↓
⬆️ git push
       ↓
🔀 Pull Request
       ↓
✅ Code Review
       ↓
🚀 Merge
```

---

# 🧠 Git em uma visão geral

O Git pode ser entendido como um sistema que registra **snapshots do seu projeto ao longo do tempo**.

```text
                 🌐 Repositório remoto
                         ↕
                    ⬆️ push / ⬇️ pull
                         ↕
                 💾 Repositório local
                         ↑
                     💬 commit
                         ↑
                  📦 Staging Area
                         ↑
                      ➕ add
                         ↑
                  📁 Working Tree
                         ↑
                      💻 Você
```

Compreender esse fluxo é mais importante do que simplesmente memorizar comandos.

---

# 📚 Referências

Este guia foi baseado principalmente nos conceitos apresentados no livro **Pro Git**.

📖 **Pro Git — Livro oficial**

👉🏻 [git-scm.com/book](https://git-scm.com/book/en/v2/)

🌐 **Site oficial do Git**

👉🏻 [git-scm.com](https://git-scm.com/)

---

<div align="center">

  <h3>📈 Git Guide to Work</h3>

  <p>
    Um guia prático para aprender, consultar e trabalhar melhor com Git.
  </p>

  <br />

&copy; 2026 - Feito com ❤️ e ☕ por <ahref="https://github.com/romaosantosalisson" target="_blank"><strong>Álisson</strong></a></div>

</div>
