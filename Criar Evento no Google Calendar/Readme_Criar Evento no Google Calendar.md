
# 📌 Agendamento de Evento no Google Calendar

## 🎯 Objetivo
Este fluxo tem como finalidade **automatizar o agendamento de eventos no Google Calendar** a partir de mensagens recebidas em um chat.  
Ele interpreta as instruções do usuário, organiza as informações de data, hora, nome e serviço, e cria o evento diretamente na agenda configurada.

---

## 🏗 Estrutura do Fluxo

### 1. When chat message received
- **Função**: Nó inicial do fluxo.  
- **Responsabilidade**: Capturar a mensagem enviada pelo usuário no chat e iniciar a automação.

---

### 2. AI Agent
- **Função**: Interpretar a mensagem recebida.  
- **Prompt do campo systemMessage**:
  ```
  Você é um assistente pessoal especializado em agendamentos no Google Calendar.
  Hoje é: {{ $now }}
  ```
- Isso garante que o modelo tenha consciência da data atual e que interprete os comandos em linguagem natural (ex.: “agende amanhã às 15h”).

---

### 3. Create an event in Google Calendar
- **Função**: Criar efetivamente o evento no Google Calendar.  
- **Configuração**:
  - **Calendar**: Neste campo você deve informar o calendário onde será criado o evento.
  - **Start**:  
    ```
    {{$fromAI('data_hora_Inicio','Data e hora do inicio do agendamento. Exemplo: yyyy-MM-dd HH:mm:ss')}}
    ```
  - **End**:  
    ```
    {{$fromAI('data_hora_Fim','Data e hora do fim do agendamento. Exemplo: yyyy-MM-dd HH:mm:ss')}}
    ```
  - **Campos Adicionais**:
    - **Description**: Nome da pessoa (campo `Nome` vindo da IA).  
    - **Summary**: Serviço escolhido (campo `Servico` vindo da IA).

---

## 🚀 Fluxo de Execução
1. Usuário envia mensagem no chat (ex.: “Agende uma consulta com João amanhã às 10h para serviço X”).  
2. O **AI Agent** interpreta a instrução usando o modelo **GPT-4o-mini**.  
3. A memória no **Postgres** ajuda a manter dados já informados pelo usuário.  
4. O **AI Agent** envia os parâmetros estruturados para o nó **Create an event in Google Calendar**.  
5. O evento é criado automaticamente no calendário configurado.
