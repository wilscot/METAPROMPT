# FLUXO COMPLETO - FRAMEWORK META-PROMPTS

## 🎯 VISÃO GERAL

Framework para criar aplicações completas usando IA, desde a ideia inicial até código funcionando.

**Fases:**
1. **PLANEJAMENTO** (Claude Web) → Define o que será construído
2. **GERAÇÃO** (Claude Web) → Cria artifacts de implementação  
3. **DESENVOLVIMENTO** (Cursor) → Transforma artifacts em código

---

## 📋 FASE 1: PLANEJAMENTO (Claude Web)

### Etapa 1: Conversa Livre 💬

**O que fazer:**
- Converse naturalmente sobre sua ideia
- Explique o problema que quer resolver
- Descreva como imagina a solução

**Quando avançar:**
- ✅ IA entendeu o conceito básico
- ✅ Você explicou a ideia principal

**Checkpoint:**
```
✅ Conceito básico explicado
✅ IA demonstrou compreensão
→ Pode avançar para Etapa 2
```

---

### Etapa 2: Descoberta Guiada (MP-00) 🔍

**Objetivo:** Capturar TODOS os detalhes antes de decisões técnicas.

**Estrutura:** 4 partes em chats separados (context limpo)

#### Chat 1: MP-00-Parte0-Historia.md
- **Input:** Conversa livre da Etapa 1
- **Output:** Resumo de contexto (motivação, situação atual, problema)
- **Checkpoint:**
  ```
  ✅ 7 perguntas respondidas
  ✅ Resumo de contexto gerado
  ✅ Insights identificados
  → Salve o resumo, avance para Chat 2
  ```

#### Chat 2: MP-00-Parte1-Criticas.md
- **Input:** Resumo da Parte 0
- **Output:** JSON com decisões técnicas (database, deploy, etc)
- **Checkpoint:**
  ```
  ✅ 8 perguntas técnicas respondidas
  ✅ JSON estruturado gerado
  ✅ Alertas de conflitos (se houver) resolvidos
  → Salve o JSON, avance para Chat 3
  ```

#### Chat 3: MP-00-Parte2-Contextuais.md
- **Input:** Resumo Parte 0 + JSON Parte 1
- **Output:** JSON atualizado + UI/UX definido (cores, telas, workflows)
- **Checkpoint:**
  ```
  ✅ 6 grupos de perguntas respondidos
  ✅ Dashboard e telas descritos
  ✅ Identidade visual definida
  ✅ JSON completo (Parte 1 + Parte 2)
  → Salve o JSON atualizado, avance para Chat 4
  ```

#### Chat 4: MP-00-Parte3-Conflitos-e-Roadmap.md
- **Input:** Resumo Parte 0 + JSON completo (Partes 1+2)
- **Output:** JSON final + roadmap pós-MVP
- **Checkpoint:**
  ```
  ✅ Conflitos detectados e resolvidos
  ✅ JSON final validado (todos campos preenchidos)
  ✅ Roadmap gerado (Fases 1, 2, 3+)
  → Salve JSON final e roadmap, avance para Etapa 3
  ```

**Arquivos gerados:**
- `decisoes-tecnicas.json` (JSON final)
- `roadmap.md` (opcional, mas útil)

---

### Etapa 3: Gerar Escopo (MP-01 Escopo) 📄

**Objetivo:** Transformar JSON da descoberta em `escopo.md` estruturado.

**Estrutura:** 2 partes em chats separados

#### Chat 5: MP-01-Gerar-Escopo-Parte1.md
- **Input:** JSON completo da descoberta guiada
- **Output:** `escopo.md` com seções 1-4
- **Checkpoint:**
  ```
  ✅ Seção 1 - Visão Geral
  ✅ Seção 2 - Tech Stack
  ✅ Seção 3 - Interface e Identidade Visual
  ✅ Seção 4 - Estrutura de Dados
  → Salve escopo.md parcial, avance para Chat 6
  ```

