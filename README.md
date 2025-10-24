# Meu App de Treino Pessoal (Demonstração) 🏋️‍♂️

Um aplicativo web demonstrativo para acompanhar rotinas de treino e progresso de cargas. Ele utiliza perfis pré-definidos (hardcoded) para simplificar o acesso e armazena os dados dos treinos no Firebase Firestore. É também um Progressive Web App (PWA) instalável com funcionalidade offline básica.

**⚠️ Atenção:** Este repositório é para fins demonstrativos. As credenciais do Firebase foram removidas/substituídas por placeholders. Para rodar este projeto, você precisará criar seu próprio projeto Firebase e inserir suas credenciais.

## ✨ Funcionalidades Atuais

* **Seleção de Perfil Simples:** Alterna facilmente entre perfis pré-definidos (ex: Diogo, Tiago) usando a barra lateral.
* **Persistência de Sessão:** Lembra o último perfil selecionado usando o `localStorage` do navegador.
* **Dados de Perfil (Hardcoded):** Exibe metas de macronutrientes específicas para o perfil selecionado, definidas diretamente no código.
* **Link para Planilha Pessoal:** Mostra um link configurado no código para a planilha do perfil ativo.
* **Rotinas de Treino (Firestore):** Carrega e exibe diferentes rotinas (ABC, ABCD, Hipertrofia) a partir de uma base de dados Firebase Firestore.
* **Acompanhamento de Carga Individual:** Permite visualizar e editar a carga de cada exercício **separadamente para cada perfil pré-definido**.
* **Salvamento no Firestore:** Salva as cargas atualizadas no Firebase Firestore, associadas ao perfil correto.
* **Cronômetro Persistente:** Inclui um cronômetro que permanece visível e ativo mesmo ao trocar entre as abas de treino.
* **Checkboxes Visuais:** Checkboxes ao lado de cada exercício para acompanhamento visual durante o treino (não salva o estado).
* **Resetar Marcações:** Botão em cada treino para desmarcar todos os checkboxes da seção.
* **Frase Motivacional:** Exibe uma frase motivacional dinâmica na aba de perfil.
* **Progressive Web App (PWA):** Configurável para ser instalado na tela inicial e funcionar offline (cache dos arquivos principais).
* **Layout Moderno:** Interface com tema escuro, navegação por sidebar e tipografia aprimorada.

## 🖼️ Visualização

Aqui estão algumas telas do aplicativo em funcionamento:



**Tela Principal (Perfil e Cronômetro):**
<br> 
<img src="https://i.postimg.cc/5yW0zXXH/Gemini-Generated-Image-wcbh5wcbh5wcbh5w-1.png" alt="Tela Principal do App - Perfil" width="150">
<img src="https://i.postimg.cc/TwJsGSvq/11.jpg" alt="Tela Principal do App - Perfil" width="150">
<img src="https://i.postimg.cc/0Q04x31Y/12.jpg" alt="Tela Principal do App - Perfil" width="150">
<img src="https://i.postimg.cc/mDynRqWy/13.jpg" alt="Tela Principal do App - Perfil" width="150">
<img src="https://i.postimg.cc/J4yJZkYc/1111.png" alt="Tela Principal do App - Treino" width="200">
<img src="https://i.postimg.cc/28PWwSg9/222222.png" alt="Tela Principal do App - Outra Visão" width="200">



## 💻 Tecnologias Utilizadas

* HTML5
* CSS3
* JavaScript (Vanilla JS)
* Firebase Firestore (SDK v8 Compat) - **Apenas para dados de treino**
* Node.js - **Apenas para rodar o script `setup.js`**.

## 🚀 Como Rodar Localmente (Usando Seu Próprio Firebase)

Siga estes passos para configurar e rodar o projeto na sua máquina com sua própria base de dados.

### Pré-requisitos

* **Node.js:** Necessário para rodar o script `setup.js`. Baixe em [nodejs.org](https://nodejs.org/).
* **Web Server Local:** Recomendado para testar funcionalidades PWA. A extensão "Live Server" no VS Code é uma boa opção.

### Configuração

1.  **Clone o Repositório:**
    ```bash
    git clone [https://github.com/seu-usuario-publico/seu-repositorio-publico.git](https://github.com/seu-usuario-publico/seu-repositorio-publico.git) # Substitua pela URL deste repo
    cd seu-repositorio-publico
    ```

2.  **Crie seu Próprio Projeto Firebase:**
    * Vá ao [Console do Firebase](https://console.firebase.google.com/) e crie um novo projeto.
    * No seu projeto, vá em **Build > Firestore Database** e crie um banco de dados (iniciar em **modo de produção**).
    * **Configure as Regras de Segurança:** Vá na aba "Regras" do Firestore e cole as seguintes regras (adequadas para teste, mas inseguras para produção sem autenticação):
        ```javascript
        rules_version = '2';
        service cloud.firestore {
          match /databases/{database}/documents {
            // Permite leitura e escrita na coleção 'treinos' e subcoleções
            match /treinos/{document=**} {
              allow read, write: if true;
            }
            // Bloqueia acesso a outras coleções (recomendado)
             match /{path=**} {
               allow read, write: if false;
            }
          }
        }
        ```
        Clique em "Publicar".
    * Vá para as **Configurações do Projeto** (ícone de engrenagem) e, na aba "Geral", crie um **App da Web**.
    * **Copie o objeto de configuração `firebaseConfig`** exibido.

3.  **Insira Suas Credenciais do Firebase:**
    * Abra os arquivos `main.js` e `setup.js` no seu editor.
    * Localize a constante `firebaseConfig` no topo de cada um (ela conterá placeholders como "SUA_API_KEY_AQUI").
    * **Substitua** o objeto placeholder pelo **SEU PRÓPRIO** `firebaseConfig` que você copiou do seu projeto Firebase.

4.  **Popule o Banco de Dados com os Treinos:**
    * Abra um terminal na pasta do projeto.
    * Instale a dependência do Firebase para o script Node.js:
        ```bash
        npm install firebase
        ```
    * Execute o script para cadastrar os treinos e a estrutura `cargaPorPerfil` no SEU Firebase:
        ```bash
        node setup.js
        ```
    * Verifique no seu Console do Firebase se a coleção `treinos` foi criada com os exercícios e a estrutura correta.

### Rodando o App

1.  Abra a pasta do projeto no VS Code.
2.  Clique com o botão direito no arquivo `index.html` e selecione "Open with Live Server".
3.  Seu navegador abrirá o aplicativo. Use a sidebar para selecionar "Diogo" ou "Tiago".

## ⚠️ Aviso Importante Sobre as Credenciais do Firebase ⚠️

As credenciais (`firebaseConfig`) nos arquivos `main.js` e `setup.js` **neste repositório público são apenas placeholders**. Elas **NÃO** darão acesso a nenhuma base de dados funcional.

Para que o aplicativo funcione, você **OBRIGATORIAMENTE** precisa:
1.  Criar seu **próprio projeto gratuito** no Firebase.
2.  Configurar o **Firestore Database** e suas **Regras de Segurança**.
3.  **Substituir** os placeholders `firebaseConfig` nos arquivos `.js` pelas **credenciais do SEU projeto**.

Isso garante que você possa rodar e modificar o aplicativo usando sua própria base de dados isolada.

---
## 📄 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.
