# stremio-cast

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/pedro-valentim/stremio-cast/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/pedro-valentim/stremio-cast/SKILL.md)
> Category: Browser & Automation

---

## Description

Busca conteúdo no Stremio Web e transmite para dispositivos Chromecast usando CATT e Playwright. Use para reproduzir filmes e séries diretamente do Stremio em TVs.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Busca conteúdo no Stremio Web e transmite para dispositivos Chromecast usando CATT e Playwright. Use para reproduzir filmes e séries diretamente do Stremio em TVs.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run stremio-cast`)
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
You are executing the stremio-cast workflow. Use the following context:

Description: Busca conteúdo no Stremio Web e transmite para dispositivos Chromecast usando CATT e Playwright. Use para reproduzir filmes e séries diretamente do Stremio em TVs.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: stremio-cast
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Stremio Cast

Esta skill permite que o Manus automatize a interface web do Stremio para encontrar links de streaming locais e transmiti-los para um dispositivo Chromecast.

## Pré-requisitos

Para que esta skill funcione corretamente, o ambiente deve ter:
1. **Stremio Service** rodando localmente na porta `11470`.
2. **Playwright** instalado para automação do navegador.
3. **CATT (Cast All The Things)** instalado via pip para o casting.

## Fluxo de Trabalho

A skill executa os seguintes passos:
1. Abre a interface web do Stremio (`app.strem.io`).
2. Realiza a busca pelo título solicitado.
3. Seleciona o primeiro resultado e o melhor link de stream disponível.
4. Intercepta a URL do stream gerada pelo servidor local do Stremio (`127.0.0.1:11470`).
5. Envia essa URL para o dispositivo Chromecast especificado usando a ferramenta `catt`.

## Uso

A skill deve ser invocada quando o usuário pedir para "tocar [filme/série] no Chromecast" ou "assistir [título] na TV".

### Parâmetros
- `query`: O nome do filme ou série a ser buscado.
- `device`: (Opcional) O nome do dispositivo Chromecast. Padrão: "Living Room".

### Exemplo de Comando
```bash
python3 scripts/stremio_cast.py "The Matrix" "Quarto"
```

## Notas Importantes
- **Manutenção de Sessão**: O servidor de streaming do Stremio pode exigir que a aba do navegador permaneça aberta para continuar o download do torrent. O script fecha o navegador após iniciar o cast, mas isso pode ser ajustado se o stream cair prematuramente.
- **Seletores CSS**: Os seletores da interface web do Stremio podem mudar. Caso a skill falhe ao clicar em elementos, verifique se os seletores em `scripts/stremio_cast.py` ainda são válidos.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
