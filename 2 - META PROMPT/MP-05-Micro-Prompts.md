# 05 - MICRO-PROMPTS

**COMO USAR:**

1. Abra Claude Web

2. Anexe seu `@escopo.md`

3. Cole este prompt completo

4. Claude gera 1 artifact com TODOS os micro-prompts numerados

5. **NÃO copie tudo de uma vez!**

6. Copie **UM prompt por vez** (cada um está em caixa única copiável)

7. Cole no Cursor Chat

8. Valide cada feature implementada antes de avançar

9. Repita até completar todos os prompts

---

```

Analise o @escopo.md e gere UM ÚNICO artifact contendo TODOS os micro-prompts de implementação, organizados por fase.

ANÁLISE DE IMPLEMENTAÇÃO:

1. FASES DO PROJETO:
   - Extrair da seção "Funcionalidades" do escopo
   - Identificar dependências entre features
   - Ordenar logicamente (setup → core → advanced → polish)

2. GRANULARIDADE:
   - Feature simples (1 componente, lógica básica): 1 prompt
   - Feature média (múltiplos arquivos, lógica moderada): 1-2 prompts
   - Feature complexa (fluxo completo, integrações): 2-4 prompts
   - Quebrar em: setup → core logic → UI → integration

3. DEPENDÊNCIAS:
   - Prompt N+1 assume que prompt N foi completado
   - Mencionar arquivos que já devem existir
   - Não repetir implementações de prompts anteriores

---

🔴 REGRA CRÍTICA: FORMATO DE CADA PROMPT

Cada prompt DEVE seguir este formato EXATO:

```
## 📦 PHASE [N]: [NOME DA FASE]

### Prompt [N.X]: [Título Descritivo]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CONTEXTO]
Breve descrição do que será implementado (1-2 frases)

[IMPLEMENTAÇÃO]

Arquivo: @caminho/completo/arquivo1.ts

Descrição: O que este arquivo faz

Conteúdo:
- Item 1: detalhes
- Item 2: detalhes
- Função X(params): lógica esperada

Schema/Interface (se aplicável):
```
código aqui se necessário
```

Comportamento:
- Ação A → Resultado B
- Validação C → Erro D

---

Arquivo: @caminho/completo/arquivo2.tsx

Descrição: O que este arquivo faz

Componente: NomeDoComponente

Props:
- prop1: tipo (descrição, valores válidos)
- prop2: tipo (comportamento esperado)

Estado:
- state1: tipo (propósito)
- state2: tipo (quando muda)

Renderização:
- Elemento 1: quando/como
- Elemento 2: condicional
- Interação X: onClick → ação

---

[ARQUIVOS ENVOLVIDOS]

Criar:
- @caminho/arquivo1.ts (propósito)
- @caminho/arquivo2.tsx (propósito)

Modificar:
- @caminho/existente.ts (adicionar X)

Usar (já existem):
- @caminho/lib.ts (função Y)
- @caminho/types.ts (tipo Z)

---

[REGRAS DE NEGÓCIO]

- Regra 1: descrição completa
- Regra 2: fórmula ou lógica
- Validação X: condição → mensagem de erro

---

[NÃO IMPLEMENTE]

❌ Feature X (será feita no prompt N.Y)
❌ Otimização Y (fase de polish)
❌ Funcionalidade Z (não está no escopo)

---

[VALIDAÇÕES ANTES DE EXECUTAR]

□ Dependência A existe (Prompt N.X)
□ Biblioteca B instalada (package.json)
□ Arquivo C criado (Prompt N.Y)

---

[CRITÉRIOS DE ACEITE]

- [ ] Comportamento 1 funciona
- [ ] Validação 2 ativa
- [ ] UI 3 renderiza corretamente
- [ ] Erro 4 é tratado
- [ ] Teste manual: ação X → resultado Y

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ FIM DO PROMPT - VALIDE ANTES DE AVANÇAR PARA PRÓXIMO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

🔴 REGRAS PARA O CONTEÚDO DOS PROMPTS:

