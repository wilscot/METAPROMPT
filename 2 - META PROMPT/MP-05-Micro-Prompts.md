# 05 - MICRO-PROMPTS

**COMO USAR:**

1. Abra Claude Web

2. Anexe seu `@escopo.md`

3. Cole este prompt completo

4. Claude gera 1 artifact com TODOS os micro-prompts numerados

5. **NAO copie tudo de uma vez!**

6. Copie **UM prompt por vez** (cada um esta em caixa unica copiavel)

7. Cole no Cursor Chat

8. Valide cada feature implementada antes de avancar

9. Repita ate completar todos os prompts

---

```

Analise o @escopo.md e gere UM UNICO artifact contendo TODOS os micro-prompts de implementacao, organizados por fase.

ANALISE DE IMPLEMENTACAO:

1. FASES DO PROJETO:
   - Extrair da secao "Funcionalidades" do escopo
   - Identificar dependencias entre features
   - Ordenar logicamente (setup -> core -> advanced -> polish)

2. GRANULARIDADE:
   - Feature simples (1 componente, logica basica): 1 prompt
   - Feature media (multiplos arquivos, logica moderada): 1-2 prompts
   - Feature complexa (fluxo completo, integracoes): 2-4 prompts
   - Quebrar em: setup -> core logic -> UI -> integration

3. DEPENDENCIAS:
   - Prompt N+1 assume que prompt N foi completado
   - Mencionar arquivos que ja devem existir
   - Nao repetir implementacoes de prompts anteriores

---

REGRA CRITICA: FORMATO DE CADA PROMPT

Cada prompt DEVE seguir este formato EXATO:

## PHASE [N]: [NOME DA FASE]

### Prompt [N.X]: [Titulo Descritivo]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CONTEXTO]
Breve descricao do que sera implementado (1-2 frases)

[IMPLEMENTACAO]

Arquivo: @caminho/completo/arquivo1.ts

Descricao: O que este arquivo faz

Conteudo:
- Item 1: detalhes
- Item 2: detalhes
- Funcao X(params): logica esperada

Schema/Interface (se aplicavel):
```
codigo aqui se necessario
```

Comportamento:
- Acao A -> Resultado B
- Validacao C -> Erro D

---

Arquivo: @caminho/completo/arquivo2.tsx

Descricao: O que este arquivo faz

Componente: NomeDoComponente

Props:
- prop1: tipo (descricao, valores validos)
- prop2: tipo (comportamento esperado)

Estado:
- state1: tipo (proposito)
- state2: tipo (quando muda)

Renderizacao:
- Elemento 1: quando/como
- Elemento 2: condicional
- Interacao X: onClick -> acao

---

[ARQUIVOS ENVOLVIDOS]

Criar:
- @caminho/arquivo1.ts (proposito)
- @caminho/arquivo2.tsx (proposito)

Modificar:
- @caminho/existente.ts (adicionar X)

Usar (ja existem):
- @caminho/lib.ts (funcao Y)
- @caminho/types.ts (tipo Z)

---

[REGRAS DE NEGOCIO]

- Regra 1: descricao completa
- Regra 2: formula ou logica
- Validacao X: condicao -> mensagem de erro

---

[NAO IMPLEMENTE]

- Feature X (sera feita no prompt N.Y)
- Otimizacao Y (fase de polish)
- Funcionalidade Z (nao esta no escopo)

---

[VALIDACOES ANTES DE EXECUTAR]

- [ ] Dependencia A existe (Prompt N.X)
- [ ] Biblioteca B instalada (package.json)
- [ ] Arquivo C criado (Prompt N.Y)

---

[CRITERIOS DE ACEITE]

- [ ] Comportamento 1 funciona
- [ ] Validacao 2 ativa
- [ ] UI 3 renderiza corretamente
- [ ] Erro 4 e tratado
- [ ] Teste manual: acao X -> resultado Y

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIM DO PROMPT - VALIDE ANTES DE AVANCAR PARA PROXIMO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

REGRAS PARA O CONTEUDO DOS PROMPTS:

1. **TUDO dentro da caixa copiavel:**
   - Contexto, arquivos, regras, validacoes, criterios
   - Zero texto fora da caixa
   - IA deve conseguir executar olhando APENAS o que esta na caixa

2. **Caminhos de arquivo SEMPRE com @:**
   - @src/app/page.tsx (nao "src/app/page.tsx")
   - @src/components/Button.tsx
   - Cursor entende @ como referencia ao arquivo

3. **Instrucoes auto-contidas:**
   - Nao assumir que IA leu prompt anterior
   - Referenciar dependencias: "usar funcao X de @src/lib/utils.ts (criada no Prompt 1.2)"
   - Especificar valores: "taxaClassico default: 11.0" (nao "valor padrao")

4. **Detalhes tecnicos completos:**
   - Tipos de dados: "quantidadeVendida: integer > 0"
   - Validacoes: "se estoque < quantidadeVendida -> erro 400 'Estoque insuficiente'"
   - Formulas: "lucro = receita - custoTotal - taxaML"

5. **Sem abreviacoes ou "...":**
   - NAO USE "Campos: nome, preco, etc"
   - USE "Campos: nome (string), precoUSD (number > 0), cotacao (number > 0)"

6. **Separadores visuais:**
   - Usar linhas para dividir secoes
   - Usar --- para dividir arquivos

---

ESTRUTURA DO ARTIFACT:

```markdown
# MICRO-PROMPTS DE IMPLEMENTACAO - [Nome do Projeto]

