---
date: 2024-11-12
tags:
  - Pensamentos
---
Acho que seria um projeto de aprendizado de programação interessante conseguir transformar todos as minhas notas do obsidian em uma mega minha wikipedia. Assim eu podia fazer com que tudo ficasse sempre online.

Isso naturalmente gera algumas questões que precisam ser tratadas. 

# 1. Conseguir um site pra guardar essas coisas 
Acho que essa é a parte mais fácil. Eu encontrei aquele site, domínios portugueses que te dá um site grátis por um ano. 
Deve ser mais do que o suficiente e, se eu achar que isso faz sentido daqui a um ano, eu só crio outra conta e coloco tudo o que eu já fiz em outro site, não deve ser relevante.

# 2. Fazer a coisa propriamente dita

É, isso parece ser a coisa mais difícil. Mas eu imagino que seja fazível, tendo em conta a forma como a informação é produzida no obsidian e etc 

# 3. Estrutura interna 

Acho que eu iria criar um arquivo que tivesse linkado em todos os outros, pra que tudo decorra dele. 

Para fins de privacidade eu poderia colocar senha em algumas partes 

# eu fiz um guia para fazer isso com o chat gpt


# Guia Detalhado: Sincronizando suas Notas do Obsidian com o GitHub

## Introdução

Este documento fornece um guia passo a passo detalhado para sincronizar suas notas do Obsidian com um repositório no GitHub usando o plugin **Obsidian Git**. Isso permitirá que você faça backup de suas notas, mantenha o controle de versão e possibilite a publicação automática do seu site posteriormente.

---

## Índice