#### Chat 6: MP-01-Gerar-Escopo-Parte2.md
- **Input:** JSON completo + escopo.md (seções 1-4)
- **Output:** `escopo.md` completo (seções 5-9)
- **Checkpoint:**
  ```
  ✅ Seção 5 - Funcionalidades MVP
  ✅ Seção 6 - Roadmap Pós-MVP
  ✅ Seção 7 - Regras de Negócio
  ✅ Seção 8 - Limitações e Restrições
  ✅ Seção 9 - Critérios de Conclusão MVP
  ✅ Tech Stack completamente definido (sem "?" ou "[a definir]")
  → Salve escopo.md completo, avance para Etapa 4
  ```

**Arquivo gerado:**
- `escopo.md` (arquivo completo e validado)

---

### Etapa 4: Instalar Regras Cursor ⚙️

**Objetivo:** Preparar Cursor para desenvolvimento com qualidade.

**Quando fazer:**
- ✅ Pode ser feito a qualquer momento após ter `escopo.md`
- ✅ **DEVE estar completo ANTES de começar a codar no Cursor**
- ⚠️ Regras são só para Cursor, não afetam geração de artifacts na Web

**Como fazer:**
1. Abra `COMANDO PARA NOVO PROJETO.md` em `00 - CURSOR - REGRAS/`
2. Copie os 6 arquivos `.mdc` para `[seu-projeto]/.cursor/rules/`
3. Arquivos necessários:
   - `00-universal-code-standards.mdc`
   - `01-ask-first.mdc`
   - `02-dependencies.mdc`
   - `03-tool-selection.mdc`
   - `04-file-size.mdc`
   - `05-external-database.mdc`

**Checkpoint:**
```
✅ Pasta .cursor/rules/ criada
✅ 6 arquivos .mdc copiados
✅ Verificação: ls .cursor/rules/ mostra 6 arquivos
→ Regras instaladas, pode avançar para Fase 2
```

---

## 🚀 FASE 2: GERAÇÃO DE ARTIFACTS (Claude Web)

**Objetivo:** Gerar artifacts de implementação baseados no `escopo.md`.

**Importante:**
- ✅ Todos os MPs podem ser no mesmo chat OU chats separados
- ✅ **SEMPRE anexe `escopo.md`** em cada chat (mesmo que seja o mesmo chat)
- ✅ Execute em ordem: MP-01 → MP-02 → MP-03 → MP-04 → MP-05

---

### MP-01: Estrutura de Pastas 📁

**Arquivo:** `2 - META PROMPT/MP-01-Estrutura-de-Pastas.md`

**O que faz:**
- Gera estrutura completa de pastas do projeto
- Baseado no tech stack do `escopo.md`

**Checkpoint:**
```
✅ Artifact gerado com estrutura de pastas
✅ Copiado para Cursor
✅ Validação: tree ou ls -R mostra estrutura criada
→ Avance para MP-02
```

---

### MP-02: Configurações ⚙️

**Arquivo:** `2 - META PROMPT/MP-02-Configuracoes.md`

**O que faz:**
- Gera `package.json`, `tsconfig.json`, `.env.example`, etc
- Configura dependências baseadas no tech stack

**Checkpoint:**
```
✅ Artifact gerado com arquivos de configuração
✅ Copiado para Cursor
✅ Validação: npm install (ou pnpm install) executa sem erros
→ Avance para MP-03
```

---

### MP-03: Documentação 📚

**Arquivo:** `2 - META PROMPT/MP-03-Documentacao.md`

**O que faz:**
- Gera documentação de database/APIs externas
- Cria `docs/database-schema.md` ou `docs/api-schema.md`

**Quando usar:**
- ✅ Se projeto tem database externo (não criado por você)
- ✅ Se projeto integra com APIs externas desconhecidas
- ❌ Pule se não aplicável

**Checkpoint (se aplicável):**
```
✅ Artifact gerado com documentação
✅ Copiado para Cursor
✅ Validação: docs/ contém arquivos de schema
→ Avance para MP-04
```

---

### MP-04: Estrutura de Código 💻

**Arquivo:** `2 - META PROMPT/MP-04-Estrutura-de-Codigo.md`

**O que faz:**
- Cria arquivos vazios com TODOs baseados nas funcionalidades
- Estrutura inicial do código (sem implementação)

**Checkpoint:**
```
✅ Artifact gerado com arquivos vazios
✅ Copiado para Cursor
✅ Validação: find src -name "*.tsx" mostra arquivos criados
→ Avance para MP-05
```

