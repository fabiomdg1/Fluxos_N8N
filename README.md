# 📂 Repositório de Fluxos n8n

Bem-vindo ao repositório de **workflows para n8n**!  
Aqui você encontrará automações e documentadas para facilitar a integração.

---

## 🧩 O que é o n8n?
O [n8n](https://n8n.io) é uma plataforma de automação open-source que permite conectar serviços, criar integrações e automatizar processos sem precisar programar do zero.  
Com ele, você pode criar fluxos visuais que conectam desde bancos de dados até APIs de IA, WhatsApp, CRMs e muito mais.  

---

## 📜 Estrutura do repositório
- Cada fluxo é disponibilizado em formato **`.json`**, pronto para ser importado no n8n.  
- Dentro da pasta `workflows/`, cada automação terá:
  - Arquivo `.json` com o fluxo.  
  - Documentação explicando a lógica e como configurar.  

Exemplo de organização:
```
├── workflows/
│   ├── envio-mensagens-aleatorias.json
│   ├── chatbot-whatsapp-ia.json
│   ├── integracao-google-sheets.json
└── README.md
```

---

## 🚀 Como usar os fluxos
1. Clone ou baixe este repositório:
   ```bash
   git clone https://github.com/seu-usuario/seu-repo.git
   ```
2. Acesse sua instância do **n8n**.  
3. Clique em **Import → From File**.  
4. Escolha o arquivo `.json` do fluxo desejado.  
5. Configure as credenciais necessárias (ex.: Evolution API, OpenAI, Google, etc.).  
6. Salve e execute! 🎉  

---

## 🤝 Contribuindo
Sinta-se à vontade para abrir **issues** ou enviar **pull requests** com melhorias, novos fluxos e correções.  

---

## 📄 Licença
Este repositório está sob a licença MIT.