**INSTRUCOES CRITICAS:**
- Cole apenas **UM** prompt por vez no Cursor Chat
- Aguarde implementacao **completa**
- **Valide** funcionamento (rode, teste, verifique)
- **NAO** avance se houver erros
- Marque cada prompt como concluido apos completado

**Total de prompts:** [X]  
**Estimativa:** [Y horas/dias]  
**Complexidade:** [Small/Medium/Large]

---

## PHASE 1: [NOME DA FASE] (Prompts 1.1 - 1.X)

### Prompt 1.1: [Titulo]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CONTEUDO COMPLETO DO PROMPT 1.1]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIM DO PROMPT - VALIDE ANTES DE AVANCAR
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

### Prompt 1.2: [Titulo]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CONTEUDO COMPLETO DO PROMPT 1.2]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIM DO PROMPT - VALIDE ANTES DE AVANCAR
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

[... continuar para todos os prompts]

---

## RESUMO DA EXECUCAO

**Total de prompts gerados:** [X]  
**Fases:** [Y]  
**Features implementadas:** [Z]

**Ordem de execucao:**
1. Execute prompts em ordem numerica
2. Valide cada um antes de avancar
3. Se erro, corrija antes de prosseguir
4. Marque como concluido apos completado

---

## CRITERIOS DE SUCESSO DO PROJETO

Sistema esta **COMPLETO** quando:
- Todos [X] prompts executados
- Todos checkboxes da secao 6 do escopo.md marcados (Criterios de Conclusao MVP)
- Testes manuais criticos passam
- `npm run build` executa sem erros
```

---

EXEMPLO DE PROMPT BEM FORMATADO:

```
### Prompt 2.3: API Route + Pagina - Produtos LAB

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CONTEXTO]
Criar pagina de produtos LAB com formulario CRUD e lista.

[IMPLEMENTACAO]

Arquivo: @src/app/lab/produtos/page.tsx

Descricao: Pagina principal de produtos LAB

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

Renderizacao:
- Botao "+ Novo Produto LAB" (onClick: abre modal com produtoEditando=null)
- <ProdutoList modo="LAB" produtos={produtos} loading={loading} onEdit={setProdutoEditando} onDelete={handleDelete} />
- <Dialog open={modalAberto} onOpenChange={setModalAberto}>
    <ProdutoForm modo="LAB" produto={produtoEditando} onSuccess={refetch} />
  </Dialog>