---

### MP-05: Micro-Prompts 🎯

**Arquivo:** `2 - META PROMPT/MP-05-Micro-Prompts.md`

**O que faz:**
- Gera prompts de implementação detalhados
- Divide em fases (evita artifacts gigantes)

**Como funciona:**
1. MP-05 pergunta: "Quantas fases tem seu projeto na seção 6 do escopo.md?"
2. Você responde: "X fases" (ex: "4 fases")
3. MP-05 gera **1 artifact por fase**
4. Após completar Fase 1, peça para gerar Fase 2, e assim por diante

**Quantidade de prompts:**
- Varia por projeto (9 a 28+ prompts típicos)
- MP-05 agrupa tarefas relacionadas quando possível

**Checkpoint (por fase):**
```
✅ Artifact da Fase X gerado
✅ Prompts numerados e organizados
✅ Cada prompt tem [PRE-REQUISITOS] e [COMANDOS DE INSTALACAO]
→ Avance para Fase 3 (desenvolvimento)
```

---

## 💻 FASE 3: DESENVOLVIMENTO (Cursor)

**Objetivo:** Transformar micro-prompts em código funcionando.

**Como fazer:**
1. Abra Cursor Chat
2. Copie **UM prompt por vez** do artifact do MP-05
3. Cole no Cursor Chat
4. IA implementa automaticamente
5. **Valide** antes de avançar:
   - Build passa? (`pnpm run build`)
   - Testes manuais funcionam?
   - Sem erros TypeScript?
6. Marque prompt como concluído
7. Repita até completar todos os prompts da fase
8. Quando terminar fase atual, peça para gerar próxima fase no Claude Web

**Checkpoint (por prompt):**
```
✅ Prompt executado
✅ Build passou
✅ Arquivos criados/modificados
✅ Testes manuais validados
✅ Sem erros TypeScript
→ Avance para próximo prompt
```

**Checkpoint (por fase):**
```
✅ Todos os prompts da Fase X executados
✅ Funcionalidades da fase funcionando
✅ Sem bugs críticos
→ Pode pedir próxima fase no Claude Web
```

---

## 📊 RESUMO VISUAL

```
┌─────────────────────────────────────────────────────────┐
│ FASE 1: PLANEJAMENTO (Claude Web)                       │
├─────────────────────────────────────────────────────────┤
│ Etapa 1: Conversa Livre                                 │
│   ↓                                                     │
│ Etapa 2: MP-00 (4 chats)                               │
│   Chat 1: Parte 0 → Resumo contexto                    │
│   Chat 2: Parte 1 → JSON técnico                        │
│   Chat 3: Parte 2 → JSON + UI/UX                        │
│   Chat 4: Parte 3 → JSON final + roadmap               │
│   ↓                                                     │
│ Etapa 3: MP-01 Escopo (2 chats)                        │
│   Chat 5: Parte 1 → escopo.md (1-4)                    │
│   Chat 6: Parte 2 → escopo.md completo (5-9)            │
│   ↓                                                     │
│ Etapa 4: Instalar Regras Cursor                        │
│   Copiar 6 arquivos .mdc → .cursor/rules/               │
└─────────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│ FASE 2: GERAÇÃO (Claude Web)                            │
├─────────────────────────────────────────────────────────┤
│ MP-01: Estrutura Pastas → Artifact                     │
│ MP-02: Configurações → Artifact                        │
│ MP-03: Documentação → Artifact (se aplicável)          │
│ MP-04: Estrutura Código → Artifact                     │
│ MP-05: Micro-Prompts → Artifacts (1 por fase)         │
└─────────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│ FASE 3: DESENVOLVIMENTO (Cursor)                        │
├─────────────────────────────────────────────────────────┤
│ Copiar artifacts → Cursor                               │
│ Executar micro-prompts sequencialmente                 │
│ Validar cada prompt antes de avançar                    │
│ Regras do Cursor garantem qualidade                     │
└─────────────────────────────────────────────────────────┘
```

---

## ✅ CHECKLIST COMPLETO

