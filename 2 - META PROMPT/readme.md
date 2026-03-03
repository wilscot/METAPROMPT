# META PROMPT - Guia de Uso

## 📋 VISÃO GERAL

Este guia cobre apenas a **FASE 2** do framework (Geração de Artifacts).

**Fluxo completo:** Veja `FLUXO_COMPLETO.md` na raiz do projeto.

---

## ⚠️ PRÉ-REQUISITOS

Antes de usar estes Meta-Prompts, você DEVE ter:

- ✅ **escopo.md** criado e validado (gerado na Fase 1)
- ✅ **Cursor Rules** instaladas (gerenciadas em repositório separado)

**Não tem escopo.md ainda?**
1. Veja `FLUXO_COMPLETO.md` → Fase 1: Planejamento
2. Execute MP-00 (Descoberta Guiada) + MP-01 Escopo
3. Volte aqui quando tiver escopo.md pronto

---

## 🚀 USANDO OS META-PROMPTS (FASE 2)

### Importante

- ✅ **SEMPRE anexe `escopo.md`** em cada chat (mesmo que seja o mesmo chat)
- ✅ Execute em ordem: MP-01 → MP-02 → MP-03 → MP-04 → MP-05
- ✅ Pode usar mesmo chat OU chats separados (desde que escopo.md esteja anexado)
- ✅ Valide cada artifact antes de avançar

---

### MP-01: Estrutura de Pastas 📁

**Arquivo:** `MP-01-Estrutura-de-Pastas.md`

**O que faz:**
- Gera estrutura completa de pastas baseada no tech stack do escopo.md
- Detecta tecnologias faltantes e pergunta antes de gerar

**Como usar:**
1. Abra chat no Claude Web
2. **Anexe escopo.md**
3. Cole o prompt completo de `MP-01-Estrutura-de-Pastas.md`
4. Claude gera artifact com estrutura de pastas
5. Copie artifact para Cursor Chat
6. Valide: `tree` ou `ls -R` mostra estrutura criada

**Checkpoint:**
```
✅ Artifact gerado
✅ Estrutura copiada para Cursor
✅ Pastas criadas corretamente
→ Avance para MP-02
```

---

### MP-02: Configurações ⚙️

**Arquivo:** `MP-02-Configuracoes.md`

**O que faz:**
- Gera `package.json`, `tsconfig.json`, `.env.example`, etc
- Configura dependências baseadas no tech stack

**Como usar:**
1. No mesmo chat OU novo chat (com escopo.md anexado)
2. Cole o prompt completo de `MP-02-Configuracoes.md`
3. Claude gera artifact com arquivos de configuração
4. Copie para Cursor
5. Execute `npm install` (ou `pnpm install`) para validar

**Checkpoint:**
```
✅ Artifact gerado
✅ Arquivos copiados para Cursor
✅ npm install executa sem erros
→ Avance para MP-03
```

---

### MP-03: Documentação 📚

**Arquivo:** `MP-03-Documentacao.md`

**O que faz:**
- Gera documentação de database/APIs externas
- Cria `docs/database-schema.md` ou `docs/api-schema.md`

**Quando usar:**
- ✅ Se projeto conecta em database externo (não criado por você)
- ✅ Se projeto integra com APIs externas desconhecidas
- ❌ **Pule se não aplicável** (maioria dos projetos)

**Como usar (se aplicável):**
1. No mesmo chat OU novo chat (com escopo.md anexado)
2. Cole o prompt completo de `MP-03-Documentacao.md`
3. Claude gera artifact com documentação
4. Copie para Cursor
5. Valide: `docs/` contém arquivos de schema

**Checkpoint (se aplicável):**
```
✅ Artifact gerado
✅ Documentação copiada
✅ docs/ contém schemas
→ Avance para MP-04
```

---

### MP-04: Estrutura de Código 💻

**Arquivo:** `MP-04-Estrutura-de-Codigo.md`

**O que faz:**
- Cria arquivos vazios com TODOs baseados nas funcionalidades do escopo.md
- Estrutura inicial do código (sem implementação)

**Como usar:**
1. No mesmo chat OU novo chat (com escopo.md anexado)
2. Cole o prompt completo de `MP-04-Estrutura-de-Codigo.md`
3. Claude gera artifact com arquivos vazios
4. Copie para Cursor
5. Valide: `find src -name "*.tsx"` mostra arquivos criados

**Checkpoint:**
```
✅ Artifact gerado
✅ Arquivos copiados para Cursor
✅ Arquivos vazios criados corretamente
→ Avance para MP-05
```

---

### MP-05: Micro-Prompts 🎯

Agora existem **dois sabores oficiais** da MP-05.

#### Opção A - Cursor Agent (copy/paste por prompt)

**Arquivo:** `MP05 - Micro-Prompts.md`

**Quando usar:**
- Fluxo tradicional com Cursor Agent
- Execução de 1 prompt por vez no chat do Cursor

