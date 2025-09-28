# 📄 Envio de Mensagens Sequenciais com Intervalo Aleatório

## 🎯 Objetivo  
Este fluxo no **n8n** tem como finalidade enviar uma sequência de mensagens para um número de WhatsApp usando a **Evolution API**, garantindo um **intervalo aleatório entre cada envio** (entre **2 e 5 segundos**).  

---

## 🧩 Estrutura do Fluxo  

1. **Start (Manual Trigger)**  
   - Inicia o fluxo manualmente.  
   - Usado apenas para testes ou disparo manual.  

2. **Mensagens para envio (Set Node)**  
   - Define as mensagens que serão enviadas.  
   - Exemplo:  
     - `msg_1`: "Oi, tudo bem? 👋"  
     - `msg_2`: "Eu sou a Fulano, da empresa XPT 🤓✨"  
     - `msg_3`: "Como nós podemos te ajudar hoje ?"  
   - ⚡ Você pode alterar os valores aqui para personalizar.  

3. **Sequência de Mensagens (Code Node)**  
   - Código em JavaScript transforma as mensagens do Set Node em lista de itens para envio individual:  

   ```js
   const mensagens = [
     $input.first().json.msg_1,
     $input.first().json.msg_2, 
     $input.first().json.msg_3
   ];

   return mensagens.map(m => ({ json: { texto: m } }));
   ```

4. **Loop Over Items (SplitInBatches)**  
   - Controla o envio **uma mensagem por vez**.  
   - Após o envio de uma mensagem, o fluxo retorna para enviar a próxima.  

5. **Espera entre mensagens (Wait Node)**  
   - Adiciona um intervalo **aleatório entre 2 e 5 segundos**.  
   - Fórmula:  

   ```js
   {{ Math.floor(Math.random() * (5 - 2 + 1)) + 2 }}
   ```

6. **Envio de msg (Evolution API Node)**  
   - Envia a mensagem pelo WhatsApp via Evolution API.  
   - Campos importantes:  
     - `instanceName`: Nome da instância configurada.  
     - `remoteJid`: Telefone do destinatário (formato `5511999999999@s.whatsapp.net`).  
     - `messageText`: `={{ $json.texto }}`.  
     - `options_message.delay`: `1200` (delay adicional de 1,2s).  

7. **Fim do ciclo (NoOp)**  
   - Fecha o ciclo e retorna para o loop até acabar.  

8. **Sticky Notes**  
   - Notas explicando onde inserir mensagens e sobre o intervalo aleatório.  

---

## 🔄 Fluxo resumido  
1. Start →  
2. Set mensagens →  
3. Code →  
4. Loop →  
5. Wait →  
6. Envio Evolution API →  
7. Loop continua →  
8. Fim.  

---

## ✅ Pontos de atenção  
- Substitua **telefone** e **instância** pelos valores reais da Evolution API.  
- O delay **não é fixo**, varia a cada envio.  
- Ideal para evitar bloqueios por **envios em massa no WhatsApp**.  
