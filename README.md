# Agente de IA de Agendamentos por Voz e Texto

Agente de agendamento inteligente via Telegram integrado ao Google Calendar usando IA (Gemini) para processar voz e texto.

## 💻 Tecnologias principais:

- <b>n8n:</b> Ferramenta de automação de fluxo de trabalho que orquestra toda a lógica do agente.

- <b>Google Gemini:</b> Cérebro da operação. Utilizado tanto para transcrição de áudio (STT) quanto como LLM para interpretar intenções.

- <b>Telegram Bot API:</b> Interface de chat utilizada para interação com o usuário (envio de áudios e mensagens de texto).

- <b>Google Calendar API:</b> Ferramenta manipulada pelo agente para buscar, criar e gerenciar eventos na agenda.

- <b>JavaScript (ES6):</b> Utilizado em nós de "Code" do n8n para lógica condicional avançada e manipulação de objetos.

## 💡 Útil

<details>
  <summary>Sobre a Transcrição de Áudio</summary>

Este workflow utiliza o **Google Gemini** nativamente para processar arquivos de áudio enviados pelo Telegram. Não é necessário utilizar APIs externas de transcrição (como Whisper), pois o modelo Gemini Flash/Pro é multimodal.

</details>

## 📦 Como rodar o projeto?

Siga os passos abaixo para importar e configurar o workflow no seu n8n:

### 1. Clone o repositório

Baixe os arquivos para sua máquina local:

```bash
git clone https://github.com/GabrielLourencoh/n8n-smart-scheduler
```

### 2. Importe o Workflow no n8n

1. Abra seu editor do n8n.
2. No menu lateral ou na tela de workflows, clique em **"Import from File"**.
3. Selecione o arquivo `workflow.json` que está dentro da pasta clonada.

### 3. Configure as Credenciais

Para que o robô funcione, você precisará configurar as seguintes credenciais dentro do n8n. Os nós aparecerão com erro até que isso seja feito:

#### 🔑 Credenciais Necessárias:

- **Telegram API:** Crie um novo bot com o @BotFather no Telegram para obter o Token.
- **Google Gemini API:** Gere sua chave no Google AI Studio.
- **Google Calendar OAuth2:**
  - Crie um projeto no Google Cloud Console.
  - Habilite a API do Google Calendar.
  - Configure a tela de consentimento e as credenciais OAuth2.
  - **Escopos necessários:** `calendar` e `calendar.events`.

### 4. Ajuste as Variáveis de Memória (Opcional)

O workflow utiliza um nó de memória simples (Window Buffer). Se desejar alterar o tempo de retenção da conversa ou conectar a um banco de dados, altere o nó de memória conectado ao "AI Agent".

## 🚀 Funcionalidades do Agente

O robô é capaz de executar as seguintes ações no Google Calendar através de comandos de **Voz** ou **Texto**:

### 📅 Buscar Eventos

- "O que eu tenho hoje?"
- "Tenho algo marcado para quinta-feira?"

### ➕ Criar Eventos

- "Agende uma reunião com o time de marketing amanhã às 14h."
- "Marcar dentista dia 20 às 10 da manhã."

### ❌ Deletar Eventos

- "Cancele a reunião de marketing."
- "Desmarque meu compromisso das 10h."

## 📋 Estrutura do Workflow:

- **Telegram Trigger:** Ouve novas mensagens.
- **Router (If):** Separa mensagens de Voz de mensagens de Texto.
- **Gemini (Transcribe):** Converte áudio em texto se necessário.
- **AI Agent:** Cérebro central que decide qual ferramenta usar.
- **Tools:** Nós específicos para interagir com o Google Calendar.