1. **TUDO dentro da caixa copiável:**
   - Contexto, arquivos, regras, validações, critérios
   - Zero texto fora da caixa
   - IA deve conseguir executar olhando APENAS o que está na caixa

2. **Caminhos de arquivo SEMPRE com @:**
   - @src/app/page.tsx (não "src/app/page.tsx")
   - @src/components/Button.tsx
   - Cursor entende @ como referência ao arquivo

3. **Instruções auto-contidas:**
   - Não assumir que IA leu prompt anterior
   - Referenciar dependências: "usar função X de @src/lib/utils.ts (criada no Prompt 1.2)"
   - Especificar valores: "taxaClassico default: 11.0" (não "valor padrão")

4. **Detalhes técnicos completos:**
   - Tipos de dados: "quantidadeVendida: integer > 0"
   - Validações: "se estoque < quantidadeVendida → erro 400 'Estoque insuficiente'"
   - Fórmulas: "lucro = receita - custoTotal - taxaML"

5. **Sem abreviações ou "...":**
   - ❌ "Campos: nome, preço, etc"
   - ✅ "Campos: nome (string), precoUSD (number > 0), cotacao (number > 0)"

6. **Separadores visuais:**
   - Usar ━━━ para dividir seções
   - Usar --- para dividir arquivos
   - Usar 🎯 ✅ ❌ □ para destacar

---

🔴 ESTRUTURA DO ARTIFACT:

```markdown
# 🎯 MICRO-PROMPTS DE IMPLEMENTAÇÃO - [Nome do Projeto]

**INSTRUÇÕES CRÍTICAS:**
- ⚠️ Cole apenas **UM** prompt por vez no Cursor Chat
- ⏳ Aguarde implementação **completa**
- ✅ **Valide** funcionamento (rode, teste, verifique)
- 🚫 **NÃO** avance se houver erros
- 📋 Marque cada prompt como ✅ após completado

**Total de prompts:** [X]  
**Estimativa:** [Y horas/dias]  
**Complexidade:** [Small/Medium/Large]

---

## 📦 PHASE 1: [NOME DA FASE] (Prompts 1.1 - 1.X)

### Prompt 1.1: [Título]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CONTEÚDO COMPLETO DO PROMPT 1.1]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ FIM DO PROMPT - VALIDE ANTES DE AVANÇAR
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

### Prompt 1.2: [Título]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CONTEÚDO COMPLETO DO PROMPT 1.2]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ FIM DO PROMPT - VALIDE ANTES DE AVANÇAR
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

[... continuar para todos os prompts]

---

## 📊 RESUMO DA EXECUÇÃO

**Total de prompts gerados:** [X]  
**Fases:** [Y]  
**Features implementadas:** [Z]

**Ordem de execução:**
1. Execute prompts em ordem numérica
2. Valide cada um antes de avançar
3. Se erro, corrija antes de prosseguir
4. Marque como ✅ após completado

---

## ✅ CRITÉRIOS DE SUCESSO DO PROJETO

Sistema está **COMPLETO** quando:
- ✅ Todos [X] prompts executados
- ✅ Todos checkboxes da seção 11 do escopo.md marcados
- ✅ Testes manuais críticos passam
- ✅ `npm run build` executa sem erros
```

---

🔴 EXEMPLO DE PROMPT BEM FORMATADO:

