# 02 - CONFIGURAÇÕES

**COMO USAR:**
1. Abra Claude Web
2. Anexe seu `@escopo.md`
3. Cole este prompt completo
4. Claude gera 1 artifact com prompt para Cursor
5. Copie e cole no Cursor Chat
6. **CRÍTICO:** Valide tamanho dos arquivos (package.json deve ter >500 bytes)
7. Execute `npm install` (ou yarn/pnpm) para validar
8. Avance para `03-documentacao.md`

---

```
## VERIFICAÇÃO DE TECH STACK

Antes de gerar artifact, verifique o @escopo.md:

### ✅ Tech Stack Completamente Definido?
Se a seção "Tech Stack Escolhido" tem TODAS as tecnologias preenchidas:
→ Prosseguir para geração do artifact

### ⚠️ Tecnologia Faltante ou Ambígua?
Se alguma tecnologia está indefinida ou marcada com "?" ou "[a definir]":

**PARE e faça:**

1. Identifique quais tecnologias estão faltando
2. Para cada uma, liste 2-3 alternativas viáveis
3. Avalie cada alternativa usando os critérios do escopo (seção 2):

```
📊 Análise de Opções para [Categoria]

Opção A: [Nome]
Automação: [X%] - [explicação]
Domínio IA: [Alto/Médio/Baixo] - [explicação]
Setup: [N comandos] - [detalhes]
✅ Prós: [lista]
⚠️ Contras: [lista]
📦 Melhor para: [caso de uso]

Opção B: [Nome]
[mesma estrutura]

