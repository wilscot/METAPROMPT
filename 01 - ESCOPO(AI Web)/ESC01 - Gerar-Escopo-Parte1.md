# ESC01 - GERAR ESCOPO (PARTE 1)

**QUANDO USAR:**
1. Apos completar DESC01-04 (Descoberta Guiada completa)
2. Ter em maos o JSON final da Parte 3
3. Abra NOVO chat no Claude (context limpo)
4. Anexe o JSON da descoberta
5. Cole este prompt

**PRE-REQUISITO:** JSON completo da descoberta guiada (Partes 0-3)

**OUTPUT:** Arquivo escopo.md (secoes 1-4)

---

```
Voce e uma IA especializada em gerar documentacao de escopo de software.

Recebi o seguinte JSON da descoberta guiada:

[COLE AQUI O JSON COMPLETO DA DESCOBERTA]

Sua tarefa: Transformar este JSON em um arquivo escopo.md estruturado.

Esta e a PARTE 1 - voce vai gerar as secoes 1 a 4.
A PARTE 2 vai continuar o mesmo arquivo com secoes 5 a 9.

---

## INSTRUCOES PARA A IA:

### 1. VERIFICACAO INICIAL

Antes de comecar, verifique se o JSON tem:
- [ ] projeto.nome
- [ ] projeto.contexto_completo ou contexto
- [ ] projeto.definicao_sucesso
- [ ] tech_stack (backend, frontend, database, infraestrutura)
- [ ] interface (dashboard, telas, identidade_visual)
- [ ] dados.entidades

Se algum campo critico estiver faltando, PARE e pergunte ao usuario.

---

### 2. GERAR SECAO 1 - VISAO GERAL

Extraia do JSON:
- projeto.nome -> Nome do Projeto
- projeto.descricao_curta -> Descricao
- projeto.contexto_completo -> Problema que Resolve
- projeto.definicao_sucesso -> Definicao de Sucesso
- projeto.urgencia -> Urgencia
- projeto.complexidade_estimada -> Complexidade

Formato:
"""
## 1. VISAO GERAL

**Descricao:** [extrair de projeto.descricao_curta]

**Tipo:** [inferir: Web App / Mobile / CLI / Backend API]

**Problema que Resolve:** [extrair de projeto.contexto_completo - resumir em 1-2 frases]

**Definicao de Sucesso:** [extrair de projeto.definicao_sucesso]

**Publico-Alvo:** [inferir do contexto]

**Urgencia:** [extrair de projeto.urgencia]

**Complexidade Estimada:** [extrair de projeto.complexidade_estimada]
"""

---

### 3. GERAR SECAO 2 - TECH STACK

Extraia do JSON:
- tech_stack.backend -> Backend
- tech_stack.frontend -> Frontend
- tech_stack.database -> Database
- tech_stack.infraestrutura -> Infraestrutura

Formato:
"""
## 2. TECH STACK

### Decisoes Tecnicas (validadas na descoberta)

#### Frontend:
- Framework: [tech_stack.frontend.framework]
- Linguagem: [tech_stack.frontend.linguagem]
- Styling: [tech_stack.frontend.styling]
- UI Components: [tech_stack.frontend.ui_components]

#### Backend:
- Framework: [tech_stack.backend.framework]
- Linguagem: [tech_stack.backend.linguagem]
- Autenticacao: [features.autenticacao.tipo ou "Nenhuma"]

#### Database:
- Tipo: [tech_stack.database.tipo]
- ORM/Query: [tech_stack.database.orm]
- Volume Estimado: [tech_stack.database.volume_estimado]
- Multiuser: [tech_stack.database.multiuser]
- Justificativa: [tech_stack.database.justificativa]

#### Infraestrutura:
- Deploy: [tech_stack.infraestrutura.deploy]
- Disponibilidade: [tech_stack.infraestrutura.disponibilidade]
- Budget: [tech_stack.infraestrutura.budget]
- Node Version: [tech_stack.infraestrutura.node_version]
- Package Manager: [tech_stack.infraestrutura.package_manager]

---

### Ferramentas Pre-Aprovadas (IA pode usar direto)

**Database e ORM:**
- SQLite + Prisma
- PostgreSQL + Prisma  
- JSON files + fs/promises (projetos simples)

**Backend:**
- Next.js API Routes
- Express.js
- Fastify

**Frontend:**
- Next.js App Router
- React + Vite

**Styling:**
- Tailwind CSS
- CSS Modules

**UI Components:**
- shadcn/ui
- Radix UI
"""

---

### 4. GERAR SECAO 3 - INTERFACE E IDENTIDADE VISUAL

Extraia do JSON:
- interface.dashboard -> Dashboard
- interface.telas -> Telas Principais
- interface.identidade_visual -> Identidade Visual
- workflows -> Workflows

Formato:
"""
## 3. INTERFACE E IDENTIDADE VISUAL

### Dashboard Inicial

**Metricas/Numeros visiveis:**
[Extrair de interface.dashboard.metricas - listar cada uma]

**Acoes Rapidas:**
[Extrair de interface.dashboard.acoes_rapidas - listar cada uma]

**Descricao visual:** [interface.dashboard.descricao]

---

### Telas Principais

[Para cada item em interface.telas, gerar:]

**Tela [N] - [tela.nome]:**
- Rota: [tela.rota]
- Proposito: [tela.proposito]
- Componentes: [tela.componentes - listar]

---

### Identidade Visual

**Logo:**
- Existe: [interface.identidade_visual.logo.existe]
- Descricao: [interface.identidade_visual.logo.arquivo ou descricao]

**Paleta de Cores:**
- Cor Primaria: [interface.identidade_visual.paleta.primaria]
- Cor Secundaria: [interface.identidade_visual.paleta.secundaria]
- Background: [interface.identidade_visual.paleta.background]
- Texto: [inferir baseado no background - escuro se light, claro se dark]
- Alerta/Erro: [#EF4444 padrao ou especificado]

**Estilo Visual:** [interface.identidade_visual.paleta.estilo]

**Tema:** [interface.identidade_visual.tema]

**Tipografia:** [interface.identidade_visual.tipografia ou "Inter"]

---

### Workflows Principais

[Para cada item em workflows, gerar:]

**Workflow [N] - [workflow.nome]:**
[Para cada passo em workflow.passos, numerar:]
1. [passo 1]
2. [passo 2]
3. [passo 3]
"""

---

### 5. GERAR SECAO 4 - ESTRUTURA DE DADOS

Extraia do JSON:
- dados.entidades -> Entidades e Campos

Formato:
"""
## 4. ESTRUTURA DE DADOS

### Entidades e Campos

[Para cada entidade em dados.entidades, gerar:]

**[entidade.nome]:**
- id: numero unico (gerado automaticamente)
[Para cada campo em entidade.campos, gerar:]
- [campo.nome]: [campo.tipo] ([campo.obrigatorio ? "obrigatorio" : "opcional"], [campo.validacao])
- createdAt: data/hora (gerado automaticamente)
- updatedAt: data/hora (atualizado automaticamente)

---

### Relacionamentos

[Para cada entidade que tem relacionamentos, gerar:]

**[entidade.nome] -> [relacionamento.com]:**
- Tipo: [relacionamento.tipo]
- Descricao: [relacionamento.descricao]

---

### Persistencia

**Tipo:** [tech_stack.database.tipo == "filesystem" ? "File system" : "Database"]
**Tecnologia:** [tech_stack.database.tipo] + [tech_stack.database.orm]
**Localizacao:** [tech_stack.infraestrutura.deploy == "local" ? "Local" : "Cloud"]

**Observacoes:**
- Timestamps automaticos em todas as entidades
- [Se tiver soft delete mencionado, adicionar]
"""

---

### 6. FINALIZAR PARTE 1

Apos gerar as 4 secoes, diga ao usuario:

"""
ESCOPO PARTE 1 GERADA!

Arquivo: escopo.md (secoes 1-4)

Conteudo gerado:
- Secao 1: Visao Geral
- Secao 2: Tech Stack
- Secao 3: Interface e Identidade Visual
- Secao 4: Estrutura de Dados

---

PROXIMO PASSO:

Abra um NOVO chat no Claude e cole o prompt:
**ESC02 - Gerar-Escopo-Parte2.md**

Anexe:
1. O JSON da descoberta (mesmo usado aqui)
2. O arquivo escopo.md gerado agora

A Parte 2 vai adicionar as secoes 5-9 no mesmo arquivo.
"""

---

## REGRAS IMPORTANTES

1. **NAO invente dados** - use apenas o que esta no JSON
2. **Se campo estiver vazio** - escreva "[A DEFINIR]" e destaque
3. **Mantenha linguagem natural** - sem codigo, sem SQL
4. **Use portugues** - todo o documento em PT-BR
5. **Seja consistente** - mesmos termos do JSON

---

## EXEMPLO DE OUTPUT

Se JSON tiver:
```json
{
  "projeto": {
    "nome": "Sistema Estoque",
    "descricao_curta": "Automatizar controle de estoque",
    "definicao_sucesso": "Zero produtos esgotados por esquecimento"
  },
  "tech_stack": {
    "database": {
      "tipo": "postgresql",
      "orm": "prisma"
    }
  }
}
```

Gerar:
"""
## 1. VISAO GERAL

**Descricao:** Automatizar controle de estoque

**Tipo:** Web App

**Problema que Resolve:** Perda de tempo com atualizacao manual de planilhas e risco de erro humano no controle de estoque.

**Definicao de Sucesso:** Zero produtos esgotados por esquecimento

...
"""
```
