# Customizacoes Backend

## Registro de Mudancas

---

### 2026-03-05 - Ajuste de fluxo da descoberta no prompt DESC01

**Escopo:** Regra de negocio do fluxo de descoberta (governanca de prompts e consolidacao de saida)
**Arquivos alterados:**
- `C:/Users/wfrancischini/Desktop/PROJETOS/__START__/00 - DESCOBERTA(AI Web)/DESC01 - Historia.md` - Ajustadas instrucoes para explicitar a sequencia completa DESC01-DESC04, restringir consolidacao final do JSON ao DESC04 e condicionar escopo/meta-prompts ao fluxo completo.

**O que foi feito:**
Foi atualizado o prompt `DESC01 - Historia` para deixar explicito que a fase de descoberta e composta por 4 prompts encadeados (`DESC01`, `DESC02`, `DESC03`, `DESC04`). A orientacao de consolidacao final em JSON foi delimitada para ocorrer apenas no `DESC04`, evitando fechamento prematuro quando o usuario envia somente o primeiro prompt. Tambem foi reforcado que a producao de escopo e meta-prompts depende da conclusao desse fluxo completo.

**Endpoints afetados:**
| Metodo | Rota | Acao |
|--------|------|------|
| N/A | N/A | N/A |

**Mudancas no banco:**
| Tabela | Campo | Tipo | Acao |
|--------|-------|------|------|
| N/A | N/A | N/A | N/A |

**Regras de negocio:**
- A descoberta deve ser tratada como fluxo sequencial de 4 etapas (DESC01-DESC04), sem inferir conclusao com base apenas no primeiro prompt.
- O JSON consolidado final deve ser emitido apenas no `DESC04`.
- Escopo e meta-prompts so podem ser derivados apos a finalizacao do fluxo completo de descoberta.

**Migrations:** N/A

**Impacto em outros modulos:** Melhora alinhamento operacional entre descoberta, escopo e geracao de meta-prompts; reduz perguntas fora de contexto e conclusoes antecipadas.

**Motivo:** Evitar conclusoes antecipadas e perguntas fora de contexto quando o usuario envia apenas o primeiro prompt da descoberta.

**Dependencias:** N/A

---

### 2026-03-05 - Reuso de contexto por alias nos prompts DESC02-DESC04

**Escopo:** Processo de descoberta (protocolo de contexto compartilhado no mesmo chat)
**Arquivos alterados:**
- `C:/Users/wfrancischini/Desktop/PROJETOS/__START__/00 - DESCOBERTA(AI Web)/DESC02 - Criticas.md` - Incluido protocolo para consumir `CONTEXTO_DESC01` e produzir/usar `JSON_DESC02` sem recolar o texto completo.
- `C:/Users/wfrancischini/Desktop/PROJETOS/__START__/00 - DESCOBERTA(AI Web)/DESC03 - Contextuais.md` - Ajustado para operar com alias de contexto e encadear resultado intermediario sem repeticao manual de blocos longos.
- `C:/Users/wfrancischini/Desktop/PROJETOS/__START__/00 - DESCOBERTA(AI Web)/DESC04 - Conflitos-e-Roadmap.md` - Atualizado para consolidar usando `JSON_DESCOBERTA_COMPLETO`, reaproveitando saidas anteriores na mesma conversa.

**O que foi feito:**
Foi aplicada uma mudanca de processo nos prompts de descoberta para habilitar a opcao 1 de uso no mesmo chat com reaproveitamento de contexto por alias. Os prompts `DESC02`, `DESC03` e `DESC04` passaram a incluir blocos de protocolo que referenciam `CONTEXTO_DESC01`, `JSON_DESC02` e `JSON_DESCOBERTA_COMPLETO`, reduzindo necessidade de copiar/colar conteudo extenso entre etapas. A decisao prioriza continuidade conversacional e previsibilidade do fluxo sem alterar o objetivo funcional da descoberta.

**Endpoints afetados:**
| Metodo | Rota | Acao |
|--------|------|------|
| N/A | N/A | N/A |

**Mudancas no banco:**
| Tabela | Campo | Tipo | Acao |
|--------|-------|------|------|
| N/A | N/A | N/A | N/A |

**Regras de negocio:**
- O fluxo de descoberta pode reaproveitar contexto anterior por aliases padronizados no mesmo chat, sem exigir republicacao integral do historico.
- A transicao entre `DESC02`, `DESC03` e `DESC04` deve preservar artefatos intermediarios (`JSON_DESC02` e `JSON_DESCOBERTA_COMPLETO`) como referencia oficial de continuidade.
- A consolidacao final permanece no `DESC04`, mas agora com menor atrito operacional por depender de referencias curtas em vez de blocos longos.

**Migrations:** N/A

**Impacto em outros modulos:** Reduz friccao operacional no fluxo de descoberta e melhora foco durante a execucao sequencial das etapas; nao afeta API, banco ou runtime da aplicacao.

**Motivo:** Reduzir atrito operacional e evitar perda de foco causada por copiar/colar contexto longo a cada etapa da descoberta.

**Dependencias:** N/A

---
