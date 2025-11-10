# 03 - DOCUMENTAÇÃO

**COMO USAR:**
1. Abra Claude Web
2. Anexe seu `@escopo.md`
3. Cole este prompt completo
4. Claude gera 1 artifact com prompt para Cursor
5. **Se projeto NÃO tem database nem APIs externas:** Pule para `04-estrutura-codigo.md`
6. **Se tem:** Copie e cole no Cursor Chat
7. Valide que docs/ contém arquivos .md
8. Avance para `04-estrutura-codigo.md`

---

```
Analise o @escopo.md e determine se documentação técnica é necessária.

VERIFICAÇÃO:
- Tem database? [sim/não]
- Tem APIs externas? [sim/não]

SE AMBOS NÃO:
  Responda: "Documentação técnica não necessária. Pule para 04-estrutura-codigo.md"
  
SE PELO MENOS UM SIM:
  Gere artifact com documentação necessária

---

GERE O ARTIFACT (se aplicável):

Título: "Prompt para Cursor: Criar Documentação Técnica"

DOCUMENTAÇÃO NECESSÁRIA:

### Se tem DATABASE:
Arquivo: docs/database-schema.md
Conteúdo: Schema completo extraído do escopo.md

Formato:
```markdown
# Database Schema

## Table: [nome]
- field1: type (constraints)
- field2: type (constraints)

## Relationships
[descrever relacionamentos]

## Common Queries
[queries exemplo baseadas nos casos de uso do escopo]
```

### Se tem APIs EXTERNAS:
Arquivo: docs/api-endpoints.md
Conteúdo: Endpoints extraídos da seção "Integrações" do escopo

Formato:
```markdown
# External API Reference

## API: [nome]
Base URL: [url]
Auth: [método]

### Endpoints:
GET /endpoint
- Purpose: [...]
- Response: [...]

POST /endpoint
- Purpose: [...]
- Body: [...]
- Response: [...]
```

ESTRUTURA DO PROMPT:

```
Crie arquivos de documentação técnica:

[SE DATABASE:]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: docs/database-schema.md

[CONTEÚDO COMPLETO baseado no escopo.md]

[SE APIs EXTERNAS:]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: docs/api-endpoints.md

[CONTEÚDO COMPLETO baseado no escopo.md]

VALIDAÇÃO:
ls docs/
cat docs/database-schema.md | wc -l
# Deve ter >20 linhas

PROPÓSITO:
Esta documentação evita que a IA faça queries exploratórias no database
ou tentativas de descobrir estrutura de APIs.
```

IMPORTANTE:
- Extrair informações APENAS do escopo.md
- NÃO inventar schema se não estiver no escopo
- NÃO adicionar endpoints não mencionados
- Ser específico e completo
```