Funcao handleDelete(id):
- Confirm dialog: "Deletar [Nome]? (sera movido para lixeira)"
- DELETE /api/produtos/[id]?modo=LAB
- Toast sucesso: "Produto deletado!"
- refetch()

Funcao refetch():
- Buscar produtos novamente
- Fechar modal
- Limpar produtoEditando

---

Arquivo: @src/components/ProdutoForm.tsx

Descricao: Formulario de cadastro/edicao de produto

Componente: ProdutoForm

Props:
- modo: 'LAB' | 'PROD' (obrigatorio)
- produto: Produto | null (null = novo, objeto = edicao)
- onSuccess: () => void (callback apos salvar)

Estado:
- Form state via shadcn/ui Form component
- Campos: nome, precoUSD, cotacao, freteTotal, fornecedor

Campos (se modo === 'LAB'):
- Nome: Input text (required, min 3 chars)
- Preco USD: Input number (required, > 0, step 0.01)
- Cotacao: Input number (required, > 0, step 0.01)
  - Botao "Buscar Cotacao" disabled (API vem depois)
- Frete Total BRL: Input number (required, >= 0, step 0.01)
- Fornecedor: Input text (opcional)

Preview em tempo real (se modo === 'LAB'):
- Custo Unitario: calcularCustoUnitario(precoUSD, cotacao, freteTotal, 1)
- Exibir em badge: "Custo Unit.: R$ XX,XX"
- Usar funcao de @src/lib/calculators.ts (criada no Prompt 1.5)

Submit:
- Validar via validarProdutoLab de @src/lib/validators.ts
- Se erros: mostrar em toast vermelho, nao enviar
- Se valido:
  - Se produto (edicao): PUT /api/produtos/[id]?modo=LAB body={dados}
  - Se novo: POST /api/produtos body={...dados, modo: 'LAB'}
- Aguardar resposta
- Toast sucesso: "Produto salvo!"
- onSuccess()

---

Arquivo: @src/components/ProdutoList.tsx

Descricao: Lista de produtos em tabela

Componente: ProdutoList

Props:
- modo: 'LAB' | 'PROD' (obrigatorio)
- produtos: Produto[] (obrigatorio)
- loading: boolean (opcional, default false)
- onEdit: (produto: Produto) => void (callback editar)
- onDelete: (id: number) => void (callback deletar)

Renderizacao:

Se loading === true:
- <LoadingSpinner /> de @src/components/LoadingSpinner.tsx (criado no Prompt 7.2)

Se produtos.length === 0 E loading === false:
- <EmptyState 
    titulo="Nenhum produto cadastrado" 
    descricao="Clique em + para adicionar seu primeiro produto"
  />

Caso contrario:
- <Table> do shadcn/ui

Colunas (se modo === 'LAB'):
- Nome: produto.nome
- Preco USD: "$ XX.XX" (2 decimais)
- Cotacao: "R$ X,XX" (2 decimais)
- Frete Total: "R$ XX,XX"
- Custo Unit.: calcularCustoUnitario(...) - formato "R$ XX,XX"
- Fornecedor: produto.fornecedor || "-"
- Acoes:
  - Botao Editar (icone Pencil) -> onEdit(produto)
  - Botao Deletar (icone Trash) -> onDelete(produto.id)

---

[ARQUIVOS ENVOLVIDOS]

Criar:
- @src/app/lab/produtos/page.tsx (pagina principal)
- @src/components/ProdutoForm.tsx (formulario)
- @src/components/ProdutoList.tsx (lista)

