
# Lembrete de Aniversários Automatizado com N8N

Este projeto tem como objetivo coletar informações de contatos (clientes, amigos, familiares, etc.) e enviar lembretes automáticos de aniversário via WhatsApp, utilizando **N8N** integrado ao **Google Sheets** e **Evolution API**.

---

## 📌 Estrutura do Projeto

O projeto é dividido em dois fluxos principais:

### 1. Salva Datas de Aniversário
- Coleta dados via formulário (Nome, Data de Nascimento e Telefone).
- Normaliza e formata as informações:
  - Converte a data de nascimento para o padrão brasileiro (`dd/mm/yyyy`).
  - Extrai apenas dia/mês para facilitar a verificação de aniversariantes do dia.
  - Formata telefone no padrão internacional (`+55`).
- Salva os dados em uma planilha do Google Sheets.

### 2. Verifica Aniversariante do Dia
- Executa automaticamente todos os dias em horário definido (exemplo: 16h).
- Busca os aniversários na planilha e compara com a data atual.
- Caso encontre aniversariantes:
  - Dispara mensagem personalizada via Evolution API (WhatsApp).
  - Atualiza o status na planilha como `"Enviado"`.
- Inclui espera de 5 segundos entre os envios dos lembretes.

---

## 🚀 Como Usar

1. Configurar planilha no Google Sheets com colunas:
   - Nome
   - Telefone
   - Data de Nasc.
   - Aniversário
   - Status
   - Data de Cadastro
   - formMode

2. Importar os fluxos no N8N:
   - `Salva Datas de Aniversario.json`
   - `Verifica Aniversariante do Dia.json`

3. Conectar credenciais no N8N:
   - Conta do Google Sheets
   - Evolution API

4. Publicar o formulário para coleta dos dados.

5. O sistema irá automaticamente:
   - Registrar aniversários
   - Verificar aniversariantes do dia
   - Enviar mensagens personalizadas
