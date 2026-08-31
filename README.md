# Meu Caderno de Receitas

Site estático para GitHub Pages (sem build e sem backend) com cadastro de receitas, estoque, lista de compras, backup local e sincronização opcional com Google Drive (`appDataFolder`).

## Publicação no GitHub Pages

1. Acesse o repositório no GitHub.
2. Vá em **Settings > Pages**.
3. Em **Build and deployment**, selecione:
   - **Source**: `Deploy from a branch`
   - **Branch**: `main`
   - **Folder**: `/(root)`
4. Salve e aguarde a publicação.
5. O site ficará disponível em: `https://alanassantos.github.io/meu-caderno-de-receitas/`.

## Configuração Google (login + Drive)

A aplicação usa Google Identity Services + Google Drive API para salvar 1 arquivo JSON no `appDataFolder`.

### 1) Ativar Google Drive API

No **Google Cloud Console**, selecione o projeto e ative a **Google Drive API**.

### 2) Configurar tela de consentimento OAuth

Configure a tela de consentimento OAuth no projeto.

> Se o app estiver em status **Testing**, o e-mail da usuária deve estar em **Test users**.

### 3) Configurar OAuth Client ID (Web)

No OAuth Client ID (tipo Web), adicione em **Authorized JavaScript origins**:

- `https://alanassantos.github.io`

A aplicação usa este Client ID público no frontend:

- `95231707243-bbe1s6rtllmnd1pb263839jkbg1dqnb6.apps.googleusercontent.com`

Escopo solicitado (somente este):

- `https://www.googleapis.com/auth/drive.appdata`

## Segurança

- O **Client ID pode ser público**.
- **Nunca** publique Client Secret.
- **Nunca** publique token fixo.

## Regra de versão de backup

A sincronização usa o campo `updatedAt`:

- A versão mais recente (maior `updatedAt`) é considerada a fonte da verdade.
- Se o backup remoto estiver mais recente que o local, o app pede confirmação antes de restaurar automaticamente.

## Importação em lote de links

A importação em lote aceita um link por linha e apenas:

- identifica a plataforma (TikTok/Instagram/Pinterest/YouTube/outro)
- cria rascunhos editáveis

Não há scraping automático de vídeos/posts nesta versão.
