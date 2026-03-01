# Implantacao do Projeto __START__

Projeto: Framework de Descoberta + Escopo + Meta-Prompts para desenvolvimento com IA.

---

## Historico de Mudancas no Framework

### 2026-02-14 - MP05 com autonomia e faseamento automatico

**Arquivo alterado:**
- `2 - META PROMPT/MP05 - Micro-Prompts.md`

**O que foi feito:**
- Removida a pergunta inicial "quantas fases?" para o usuario.
- A IA Web agora analisa o `@escopo.md` e define a divisao em fases/sub-fases automaticamente.
- Adicionada regra de autonomia: so perguntar ao usuario se houver ambiguidade real que impeça continuar.
- Definido limite de 4-6 prompts por sub-fase para evitar artifacts muito grandes.
- Incluida orientacao para ignorar itens de roadmap/futuro sem detalhamento suficiente.
- A IA deve exibir o plano de fases identificado e, em seguida, gerar imediatamente o artifact da Fase 1 (sem esperar confirmacao).
- Atualizada a secao "COMO USAR" para refletir o novo fluxo sem pergunta manual de fases.

**Motivo:** Reduzir friccao no uso da MP05, evitar perguntas desnecessarias e diminuir risco de decisoes por "achismo" quando a informacao ja existe no escopo.

### 2026-03-01 - [MODO CURSOR] em MP01 a MP04

**Arquivos alterados:**
- `2 - META PROMPT/MP01 - Estrutura-de-Pastas.md`
- `2 - META PROMPT/MP02 - Configuracoes.md`
- `2 - META PROMPT/MP03 - Documentacao.md`
- `2 - META PROMPT/MP04 - Estrutura-de-Codigo.md`

**O que foi feito:**
Adicionado bloco [MODO CURSOR] em todos os MPs (exceto MP05 que ja tinha) para orientar o usuario a colar o artifact no modo AGENT (execucao direta) ou AGENT com PLAN. MP01 e MP03 tem modo fixo (sempre AGENT direto). MP02 e MP04 tem logica de julgamento pela IA Web: avalia complexidade/número de arquivos e escolhe entre os dois modos.

**Regras de julgamento (MP02):**
- AGENT direta: ate 8 arquivos, sem deps nativas
- AGENT com PLAN: 9+ arquivos, deps nativas, configs complexas

**Regras de julgamento (MP04):**
- AGENT direta: ate 15 arquivos
- AGENT com PLAN: 16+ arquivos

**Motivo:** Padronizar com MP05 e dar orientacao clara sobre modo Cursor em todos os artifacts.

### 2026-02-27 - Validacao Git e Proximo Fluxo da Fase 00

**Arquivos alterados:**
- `docs/01-implantacao.md`

**O que foi feito:**
Registrada a validacao de sincronizacao entre Git local e remoto e formalizada a decisao operacional da fase 00 de descoberta. Nao houve alteracao de codigo-fonte; esta entrada documenta exclusivamente verificacao e decisao de processo para manter rastreabilidade da sessao.

**Pontos-chave:**
- Verificacao Git: repositorio local e remoto validados como atualizados/sincronizados.
- Fluxo correto apos DESC02: executar `DESC03` e, na sequencia, seguir para `DESC04`.
- Insumos necessarios para DESC03: saidas de `DESC01` e o JSON gerado em `DESC02`.

**Motivo:** Registrar decisao operacional do framework e garantir rastreabilidade desta sessao sem impacto em implementacao de codigo.

### 2026-03-01 - MP05 padronizado para Copy no Claude Web e selecao de modo

**Arquivos alterados:**
- `C:/Users/wfrancischini/Desktop/PROJETOS/__START__/2 - META PROMPT/MP05 - Micro-Prompts.md`

**O que foi feito:**
O `MP05 - Micro-Prompts` foi atualizado para exigir que cada prompt do artifact fique dentro de bloco de codigo com triple backticks, incluindo separadores visuais `━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━`, para habilitar o botao nativo `Copy` no Claude Web e reduzir erros de copia parcial. Tambem foi inserido o campo `[MODO CURSOR]` antes de `[PRE-REQUISITOS]` com dois formatos de uso: `🔵 AGENT direto` (execucao direta) e `🟡 AGENT com PLAN` (revisao antes de executar).

**Regras e estrutura atualizadas:**
- Ajustada a regra de escolha entre modos (`AGENT direto` vs `AGENT com PLAN`) no proprio prompt.
- Atualizada a estrutura do artifact para manter o formato copiavel de ponta a ponta.
- Revisado o exemplo de prompt e o checklist de qualidade para refletir o novo padrao de renderizacao/copia.
- Atualizado o Passo 7 de **COMO USAR** para orientar uso do botao `Copy`.

**Dependencias:** N/A

**Commit de referencia:** `e112232`

**Motivo:** Melhorar a experiencia de uso no Claude Web, aumentar confiabilidade da copia dos micro-prompts e tornar explicito o fluxo de execucao por modo no Cursor.

### 2026-03-01 - MP05 com resiliencia de first-run e validacao de runtime

**Arquivos alterados:**
- `C:/Users/wfrancischini/Desktop/PROJETOS/__START__/2 - META PROMPT/MP05 - Micro-Prompts.md`

**O que foi feito:**
Foi fortalecida a orientacao do `MP05 - Micro-Prompts` para reduzir falhas no primeiro ciclo de execucao e aumentar previsibilidade operacional em ambiente local com Docker. Em **REGRAS PARA O CONTEUDO DOS PROMPTS**, foram adicionadas: (1) regra de resiliencia de configuracao no first-run cobrindo `env` ausente, invalida e valida, com fallback em DEV e fail-fast em PROD; e (2) regra anti-friccao para portas Docker locais, evitando assumir porta host livre e orientando variavel de porta host com fallback. Em **INSTRUCOES DE VALIDACAO PARA A IA**, foram adicionadas validacoes de runtime (smoke test de inicializacao real, health/readiness de servicos via Docker Compose e checagem de logs de startup), alem de dois novos itens no checklist automatico: app inicializou sem crash e servicos saudaveis. No **CHECKLIST DE QUALIDADE**, foram incluidos criterios para validar `env` em 3 estados, diferenciar comportamento DEV vs PROD, executar smoke test runtime, validar startup do Docker Compose e evitar crash por placeholders de `.env.example`.

**Dependencias:** N/A

**Motivo:** O primeiro micro-prompt falhou por tratar apenas `env` vazia e nao cobrir `env` invalida; a atualizacao torna a geracao/validacao mais robusta, reduz falhas de runtime no first-run e diminui friccao recorrente com portas locais em uso.
