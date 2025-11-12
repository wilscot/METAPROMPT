# ESCOPO DO PROJETO: [Nome do Projeto]

---
⚠️ **ATENÇÃO ANTES DE GERAR ESTE DOCUMENTO:**

Este template define APENAS o que vai no escopo (O QUE construir).
NÃO adicione NADA além do que está explicitamente pedido nos placeholders [colchetes].

Se você sentir vontade de adicionar:
- SQL CREATE TABLE → PARE. Não adicione.
- Comandos bash/npm/git → PARE. Não adicione.  
- URLs específicas → PARE. Não adicione.
- Nomes de arquivos .tsx/.ts → PARE. Não adicione.
- Estrutura de pastas → PARE. Não adicione.

Quando em dúvida sobre adicionar algo: NÃO ADICIONE.
Quando placeholder tiver exemplo "ex: X ou Y": escolha um, não expanda.
Quando achar que "falta informação": deixe simples, não invente.

**MENOS É MAIS. Este documento é minimalista por design.**
---

## 1. VISÃO GERAL

**Descrição:** [Descrever o que o projeto faz em 2-3 frases]

**Tipo:** [Web App / Mobile App / Desktop / CLI / Backend API]

**Objetivo Principal:** [Problema que resolve / Necessidade que atende]

**Público-Alvo:** [Quem vai usar: uso pessoal / equipe pequena / produção / etc]

**Complexidade Estimada:** [Small / Medium / Large]

---

## 2. TECH STACK (OBRIGATÓRIO)

### ⚠️ CRITÉRIOS OBRIGATÓRIOS PARA SELEÇÃO DE FERRAMENTAS

Ao escolher qualquer ferramenta/serviço, considerar estes critérios:

#### 1. Grau de Automação
- ✅ **Ideal:** Tudo criável via código/CLI (100% automação)
- ⚠️ **Aceitável:** Requer 1-2 passos manuais simples
- ❌ **Evitar:** Requer criação manual de múltiplos recursos (tabelas, configs, etc)

**Perguntas-chave:**
- Schema/estrutura criável via arquivos? (migrations, schema files)
- Setup inicial automatizável? (scripts, comandos)
- Configs versionáveis em git?

#### 2. Domínio da IA
- ✅ **Alto:** IA conhece profundamente, documentação clara e acessível
- ⚠️ **Médio:** IA conhece o básico, pode precisar consultar docs
- ❌ **Baixo:** IA tem conhecimento limitado ou ferramenta muito nova

**Perguntas-chave:**
- IA consegue gerar código completo desta ferramenta?
- Documentação está amplamente disponível?
- Ferramenta é bem estabelecida (>2 anos no mercado)?

#### 3. Complexidade de Setup
- ✅ **Simples:** 1-3 comandos para inicializar
- ⚠️ **Moderado:** 4-8 comandos ou requer conta externa simples
- ❌ **Complexo:** >10 passos ou múltiplas dependências externas

**Perguntas-chave:**
- Quantos comandos para projeto funcionar?
- Requer serviços externos com limites restritivos?
- Funciona local/offline?

---

### 🤖 PROCESSO DE SELEÇÃO (para IA)

**Se tech stack NÃO está completamente especificado neste escopo:**

A IA DEVE, ANTES de gerar qualquer artifact:

1. **Identificar** tecnologias faltantes ou ambíguas
2. **Analisar** 2-3 opções viáveis para cada
3. **Apresentar** análise objetiva:

```
📊 Análise de Opções para [Categoria - ex: Database]

Opção A: [Nome - ex: SQLite + Prisma]
✅ Prós:
  - Automação: 100% - schema via Prisma, migrations automáticas
  - Domínio IA: Alto - Prisma amplamente conhecido
  - Setup: 2 comandos (prisma init + generate)
  - Local-first: Funciona offline
  
⚠️ Contras:
  - Não ideal para dados >100GB
  - Sem recursos avançados (replicação, etc)

📦 Melhor para: Projetos pequenos/médios, desenvolvimento local

---

Opção B: [Nome - ex: PostgreSQL + Prisma]
✅ Prós:
  - Automação: 100% - schema via Prisma
  - Domínio IA: Alto
  - Escalável, recursos avançados
  
⚠️ Contras:
  - Setup: 4 comandos (Docker + Prisma)
  - Requer Docker rodando

📦 Melhor para: Projetos médios/grandes, produção

---

Opção C: [Nome - ex: Supabase]
✅ Prós:
  - Features prontas (auth, storage)
  - Interface visual para debug
  
⚠️ Contras:
  - Automação: 60% - schema via SQL mas precisa UI para algumas configs
  - Domínio IA: Médio - menos documentação clara
  - Rate limits no free tier
  - Requer conta externa

📦 Melhor para: MVPs rápidos com auth pronta

---

❓ PERGUNTA: Qual opção prefere? Ou tem outra em mente?
```