**Saída esperada:**
- Artifact com micro-prompts numerados por fase
- Estrutura otimizada para copiar e colar no Cursor Chat

#### Opção B - Claude Code (execução autônoma por fase)

**Arquivo:** `MP05 - Micro-Prompts-ClaudeCode.md`

**Quando usar:**
- Claude Code via extensão ou terminal dentro do Cursor
- Execução por arquivo `fase_X.md` com subtarefas sequenciais

**Saída esperada:**
- `fase_01.md`, `fase_02.md`, ...
- Cada fase inclui bloco de controle, critérios de conclusão e handoff

#### Regra de escolha rápida

- Quer fluxo interativo de copy/paste: use `MP05 - Micro-Prompts.md`
- Quer fluxo autônomo orientado a fases: use `MP05 - Micro-Prompts-ClaudeCode.md`

#### Checkpoint (por fase)
```
✅ Artifact da Fase X gerado no formato correto (micro-prompts OU fase_X.md)
✅ Dependências e validações descritas
✅ Critério de conclusão presente
→ Avance para desenvolvimento
```

---

## 💻 DESENVOLVIMENTO NO CURSOR (FASE 3)

**Após ter todos os artifacts:**

1. Abra Cursor Chat
2. Copie **UM prompt por vez** do artifact do MP-05
3. Cole no Cursor Chat
4. IA implementa automaticamente
5. **Valide antes de avançar:**
   - Build passa? (`pnpm run build`)
   - Arquivos criados corretamente?
   - Sem erros TypeScript?
   - Testes manuais funcionam?
6. Marque prompt como concluído
7. Repita até completar todos os prompts da fase
8. Quando terminar fase atual, volte ao Claude Web e peça próxima fase

**Checkpoint (por prompt):**
```
✅ Prompt executado
✅ Build passou
✅ Arquivos criados/modificados
✅ Testes manuais validados
✅ Sem erros TypeScript
→ Avance para próximo prompt
```

---

## 📂 ESTRUTURA ESPERADA DO PROJETO

```
seu-projeto/
├── .cursor/
│   └── rules/              ← Cursor Rules (repositório separado)
├── escopo.md               ← Criado na Fase 1 (SEMPRE anexar)
├── src/                    ← MP-01 cria estrutura
├── package.json            ← MP-02 cria
├── tsconfig.json           ← MP-02 cria
├── docs/                   ← MP-03 cria (se aplicável)
└── [arquivos vazios]       ← MP-04 cria
```

---

## ✅ CHECKLIST RÁPIDO

### Antes de começar (Pré-requisitos):
- [ ] escopo.md criado e validado
- [ ] Cursor Rules instaladas (repositório separado)
- [ ] escopo.md anexado no chat

### Fase 2: Geração de Artifacts:
- [ ] MP-01: Estrutura de pastas gerada e copiada
- [ ] MP-02: Configurações geradas e validadas (`npm install` OK)
- [ ] MP-03: Documentação gerada (se aplicável)
- [ ] MP-04: Estrutura de código gerada
- [ ] MP-05: Micro-prompts Fase 1 gerados

### Fase 3: Desenvolvimento:
- [ ] MP05 escolhido corretamente (Cursor Agent ou ClaudeCode)
- [ ] Prompts/subtarefas executados sequencialmente
- [ ] Cada prompt validado antes de avançar
- [ ] MVP completo e funcionando

---

## 🎯 DICAS IMPORTANTES

1. **SEMPRE anexe escopo.md** em todos os chats da Fase 2
2. **Escolha o sabor correto da MP05** antes de iniciar (Cursor Agent vs ClaudeCode)
3. **Execução sequencial**: prompt por prompt (Cursor Agent) ou subtarefa por subtarefa (ClaudeCode)
4. **Valide antes de avançar** (build, testes, sem erros)
5. **Cursor Rules** são gerenciadas em repositório separado
6. **MP-05 gera em fases** (evita artifacts gigantes cortados)
7. **Mesmo chat OK** para MP-01 a MP-05 (desde que escopo.md esteja anexado)

---

## 📚 DOCUMENTAÇÃO COMPLETA

- **Fluxo completo:** `FLUXO_COMPLETO.md` (raiz do projeto)
- **Descoberta guiada:** `00 - DESCOBERTA(AI Web)/`
- **Geração de escopo:** `01 - ESCOPO(AI Web)/`
- **Cursor Rules:** Gerenciadas em repositório separado

---

## ❓ PERGUNTAS FREQUENTES

**Q: Posso fazer MP-01 a MP-05 no mesmo chat?**  
A: Sim! Desde que `escopo.md` esteja anexado em cada execução.

**Q: Quantos prompts o MP-05 gera?**  
A: Depende do projeto. Típico: 9 a 28+ prompts. MP-05 agrupa tarefas relacionadas quando possível.

**Q: Preciso anexar escopo.md em todos os MPs?**  
A: Sim! Tanto no Cursor quanto nos chats da Web que geram artifacts.

---

**Última atualização:** 2026-01-26