1. [Pré-requisitos](#1-pré-requisitos)
2. [Instalando o Plugin Obsidian Git](#2-instalando-o-plugin-obsidian-git)
3. [Configurando o Obsidian Git](#3-configurando-o-obsidian-git)
   - 3.1. [Configurações Básicas](#31-configurações-básicas)
   - 3.2. [Configurações Avançadas (Opcional)](#32-configurações-avançadas-opcional)
4. [Criando um Repositório no GitHub](#4-criando-um-repositório-no-github)
5. [Inicializando o Repositório Git Localmente](#5-inicializando-o-repositório-git-localmente)
   - 5.1. [Usando o Terminal/Prompt de Comando](#51-usando-o-terminalprompt-de-comando)
   - 5.2. [Usando o Plugin Obsidian Git](#52-usando-o-plugin-obsidian-git)
6. [Testando a Sincronização](#6-testando-a-sincronização)
7. [Dicas e Boas Práticas](#7-dicas-e-boas-práticas)
8. [Resolução de Problemas](#8-resolução-de-problemas)
9. [Conclusão](#9-conclusão)

---

## 1. Pré-requisitos

Antes de começar, certifique-se de ter o seguinte:

- **Obsidian** instalado em seu computador.
- **Conta no GitHub** ativa.
- **Git** instalado em seu computador.
  - [Download do Git](https://git-scm.com/downloads)
- Conhecimento básico de linha de comando (Terminal no macOS/Linux ou Prompt de Comando/PowerShell no Windows).

---

## 2. Instalando o Plugin Obsidian Git

O **Obsidian Git** é um plugin que permite integrar o controle de versão Git diretamente no Obsidian, facilitando a sincronização de suas notas com o GitHub.

### Passos:

1. **Abra o Obsidian.**

2. **Acesse as Configurações:**
   - Clique no ícone de **engrenagem** no canto inferior esquerdo ou pressione `Ctrl + ,` (Windows/Linux) ou `Cmd + ,` (macOS).

3. **Habilite Plugins da Comunidade:**
   - No menu lateral, clique em **"Community Plugins"** (Plugins da Comunidade).
   - Se for a primeira vez, você precisará habilitar os plugins da comunidade:
     - Clique em **"Turn on community plugins"** (Ativar plugins da comunidade).
     - Confirme clicando em **"Yes"**.

4. **Instale o Plugin Obsidian Git:**
   - Ainda em **Community Plugins**, clique em **"Browse"** (Navegar).
   - No campo de busca, digite **"Obsidian Git"**.
   - Clique no plugin **"Obsidian Git"** nos resultados.
   - Clique em **"Install"** (Instalar).
   - Após a instalação, clique em **"Enable"** (Ativar).

---

## 3. Configurando o Obsidian Git

Após instalar o plugin, é necessário configurá-lo para que funcione corretamente com o seu repositório Git.

### 3.1. Configurações Básicas

1. **Acesse as Configurações do Plugin:**
   - Nas configurações do Obsidian, no menu lateral, desça até **"Plugin Options"** (Opções de Plugins).
   - Clique em **"Obsidian Git"**.

2. **Configurar Auto Pull e Auto Push:**
   - **Auto Pull Interval (minutos):**
     - Define a frequência com que o Obsidian Git fará pull das alterações do repositório remoto.
     - Recomenda-se definir para **10** minutos.
   - **Auto Push Interval (minutos):**
     - Define a frequência com que o plugin enviará (push) suas alterações para o repositório remoto.
     - Defina o mesmo intervalo de **10** minutos.

3. **Configurar Mensagens de Commit:**
   - **Commit Message:**
     - Você pode personalizar a mensagem padrão dos commits.
     - Exemplo: `"Atualização automática: {{date}}"`, onde `{{date}}` será substituído pela data atual.

4. **Outras Configurações Úteis:**
   - **Disable Push:** (Desabilitar Push)
     - Marque esta opção se não quiser que o plugin faça push automático das alterações.
   - **Track All Files:** (Rastrear Todos os Arquivos)
     - Certifique-se de que esta opção esteja marcada para que todos os arquivos sejam incluídos.

### 3.2. Configurações Avançadas (Opcional)

Se desejar uma autenticação mais segura e evitar digitar sua senha do GitHub com frequência, você pode configurar uma chave SSH.

#### Configurando Chave SSH:

1. **Gerar uma Chave SSH (se ainda não tiver):**
   - Abra o Terminal (macOS/Linux) ou Git Bash (Windows).
   - Digite o comando:
     ```bash
     ssh-keygen -t ed25519 -C "seu-email@example.com"
     ```
     - Pressione **Enter** para aceitar o local padrão.
     - Crie uma senha para a chave ou deixe em branco.

2. **Adicionar a Chave SSH ao SSH-Agent:**
   - Inicie o ssh-agent:
     ```bash
     eval "$(ssh-agent -s)"
     ```
   - Adicione sua chave privada ao agente:
     ```bash
     ssh-add ~/.ssh/id_ed25519
     ```

3. **Adicionar a Chave SSH ao GitHub:**
   - Copie o conteúdo da chave pública:
     ```bash
     cat ~/.ssh/id_ed25519.pub
     ```
     - Selecione e copie o texto exibido.
   - No GitHub:
     - Vá em **Settings** (Configurações) da sua conta (não do repositório).
     - Clique em **"SSH and GPG keys"**.
     - Clique em **"New SSH key"**.
     - Dê um título (exemplo: "Chave do Obsidian") e cole a chave pública.
     - Clique em **"Add SSH key"**.

---

## 4. Criando um Repositório no GitHub

Agora, você precisa criar um repositório onde suas notas serão armazenadas.

### Passos:

1. **Acesse o GitHub e Faça Login:**
   - Vá para [github.com](https://github.com/) e entre na sua conta.

2. **Criar um Novo Repositório:**
   - Clique no botão **"+"** no canto superior direito e selecione **"New repository"**.

3. **Configurar o Repositório:**
   - **Repository Name:** Dê um nome ao repositório (exemplo: "meu-vault-obsidian").
   - **Description:** (Opcional) Adicione uma descrição.
   - **Public/Private:**
     - **Public:** Qualquer pessoa pode ver este repositório.
     - **Private:** Apenas você (e colaboradores) podem ver.
     - Se suas notas contêm informações pessoais, escolha **Private**.
   - **Initialize this repository with:**
     - **Não marque** nenhuma das opções (README, .gitignore, licença).
   - Clique em **"Create repository"**.

---

## 5. Inicializando o Repositório Git Localmente

Agora, você vai conectar seu vault do Obsidian ao repositório que acabou de criar.

### 5.1. Usando o Terminal/Prompt de Comando

1. **Abra o Terminal/CMD:**
   - **Windows:** Use o Prompt de Comando ou PowerShell.
   - **macOS/Linux:** Use o Terminal.

2. **Navegue até a Pasta do Seu Vault:**
   - Use o comando `cd` para mudar de diretório.
     ```bash
     cd /caminho/para/seu/vault
     ```
     - No Windows, o caminho pode ser algo como `C:\Users\SeuUsuario\Documents\Obsidian Vault\`.

3. **Inicialize o Repositório Git:**
   - Execute:
     ```bash
     git init
     ```

4. **Adicione o Repositório Remoto:**
   - Se você configurou chave SSH:
     ```bash
     git remote add origin git@github.com:seu-usuario/seu-repositorio.git
     ```
   - Se não configurou chave SSH e deseja usar HTTPS:
     ```bash
     git remote add origin https://github.com/seu-usuario/seu-repositorio.git
     ```

5. **Adicionar Todos os Arquivos:**
   - Execute:
     ```bash
     git add .
     ```

6. **Fazer o Primeiro Commit:**
   - Execute:
     ```bash
     git commit -m "Primeiro commit"
     ```

7. **Enviar para o Repositório Remoto:**
   - Execute:
     ```bash
     git push -u origin master
     ```
     - Se receber um erro sobre a branch principal ser `main` ao invés de `master`, use:
       ```bash
       git push -u origin main
       ```

### 5.2. Usando o Plugin Obsidian Git

Se preferir realizar todo o processo dentro do Obsidian:

1. **Iniciar o Repositório com o Plugin:**
   - No Obsidian, pressione `Ctrl + P` (Windows/Linux) ou `Cmd + P` (macOS) para abrir o **Command Palette**.
   - Digite **"Obsidian Git: Initialize Repo"** e selecione o comando.

2. **Configurar o Repositório Remoto:**
   - Ainda no **Command Palette**, execute **"Obsidian Git: Set Remote"**.
   - Insira a URL do seu repositório:
     - **SSH:** `git@github.com:seu-usuario/seu-repositorio.git`
     - **HTTPS:** `https://github.com/seu-usuario/seu-repositorio.git`

3. **Fazer o Primeiro Commit e Push:**
   - Execute **"Obsidian Git: Commit all changes"** para comitar as alterações.
   - Em seguida, execute **"Obsidian Git: Push"** para enviar ao GitHub.

---

## 6. Testando a Sincronização

É importante verificar se tudo está funcionando corretamente.

1. **Criar uma Nova Nota no Obsidian:**
   - Adicione algum conteúdo de teste.

2. **Salvar e Verificar o Plugin:**
   - O Obsidian Git deve detectar as alterações automaticamente.
   - Você pode forçar um commit usando o comando **"Obsidian Git: Commit all changes"**.

3. **Verificar o GitHub:**
   - Vá ao seu repositório no GitHub.
   - Atualize a página e verifique se a nova nota aparece.

---

## 7. Dicas e Boas Práticas

- **.gitignore:**
  - Se houver arquivos ou pastas que você **não** deseja sincronizar (como anexos grandes ou notas privadas), crie um arquivo `.gitignore` na raiz do seu vault e liste esses itens.
    ```gitignore
    # Ignorar a pasta de anexos
    attachments/
    
    # Ignorar notas privadas
    notas-privadas/
    ```

- **Frequência de Sincronização:**
  - Ajuste os intervalos de Auto Pull e Auto Push conforme sua necessidade.

- **Mensagens de Commit:**
  - Personalize as mensagens para melhor rastreamento.

- **Backups:**
  - Embora o GitHub seja um ótimo lugar para backups, é recomendável manter backups adicionais de suas notas importantes.

---

## 8. Resolução de Problemas

- **Erro de Autenticação:**
  - Se receber erros ao fazer push, verifique suas credenciais.
  - Se estiver usando HTTPS, pode ser necessário inserir seu nome de usuário e token de acesso pessoal (ao invés da senha).

- **Conflitos de Merge:**
  - Podem ocorrer se houver alterações conflitantes entre o repositório local e remoto.
  - Use o comando **"Obsidian Git: Pull"** para atualizar antes de fazer push.

- **Plugin Não Funciona:**
  - Verifique se o plugin está atualizado.
  - Consulte o console de desenvolvimento do Obsidian (pressione `Ctrl + Shift + I`) para mensagens de erro.

---

## 9. Conclusão

Você configurou com sucesso a sincronização das suas notas do Obsidian com o GitHub usando o plugin Obsidian Git. Isso permite que você tenha backups automáticos, controle de versão e prepara o terreno para a publicação automática do seu site nas etapas seguintes.

---

## Anexos (Opcional)

- **Links Úteis:**
  - [Documentação do Obsidian Git](https://github.com/denolehov/obsidian-git)
  - [Como Usar o Git no Terminal](https://rogerdudler.github.io/git-guide/index.pt_BR.html)
  - [Gerando uma Chave SSH e Conectando ao GitHub](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh)

- **Comandos Git Comuns:**
  - `git status` - Ver o estado atual do repositório.
  - `git log` - Ver o histórico de commits.
  - `git pull` - Atualizar o repositório local com as alterações remotas.

---

**Nota:** Agora que suas notas estão sincronizadas com o GitHub, você está pronto para prosseguir para a próxima etapa, que é configurar o site com o GitHub Pages e publicar suas notas online.

---

# Guia Detalhado: Configurando o Site com Jekyll e GitHub Pages

## Introdução

Este documento fornece um guia passo a passo detalhado para configurar um site estático usando **Jekyll** e **GitHub Pages** para publicar suas notas do Obsidian online. O objetivo é permitir que você aproveite os recursos do Obsidian, como backlinks e wikilinks, em um site hospedado gratuitamente no GitHub Pages, com suporte a um domínio personalizado.

---

## Índice

1. [Pré-requisitos](#1-pré-requisitos)
2. [Escolhendo um Template que Suporte Wikilinks e Backlinks](#2-escolhendo-um-template-que-suporte-wikilinks-e-backlinks)
3. [Criando um Fork do Template no GitHub](#3-criando-um-fork-do-template-no-github)
4. [Clonando o Repositório Forkado para o Seu Computador](#4-clonando-o-repositório-forkado-para-o-seu-computador)
5. [Integrando suas Notas do Obsidian ao Projeto Jekyll](#5-integrando-suas-notas-do-obsidian-ao-projeto-jekyll)
6. [Configurando o Arquivo `_config.yml`](#6-configurando-o-arquivo-_configyml)
7. [Configurando o GitHub Pages para Hospedar o Site](#7-configurando-o-github-pages-para-hospedar-o-site)
8. [Testando o Site Localmente (Opcional)](#8-testando-o-site-localmente-opcional)
9. [Publicando o Site no GitHub Pages](#9-publicando-o-site-no-github-pages)
10. [Configurando Plugins e Recursos Adicionais](#10-configurando-plugins-e-recursos-adicionais)
11. [Resolução de Problemas Comuns](#11-resolução-de-problemas-comuns)
12. [Conclusão](#12-conclusão)

---

## 1. Pré-requisitos

Antes de iniciar, certifique-se de ter os seguintes itens:

- **Conta no GitHub** ativa.
- **Git** instalado em seu computador.
  - [Download do Git](https://git-scm.com/downloads)
- **Ruby** e **Bundler** instalados (para testes locais, opcional).
  - [Instalação do Ruby](https://www.ruby-lang.org/pt/downloads/)
- Conhecimento básico de linha de comando (Terminal no macOS/Linux ou Prompt de Comando/PowerShell no Windows).

---

## 2. Escolhendo um Template que Suporte Wikilinks e Backlinks

Para aproveitar os recursos do Obsidian, é necessário escolher um template Jekyll que suporte **wikilinks** (`[[links]]`) e **backlinks**.

### Opção Recomendada: **Digital Garden Jekyll Template**

- **Repositório:** [maximevaillancourt/digital-garden-jekyll-template](https://github.com/maximevaillancourt/digital-garden-jekyll-template)
- **Características:**
  - Suporte a wikilinks do Obsidian.
  - Geração automática de backlinks.
  - Layout limpo e personalizável.
  - Ideal para criar uma wiki pessoal online.

---

## 3. Criando um Fork do Template no GitHub

Fazer um fork do repositório permite que você tenha sua própria cópia do template para personalizar.

### Passos:

1. **Acesse o Repositório do Template:**
   - Vá para [maximevaillancourt/digital-garden-jekyll-template](https://github.com/maximevaillancourt/digital-garden-jekyll-template).

2. **Faça o Fork do Repositório:**
   - Clique no botão **"Fork"** no canto superior direito da página.
   - Selecione sua conta pessoal como destino do fork.

3. **Renomeie o Repositório (Opcional):**
   - Após o fork, você pode renomear o repositório em **Settings** > **Repository name**.

---

## 4. Clonando o Repositório Forkado para o Seu Computador

Você precisa clonar o repositório para poder adicionar suas notas e fazer customizações.

### Passos:

1. **Obtenha a URL do Repositório Forkado:**
   - No seu repositório forkado, clique em **"Code"**.
   - Copie a URL **SSH** ou **HTTPS** (se você configurou chaves SSH, prefira a URL SSH).

2. **Abra o Terminal/CMD:**

3. **Navegue até o Diretório Desejado:**
   - Escolha onde você deseja clonar o repositório (por exemplo, sua pasta de projetos).

4. **Clone o Repositório:**
   ```bash
   git clone git@github.com:seu-usuario/digital-garden-jekyll-template.git
   ```
   - Se estiver usando HTTPS:
     ```bash
     git clone https://github.com/seu-usuario/digital-garden-jekyll-template.git
     ```

5. **Acesse a Pasta do Repositório:**
   ```bash
   cd digital-garden-jekyll-template
   ```

---

## 5. Integrando suas Notas do Obsidian ao Projeto Jekyll

Agora, você vai copiar suas notas do Obsidian para o projeto Jekyll.

### Passos:

1. **Localize a Pasta de Notas do Projeto:**
   - No template, geralmente as notas são armazenadas em uma pasta chamada `_notes` ou `notes`.

2. **Copie suas Notas para a Pasta do Projeto:**
   - Copie todas as suas notas em formato Markdown (`.md`) do seu vault do Obsidian para a pasta de notas do projeto.

3. **Preserve a Estrutura de Pastas (Opcional):**
   - Se desejar manter a estrutura de pastas das suas notas, copie as pastas correspondentes.

4. **Verifique os Links Internos:**
   - Certifique-se de que os links internos entre as notas estejam funcionando corretamente.

---

## 6. Configurando o Arquivo `_config.yml`

O arquivo `_config.yml` é o principal arquivo de configuração do Jekyll. Nele, você pode definir parâmetros importantes para o seu site.

### Passos:

1. **Abra o Arquivo `_config.yml`:**
   - Localize o arquivo na raiz do seu projeto e abra-o em um editor de texto.

2. **Atualize as Informações Básicas:**
   - **title:** Defina o título do seu site.
     ```yaml
     title: "Minha Wiki Pessoal"
     ```
   - **description:** Adicione uma descrição.
     ```yaml
     description: "Um jardim digital das minhas notas e pensamentos."
     ```
   - **url:** Defina a URL base do seu site (deixe vazio por enquanto).
     ```yaml
     url: ""
     ```
   - **baseurl:** Se o site estiver no root (sem subdiretório), deixe vazio.
     ```yaml
     baseurl: ""
     ```

3. **Configurações para Wikilinks:**
   - Verifique se as seguintes configurações estão presentes:
     ```yaml
     collections:
       notes:
         output: true
         permalink: /:title/
     ```

4. **Plugins Necessários:**
   - Certifique-se de que os plugins necessários estão listados:
     ```yaml
     plugins:
       - jekyll-optional-front-matter
       - jekyll-note-link
     ```

5. **Outras Configurações Importantes:**
   - **markdown:** Defina o processador de Markdown.
     ```yaml
     markdown: kramdown
     ```
   - **theme:** Se desejar usar o tema padrão ou alterar para outro.

6. **Salvar e Fechar o Arquivo.**

---

## 7. Configurando o GitHub Pages para Hospedar o Site

Agora, você vai configurar o GitHub Pages para hospedar seu site diretamente do repositório.

### Passos:

1. **Acesse as Configurações do Repositório no GitHub:**
   - No seu repositório, clique em **"Settings"**.

2. **Navegue até GitHub Pages:**
   - No menu lateral, clique em **"Pages"**.

3. **Configurar a Fonte do GitHub Pages:**
   - **Source:** Selecione a branch que contém seu código (`main` ou `master`).
   - **Folder:** Selecione a pasta `/ (root)`.
   - Clique em **"Save"**.

4. **Verifique a URL do Site:**
   - Após salvar, o GitHub fornecerá a URL onde seu site estará disponível.
     - Geralmente é `https://seu-usuario.github.io/nome-do-repositorio`.

---

## 8. Testando o Site Localmente (Opcional)

É recomendável testar o site localmente antes de publicá-lo para garantir que tudo funcione corretamente.

### Pré-requisitos:

- **Ruby** instalado.
- **Bundler** instalado.
  ```bash
  gem install bundler
  ```

### Passos:

1. **Instale as Dependências:**
   - No terminal, na pasta do seu projeto, execute:
     ```bash
     bundle install
     ```

2. **Inicie o Servidor Local:**
   ```bash
   bundle exec jekyll serve
   ```
   - O site estará disponível em `http://localhost:4000`.

3. **Teste o Site:**
   - Navegue pelas páginas, verifique os links, backlinks e layout.

4. **Interrompa o Servidor:**
   - Pressione `Ctrl + C` no terminal para parar o servidor.

---

## 9. Publicando o Site no GitHub Pages

Após confirmar que o site está funcionando corretamente, você pode fazer o push das alterações para o GitHub.

### Passos:

1. **Adicionar as Alterações ao Git:**
   ```bash
   git add .
   ```

2. **Fazer o Commit das Alterações:**
   ```bash
   git commit -m "Adiciona notas e configurações iniciais"
   ```

3. **Enviar para o GitHub:**
   ```bash
   git push origin main
   ```
   - Substitua `main` por `master` se for o nome da sua branch.

4. **Verificar o Status no GitHub:**
   - Vá até o repositório no GitHub e verifique se os arquivos foram atualizados.

5. **Aguardar a Publicação:**
   - O GitHub Pages geralmente leva alguns minutos para processar o site.

6. **Acessar o Site Online:**
   - Visite a URL fornecida pelo GitHub Pages para ver seu site publicado.

---

## 10. Configurando Plugins e Recursos Adicionais

Para suportar recursos do Obsidian, como wikilinks e backlinks, pode ser necessário configurar plugins adicionais.

### 10.1. Suporte a Wikilinks (`[[links]]`)

O Jekyll não suporta wikilinks nativamente. Você precisará de um plugin.

#### Usando o Plugin `jekyll-note-link`:

1. **Adicionar o Plugin ao `Gemfile`:**
   ```ruby
   gem 'jekyll-note-link'
   ```

2. **Adicionar o Plugin ao `_config.yml`:**
   ```yaml
   plugins:
     - jekyll-note-link
   ```

3. **Configurar o Plugin (se necessário):**
   - Verifique a documentação do plugin para configurações adicionais.

### 10.2. Suporte a Backlinks

Para gerar backlinks (mostrar quais notas referenciam a nota atual), você pode utilizar um script personalizado ou um plugin.

#### Exemplo de Implementação Simples:

1. **Criar um Arquivo de Plugin em `_plugins/backlinks.rb`:**

   ```ruby
   Jekyll::Hooks.register :notes, :post_write do |note|
     all_notes = note.site.collections['notes'].docs
     backlinks = all_notes.select do |other_note|
       other_note.content.include?("[[#{note.data['title']}]]")
     end

     unless backlinks.empty?
       File.open(note.destination('.html'), 'a') do |file|
         file.puts "<h2>Backlinks</h2>"
         file.puts "<ul>"
         backlinks.each do |backlink|
           file.puts "<li><a href='#{backlink.url}'>#{backlink.data['title']}</a></li>"
         end
         file.puts "</ul>"
       end
     end
   end
   ```

2. **Modificar o Layout para Exibir Backlinks:**
   - No arquivo de layout (por exemplo, `_layouts/note.html`), inclua uma seção para backlinks.

### 10.3. Configurar GitHub Actions para Build Personalizado

O GitHub Pages tem restrições sobre plugins. Para usar plugins personalizados, você precisa configurar o GitHub Actions para construir o site.

#### Passos:

1. **Criar o Arquivo de Workflow:**
   - Crie `.github/workflows/jekyll.yml` no seu projeto.

2. **Adicionar o Seguinte Conteúdo:**

   ```yaml
   name: Build and Deploy Jekyll Site

   on:
     push:
       branches:
         - main

   jobs:
     build-deploy:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout
           uses: actions/checkout@v2

         - name: Setup Ruby
           uses: ruby/setup-ruby@v1
           with:
             ruby-version: '2.7'

         - name: Install Dependencies
           run: |
             gem install bundler
             bundle install

         - name: Build Site
           run: bundle exec jekyll build

         - name: Deploy to GitHub Pages
           uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./_site
   ```

3. **Configurar o GitHub Pages para Usar a Branch `gh-pages`:**
   - Vá em **Settings** > **Pages**.
   - Em **Source**, selecione a branch `gh-pages` e a pasta `/ (root)`.

4. **Commit e Push:**
   - Faça commit das alterações e envie para o GitHub.
   - O GitHub Actions será acionado automaticamente.

---

## 11. Resolução de Problemas Comuns

### Problema: **O site não está carregando ou exibe um erro 404.**

**Soluções Possíveis:**

- Verifique se o GitHub Pages está configurado corretamente.
- Aguarde alguns minutos após o push, pois o GitHub Pages pode demorar para atualizar.
- Certifique-se de que o site está sendo construído sem erros (verifique o log do GitHub Actions).

### Problema: **Wikilinks não estão sendo convertidos em links clicáveis.**

**Soluções Possíveis:**

- Certifique-se de que o plugin para wikilinks está instalado e configurado.
- Verifique se os plugins personalizados estão sendo executados (pode ser necessário usar o GitHub Actions).

### Problema: **Backlinks não estão aparecendo nas notas.**

**Soluções Possíveis:**

- Verifique a implementação do script de backlinks.
- Certifique-se de que o layout das notas inclui a seção de backlinks.

---

## 12. Conclusão

Parabéns! Você configurou com sucesso um site estático usando Jekyll e GitHub Pages para publicar suas notas do Obsidian online. Seu site suporta wikilinks e backlinks, permitindo uma navegação rica entre suas notas, e está hospedado gratuitamente no GitHub Pages.

---

## Anexos

### Links Úteis

- **Documentação do Jekyll:** [https://jekyllrb.com/docs/](https://jekyllrb.com/docs/)
- **GitHub Pages com Jekyll:** [https://docs.github.com/pt/pages/setting-up-a-github-pages-site-with-jekyll](https://docs.github.com/pt/pages/setting-up-a-github-pages-site-with-jekyll)
- **Template Digital Garden:** [https://github.com/maximevaillancourt/digital-garden-jekyll-template](https://github.com/maximevaillancourt/digital-garden-jekyll-template)
- **Configuração de Domínio Personalizado no GitHub Pages:** [https://docs.github.com/pt/pages/configuring-a-custom-domain-for-your-github-pages-site](https://docs.github.com/pt/pages/configuring-a-custom-domain-for-your-github-pages-site)

### Comandos Git Comuns

- **Status do Repositório:**
  ```bash
  git status
  ```
- **Adicionar Alterações:**
  ```bash
  git add .
  ```
- **Fazer Commit:**
  ```bash
  git commit -m "Mensagem de commit"
  ```
- **Enviar para o GitHub:**
  ```bash
  git push origin main
  ```

---

**Nota:** Nas próximas etapas, você pode personalizar ainda mais o layout e o tema do seu site para que ele se pareça mais com a Wikipédia, conforme desejado. Além disso, poderá configurar seu domínio personalizado para que o site seja acessível através do seu próprio endereço na web.

---

## Próximos Passos

- **Passo 3:** Customizar o tema do site para que tenha uma aparência limpa e semelhante à Wikipédia.
- **Passo 4:** Configurar backlinks e wikilinks avançados.
- **Passo 5:** Automatizar as atualizações do site para refletir automaticamente as alterações feitas no seu computador.

Se precisar de assistência adicional ou tiver dúvidas, sinta-se à vontade para buscar recursos adicionais ou entrar em contato para obter ajuda.

---

**Fim do Documento**

# Guia Detalhado: Customizando o Tema para Parecer com a Wikipédia

## Introdução

Este documento fornece um guia passo a passo detalhado para personalizar o tema do seu site Jekyll hospedado no GitHub Pages, de forma que ele tenha uma aparência limpa e semelhante à da Wikipédia. O objetivo é criar uma interface familiar e intuitiva, com uma página inicial que possua links clicáveis para todas as outras páginas, facilitando a navegação pelo conteúdo das suas notas do Obsidian.

---

## Índice

1. [Pré-requisitos](#1-pré-requisitos)
2. [Escolhendo um Tema Base Apropriado](#2-escolhendo-um-tema-base-apropriado)
3. [Integrando o Tema ao Seu Projeto Jekyll](#3-integrando-o-tema-ao-seu-projeto-jekyll)
4. [Customizando o Layout para Semelhança com a Wikipédia](#4-customizando-o-layout-para-semelhança-com-a-wikipédia)
   - 4.1. [Estrutura de Páginas](#41-estrutura-de-páginas)
   - 4.2. [Barra de Navegação](#42-barra-de-navegação)
   - 4.3. [Estilos CSS Personalizados](#43-estilos-css-personalizados)
5. [Criando uma Página Inicial com Links para Todas as Páginas](#5-criando-uma-página-inicial-com-links-para-todas-as-páginas)
6. [Adicionando Funcionalidades Semelhantes à Wikipédia](#6-adicionando-funcionalidades-semelhantes-à-wikipédia)
   - 6.1. [Pesquisa Interna](#61-pesquisa-interna)
   - 6.2. [Tabela de Conteúdos](#62-tabela-de-conteúdos)
7. [Testando as Alterações Localmente](#7-testando-as-alterações-localmente)
8. [Publicando as Alterações no GitHub Pages](#8-publicando-as-alterações-no-github-pages)
9. [Resolução de Problemas Comuns](#9-resolução-de-problemas-comuns)
10. [Conclusão](#10-conclusão)

---

## 1. Pré-requisitos

Antes de começar, certifique-se de ter concluído as etapas anteriores:

- Suas notas do Obsidian estão sincronizadas com um repositório no GitHub.
- Você configurou um site Jekyll básico usando o GitHub Pages.
- O site está funcionando e suas notas estão sendo exibidas online.

Além disso, você precisará de:

- **Conhecimento básico de HTML e CSS**.
- **Um editor de texto ou IDE** (por exemplo, Visual Studio Code, Sublime Text).

---

## 2. Escolhendo um Tema Base Apropriado

Para facilitar o processo de personalização, é recomendável começar com um tema Jekyll que seja simples e fácil de modificar.

### Opção Recomendada: **Tema "Just the Docs"**

- **Repositório:** [pmarsceill/just-the-docs](https://github.com/pmarsceill/just-the-docs)
- **Características:**
  - Layout limpo e responsivo.
  - Navegação lateral semelhante à da Wikipédia.
  - Suporte a busca integrada.
  - Fácil de personalizar com variáveis no `_config.yml`.

---

## 3. Integrando o Tema ao Seu Projeto Jekyll

### Passos:

1. **Adicionar o Tema ao `Gemfile`:**

   No arquivo `Gemfile` do seu projeto, adicione a linha:

   ```ruby
   gem "just-the-docs"
   ```

2. **Atualizar o Arquivo `_config.yml`:**

   No seu arquivo `_config.yml`, defina o tema:

   ```yaml
   theme: just-the-docs
   ```

   **Nota:** Se você estiver usando GitHub Pages, use a versão compatível:

   ```yaml
   remote_theme: pmarsceill/just-the-docs
   ```

3. **Instalar as Dependências:**

   No terminal, execute:

   ```bash
   bundle install
   ```

   **Nota:** Se estiver usando GitHub Actions para construir o site, as dependências serão instaladas automaticamente.

4. **Remover ou Ajustar Configurações de Temas Anteriores:**

   - Verifique se não há conflitos com outros temas ou plugins.
   - Comente ou remova quaisquer referências a outros temas no `_config.yml`.

---

## 4. Customizando o Layout para Semelhança com a Wikipédia

Agora que o tema básico está integrado, você pode personalizá-lo para que se pareça mais com a Wikipédia.

### 4.1. Estrutura de Páginas

- **Organização de Conteúdo:**
  - A Wikipédia utiliza uma estrutura hierárquica e categorias para organizar conteúdo.
  - Crie pastas ou coleções em seu projeto Jekyll para representar diferentes categorias ou tópicos.

- **Front Matter das Páginas:**
  - Adicione metadados às suas notas para melhor controle.
  - Exemplo de front matter:

    ```yaml
    ---
    title: "Título da Página"
    nav_order: 1
    has_children: true
    ---
    ```

### 4.2. Barra de Navegação

- **Configurar a Navegação:**

  - O tema "Just the Docs" permite criar uma navegação lateral automática.
  - Use o parâmetro `nav_order` no front matter para ordenar as páginas.

- **Exemplo de Configuração:**

  - Página inicial (`index.md`):

    ```yaml
    ---
    title: "Página Inicial"
    nav_order: 1
    has_children: true
    ---
    ```

  - Subpágina (`subpagina.md`):

    ```yaml
    ---
    title: "Subpágina"
    parent: "Página Inicial"
    nav_order: 2
    ---
    ```

### 4.3. Estilos CSS Personalizados

Para ajustar o visual do site e aproximá-lo do estilo da Wikipédia, você pode adicionar CSS personalizado.

#### Passos:

1. **Criar um Arquivo CSS Personalizado:**

   - Crie uma pasta `assets/css` se ainda não existir.
   - Dentro dela, crie um arquivo chamado `custom.css`.

2. **Incluir o CSS Personalizado no `_config.yml`:**

   ```yaml
   # Adicione ao seu _config.yml
   just_the_docs:
     additional_css:
       - assets/css/custom.css
   ```

3. **Editar o `custom.css` para Ajustar Estilos:**

   - Ajuste as fontes, cores e outros estilos para se assemelhar à Wikipédia.

   **Exemplo:**

   ```css
   /* Fonte similar à da Wikipédia */
   body {
     font-family: "Linux Libertine", "Georgia", serif;
     font-size: 16px;
     background-color: #f9f9f9;
     color: #202122;
   }

   /* Estilo dos links */
   a {
     color: #0645ad;
     text-decoration: none;
   }

   a:hover {
     text-decoration: underline;
   }

   /* Ajustes na barra de navegação */
   .sidebar {
     background-color: #f5f5f5;
   }

   /* Títulos */
   h1, h2, h3, h4, h5, h6 {
     color: #000;
   }
   ```

4. **Incluir Fontes Externas (Opcional):**

   - Para usar fontes específicas, inclua-as no `<head>` do seu layout.

   **Passos:**

   - Crie um arquivo `_includes/head-custom.html`.
   - Adicione o código de inclusão da fonte:

     ```html
     <!-- _includes/head-custom.html -->
     <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Linux+Libertine">
     ```

   - No `_config.yml`, informe ao tema para incluir seu arquivo personalizado:

     ```yaml
     just_the_docs:
       head_html: "_includes/head-custom.html"
     ```

---

## 5. Criando uma Página Inicial com Links para Todas as Páginas

A página inicial deve servir como um índice, facilitando o acesso a todas as suas notas.

### Passos:

1. **Editar o `index.md`:**

   - Localize ou crie o arquivo `index.md` na raiz do seu projeto.

2. **Adicionar Conteúdo ao `index.md`:**

   ```markdown
   ---
   title: "Página Inicial"
   nav_order: 1
   has_children: true
   permalink: /
   ---

   # Bem-vindo à Minha Wiki Pessoal

   Aqui você encontrará uma coleção de notas e artigos sobre diversos assuntos.

   ## Todas as Páginas

   {% assign pages_list = site.pages | sort: 'title' %}
   {% for page in pages_list %}
   - [{{ page.title }}]({{ page.url | relative_url }})
   {% endfor %}
   ```

   **Nota:** O código acima gera uma lista de todas as páginas do site, ordenadas por título.

3. **Personalizar a Lista de Páginas (Opcional):**

   - Você pode filtrar ou categorizar as páginas conforme necessário.
   - Por exemplo, listar apenas as páginas dentro de uma categoria específica.

---

## 6. Adicionando Funcionalidades Semelhantes à Wikipédia

Para enriquecer a experiência do usuário, você pode adicionar recursos adicionais.

### 6.1. Pesquisa Interna

O tema "Just the Docs" já inclui suporte a pesquisa.

#### Configuração:

1. **Ativar a Pesquisa no `_config.yml`:**

   ```yaml
   just_the_docs:
     search_enabled: true
     search_tokenizer_separator: /[\s/]+/
   ```

2. **Personalizar a Pesquisa (Opcional):**

   - Você pode ajustar a sensibilidade da pesquisa e outros parâmetros.

### 6.2. Tabela de Conteúdos

Adicionar uma tabela de conteúdos nas páginas facilita a navegação em conteúdos longos.

#### Implementação:

1. **Ativar a TOC no Front Matter da Página:**

   ```yaml
   ---
   title: "Título da Página"
   nav_order: 2
   has_toc: true
   toc_label: "Conteúdo"
   toc_sticky: true
   ---
   ```

2. **Personalizar a Aparência da TOC (Opcional):**

   - Use CSS personalizado para ajustar o estilo da tabela de conteúdos.

---

## 7. Testando as Alterações Localmente

Antes de publicar as alterações, é recomendável testá-las localmente.

### Passos:

1. **Iniciar o Servidor Jekyll:**

   ```bash
   bundle exec jekyll serve
   ```

2. **Acessar o Site Localmente:**

   - Abra o navegador e acesse `http://localhost:4000`.

3. **Verificar o Layout e Funcionalidades:**

   - Navegue pelo site, teste a pesquisa, links e verifique se a aparência está conforme o esperado.

---

## 8. Publicando as Alterações no GitHub Pages

Após confirmar que tudo está funcionando corretamente, você pode publicar as alterações.

### Passos:

1. **Adicionar os Arquivos Modificados ao Git:**

   ```bash
   git add .
   ```

2. **Fazer Commit das Alterações:**

   ```bash
   git commit -m "Customiza tema para semelhança com a Wikipédia"
   ```

3. **Enviar as Alterações para o GitHub:**

   ```bash
   git push origin main
   ```

4. **Aguardar a Atualização do GitHub Pages:**

   - O GitHub Pages processará as alterações e atualizará o site em alguns minutos.

5. **Verificar o Site Online:**

   - Acesse o site em seu domínio personalizado ou URL do GitHub Pages para verificar as mudanças.

---

## 9. Resolução de Problemas Comuns

### Problema: **As alterações de estilo não estão sendo refletidas no site.**

**Soluções Possíveis:**

- Certifique-se de que o caminho para o arquivo CSS personalizado está correto no `_config.yml`.
- Verifique se o cache do navegador não está exibindo a versão antiga. Tente atualizar a página ou limpar o cache.

### Problema: **A pesquisa não está funcionando.**

**Soluções Possíveis:**

- Verifique se a pesquisa está habilitada no `_config.yml`.
- Certifique-se de que não há erros no console do navegador que indiquem problemas com JavaScript.

### Problema: **Links internos não estão funcionando corretamente.**

**Soluções Possíveis:**

- Verifique se os links estão usando URLs relativos corretos.
- Certifique-se de que as páginas referenciadas existem e estão sendo geradas pelo Jekyll.

---

## 10. Conclusão

Seguindo este guia, você personalizou o tema do seu site para que ele tenha uma aparência limpa e semelhante à da Wikipédia. Com uma página inicial que contém links para todas as suas notas e recursos adicionais como pesquisa interna e tabela de conteúdos, seu site agora oferece uma experiência de usuário aprimorada.

---

## Anexos

### Links Úteis

- **Tema Just the Docs:**
  - [Documentação](https://just-the-docs.github.io/just-the-docs/)
  - [Repositório no GitHub](https://github.com/just-the-docs/just-the-docs)

- **Personalizando Temas no Jekyll:**
  - [Documentação Oficial](https://jekyllrb.com/docs/themes/)

- **Fontes Livres para Uso:**
  - [Google Fonts](https://fonts.google.com/)
  - [Linux Libertine Font](https://www.fontsquirrel.com/fonts/linux-libertine)

### Comandos Úteis

- **Iniciar o Servidor Jekyll Localmente:**

  ```bash
  bundle exec jekyll serve
  ```

- **Adicionar e Comitar Alterações no Git:**

  ```bash
  git add .
  git commit -m "Mensagem do commit"
  ```

- **Enviar Alterações para o GitHub:**

  ```bash
  git push origin main
  ```

---

**Nota:** Lembre-se de que a personalização é um processo iterativo. Sinta-se à vontade para ajustar os estilos e layouts conforme suas preferências. A comunidade do Jekyll e do Obsidian é bastante ativa, e há muitos recursos disponíveis para ajudá-lo a atingir o visual desejado.

---

**Fim do Documento**

# Guia Detalhado: Configurando Seu Domínio Personalizado com GitHub Pages

## Introdução

Este documento fornece um guia passo a passo detalhado para configurar seu domínio personalizado para apontar para o site hospedado no **GitHub Pages**. Ao usar seu próprio domínio, você oferece aos visitantes um endereço mais profissional e fácil de lembrar, além de fortalecer sua presença online.

---

## Índice

1. [Pré-requisitos](#1-pré-requisitos)
2. [Configurando o Domínio no GitHub Pages](#2-configurando-o-domínio-no-github-pages)
3. [Atualizando os Registros DNS do Seu Domínio](#3-atualizando-os-registros-dns-do-seu-domínio)
   - 3.1. [Para Domínio Raiz (seudominio.com)](#31-para-domínio-raiz-seudominiocom)
   - 3.2. [Para Subdomínio (www.seudominio.com)](#32-para-subdomínio-wwwseudominiocom)
4. [Habilitando HTTPS no GitHub Pages](#4-habilitando-https-no-github-pages)
5. [Verificando a Configuração](#5-verificando-a-configuração)
6. [Resolução de Problemas Comuns](#6-resolução-de-problemas-comuns)
7. [Conclusão](#7-conclusão)

---

## 1. Pré-requisitos

Antes de iniciar o processo, certifique-se de ter os seguintes itens:

- **Um domínio registrado** com acesso ao painel de controle DNS. Pode ser de qualquer registrador, como GoDaddy, Namecheap, Registro.br, etc.
- **Um site hospedado no GitHub Pages**, configurado e funcionando em `https://seu-usuario.github.io/seu-repositorio/`.
- **Permissões administrativas** tanto no seu repositório GitHub quanto na conta do domínio.

---

## 2. Configurando o Domínio no GitHub Pages

Primeiro, você precisa informar ao GitHub que deseja usar um domínio personalizado para o seu site.

### Passos:

1. **Acesse as Configurações do Repositório no GitHub:**

   - Vá para o repositório que hospeda seu site.
   - Clique em **"Settings"** (Configurações).

2. **Navegue até GitHub Pages:**

   - No menu lateral, desça até a seção **"Pages"**.

3. **Defina a Fonte do GitHub Pages (se ainda não o fez):**

   - Em **"Source"**, certifique-se de que a branch correta está selecionada (geralmente `gh-pages`, `main` ou `master`).
   - Certifique-se de que a pasta é a raiz (`/ (root)`).

4. **Adicionar o Domínio Personalizado:**

   - Na seção **"Custom domain"**, insira seu domínio personalizado, por exemplo, `www.seudominio.com` ou `seudominio.com`.
   - Clique em **"Save"**.

5. **Verificar a Opção de Enforcement do HTTPS:**

   - Após salvar, o GitHub tentará verificar se o domínio está apontando para o GitHub Pages.
   - Inicialmente, pode aparecer uma mensagem de erro, pois os registros DNS ainda não foram configurados (faremos isso na próxima etapa).

---

## 3. Atualizando os Registros DNS do Seu Domínio

Agora, você precisa configurar os registros DNS do seu domínio para apontar para os servidores do GitHub Pages.

### Acesso ao Painel DNS

- Faça login na conta do seu provedor de domínio (por exemplo, GoDaddy, Namecheap, Registro.br).
- Acesse a seção de gerenciamento de DNS ou zona DNS.

### Escolha entre Domínio Raiz e Subdomínio

Você pode configurar seu site para ser acessado via:

- **Domínio Raiz**: `seudominio.com`
- **Subdomínio**: `www.seudominio.com`

#### Nota:

- **Recomendação**: Usar `www.seudominio.com` é mais simples, pois apontar o domínio raiz (`seudominio.com`) requer configurações adicionais (registros A).

### 3.1. Para Domínio Raiz (`seudominio.com`)

#### Passos:

1. **Adicionar Registros A**

   - Adicione os seguintes registros **A**:

     | Tipo | Nome              | Valor                |
     |------|-------------------|----------------------|
     | A    | @                 | 185.199.108.153      |
     | A    | @                 | 185.199.109.153      |
     | A    | @                 | 185.199.110.153      |
     | A    | @                 | 185.199.111.153      |

   - **Nota**: O símbolo `@` representa o domínio raiz.

2. **Excluir Outros Registros A**

   - Certifique-se de que não há outros registros A configurados para o domínio raiz, pois isso pode causar conflitos.

3. **Adicionar Registro CNAME para "www" (Opcional)**

   - Se quiser que `www.seudominio.com` também funcione, adicione um registro **CNAME**:

     | Tipo  | Nome | Valor                      |
     |-------|------|----------------------------|
     | CNAME | www  | seu-usuario.github.io.     |

   - **Nota**: O ponto no final do valor (`.github.io.`) pode ser necessário em alguns provedores.

### 3.2. Para Subdomínio (`www.seudominio.com`)

#### Passos:

1. **Adicionar Registro CNAME**

   - Adicione o seguinte registro **CNAME**:

     | Tipo  | Nome | Valor                      |
     |-------|------|----------------------------|
     | CNAME | www  | seu-usuario.github.io.     |

   - **Nota**: Substitua `seu-usuario` pelo seu nome de usuário no GitHub.

2. **Excluir Outros Registros CNAME ou A para "www"**

   - Certifique-se de que não há outros registros CNAME ou A para `www`.

### Salvar e Aplicar as Alterações

- Após adicionar os registros, salve as alterações.
- A propagação das alterações DNS pode levar de alguns minutos a 48 horas, embora geralmente ocorra em menos de uma hora.

---

## 4. Habilitando HTTPS no GitHub Pages

Após os registros DNS propagarem, você pode habilitar o HTTPS para o seu domínio.

### Passos:

1. **Retornar às Configurações do GitHub Pages:**

   - No repositório, vá novamente em **"Settings"** > **"Pages"**.

2. **Verificar o Status do Domínio Personalizado:**

   - Se os registros DNS estiverem configurados corretamente, você verá uma mensagem indicando que o domínio foi verificado.
   - O GitHub irá provisionar automaticamente um certificado SSL para o seu domínio.

3. **Habilitar Enforce HTTPS:**

   - Marque a opção **"Enforce HTTPS"** para garantir que todas as conexões ao seu site usem HTTPS.

4. **Aguardar a Emissão do Certificado SSL:**

   - Pode levar alguns minutos para que o certificado SSL seja emitido.
   - Enquanto isso, o site pode exibir um aviso de segurança ou não estar acessível via HTTPS.

---

## 5. Verificando a Configuração

Após concluir as etapas anteriores, é hora de testar se o seu site está funcionando corretamente com o domínio personalizado.

### Passos:

1. **Acessar o Seu Domínio no Navegador:**

   - Digite `http://seudominio.com` ou `http://www.seudominio.com` na barra de endereço.

2. **Verificar se o Site Carrega Corretamente:**

   - O site deve ser exibido como esperado.
   - Verifique se todos os recursos (imagens, links, etc.) estão funcionando.

3. **Testar o HTTPS:**

   - Acesse `https://seudominio.com` ou `https://www.seudominio.com`.
   - Verifique se o cadeado de segurança é exibido no navegador, indicando uma conexão segura.

4. **Verificar Redirecionamentos (Opcional):**

   - Tente acessar o domínio sem "www" se configurou ambos.
   - Certifique-se de que o site redireciona corretamente para o domínio desejado.

---

## 6. Resolução de Problemas Comuns

### Problema 1: **O site não carrega no domínio personalizado.**

**Possíveis Causas e Soluções:**

- **Propagação DNS Incompleta:**

  - Pode levar até 48 horas para a propagação completa.
  - Use ferramentas como [WhatsMyDNS](https://www.whatsmydns.net/) para verificar os registros DNS globalmente.

- **Registros DNS Incorretos:**

  - Verifique se os registros A e CNAME estão configurados corretamente.
  - Certifique-se de não ter registros conflitantes.

### Problema 2: **HTTPS não está funcionando ou mostra um aviso de segurança.**

**Possíveis Causas e Soluções:**

- **Certificado SSL Ainda Não Emitido:**

  - Aguarde alguns minutos e tente novamente.

- **Domínio Não Verificado no GitHub Pages:**

  - Verifique se o domínio foi reconhecido no GitHub Pages (sem mensagens de erro).

### Problema 3: **Erro "Page build warning" ou "Domain's DNS record could not be retrieved" no GitHub.**

**Possíveis Causas e Soluções:**

- **Registros DNS Não Apontam para o GitHub:**

  - Verifique novamente os registros DNS.

- **Arquivos CNAME Confusos:**

  - Certifique-se de que não há um arquivo `CNAME` no repositório com informações incorretas.

### Problema 4: **Redirecionamentos Não Funcionam Como Esperado.**

**Possíveis Causas e Soluções:**

- **Configuração de Redirecionamento Necessária:**

  - Se desejar que `seudominio.com` redirecione para `www.seudominio.com` ou vice-versa, pode ser necessário configurar redirecionamentos no seu provedor de domínio.

---

## 7. Conclusão

Você configurou com sucesso seu domínio personalizado para apontar para o site hospedado no GitHub Pages. Agora, seus visitantes podem acessar seu site através de um endereço profissional e personalizado, como `www.seudominio.com`.

---

## Anexos

### Links Úteis

- **Documentação do GitHub Pages sobre Domínio Personalizado:**

  - [Configurando um domínio personalizado para seu site do GitHub Pages](https://docs.github.com/pt/pages/configuring-a-custom-domain-for-your-github-pages-site)

- **Ferramentas de Verificação DNS:**

  - [WhatsMyDNS](https://www.whatsmydns.net/)
  - [DNSChecker](https://dnschecker.org/)

### Exemplos de Registros DNS

#### Para Domínio Raiz (`seudominio.com`):

| Tipo | Nome | Valor             | TTL    |
|------|------|-------------------|--------|
| A    | @    | 185.199.108.153   | 3600   |
| A    | @    | 185.199.109.153   | 3600   |
| A    | @    | 185.199.110.153   | 3600   |
| A    | @    | 185.199.111.153   | 3600   |
| CNAME| www  | seu-usuario.github.io. | 3600 |

#### Para Subdomínio (`www.seudominio.com`):

| Tipo | Nome | Valor                      | TTL    |
|------|------|----------------------------|--------|
| CNAME| www  | seu-usuario.github.io.     | 3600   |

---

**Nota:** A configuração de um domínio personalizado pode parecer complexa à primeira vista, mas seguindo este guia passo a passo, você deve ser capaz de completar o processo sem grandes dificuldades. Se encontrar problemas, não hesite em consultar a documentação oficial do GitHub ou entrar em contato com o suporte do seu provedor de domínio.

---

**Fim do Documento**
# Guia Detalhado: Automatizando Atualizações do Site para Refletir Automaticamente as Alterações Feitas no Seu Computador

## Introdução

Este documento fornece um guia passo a passo detalhado para automatizar o processo de atualização do seu site hospedado no **GitHub Pages**, de forma que qualquer alteração feita em suas notas do **Obsidian** no seu computador seja refletida automaticamente no site. Isso permite que você mantenha seu site sempre atualizado sem a necessidade de intervenções manuais frequentes.

---

## Índice

1. [Pré-requisitos](#1-pré-requisitos)
2. [Visão Geral do Processo](#2-visão-geral-do-processo)
3. [Configurando o Obsidian Git para Atualizações Automáticas](#3-configurando-o-obsidian-git-para-atualizações-automáticas)
   - 3.1. [Agendando Commits e Push Automáticos](#31-agendando-commits-e-push-automáticos)
   - 3.2. [Resolvendo Conflitos Automáticos](#32-resolvendo-conflitos-automáticos)
4. [Configurando GitHub Actions para Build e Deploy Automático](#4-configurando-github-actions-para-build-e-deploy-automático)
   - 4.1. [Criando um Workflow do GitHub Actions](#41-criando-um-workflow-do-github-actions)
   - 4.2. [Configurando o Workflow para Construir e Implantar o Site](#42-configurando-o-workflow-para-construir-e-implantar-o-site)
5. [Testando a Automatização](#5-testando-a-automatização)
6. [Monitorando e Mantendo o Processo Automatizado](#6-monitorando-e-mantendo-o-processo-automatizado)
7. [Resolução de Problemas Comuns](#7-resolução-de-problemas-comuns)
8. [Conclusão](#8-conclusão)

---

## 1. Pré-requisitos

Antes de iniciar, certifique-se de ter concluído as etapas anteriores:

- Suas notas do **Obsidian** estão sincronizadas com um repositório no **GitHub** usando o plugin **Obsidian Git**.
- Você configurou um site **Jekyll** ou **Hugo** hospedado no **GitHub Pages**.
- O site está personalizado conforme desejado e funcionando corretamente.
- Você tem conhecimento básico de Git, GitHub e edição de arquivos YAML.

---

## 2. Visão Geral do Processo

Para automatizar as atualizações do site, seguiremos os seguintes passos:

1. **Configurar o Obsidian Git para realizar commits e push automaticamente** sempre que alterações forem feitas nas notas.

2. **Configurar o GitHub Actions** para automaticamente construir e implantar o site no GitHub Pages sempre que houver novos commits no repositório.

Isso criará um fluxo contínuo de integração e implantação (CI/CD), onde suas alterações locais serão refletidas no site sem intervenção manual.

---

## 3. Configurando o Obsidian Git para Atualizações Automáticas

O plugin **Obsidian Git** permite automatizar o processo de commit e push das suas alterações para o GitHub.

### 3.1. Agendando Commits e Push Automáticos

#### Passos:

1. **Acesse as Configurações do Obsidian Git:**

   - No Obsidian, clique no ícone de **engrenagem** para acessar as configurações.
   - No menu lateral, desça até **"Plugin Options"** e selecione **"Obsidian Git"**.

2. **Configurar o Intervalo de Auto Commit:**

   - **Auto Commit Interval (minutos):**
     - Define a frequência com que o plugin realizará commits automáticos das suas alterações.
     - Defina um intervalo adequado às suas necessidades. Por exemplo, **5 minutos**.
     - Se você fizer muitas alterações em curtos períodos, um intervalo menor pode ser adequado.

3. **Configurar o Intervalo de Auto Push:**

   - **Auto Push Interval (minutos):**
     - Define a frequência com que o plugin enviará (push) os commits para o GitHub.
     - Recomenda-se definir o mesmo valor do auto commit ou um valor maior.
     - Exemplo: **5 minutos**.

4. **Configurar Auto Pull (Opcional):**

   - **Auto Pull Interval (minutos):**
     - Se você também fizer alterações diretamente no repositório remoto ou em outros dispositivos, ative o auto pull.
     - Defina um intervalo, como **10 minutos**.

5. **Salvar as Configurações:**

   - Certifique-se de que as alterações estão salvas e que o plugin está ativo.

### 3.2. Resolvendo Conflitos Automáticos

Conflitos podem ocorrer quando há alterações divergentes entre o repositório local e o remoto.

#### Configurações:

1. **Ativar a Resolução Automática de Conflitos:**

   - Nas configurações do Obsidian Git, procure a opção **"Auto Merge Conflicts"** ou **"Commit message on conflict merge"**.
   - Ative a opção para que o plugin tente resolver conflitos automaticamente.

2. **Configurar Estratégias de Merge:**

   - Se disponível, defina a estratégia de merge, como **"theirs"** (mantém as alterações do repositório remoto) ou **"ours"** (mantém as alterações locais).
   - **Atenção:** Use com cuidado, pois pode resultar na perda de alterações.

3. **Notificações de Conflitos:**

   - Habilite notificações para ser alertado quando ocorrer um conflito que não possa ser resolvido automaticamente.

---

## 4. Configurando GitHub Actions para Build e Deploy Automático

O **GitHub Actions** permite automatizar fluxos de trabalho, como a construção e implantação do seu site sempre que houver novas alterações.

### 4.1. Criando um Workflow do GitHub Actions

#### Passos:

1. **Criar o Diretório de Workflows:**

   - Na raiz do seu repositório, crie a pasta `.github/workflows` se ela ainda não existir.

2. **Criar um Arquivo de Workflow:**

   - Dentro da pasta `workflows`, crie um arquivo chamado `deploy.yml` ou `main.yml`.

### 4.2. Configurando o Workflow para Construir e Implantar o Site

#### Exemplo de Workflow para um Site Jekyll:

```yaml
name: Build and Deploy Jekyll Site

on:
  push:
    branches:
      - main  # Substitua por 'master' se for o caso

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.0'  # Use a versão recomendada para o Jekyll

      - name: Install Dependencies
        run: |
          gem install bundler
          bundle install

      - name: Build Site
        run: bundle exec jekyll build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_site
```

#### Explicação das Etapas:

- **on.push.branches:** O workflow será acionado sempre que houver um push na branch especificada (geralmente `main` ou `master`).

- **jobs.build-deploy:** Define o trabalho de construção e implantação.

- **steps:**
  - **Checkout:** Faz o checkout do repositório.
  - **Setup Ruby:** Configura o ambiente Ruby necessário para executar o Jekyll.
  - **Install Dependencies:** Instala o Bundler e as dependências listadas no `Gemfile`.
  - **Build Site:** Constrói o site usando o Jekyll.
  - **Deploy to GitHub Pages:** Implanta o site na branch `gh-pages`, que é usada pelo GitHub Pages.

#### Personalizações Necessárias:

- **Branch de Origem:**

  - Certifique-se de que o nome da branch especificada em `on.push.branches` corresponde à sua branch principal.

- **Versão do Ruby:**

  - Ajuste `ruby-version` conforme necessário. Consulte a [documentação do Jekyll](https://jekyllrb.com/docs/installation/) para verificar a versão compatível.

- **Publicação em Pasta Diferente (Opcional):**

  - Se o diretório de saída do seu site for diferente de `./_site`, ajuste o valor de `publish_dir`.

#### Configurando o GitHub Pages para Usar a Branch `gh-pages`:

1. **Acesse as Configurações do Repositório:**

   - No GitHub, vá para **"Settings"** do repositório.

2. **Configurar GitHub Pages:**

   - No menu lateral, clique em **"Pages"**.
   - Em **"Source"**, selecione a branch `gh-pages` e a pasta `/ (root)`.
   - Salve as configurações.

---

## 5. Testando a Automatização

Para garantir que tudo está funcionando corretamente, faça uma alteração de teste.

### Passos:

1. **Editar uma Nota no Obsidian:**

   - Faça uma pequena alteração em uma nota existente ou crie uma nova nota.

2. **Salvar a Alteração:**

   - Certifique-se de que a alteração foi salva no Obsidian.

3. **Observar o Obsidian Git:**

   - O plugin deve detectar a alteração e, conforme as configurações, realizar um commit e push automaticamente dentro do intervalo definido.

4. **Verificar o Repositório no GitHub:**

   - Após alguns minutos, vá para o seu repositório no GitHub e verifique se o novo commit está presente.

5. **Verificar o Workflow do GitHub Actions:**

   - No repositório, clique em **"Actions"**.
   - Verifique se um novo workflow foi acionado.
   - Certifique-se de que o workflow concluiu com sucesso.

6. **Acessar o Site:**

   - Visite seu site no GitHub Pages ou em seu domínio personalizado.
   - Verifique se a alteração está refletida no site.

---

## 6. Monitorando e Mantendo o Processo Automatizado

### Verificando Logs do GitHub Actions

- **Acessar Logs:**

  - No repositório, vá em **"Actions"** e selecione o workflow recente.
  - Clique nas etapas para ver os logs detalhados.

- **Monitorar Erros:**

  - Se o workflow falhar, os logs indicarão em qual etapa ocorreu o erro.
  - Com base nas mensagens de erro, você pode diagnosticar e corrigir problemas.

### Manutenção do Obsidian Git

- **Atualizações do Plugin:**

  - Verifique periodicamente se há atualizações para o plugin **Obsidian Git**.
  - Atualizações podem trazer correções de bugs e melhorias.

- **Verificar Conflitos:**

  - Embora a configuração automática de merge possa resolver muitos conflitos, ocasionalmente pode ser necessário intervir manualmente.
  - Esteja atento a notificações de conflitos não resolvidos.

### Segurança

- **Tokens de Acesso:**

  - O `GITHUB_TOKEN` usado no GitHub Actions é fornecido automaticamente e tem permissões limitadas.
  - Não é necessário adicionar tokens pessoais adicionais.

- **Proteção de Branch:**

  - Se você configurou proteções em branches, certifique-se de que o GitHub Actions tenha permissão para fazer push.

---

## 7. Resolução de Problemas Comuns

### Problema 1: **O Workflow do GitHub Actions Falha na Etapa de Build**

**Possíveis Causas e Soluções:**

- **Erro na Configuração do Jekyll:**

  - Verifique o arquivo `_config.yml` para erros de sintaxe.

- **Dependências Ausentes:**

  - Certifique-se de que todas as dependências necessárias estão listadas no `Gemfile`.

- **Versão Incompatível do Ruby:**

  - Ajuste `ruby-version` no workflow para uma versão compatível.

### Problema 2: **O Obsidian Git Não Está Fazendo Commit ou Push Automaticamente**

**Possíveis Causas e Soluções:**

- **Configurações de Intervalo Incorretas:**

  - Verifique se os intervalos de auto commit e auto push estão definidos corretamente.

- **Plugin Desativado:**

  - Certifique-se de que o plugin **Obsidian Git** está ativo.

- **Problemas de Autenticação:**

  - Se houver erros de autenticação, verifique as credenciais ou chaves SSH configuradas.

### Problema 3: **Conflitos de Merge Persistentes**

**Possíveis Causas e Soluções:**

- **Alterações Simultâneas no Repositório Remoto:**

  - Evite editar diretamente no GitHub se estiver usando o Obsidian Git para sincronização.

- **Resolução Automática de Conflitos Desativada:**

  - Ative a opção de resolução automática ou resolva os conflitos manualmente.

---

## 8. Conclusão

Ao configurar o **Obsidian Git** para realizar commits e push automáticos e o **GitHub Actions** para construir e implantar o site automaticamente, você criou um fluxo de trabalho contínuo que mantém seu site sempre atualizado com as últimas alterações feitas em suas notas no Obsidian. Isso economiza tempo e reduz a chance de erros humanos no processo de atualização.

---

## Anexos

### Links Úteis

- **Documentação do Obsidian Git:**

  - [Obsidian Git Plugin](https://github.com/denolehov/obsidian-git)

- **Documentação do GitHub Actions:**

  - [Introdução ao GitHub Actions](https://docs.github.com/pt/actions/learn-github-actions/understanding-github-actions)

- **Exemplo de Workflows:**

  - [GitHub Actions Workflows para Jekyll](https://github.com/marketplace/actions/jekyll-build-pages)

### Comandos Úteis

- **Forçar um Commit e Push Manual no Obsidian Git:**

  - Abra o **Command Palette** (`Ctrl + P` ou `Cmd + P`).
  - Digite **"Obsidian Git: Commit all changes"** e execute o comando.
  - Em seguida, execute **"Obsidian Git: Push"**.

- **Verificar o Status do Git Localmente (Opcional):**

  ```bash
  git status
  ```

- **Resolver Conflitos Manualmente (Opcional):**

  - Use o Git no terminal para identificar e resolver conflitos.

---

**Nota:** Lembre-se de que a automação é uma ferramenta poderosa, mas requer monitoramento ocasional para garantir que tudo esteja funcionando conforme o esperado. Mantenha-se atualizado com as melhores práticas e atualizações das ferramentas que você está usando.

---

**Fim do Documento**