4. **AGUARDAR** decisão do usuário
5. **Só então** gerar artifacts com a tecnologia escolhida

---

### 📋 Tech Stack Escolhido

**Preencha esta seção APÓS definir as tecnologias (seja você ou após consulta com IA):**

#### Frontend:
- Framework: [Next.js 14 / React / Vue / Angular / Vanilla / etc]
- Linguagem: [TypeScript / JavaScript]
- Styling: [Tailwind CSS / CSS Modules / Styled Components / etc]
- UI Components: [shadcn/ui / Material-UI / Ant Design / Custom / etc]
- Ícones: [Lucide React / Heroicons / Font Awesome / etc]

#### Backend:
- Framework: [Next.js API Routes / Express / FastAPI / Flask / etc]
- Linguagem: [TypeScript / JavaScript / Python / Go / etc]
- Autenticação: [NextAuth / Clerk / Supabase Auth / JWT custom / Nenhuma]

#### Database:
- Tipo: [PostgreSQL / MySQL / MongoDB / SQLite / File system (JSON) / Nenhum]
- ORM/Query: [Prisma / Drizzle / TypeORM / Mongoose / Raw SQL / fs/promises]
- Justificativa: [Por que esta escolha? Ex: "Local-first, 100% automatizável via Prisma"]

#### Infraestrutura:
- Deploy: [Vercel / Netlify / AWS / Docker / Local only]
- Node Version: [20.x / 18.x / etc]
- Package Manager: [npm / yarn / pnpm]

---

### ✅ Ferramentas Pré-Aprovadas (IA pode usar direto)

Se escolher estas, IA NÃO precisa perguntar (alto domínio + alta automação):

**Database & ORM:**
- SQLite + Prisma
- PostgreSQL (local via Docker) + Prisma  
- JSON files + fs/promises (projetos simples)

**Backend:**
- Next.js API Routes
- Express.js
- Fastify

**Frontend:**
- Next.js App Router
- React + Vite
- Vanilla HTML/JS

**Styling:**
- Tailwind CSS
- CSS Modules

**UI Components:**
- shadcn/ui (copy-paste, zero deps)
- Radix UI (headless)

---

## 3. INTEGRAÇÕES EXTERNAS

**Tem integrações com APIs ou serviços externos?** [Sim / Não]

### Se SIM, listar:

#### API/Serviço 1:
- Nome: [Ex: Stripe Payment]
- Tipo: [REST API / GraphQL / SDK]
- Autenticação: [API Key / OAuth / Bearer Token]
- Endpoints usados: [Listar principais endpoints]
- Documentação: [URL da doc]