Usar (ja existem):
- @src/lib/calculators.ts (Prompt 1.5) - calcularCustoUnitario
- @src/lib/validators.ts (Prompt 1.5) - validarProdutoLab
- @src/components/ui/* (Prompt 1.3) - shadcn components
- @src/app/api/produtos/route.ts (Prompt 2.2) - endpoints

---

[REGRAS DE NEGOCIO]

- Produtos LAB tem preco, cotacao, frete (para simulacao)
- Custo unitario e calculado em tempo real: (precoUSD x cotacao + freteTotal) / 1
- Arredondar para 2 casas decimais
- Soft delete: produto vai para lixeira (deletedAt != NULL)
- Validacoes:
  - Nome: min 3 caracteres
  - Preco USD: > 0
  - Cotacao: > 0
  - Frete Total: >= 0

---

[NAO IMPLEMENTE]

- Botao "Exportar para PROD" (vem no Prompt 3.3)
- Buscar cotacao API (endpoint vem no Prompt 6.3)
- Filtros ou busca (feature futura)
- Ordenacao customizada (apenas createdAt DESC da API)

---

[VALIDACOES ANTES DE EXECUTAR]

- [ ] API produtos existe (Prompt 2.2) - GET, POST, PUT, DELETE
- [ ] shadcn/ui instalado (Prompt 1.3) - Dialog, Table, Button, Input
- [ ] Calculators prontos (Prompt 1.5) - calcularCustoUnitario
- [ ] Validators prontos (Prompt 1.5) - validarProdutoLab
- [ ] Tipos definidos (Prompt 2.1) - Produto, ProdutoInput

---

[CRITERIOS DE ACEITE]

- [ ] Pagina /lab/produtos renderiza sem erros
- [ ] Botao "+ Novo Produto" abre modal
- [ ] Formulario valida campos (erro se nome < 3 chars)
- [ ] Preview de custo unitario atualiza em tempo real
- [ ] Salvar novo produto: POST /api/produtos funciona
- [ ] Lista mostra produtos cadastrados
- [ ] Custo unitario na lista e calculado corretamente
- [ ] Botao Editar abre modal com dados preenchidos
- [ ] Editar produto: PUT /api/produtos/[id] funciona
- [ ] Botao Deletar mostra confirm dialog
- [ ] Deletar produto: soft delete funciona (vai para lixeira)
- [ ] Toast de feedback aparece em todas acoes
- [ ] Loading state visivel durante fetch
- [ ] Empty state aparece se lista vazia

Teste manual:
1. Criar produto "Teste A" com preco $10, cotacao 5.5, frete 100
2. Verificar custo unitario: deve ser (10 x 5.5 + 100) / 1 = R$ 155,00
3. Editar produto, mudar preco para $20
4. Verificar custo atualiza: (20 x 5.5 + 100) / 1 = R$ 210,00
5. Deletar produto, verificar que sumiu da lista

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIM DO PROMPT - VALIDE ANTES DE AVANCAR PARA PROXIMO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

CHECKLIST DE QUALIDADE DE CADA PROMPT:

Antes de gerar cada prompt, verificar:

- [ ] TUDO dentro de uma unica caixa copiavel (linhas inicio/fim)
- [ ] Caminhos de arquivo com @ (@src/app/page.tsx)
- [ ] Dependencias referenciadas: "funcao X de @path (criada no Prompt N.Y)"
- [ ] Valores especificos: "taxaClassico: 11.0" (nao "valor padrao")
- [ ] Formulas completas: "lucro = receita - custo - taxa"
- [ ] Validacoes detalhadas: "se X < 0 -> erro 'mensagem'"
- [ ] Tipos de dados: "quantidade: integer > 0"
- [ ] Sem "...", "etc", ou abreviacoes
- [ ] Secao [ARQUIVOS ENVOLVIDOS] completa
- [ ] Secao [REGRAS DE NEGOCIO] com formulas
- [ ] Secao [NAO IMPLEMENTE] previne feature creep
- [ ] Secao [VALIDACOES ANTES DE EXECUTAR] lista deps
- [ ] Secao [CRITERIOS DE ACEITE] tem teste manual

---

IMPORTANTE:

- Cada prompt e INDEPENDENTE (pode ser executado sozinho)
- IA do Cursor deve conseguir implementar olhando APENAS o que esta na caixa
- Zero friccao: copiar -> colar -> executar
- Zero ambiguidade: tudo especificado

GERE O ARTIFACT seguindo estas regras rigorosamente.
```