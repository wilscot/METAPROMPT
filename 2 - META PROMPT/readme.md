# META PROMPT - Guia de Uso

## ⚠️ PRÉ-REQUISITO

Você já deve ter:
- ✅ escopo.md criado e validado
- ✅ Cursor Rules instaladas (.cursor/rules/)

Se não tem escopo.md ainda:
1. Abra novo chat no Claude
2. Use o template em `0 - ESCOPO/escopo-template.md`
3. Discuta seu projeto
4. IA gera escopo.md
5. Valide e salve no Cursor

---

## 🚀 USANDO OS META-PROMPTS

### 1. Abra chat no Claude
- Anexe seu escopo.md
- Tenha Cursor aberto em outra janela

### 2. Execute em ordem:

**MP-01: Estrutura de Pastas**
- Cole prompt completo
- Claude gera artifact
- Copie para Cursor Chat
- Valide com `tree` ou `ls -R`

**MP-02: Configurações**
- Cole prompt
- Gera package.json, tsconfig.json, etc
- Copie para Cursor
- Execute `npm install` para validar

**MP-03: Documentação** (se aplicável)
- Apenas se tem database/APIs externas
- Pule se não aplicável

**MP-04: Estrutura de Código**
- Gera arquivos vazios com TODOs
- Copie para Cursor
- Valide com `find src -name "*.tsx"`

**MP-05: Micro-Prompts**
- Gera TODOS os prompts de implementação
- NÃO copie tudo de uma vez!
- Copie 1 prompt por vez no Cursor
- Valide antes de avançar

### 3. Desenvolvimento
- Use micro-prompts sequencialmente
- Cursor Rules garantem qualidade
- Valide cada etapa

---

## 📂 ESTRUTURA ESPERADA
```
seu-projeto/
├── .cursor/rules/          ← 6 regras instaladas
├── escopo.md               ← Criado na Fase 1
├── src/                    ← MP-01 cria
├── package.json            ← MP-02 cria
├── docs/                   ← MP-03 cria (se aplicável)
└── [arquivos vazios]       ← MP-04 cria
```

---

## 🔄 FLUXO VISUAL
```
FASE 1 (Chat de Planejamento):
Template Escopo → Discussão → escopo.md ✓

FASE 2 (Chat de Desenvolvimento):
escopo.md + MP-01 a MP-05 → Artifacts → Cursor → Código ✓
```