```
### Prompt 2.3: API Route + Página - Produtos LAB

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CONTEXTO]
Criar página de produtos LAB com formulário CRUD e lista.

[IMPLEMENTAÇÃO]

Arquivo: @src/app/lab/produtos/page.tsx

Descrição: Página principal de produtos LAB

Componente: ProdutosLabPage

Estado:
- produtos: Produto[] (lista de produtos)
- modalAberto: boolean (controla dialog)
- produtoEditando: Produto | null (produto sendo editado)
- loading: boolean (estado de carregamento)

useEffect:
- Executar ao montar: buscar produtos via GET /api/produtos?modo=LAB
- Setar loading=true antes, loading=false depois
- Salvar em estado produtos

Renderização:
- Botão "+ Novo Produto LAB" (onClick: abre modal com produtoEditando=null)
- <ProdutoList modo="LAB" produtos={produtos} loading={loading} onEdit={setProdutoEditando} onDelete={handleDelete} />
- <Dialog open={modalAberto} onOpenChange={setModalAberto}>
    <ProdutoForm modo="LAB" produto={produtoEditando} onSuccess={refetch} />
  </Dialog>

Função handleDelete(id):
- Confirm dialog: "Deletar [Nome]? (será movido para lixeira)"
- DELETE /api/produtos/[id]?modo=LAB
- Toast sucesso: "Produto deletado!"
- refetch()

Função refetch():
- Buscar produtos novamente
- Fechar modal
- Limpar produtoEditando

---

Arquivo: @src/components/ProdutoForm.tsx

Descrição: Formulário de cadastro/edição de produto

Componente: ProdutoForm

Props:
- modo: 'LAB' | 'PROD' (obrigatório)
- produto: Produto | null (null = novo, objeto = edição)
- onSuccess: () => void (callback após salvar)

Estado:
- Form state via shadcn/ui Form component
- Campos: nome, precoUSD, cotacao, freteTotal, fornecedor

Campos (se modo === 'LAB'):
- Nome: Input text (required, min 3 chars)
- Preço USD: Input number (required, > 0, step 0.01)
- Cotação: Input number (required, > 0, step 0.01)
  - Botão "Buscar Cotação" disabled (API vem depois)
- Frete Total BRL: Input number (required, >= 0, step 0.01)
- Fornecedor: Input text (opcional)

Preview em tempo real (se modo === 'LAB'):
- Custo Unitário: calcularCustoUnitario(precoUSD, cotacao, freteTotal, 1)
- Exibir em badge: "Custo Unit.: R$ XX,XX"
- Usar função de @src/lib/calculators.ts (criada no Prompt 1.5)

Submit:
- Validar via validarProdutoLab de @src/lib/validators.ts
- Se erros: mostrar em toast vermelho, não enviar
- Se válido:
  - Se produto (edição): PUT /api/produtos/[id]?modo=LAB body={dados}
  - Se novo: POST /api/produtos body={...dados, modo: 'LAB'}
- Aguardar resposta
- Toast sucesso: "Produto salvo!"
- onSuccess()

---

Arquivo: @src/components/ProdutoList.tsx

Descrição: Lista de produtos em tabela

Componente: ProdutoList

Props:
- modo: 'LAB' | 'PROD' (obrigatório)
- produtos: Produto[] (obrigatório)
- loading: boolean (opcional, default false)
- onEdit: (produto: Produto) => void (callback editar)
- onDelete: (id: number) => void (callback deletar)

Renderização:

Se loading === true:
- <LoadingSpinner /> de @src/components/LoadingSpinner.tsx (criado no Prompt 7.2)

Se produtos.length === 0 E loading === false:
- <EmptyState 
    titulo="Nenhum produto cadastrado" 
    descricao="Clique em + para adicionar seu primeiro produto"
  />

Caso contrário:
- <Table> do shadcn/ui

Colunas (se modo === 'LAB'):
- Nome: produto.nome
- Preço USD: "$ XX.XX" (2 decimais)
- Cotação: "R$ X,XX" (2 decimais)
- Frete Total: "R$ XX,XX"
- Custo Unit.: calcularCustoUnitario(...) - formato "R$ XX,XX"
- Fornecedor: produto.fornecedor || "-"
- Ações:
  - Botão Editar (ícone Pencil) → onEdit(produto)
  - Botão Deletar (ícone Trash) → onDelete(produto.id)

---

[ARQUIVOS ENVOLVIDOS]

Criar:
- @src/app/lab/produtos/page.tsx (página principal)
- @src/components/ProdutoForm.tsx (formulário)
- @src/components/ProdutoList.tsx (lista)

Usar (já existem):
- @src/lib/calculators.ts (Prompt 1.5) - calcularCustoUnitario
- @src/lib/validators.ts (Prompt 1.5) - validarProdutoLab
- @src/components/ui/* (Prompt 1.3) - shadcn components
- @src/app/api/produtos/route.ts (Prompt 2.2) - endpoints

---

[REGRAS DE NEGÓCIO]

- Produtos LAB têm preço, cotação, frete (para simulação)
- Custo unitário é calculado em tempo real: (precoUSD × cotacao + freteTotal) ÷ 1
- Arredondar para 2 casas decimais
- Soft delete: produto vai para lixeira (deletedAt != NULL)
- Validações:
  - Nome: min 3 caracteres
  - Preço USD: > 0
  - Cotação: > 0
  - Frete Total: >= 0

---

[NÃO IMPLEMENTE]

❌ Botão "Exportar para PROD" (vem no Prompt 3.3)
❌ Buscar cotação API (endpoint vem no Prompt 6.3)
❌ Filtros ou busca (feature futura)
❌ Ordenação customizada (apenas createdAt DESC da API)

---

[VALIDAÇÕES ANTES DE EXECUTAR]

□ API produtos existe (Prompt 2.2) - GET, POST, PUT, DELETE
□ shadcn/ui instalado (Prompt 1.3) - Dialog, Table, Button, Input
□ Calculators prontos (Prompt 1.5) - calcularCustoUnitario
□ Validators prontos (Prompt 1.5) - validarProdutoLab
□ Tipos definidos (Prompt 2.1) - Produto, ProdutoInput

---

[CRITÉRIOS DE ACEITE]

- [ ] Página /lab/produtos renderiza sem erros
- [ ] Botão "+ Novo Produto" abre modal
- [ ] Formulário valida campos (erro se nome < 3 chars)
- [ ] Preview de custo unitário atualiza em tempo real
- [ ] Salvar novo produto: POST /api/produtos funciona
- [ ] Lista mostra produtos cadastrados
- [ ] Custo unitário na lista é calculado corretamente
- [ ] Botão Editar abre modal com dados preenchidos
- [ ] Editar produto: PUT /api/produtos/[id] funciona
- [ ] Botão Deletar mostra confirm dialog
- [ ] Deletar produto: soft delete funciona (vai para lixeira)
- [ ] Toast de feedback aparece em todas ações
- [ ] Loading state visível durante fetch
- [ ] Empty state aparece se lista vazia

Teste manual:
1. Criar produto "Teste A" com preço $10, cotação 5.5, frete 100
2. Verificar custo unitário: deve ser (10 × 5.5 + 100) ÷ 1 = R$ 155,00
3. Editar produto, mudar preço para $20
4. Verificar custo atualiza: (20 × 5.5 + 100) ÷ 1 = R$ 210,00
5. Deletar produto, verificar que sumiu da lista

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ FIM DO PROMPT - VALIDE ANTES DE AVANÇAR PARA PRÓXIMO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

🔴 CHECKLIST DE QUALIDADE DE CADA PROMPT:

Antes de gerar cada prompt, verificar:

- [ ] TUDO dentro de uma única caixa copiável (━━━ início/fim)
- [ ] Caminhos de arquivo com @ (@src/app/page.tsx)
- [ ] Dependências referenciadas: "função X de @path (criada no Prompt N.Y)"
- [ ] Valores específicos: "taxaClassico: 11.0" (não "valor padrão")
- [ ] Fórmulas completas: "lucro = receita - custo - taxa"
- [ ] Validações detalhadas: "se X < 0 → erro 'mensagem'"
- [ ] Tipos de dados: "quantidade: integer > 0"
- [ ] Sem "...", "etc", ou abreviações
- [ ] Seção [ARQUIVOS ENVOLVIDOS] completa
- [ ] Seção [REGRAS DE NEGÓCIO] com fórmulas
- [ ] Seção [NÃO IMPLEMENTE] previne feature creep
- [ ] Seção [VALIDAÇÕES ANTES DE EXECUTAR] lista deps
- [ ] Seção [CRITÉRIOS DE ACEITE] tem teste manual

---

IMPORTANTE:

- Cada prompt é INDEPENDENTE (pode ser executado sozinho)
- IA do Cursor deve conseguir implementar olhando APENAS o que está na caixa
- Zero fricção: copiar → colar → executar
- Zero ambiguidade: tudo especificado

GERE O ARTIFACT seguindo estas regras rigorosamente.
```
