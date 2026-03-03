# 05 - MICRO-PROMPTS (CLAUDE CODE)

## Governanca

- Base: `MP05 - Micro-Prompts.md` (snapshot de referencia: 2026-03-03)
- Politica de sincronizacao: sempre que a MP05 original mudar (regras, validacoes, resiliencia, criterios), revisar e sincronizar manualmente esta versao antes de novo uso em producao.
- Escopo desta versao: manter o core tecnico da MP05 original e adaptar somente o contrato de saida/execucao para Claude Code.

---

## Como usar

1. Abra Claude Code (via extensao no Cursor ou terminal do Cursor).
2. Anexe `@escopo.md`.
3. Cole o prompt completo desta MP05-ClaudeCode.
4. A IA analisa o escopo, define fases e gera apenas `fase_01.md`.
5. Execute a fase 1 no Claude Code em modo autonomo, com checkpoints por subtarefa.
6. Ao concluir, peca `fase_02.md`, e assim por diante.

Regra operacional:
- Nao gerar todas as fases de uma vez.
- Nao ultrapassar o limite de contexto definido no bloco de controle.
- Se aproximar do limite, parar e gerar handoff estruturado.

---

```md
PASSO 1: ANALISAR FASES AUTOMATICAMENTE

REGRA DE AUTONOMIA:
Nao pergunte ao usuario a menos que exista ambiguidade REAL no escopo.md que impeca prosseguir (ex: secoes contraditorias, feature citada sem nenhum detalhamento). Se a informacao estiver no escopo, use-a e decida.

Analise o @escopo.md e determine a divisao em fases:

1. Leia a secao "Funcionalidades" (ou equivalente).
2. Identifique TODAS as features listadas.
3. Agrupe em sub-fases logicas:
   - Fase 1: Setup/Infra (banco, auth, config base, libs compartilhadas)
   - Fase 2: Core/Backend (models, APIs, logica de negocio)
   - Fase 3: Frontend (paginas, componentes, formularios)
   - Fase 4: Integracoes/Polish (APIs externas, otimizacoes, ajustes finais)
4. Se o escopo tiver apenas 1 fase (MVP), subdivida conforme acima.
5. Se o escopo ja trouxer fases, respeite a divisao e aplique sub-divisao interna quando necessario.
6. Cada sub-fase deve ter no maximo 4-6 subtarefas.
7. Features de roadmap/futuro sem detalhamento completo devem ser IGNORADAS.

Apresente o plano antes de gerar fase:

PLANO DE FASES IDENTIFICADO:
- Fase 1: [nome] ([N] subtarefas) - [resumo]
- Fase 2: [nome] ([N] subtarefas) - [resumo]
- ...
Total: [X] fases, [Y] subtarefas

[Se houver:]
IGNORADAS (sem detalhamento suficiente): [lista]

Depois do plano, gere IMEDIATAMENTE o arquivo `fase_01.md`.
Nao espere confirmacao para gerar a primeira fase.

PASSO 2: GERAR APENAS UMA FASE POR VEZ

Gere APENAS os detalhes da primeira fase em `fase_01.md`.
As proximas fases so devem ser geradas quando solicitadas.

PASSO 3: ESTRUTURA OBRIGATORIA DE CADA fase_X.md

Cada `fase_X.md` DEVE comecar com este BLOCO DE CONTROLE:

## BLOCO_DE_CONTROLE_DE_EXECUCAO
- MODO_EXECUCAO: batch | step-by-step
- NIVEL_COMPLEXIDADE: baixo | medio | alto
- LIMITE_CONTEXTO: parar ao atingir 55-60% e emitir handoff
- POLITICA_HANDOFF:
  - registrar progresso por subtarefa
  - listar arquivos alterados
  - listar testes executados e status
  - listar pendencias/riscos
  - sugerir proximo passo exato
- SAIDA_OBRIGATORIA:
  - resumo executivo da fase
  - arquivos criados/modificados
  - comandos executados
  - validacoes automaticas
  - pendencias e proximos passos

Depois do bloco de controle, o `fase_X.md` DEVE conter:

## OBJETIVO_DA_FASE
## ESCOPO_IN
## ESCOPO_OUT
## DEPENDENCIAS
## SUBTAREFAS_SEQUENCIAIS
## ARQUIVOS_ALVO
## REGRAS_DE_NEGOCIO
## NAO_IMPLEMENTE
## TESTES_AUTOMATIZADOS_OBRIGATORIOS
## VALIDACAO_MANUAL_OPCIONAL
## CRITERIO_DE_CONCLUSAO
## FORMATO_DE_HANDOFF

PASSO 4: CONTEUDO OBRIGATORIO DAS SUBTAREFAS

Cada subtarefa deve ser auto-contida e incluir:

[PRE-REQUISITOS]
- Dependencias de subtarefas anteriores
- Arquivos/rotas/tabelas que precisam existir

[COMANDOS_DE_INSTALACAO]
- Apenas se necessario
- Se ja executado antes, explicitar que pode ser ignorado

[CONTEXTO]
- 1-2 frases com objetivo tecnico da subtarefa

[IMPLEMENTACAO]
- Arquivos com caminho completo
- O que criar/modificar
- Interfaces, tipos, funcoes, formulas e validacoes

[ARQUIVOS_ENVOLVIDOS]
- Criar
- Modificar
- Reutilizar (ja existentes)

[REGRAS_DE_NEGOCIO]
- Regras explicitas
- Formulas completas
- Validacoes com condicao e erro esperado

[NAO_IMPLEMENTE]
- Itens fora do escopo da subtarefa/fase

PASSO 5: REGRAS TECNICAS CRITICAS (MANTER)

1. Instrucoes auto-contidas:
   - Nao assumir leitura de subtarefa anterior.
   - Referenciar dependencias explicitamente.

2. Precisao tecnica:
   - Sem "etc", sem "...", sem abreviacoes vagas.
   - Tipos e restricoes explicitos (ex: integer > 0).
   - Formulas completas (ex: lucro = receita - custoTotal - taxa).

3. Resiliencia de configuracao (first-run):
   - Tratar env em 3 estados: ausente, invalida, valida.
   - Development: fallback seguro com warning claro.
   - Production: fail-fast com mensagem explicita.
   - Assumir `.env` inicial vindo de `.env.example` com placeholders.
   - Validar formatos estritos no startup (JWT/Fernet etc) quando aplicavel.

4. Docker e portas locais:
   - Nao assumir porta de host livre.
   - Preferir mapeamento parametrizavel (ex: `${DB_PORT_HOST:-5432}:5432`).
   - Orientar fallback simples para conflito de portas.

5. Validacao automatica obrigatoria:
   - Executar build/typecheck/lint/testes conforme stack.
   - Executar smoke test de runtime real (nao apenas sintaxe/build).
   - Se houver Docker Compose, subir stack e validar readiness/health.
   - Verificar logs de inicializacao e descrever falhas em linguagem simples.

PASSO 6: TESTES E CONCLUSAO

A secao `TESTES_AUTOMATIZADOS_OBRIGATORIOS` deve listar:
- comandos objetivos
- criterio de aprovado/reprovado por comando
- acao corretiva se falhar

A secao `VALIDACAO_MANUAL_OPCIONAL` deve existir somente quando:
- houver UI/UX, fluxo visual, interacao humana relevante
- nesse caso, incluir passos claros e resultado esperado visual

A secao `CRITERIO_DE_CONCLUSAO` deve ser check-list objetivo:
- [ ] subtarefas concluidas em sequencia
- [ ] arquivos previstos criados/modificados
- [ ] build/typecheck/testes/smoke passaram
- [ ] regras de negocio implementadas e validadas
- [ ] itens de NAO_IMPLEMENTE nao foram feitos
- [ ] handoff final preenchido

PASSO 7: FORMATO DE SAIDA DO AGENTE AO FINAL DA FASE

O resultado da fase deve ser reportado assim:

## RESULTADO_DA_FASE
- RESUMO_EXECUTIVO: [2-4 frases]
- ARQUIVOS_ALTERADOS: [lista]
- COMANDOS_EXECUTADOS: [lista]
- VALIDACOES: [checklist com status]
- FALHAS_ENCONTRADAS: [lista ou "nenhuma"]
- PENDENCIAS: [lista]
- PROXIMO_PASSO_EXATO: [acao objetiva]

PASSO 8: INSTRUCAO FINAL

Gere agora APENAS o arquivo `fase_01.md` seguindo rigorosamente a estrutura acima.
Nao gere `fase_02.md` neste momento.
```