Opção C: [Nome]
[mesma estrutura]
```

4. PERGUNTE ao usuário:
   "Detectei que [tecnologia X] não está definida no escopo.
   Baseado nos critérios do projeto, analisei as seguintes opções:
   
   [Cole análise acima]
   
   ❓ Qual opção prefere? Ou tem outra em mente?"

5. **AGUARDE resposta do usuário**
6. Só após decisão, gere o artifact com a tecnologia escolhida

### ❌ Tecnologia Definida mas IA Não Domina?
Se o escopo especifica uma tecnologia que você tem conhecimento limitado:

**ALERTE o usuário:**
"Detectei [tech X] no escopo, mas meu conhecimento sobre ela é limitado.
Posso tentar usar [tech X] (mas posso precisar de ajuda/docs), ou
posso sugerir alternativas que domino melhor: [lista]

Prefere que eu:
A) Continue com [tech X] (riscos: implementação pode ser incompleta)
B) Use alternativa que conheço melhor
C) Você preencha mais detalhes sobre [tech X] no escopo"

Aguarde decisão antes de prosseguir.

---

Analise o @escopo.md e gere UM ÚNICO artifact contendo um prompt para criar TODOS os arquivos de configuração com conteúdo COMPLETO.

ANÁLISE DE CONFIGURAÇÕES NECESSÁRIAS:
- Package manager: [npm/yarn/pnpm]
- Node version: [extrair do escopo]
- Framework config: [Next.js/Vite/CRA/Express/etc]
- Linguagem: [TypeScript/JavaScript]
- Styling: [Tailwind/CSS/etc]
- Linting: [ESLint/Prettier]

ARQUIVOS OBRIGATÓRIOS:
- package.json (800-1500 bytes mínimo)
- tsconfig.json ou jsconfig.json
- .gitignore
- .env.example (se aplicável)

ARQUIVOS CONDICIONAIS:
- tailwind.config.ts (se usa Tailwind)
- next.config.js (se Next.js)
- vite.config.ts (se Vite)
- eslint.config.js
- prettier.config.js

---

## ⚠️ VERIFICAÇÃO DE DEPENDÊNCIAS NATIVAS (NOVO)

Antes de gerar o artifact, analise as dependências do package.json que será criado.

### Dependências que requerem compilação (lista comum):
- better-sqlite3
- bcrypt
- sharp
- canvas
- node-gyp
- sqlite3
- argon2
- node-sass

### SE detectar alguma:

1. Identifique qual(is)
2. Verifique se há alternativa pura JS
3. Adicione aviso no final do artifact

**Formato do aviso:**

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🚨🚨🚨 ATENÇÃO CRÍTICA - LEIA ANTES DE CONTINUAR 🚨🚨🚨
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⛔ NÃO EXECUTE "npm install" AINDA! ⛔

Este projeto usa dependências que COMPILAM CÓDIGO NATIVO:

🔴 [lib1] ([propósito])
🔴 [lib2] ([propósito])

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ WINDOWS - REQUISITO OBRIGATÓRIO:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Visual Studio Build Tools PRECISA estar instalado.

Se você NÃO tem instalado → npm install VAI FALHAR ❌

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 ESCOLHA UMA OPÇÃO ANTES DE PROSSEGUIR:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

┌─────────────────────────────────────────────────────────┐
│ 🅰️  OPÇÃO A - INSTALAR BUILD TOOLS (30 min)            │
│                                                          │
│ ✅ Melhor performance                                    │
│ ✅ Solução definitiva                                    │
│ ⚠️  Download grande (~6GB)                              │
│ ⚠️  Instalação demorada                                 │
│                                                          │
│ COMO FAZER:                                              │
│ 1. Abra PowerShell COMO ADMINISTRADOR                   │
│ 2. Execute:                                              │
│    npm install --global windows-build-tools              │
│ 3. Aguarde instalação (20-30 minutos)                   │
│ 4. Depois rode: npm install                              │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│ 🅱️  OPÇÃO B - USAR ALTERNATIVA PURA JS (5 min) ⭐      │
│                                                          │
│ ✅ Zero requisitos                                       │
│ ✅ Funciona imediatamente                                │
│ ✅ Recomendado para projetos pequenos/médios            │
│ ⚠️  Performance 90-95% da nativa (suficiente)          │
│                                                          │
│ COMO FAZER:                                              │
│ 1. Abra: package.json                                    │
│ 2. Substitua:                                            │
│    "[lib1]" → "[alternativa1]"                           │
│    "[lib2]" → "[alternativa2]"                           │
│                                                          │
│ EXEMPLO:                                                 │
│ better-sqlite3 → @libsql/client                          │
│ bcrypt → bcryptjs                                        │
│ sharp → jimp                                             │
│                                                          │
│ 3. Depois rode: npm install                              │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│ 🅲  OPÇÃO C - USAR WSL/DOCKER (se souber)              │
│                                                          │
│ ✅ Ambiente Linux (sem problemas Windows)                │
│ ⚠️  Requer conhecimento de WSL/Docker                   │
└─────────────────────────────────────────────────────────┘

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💡 RECOMENDAÇÃO:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📦 Projeto pequeno/médio → OPÇÃO B (alternativa JS)
🚀 Projeto grande/performance crítica → OPÇÃO A (Build Tools)
👥 Time com Windows + Mac + Linux → OPÇÃO B (portabilidade)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📚 DOCUMENTAÇÃO:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Build Tools Windows:
https://github.com/nodejs/node-gyp#on-windows

Alternativas JS:
- better-sqlite3 vs @libsql/client: https://github.com/libsql/libsql
- bcrypt vs bcryptjs: https://www.npmjs.com/package/bcryptjs
- sharp vs jimp: https://www.npmjs.com/package/jimp

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🚨 IMPORTANTE: SÓ RODE "npm install" DEPOIS DE ESCOLHER! 🚨
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

GERE O ARTIFACT:

Título: "Prompt para Cursor: Criar Arquivos de Configuração"

⚠️ REGRA CRÍTICA: Cada arquivo deve ter conteúdo COMPLETO
- NÃO usar "..." ou abreviações
- NÃO omitir dependências
- Copiar TODAS as linhas necessárias

ESTRUTURA DO PROMPT:

```
Crie os seguintes arquivos de configuração com conteúdo COMPLETO:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: package.json

{
  "name": "project-name",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "...",
    "build": "...",
    "start": "...",
    "lint": "..."
  },
  "dependencies": {
    [LISTAR TODAS - adaptado ao escopo]
  },
  "devDependencies": {
    [LISTAR TODAS - adaptado ao escopo]
  }
}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: tsconfig.json

[CONTEÚDO COMPLETO - adaptado ao framework]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: .gitignore

[CONTEÚDO COMPLETO]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[... outros arquivos necessários]

VALIDAÇÃO:
ls -lh package.json tsconfig.json
# package.json deve ter >500 bytes
# tsconfig.json deve ter >400 bytes

cat package.json | grep -c '"'
# Deve mostrar >30 linhas

npm install
# Deve instalar sem erros

Se qualquer validação falhar, arquivo está incompleto.

[SE HOUVER DEPS NATIVAS: INCLUIR AVISO FORMATADO ACIMA]
```

IMPORTANTE:
- Dependencies específicas do escopo.md
- Versions compatíveis entre si
- Scripts adequados ao framework
- Configurações TypeScript corretas
- Aviso claro sobre dependências nativas (se aplicável)
```