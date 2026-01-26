# META PROMPT - Guia de Uso

## 📋 VISÃO GERAL

Este guia cobre apenas a **FASE 2** do framework (Geração de Artifacts).

**Fluxo completo:** Veja `FLUXO_COMPLETO.md` na raiz do projeto.

---

## ⚠️ PRÉ-REQUISITOS

Antes de usar estes Meta-Prompts, você DEVE ter:

- ✅ **escopo.md** criado e validado (gerado na Fase 1)
- ✅ **Cursor Rules** instaladas em `.cursor/rules/` (6 arquivos .mdc)
  - ⚠️ **Importante:** Regras devem estar instaladas ANTES de começar a codar
  - ✅ Podem ser instaladas a qualquer momento após ter escopo.md

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

**Arquivo:** `MP-05-Micro-Prompts.md`

**O que faz:**
- Gera prompts de implementação detalhados
- Divide em fases (evita artifacts gigantes que são cortados)

**Como funciona:**
1. MP-05 pergunta: "Quantas fases tem seu projeto na seção 6 do escopo.md?"
2. Você responde: "X fases" (ex: "4 fases")
3. MP-05 gera **1 artifact por fase** (não tudo junto!)
4. Após completar Fase 1 no Cursor, volte ao Claude Web e peça para gerar Fase 2

**Quantidade de prompts:**
- Varia por projeto (típico: 9 a 28+ prompts)
- MP-05 agrupa tarefas relacionadas quando possível

**Como usar:**
1. No mesmo chat OU novo chat (com escopo.md anexado)
2. Cole o prompt completo de `MP-05-Micro-Prompts.md`
3. Responda quantas fases tem o projeto
4. Claude gera artifact da **Fase 1** apenas
5. Copie para Cursor
6. Execute prompts sequencialmente (1 por vez)
7. Quando terminar Fase 1, volte ao Claude Web e peça: "Gere os prompts da Fase 2"

**Checkpoint (por fase):**
```
✅ Artifact da Fase X gerado
✅ Prompts numerados e organizados
✅ Cada prompt tem [PRE-REQUISITOS] e [COMANDOS DE INSTALACAO]
→ Avance para desenvolvimento no Cursor
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
│   └── rules/              ← 6 regras instaladas (ANTES de codar)
│       ├── 00-universal-code-standards.mdc
│       ├── 01-ask-first.mdc
│       ├── 02-dependencies.mdc
│       ├── 03-tool-selection.mdc
│       ├── 04-file-size.mdc
│       └── 05-external-database.mdc
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
- [ ] Regras Cursor instaladas (6 arquivos .mdc)
- [ ] escopo.md anexado no chat

### Fase 2: Geração de Artifacts:
- [ ] MP-01: Estrutura de pastas gerada e copiada
- [ ] MP-02: Configurações geradas e validadas (`npm install` OK)
- [ ] MP-03: Documentação gerada (se aplicável)
- [ ] MP-04: Estrutura de código gerada
- [ ] MP-05: Micro-prompts Fase 1 gerados

### Fase 3: Desenvolvimento:
- [ ] Prompts executados sequencialmente (1 por vez)
- [ ] Cada prompt validado antes de avançar
- [ ] MVP completo e funcionando

---

## 🎯 DICAS IMPORTANTES

1. **SEMPRE anexe escopo.md** em todos os chats da Fase 2
2. **Um prompt por vez** no Cursor (não copie tudo de uma vez)
3. **Valide antes de avançar** (build, testes, sem erros)
4. **Regras são só para Cursor** (não afetam geração na Web)
5. **MP-05 gera em fases** (evita artifacts gigantes cortados)
6. **Mesmo chat OK** para MP-01 a MP-05 (desde que escopo.md esteja anexado)

---

## 📚 DOCUMENTAÇÃO COMPLETA

- **Fluxo completo:** `FLUXO_COMPLETO.md` (raiz do projeto)
- **Descoberta guiada:** `00 - DESCOBERTA(AI Web)/`
- **Geração de escopo:** `01 - ESCOPO(AI Web)/`
- **Regras Cursor:** `00 - CURSOR - REGRAS/COMANDO PARA NOVO PROJETO.md`

---

## ❓ PERGUNTAS FREQUENTES

**Q: Posso fazer MP-01 a MP-05 no mesmo chat?**  
A: Sim! Desde que `escopo.md` esteja anexado em cada execução.

**Q: Quando instalar as regras do Cursor?**  
A: Pode ser a qualquer momento após ter `escopo.md`, mas **DEVE estar completo ANTES de começar a codar**.

**Q: Quantos prompts o MP-05 gera?**  
A: Depende do projeto. Típico: 9 a 28+ prompts. MP-05 agrupa tarefas relacionadas quando possível.

**Q: Preciso anexar escopo.md em todos os MPs?**  
A: Sim! Tanto no Cursor quanto nos chats da Web que geram artifacts.

---

**Última atualização:** 2026-01-26