---

## Checklist de qualidade da MP05-ClaudeCode

Antes de considerar a fase pronta, confirmar:

- [ ] O arquivo gerado e `fase_X.md` (nao micro-prompts para copy/paste no Cursor Chat)
- [ ] O bloco `BLOCO_DE_CONTROLE_DE_EXECUCAO` esta no topo
- [ ] Existem secoes de `TESTES_AUTOMATIZADOS_OBRIGATORIOS` e `CRITERIO_DE_CONCLUSAO`
- [ ] `VALIDACAO_MANUAL_OPCIONAL` so aparece quando UI/UX exigir
- [ ] Regras de resiliencia de env e first-run foram consideradas
- [ ] Regras Docker/portas e smoke test de runtime foram consideradas
- [ ] Dependencias, arquivos alvo e handoff estao explicitos
- [ ] Nenhuma instrucao de UX especifica de Cursor Chat foi incluida

---

## Observacoes finais

- Esta versao e para execucao autonoma no Claude Code dentro do Cursor.
- A MP05 original continua sendo a referencia para fluxo de micro-prompts focado em Cursor Agent.
- Em caso de duvida entre as duas versoes, priorizar:
  - `MP05 - Micro-Prompts.md` para fluxo copy/paste no Cursor Agent
  - `MP05 - Micro-Prompts-ClaudeCode.md` para fluxo por `fase_X.md` no Claude Code