### Fase 1: Planejamento
- [ ] Conversa livre concluída
- [ ] MP-00 Parte 0: Resumo contexto gerado
- [ ] MP-00 Parte 1: JSON técnico gerado
- [ ] MP-00 Parte 2: JSON + UI/UX gerado
- [ ] MP-00 Parte 3: JSON final + roadmap gerado
- [ ] MP-01 Parte 1: escopo.md (1-4) gerado
- [ ] MP-01 Parte 2: escopo.md completo (5-9) gerado
- [ ] escopo.md validado (tech stack completo, sem "?")
- [ ] Regras Cursor instaladas (6 arquivos .mdc)

### Fase 2: Geração
- [ ] MP-01: Artifact estrutura pastas gerado
- [ ] MP-02: Artifact configurações gerado
- [ ] MP-03: Artifact documentação gerado (se aplicável)
- [ ] MP-04: Artifact estrutura código gerado
- [ ] MP-05: Artifacts micro-prompts gerados (1 por fase)

### Fase 3: Desenvolvimento
- [ ] Artifacts copiados para Cursor
- [ ] Estrutura de pastas criada
- [ ] Configurações instaladas (`npm install` OK)
- [ ] Micro-prompts executados sequencialmente
- [ ] Cada prompt validado antes de avançar
- [ ] MVP completo e funcionando

---

## 🎯 DICAS IMPORTANTES

1. **Sempre anexe `escopo.md`** em todos os chats da Fase 2
2. **Um prompt por vez** no Cursor (não copie tudo de uma vez)
3. **Valide antes de avançar** (build, testes, sem erros)
4. **Regras são só para Cursor** (não afetam geração na Web)
5. **MP-05 gera em fases** (evita artifacts gigantes cortados)
6. **Chats separados = context limpo** (recomendado para MP-00 e MP-01 Escopo)
7. **Mesmo chat OK** para MP-01 a MP-05 (desde que escopo.md esteja anexado)

---

## 📚 ARQUIVOS DE REFERÊNCIA

**Descoberta Guiada:**
- `00 - DESCOBERTA(AI Web)/MP-00-Parte0-Historia.md`
- `00 - DESCOBERTA(AI Web)/MP-00-Parte1-Criticas.md`
- `00 - DESCOBERTA(AI Web)/MP-00-Parte2-Contextuais.md`
- `00 - DESCOBERTA(AI Web)/MP-00-Parte3-Conflitos-e-Roadmap.md`

**Geração de Escopo:**
- `01 - ESCOPO(AI Web)/MP-01-Gerar-Escopo-Parte1.md`
- `01 - ESCOPO(AI Web)/MP-01-Gerar-Escopo-Parte2.md`
- `01 - ESCOPO(AI Web)/escopo-template.md`

**Meta-Prompts de Desenvolvimento:**
- `2 - META PROMPT/MP-01-Estrutura-de-Pastas.md`
- `2 - META PROMPT/MP-02-Configuracoes.md`
- `2 - META PROMPT/MP-03-Documentacao.md`
- `2 - META PROMPT/MP-04-Estrutura-de-Codigo.md`
- `2 - META PROMPT/MP-05-Micro-Prompts.md`

**Regras Cursor:**
- `00 - CURSOR - REGRAS/COMANDO PARA NOVO PROJETO.md`
- `00 - CURSOR - REGRAS/*.mdc` (6 arquivos)

---

## ❓ PERGUNTAS FREQUENTES

**Q: Posso fazer MP-01 a MP-05 no mesmo chat?**  
A: Sim! Desde que `escopo.md` esteja anexado em cada execução.

**Q: Quando instalar as regras do Cursor?**  
A: Pode ser a qualquer momento após ter `escopo.md`, mas DEVE estar completo antes de começar a codar.

**Q: Quantos prompts o MP-05 gera?**  
A: Depende do projeto. Típico: 9 a 28+ prompts. MP-05 agrupa tarefas relacionadas quando possível.

**Q: Preciso anexar escopo.md em todos os MPs?**  
A: Sim! Tanto no Cursor quanto nos chats da Web que geram artifacts.

**Q: E se o tech stack não estiver completo no escopo.md?**  
A: MP-01 (Estrutura) vai detectar e perguntar antes de gerar artifact.

---

**Última atualização:** 2026-01-26