#### API/Serviço 2:
- Nome: [Ex: SendGrid Email]
- Tipo: [REST API]
- Autenticação: [API Key]
- Endpoints usados: [POST /v3/mail/send]
- Documentação: [https://docs.sendgrid.com]

### Se NÃO:
- ✓ Aplicação standalone / offline
- ✓ Sem dependências externas

---

## 4. DEPENDÊNCIAS PRINCIPAIS

**Liste as principais bibliotecas/pacotes que serão usados:**

### Produção:
```
- next (ou framework principal)
- react
- typescript
- tailwindcss
- [outras libs específicas do projeto]
```

### Desenvolvimento:
```
- @types/node
- @types/react
- eslint
- prettier
- [outras dev tools]
```
## 4.1 REQUISITOS DE AMBIENTE

⚠️ **Liste requisitos específicos de sistema operacional ou ferramentas necessárias**

---

### Sistema Operacional:
[Windows / Linux / macOS / Todos / Qualquer]

---

### Pré-requisitos de Software:

**Obrigatórios:**
- Node.js: [versão mínima, ex: 18.x ou superior]
- [Outro software obrigatório, se aplicável]

**Opcionais:**
- [Software opcional que melhora desenvolvimento]

---

### ⚠️ Dependências com Requisitos Especiais

**Se seu projeto usa bibliotecas que compilam código nativo, documente aqui:**

**Formato:**
```
📦 [Nome da biblioteca]:
- Propósito: [para que serve]
- Requisito especial: [o que precisa instalar]
- Afeta: [Windows / macOS / Linux / Todos]
- Alternativa: [biblioteca equivalente sem requisitos, se existir]
```

**Exemplo preenchido:**
```
📦 better-sqlite3:
- Propósito: Database SQLite local de alta performance
- Requisito especial: Visual Studio Build Tools (Windows)
- Afeta: Windows
- Alternativa: @libsql/client (puro JavaScript, performance similar)

📦 bcrypt:
- Propósito: Hash de senhas seguro
- Requisito especial: Python + C++ compiler
- Afeta: Windows, macOS
- Alternativa: bcryptjs (puro JavaScript, mais lento mas funcional)
```

**Suas dependências especiais:**

[Preencha aqui se aplicável, ou deixe "Nenhuma"]

---

### 📋 Lista de Bibliotecas Comuns com Requisitos:

**Se usar alguma destas, documente acima:**
- better-sqlite3 (SQLite nativo)
- bcrypt (hash de senhas)
- sharp (processamento de imagens)
- canvas (manipulação canvas)
- node-gyp (qualquer lib que use)
- sqlite3 (SQLite nativo)
- argon2 (hash de senhas)
- node-sass (Sass/SCSS)

---

### 🔧 Instruções de Instalação (se necessário)

**Se tem requisitos especiais, forneça comandos:**

**Windows:**
```
[Comandos específicos Windows, se aplicável]
Exemplo: npm install --global windows-build-tools
```

**macOS:**
```
[Comandos específicos macOS, se aplicável]
Exemplo: xcode-select --install
```

**Linux:**
```
[Comandos específicos Linux, se aplicável]
Exemplo: sudo apt-get install build-essential
```

**Ou escreva:** "Não há comandos especiais necessários" se não aplicável.

---

### ✅ Quando NÃO Preencher Esta Seção:

**Deixe como "Nenhum requisito especial" se:**
- Projeto usa apenas JavaScript/TypeScript puro
- Todas as dependências são puras JS (sem compilação)
- Funciona em qualquer SO sem instalações extras
- Node.js + npm/yarn/pnpm é suficiente

---

### 💡 DICA: Como Saber Se Precisa?

**Sinais de que você precisa documentar:**
- 🔴 Erro "node-gyp" ao rodar npm install
- 🔴 Erro "Python not found" ao instalar deps
- 🔴 Erro "Visual Studio Build Tools required"
- 🔴 Biblioteca usa código C/C++/Rust/Go

**Se não viu nenhum desses erros:** Deixe como "Nenhum"

---

### 📌 EXEMPLO COMPLETO:

```markdown

## 4.1 REQUISITOS DE AMBIENTE

### Sistema Operacional:
Todos (Windows, macOS, Linux)

### Pré-requisitos de Software:

**Obrigatórios:**
- Node.js: 20.x ou superior
- pnpm: 8.x ou superior

**Opcionais:**
- Docker (se quiser rodar PostgreSQL local)

### ⚠️ Dependências com Requisitos Especiais

📦 better-sqlite3:
- Propósito: Database SQLite local de alta performance
- Requisito especial: Visual Studio Build Tools (Windows)
- Afeta: Windows
- Alternativa: @libsql/client (puro JavaScript)

### 🔧 Instruções de Instalação

**Windows:**
Instalar Build Tools (escolha uma opção):

Opção A - Via npm:
```bash
npm install --global windows-build-tools
```

Opção B - Manual:
Baixar Visual Studio Build Tools:
https://visualstudio.microsoft.com/downloads/

Opção C - Usar alternativa:
Trocar better-sqlite3 por @libsql/client no package.json

**macOS/Linux:**
Nenhuma instalação adicional necessária.
```
---

## 5. REGRAS DE NEGÓCIO

**Descreva as regras críticas do domínio do projeto:**

### Regra 1: [Nome da regra]
**Descrição:** [O que a regra define]

**Fórmula/Lógica:** [Se aplicável]
```
Exemplo:
Total = Preço × Quantidade - Desconto
```

**Validações:**
- [Validação 1]
- [Validação 2]

**Exceções:**
- [Caso especial 1]
- [Caso especial 2]

### Regra 2: [Nome da regra]
[Repetir estrutura]

---

## 6. FUNCIONALIDADES

### FASE 1: [Nome da Fase - Ex: Setup Inicial]

#### Feature 1.1: [Nome da Feature]
**Descrição:** [O que faz]

**Requisitos:**
- [Requisito 1]
- [Requisito 2]

**UI/UX:**
- [Componente/Tela envolvida]
- [Interações do usuário]

**Validações:**
- [Validação 1]
- [Validação 2]

#### Feature 1.2: [Nome da Feature]
[Repetir estrutura]

### FASE 2: [Nome da Fase]
[Repetir estrutura de features]

### FASE 3: [Nome da Fase]
[Repetir estrutura de features]

---

## 7. O QUE NÃO FAZER

**Lista explícita de features que NÃO devem ser implementadas:**

### Funcionalidades Excluídas:
- ❌ [Feature não desejada 1]
- ❌ [Feature não desejada 2]
- ❌ [Feature não desejada 3]

**Motivo:** [Opcional: explicar por que não incluir]

### Preferências de Implementação:
- ⚠️ [Abordagem X não é ideal - preferir abordagem Y porque...]
- ⚠️ [Ferramenta Z tem limitação W - considerar alternativas]

**Nota:** Esta seção orienta escolhas, mas IA deve dialogar antes de decidir.

---

## 8. ESTRUTURA DE DADOS

⚠️ **IMPORTANTE: Esta seção usa APENAS linguagem natural. Nada de código!**

---

### 📋 Entidades e Campos

Liste cada entidade (tabela/modelo/collection) com seus campos em formato de lista simples.

**Formato:**
```
[Nome da Entidade]:
- campo1: tipo (constraints/descrição)
- campo2: tipo (constraints/descrição)
```

**Exemplo preenchido:**
```
Produto:
- id: número único (gerado automaticamente)
- nome: texto (obrigatório, máximo 200 caracteres)
- precoUSD: decimal (obrigatório, valor positivo)
- cotacao: decimal (obrigatório, valor positivo)
- freteTotal: decimal (obrigatório, pode ser zero)
- quantidade: inteiro (obrigatório, padrão 0, não negativo)
- fornecedor: texto (opcional)
- tipo: texto (valores: 'LAB' ou 'PROD')
- deletedAt: data/hora (null se ativo)
- createdAt: data/hora (gerado automaticamente)
- updatedAt: data/hora (atualizado automaticamente)

Cenario:
- id: número único (gerado automaticamente)
- produtoId: número (referência ao Produto)
- nome: texto (obrigatório)
- precoVendaClassico: decimal (obrigatório)
- precoVendaPremium: decimal (obrigatório)
- taxaClassico: decimal (obrigatório, percentual)
- taxaPremium: decimal (obrigatório, percentual)
- freteCobrado: decimal (obrigatório)
- lucroClassico: decimal (calculado)
- lucroPremium: decimal (calculado)
- createdAt: data/hora (gerado automaticamente)
- updatedAt: data/hora (atualizado automaticamente)
```

**Suas entidades:**

[Preencha aqui suas entidades no mesmo formato acima]

---

### 🔗 Relacionamentos

Descreva como as entidades se relacionam em linguagem natural.

**Formato:**
```
[Entidade A] → [Entidade B]:
- Tipo: [um-para-muitos / muitos-para-muitos / um-para-um]
- Descrição: [explicação em português]
```

**Exemplo preenchido:**
```
Produto → Cenario:
- Tipo: um-para-muitos
- Um produto pode ter múltiplos cenários de simulação
- Cada cenário pertence a apenas um produto

Produto → Venda:
- Tipo: um-para-muitos
- Um produto pode ter múltiplas vendas registradas
- Cada venda é de um único produto
```

**Seus relacionamentos:**

[Preencha aqui seus relacionamentos no mesmo formato acima]

---

### 💾 Persistência

**Tipo:** [Database / File system / LocalStorage / Memory / etc]

**Tecnologia específica (se definida):** [SQLite / PostgreSQL / MongoDB / JSON files / etc]

**Localização:** [Banco local / Cloud / Browser storage / Server]

**Formato e Organização:**
[Descreva textualmente como os dados são organizados]

**Exemplo:**
```
- SQLite local no diretório raiz do projeto
- Dois schemas separados: 'lab' para simulações e 'prod' para dados reais
- Soft delete implementado (campo deletedAt em vez de DELETE real)
- Timestamps automáticos em todas as tabelas
```

**Seu formato:**

[Descreva aqui]

**Observações adicionais:**
[Qualquer detalhe relevante sobre persistência, backup, migração, etc]

---

### ⚠️ VALIDAÇÃO DESTA SEÇÃO

Antes de continuar, verifique:

**❌ VOCÊ NÃO DEVE TER ESCRITO:**
- [ ] Código TypeScript (interface, type, export, etc)
- [ ] SQL (CREATE TABLE, ALTER TABLE, etc)
- [ ] Schema de ORM (Prisma schema, Drizzle schema, etc)
- [ ] Blocos de código com ```typescript ou ```sql
- [ ] Imports ou exports
- [ ] Chaves { } ou colchetes [ ] de código
- [ ] Ponto-e-vírgula ; no final de linhas
- [ ] Palavras-chave de programação (const, let, var, function, etc)

**✅ VOCÊ DEVE TER APENAS:**
- [ ] Listas com hífen (-) ou bullet points
- [ ] Descrições em português/linguagem natural
- [ ] Tipos escritos por extenso (texto, número, decimal, data/hora)
- [ ] Relacionamentos descritos textualmente

Se você tem algo da lista ❌ → REMOVA e reescreva em linguagem natural!

---

### 💡 POR QUE SEM CÓDIGO?

O código será gerado automaticamente pelos meta-prompts baseado nesta descrição.

**Vantagens de manter sem código:**
- ✅ Escopo fica legível para não-programadores
- ✅ Pode mudar tech stack sem reescrever escopo
- ✅ Foco no "O QUE" (negócio), não no "COMO" (técnico)
- ✅ Documentação clara separada de implementação

## 9. CASOS DE USO

### UC1: [Nome do Caso de Uso]

**Ator:** [Quem executa]

**Fluxo Principal:**
1. [Passo 1]
2. [Passo 2]
3. [Passo 3]

**Fluxo Alternativo:**
- [Cenário alternativo se aplicável]

**Regras:**
- [Regra aplicável]
- [Validação específica]

### UC2: [Nome do Caso de Uso]
[Repetir estrutura]

---

## 10. VALIDAÇÕES E REGRAS DE CAMPO

### Formulário/Tela: [Nome]

**Campo 1:**
- Tipo: [text / number / email / etc]
- Obrigatório: [Sim / Não]
- Validação: [regex / tamanho / formato]
- Mensagem de erro: [Texto específico]

**Campo 2:**
[Repetir estrutura]

---

## 11. CRITÉRIOS DE ACEITE

**O sistema estará completo quando:**

### Funcionalidades:
- [ ] [Funcionalidade 1 completa e testada]
- [ ] [Funcionalidade 2 completa e testada]
- [ ] [Funcionalidade N completa e testada]

### Validações:
- [ ] [Todas validações de campo funcionando]
- [ ] [Mensagens de erro claras]
- [ ] [Feedback visual adequado]

### UX:
- [ ] [Interface intuitiva]
- [ ] [Responsivo (se aplicável)]
- [ ] [Loading states visíveis]
- [ ] [Empty states implementados]

### Técnico:
- [ ] [Código sem erros TypeScript]
- [ ] [Sem warnings no console]
- [ ] [Performance adequada]
- [ ] [Persistência funcionando]

---

## 12. DEPLOYMENT

⚠️ **NÃO ADICIONE COMANDOS (npm, git, pnpm) OU URLs (localhost:3000) AQUI.**

**Tipo:** [Produção / Staging / Local only]

**Ambiente de desenvolvimento:** [Descrever ambiente apenas se houver algo não-padrão]

**Não precisa:**
- [ ] Deploy em servidor
- [ ] CI/CD
- [ ] Monitoramento
- [ ] [Outros itens desnecessários]

---

## 13. MANUTENÇÃO FUTURA (Opcional)

**Features que PODEM ser adicionadas depois (não agora):**

- [Feature futura 1]
- [Feature futura 2]
- [Feature futura N]

**Condição:** Implementar apenas se usuário pedir explicitamente.

---

## 14. RESUMO EXECUTIVO

**O que é:** [Descrição de 1 frase]

**Diferencial:** [O que torna único ou útil]

**Tecnologia:** [Stack principal resumida]

**Complexidade:** [Small/Medium/Large]

**Prazo estimado:** [X horas/dias de desenvolvimento]

**Usuário final:** [Perfil de quem vai usar]

---

## 📌 INSTRUÇÕES DE PREENCHIMENTO

**Para o Claude gerar este escopo:**

```
Após discutir detalhes do projeto comigo, gere um escopo.md 
seguindo exatamente este template:
[colar link ou estrutura deste template]

Preencha TODAS as seções marcadas com [colchetes].
Seja específico e detalhado.
Se alguma seção não se aplicar, escreva "Não aplicável" com justificativa.

CRÍTICO - NÃO DEDUZA, NÃO EXPANDA:

❌ NÃO inclua detalhes de implementação técnica:
   - Estrutura de pastas ou árvore de diretórios
   - Nomes de arquivos específicos (.tsx, .ts, .sql)
   - Padrões de nomenclatura de código (PascalCase, camelCase)
   - Comandos de instalação (npm, yarn, pnpm, git, etc)
   - URLs específicas (localhost:3000, domínios)
   - Requisitos específicos de sistema (2GB RAM, Node 20.x)
   - Instruções de "como implementar"

❌ NÃO expanda placeholders com detalhes técnicos:
   - [versão] = deixe como está, NÃO substitua por "20.x"
   - [se relevante] = deixe como está, NÃO adicione valores
   - Se o template não pede, NÃO adicione

❌ NÃO adicione SQL schema completo:
   - Seção 8 pede interfaces TypeScript
   - Seção 8 pede descrição do formato ("SQL com 2 schemas")
   - Seção 8 NÃO pede CREATE TABLE detalhado

❌ NÃO leia arquivos antigos do projeto:
   - Ignore qualquer arquivo de escopo anterior no projeto
   - Use APENAS este template como referência
   - Se há arquivo "escopo_antigo.md", IGNORE-O

✅ O escopo define O QUE construir, não COMO construir.
✅ O meta-prompt decide estrutura técnica e implementação.
✅ Quando em dúvida: menos é mais. Não adicione.
```

---

## ✅ CHECKLIST DE VALIDAÇÃO

Antes de enviar ao meta-prompt, verificar:

**O que DEVE ter:**
- [ ] Seção 2 (Tech Stack) está completa
- [ ] Seção 3 (Integrações) está respondida (Sim/Não)
- [ ] Seção 6 (Funcionalidades) lista pelo menos 3 features
- [ ] Seção 7 (O que NÃO fazer) lista exclusões/preferências importantes
- [ ] Seção 8 (Estrutura de Dados) tem interfaces TypeScript
- [ ] Seção 11 (Critérios de Aceite) tem checkboxes validáveis
- [ ] Nenhuma seção ficou com [placeholder] vazio

**O que NÃO deve ter:**
- [ ] ❌ Estrutura de pastas ou árvore de diretórios (├── └──)
- [ ] ❌ Nomes de arquivos específicos (.tsx, .ts, .sql)
- [ ] ❌ SQL CREATE TABLE detalhado
- [ ] ❌ Comandos bash (npm, git, pnpm, yarn)
- [ ] ❌ URLs específicas (localhost:3000)
- [ ] ❌ Requisitos específicos (Node 20.x, 2GB RAM)
- [ ] ❌ Padrões de código (PascalCase, camelCase)
- [ ] ❌ Seção "Arquitetura Técnica"
- [ ] ❌ Seção "Variáveis de Ambiente" com exemplos de .env
- [ ] ❌ Instruções de "Como rodar" com comandos

**Se todos checkboxes positivos ✓ e nenhum negativo ✗ → Escopo pronto para meta-prompt!**
