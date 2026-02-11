# lista-sms

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/david-evaristo/lista-sms/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/david-evaristo/lista-sms/SKILL.md)
> Category: Communication

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run lista-sms`)
**Workflow:** Execute skill logic with context from AiDarr's ATLAS memory

### T - Tools
Required tools (add as needed):
- HTTP requests (for API calls)
- Memory system (ATLAS for persistence)
- Context retrieval (from GOTCHA workspace)

### C - Context
Required context sources:
- User preferences from ATLAS memory
- Relevant documents from workspace
- Historical execution data

### H - Hard Prompts

```prompt
You are executing the lista-sms workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: lista-sms
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

name: lista-sms
description: Recupera, filtra e formata automaticamente mensagens SMS não lidas do dispositivo conectado.

--- # SKILL: Lista SMS ## 📋 Descrição A skill `lista_sms` permite que o sistema acesse a caixa de entrada do dispositivo para identificar mensagens que ainda não foram visualizadas. Ela utiliza um script Python para realizar a ponte entre a interface de comando e o banco de dados de mensagens do dispositivo, retornando o remetente, o conteúdo e o horário da mensagem de forma estruturada. **Dispositivos Suportados:** * Smartphones Android (via interface de depuração ou API de sistema). * Módulos GSM compatíveis com comandos AT. --- ## 🚀 Como Usar ### Linguagem Natural Você pode ativar esta skill com comandos simples, como: * "Quais são as minhas novas mensagens?" * "Liste meus SMS não lidos." * "Tenho algum SMS novo?" ### Integração Técnica Para executar a funcionalidade diretamente via código, utilize o módulo principal: --- ## ⚙️ Instruções para o Agente **IMPORTANTE:** Ao executar esta skill, o agente deve: 1. **Mostrar o retorno do código**: Exibir na conversa toda a saída gerada pelo script, incluindo: - A contagem de mensagens por SIM (ex: "SIM 1: 5 mensagens") - A confirmação de salvamento do arquivo CSV (ex: "Arquivo CSV salvo: sms_list_2026-02-03.csv") 2. **Enviar o arquivo CSV gerado**: O script gera automaticamente um arquivo CSV com o formato `sms_list_YYYYMMDD-HHMMSS.csv` contendo todas as mensagens SMS não lidas. O agente deve **ENVIAR O ARQUIVO COMPLETO** na conversa, não apenas listar ou exibir os registros. O arquivo deve ser anexado/enviado como arquivo na resposta. 3. **Local Arquivo**: O script vai salvar o arquivo em /home/evaristo/.openclaw/skills/lista_sms/sms_list_YYYYMMDD-HHMMSS.csv. - Envie o arquivo na conversa **Nota:** O arquivo CSV contém as colunas: SIM, Operadora, Número, Data e Mensagem.
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
