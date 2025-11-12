# MICRO-PROMPTS DE IMPLEMENTAÇÃO
## Sistema de Gestão Mercado Livre - 2025-11-11

**INSTRUÇÕES:**
- Cole apenas UM prompt por vez no Cursor Chat
- Aguarde implementação completa
- Valide funcionamento antes de avançar para o próximo
- NÃO copie todos os prompts de uma vez

**Total de prompts:** 18  
**Estimativa:** 3-4 dias de desenvolvimento

---

## PHASE 0: SETUP BASE

### Prompt 0.1: Database Schema e Setup Inicial

**Contexto:** Implementar schema Drizzle ORM e script de setup do banco SQLite.

**Implementação:**

Implementar COMPLETAMENTE os arquivos de database:

1. **src/db/schema.ts:**
   - Importar sqliteTable, text, integer, real, sql de drizzle-orm
   - Definir tabela `produtos` com TODOS os campos do escopo (id, nome, precoUSD, cotacao, freteTotal, quantidade, fornecedor, tipo ENUM['LAB','PROD'], deletedAt, createdAt, updatedAt)
   - Definir tabela `cenarios` com FK para produtos (id, produtoId, nome, precoVendaClassico, precoVendaPremium, taxaClassico, taxaPremium, freteCobrado, lucroClassico, lucroPremium, createdAt, updatedAt)
   - Definir tabela `vendas` com FK para produtos (id, produtoId, quantidadeVendida, precoVenda, tipoAnuncio ENUM['CLASSICO','PREMIUM'], freteCobrado, taxaML, lucroLiquido, data, createdAt)
   - Definir tabela `configuracoes` singleton (id, taxaClassico DEFAULT 11, taxaPremium DEFAULT 16, cotacaoDolar, updatedAt)
   - Exportar tipos TypeScript inferidos: Produto, NovoProduto, Cenario, NovoCenario, Venda, NovaVenda, Configuracao, NovaConfiguracao

2. **src/db/index.ts:**
   - Criar conexão SQLite para ./db/data.db usando better-sqlite3
   - Criar instância drizzle
   - Exportar db e schema

3. **scripts/setup-db.ts:**
   - Executar migrations via drizzle-kit
   - Seed configuracoes com valores default (id=1, taxaClassico=11, taxaPremium=16)
   - Log de sucesso

**Regras de Negócio:**

- tipo deve ser ENUM: 'LAB' ou 'PROD' apenas
- deletedAt NULL = ativo, NOT NULL = deletado (soft delete)
- Timestamps em formato Unix epoch (integer)
- configuracoes é singleton (sempre id=1)

**NÃO IMPLEMENTE:**

❌ Migrations complexas (usar drizzle-kit push)
❌ Validações de dados (será feito em validators.ts)
❌ Queries ou helpers (será feito em db-client.ts)

**Arquivos:**

- **Criar:** `src/db/schema.ts`
- **Criar:** `src/db/index.ts`
- **Criar:** `scripts/setup-db.ts`
- **Referência:** `docs/database-schema.md` (schema completo)

**Validações antes de executar:**

□ pnpm instalado e dependências rodadas
□ Pasta db/ existe
□ drizzle.config.ts configurado

**Critérios de aceite:**

- [ ] Schema define 4 tabelas com tipos corretos
- [ ] Conexão SQLite funciona
- [ ] Script setup-db.ts cria banco e seed config
- [ ] pnpm db:push executa sem erros
- [ ] pnpm db:studio abre Drizzle Studio

---

### Prompt 0.2: Utilities e Helpers Base

**Contexto:** Implementar funções utilitárias essenciais para o projeto.

**Implementação:**

1. **src/lib/utils.ts:**
   - Função cn() para merge de classNames (clsx + tailwind-merge)
   - Exportar para uso em componentes shadcn/ui

2. **src/lib/calculators.ts:**
   - `calcularCustoTotal(precoUSD, cotacao, freteTotal, quantidade)`: retorna custo total em BRL
   - `calcularTaxaML(precoVenda, taxaPercent)`: retorna valor da taxa em BRL
   - `calcularLucro(precoVenda, quantidade, freteCobrado, custoTotal, taxaML)`: retorna lucro líquido
   - Todas as funções devem receber números e retornar números com 2 casas decimais

3. **src/lib/validators.ts:**
   - `validarProduto(data: NovoProduto)`: valida campos obrigatórios, valores > 0, retorna {valid: boolean, errors: string[]}
   - `validarCenario(data: NovoCenario)`: valida campos obrigatórios, valores > 0
   - `validarVenda(data: NovaVenda, estoque: number)`: valida campos + estoque suficiente

4. **src/lib/cotacao.ts:**
   - `buscarCotacaoDolar()`: async function que chama AwesomeAPI
   - URL: https://economia.awesomeapi.com.br/json/last/USD-BRL
   - Retorna parseFloat(data.USDBRL.bid) ou null em caso de erro
   - Usar try/catch para erros de rede

**Campos/Props/Parâmetros:**

calcularCustoTotal:
- precoUSD: number (preço unitário em USD, > 0)
- cotacao: number (cotação BRL/USD, > 0)
- freteTotal: number (frete total em BRL, >= 0)
- quantidade: number (quantidade, > 0)
- return: number (custo unitário em BRL)

calcularTaxaML:
- precoVenda: number (preço de venda, > 0)
- taxaPercent: number (taxa em %, ex: 11 ou 16)
- return: number (valor da taxa em BRL)

calcularLucro:
- precoVenda: number (preço unitário, > 0)
- quantidade: number (quantidade vendida, > 0)
- freteCobrado: number (frete cobrado do cliente, >= 0)
- custoTotal: number (custo unitário, > 0)
- taxaML: number (valor da taxa ML, >= 0)
- return: number (lucro líquido total)

**Regras de Negócio:**

- Custo unitário = (precoUSD * cotacao + freteTotal) / quantidade
- Taxa ML = (precoVenda * taxaPercent) / 100
- Lucro = (precoVenda * quantidade) + freteCobrado - (custoTotal * quantidade) - taxaML
- Todos valores com 2 casas decimais (usar toFixed(2) e parseFloat)

**NÃO IMPLEMENTE:**

❌ Validações de UI/formulários (será em componentes)
❌ Chamadas ao banco (será em db-client.ts)
❌ Lógica de negócio complexa (manter funções puras)

**Arquivos:**

- **Criar:** `src/lib/utils.ts`
- **Criar:** `src/lib/calculators.ts`
- **Criar:** `src/lib/validators.ts`
- **Criar:** `src/lib/cotacao.ts`
- **Referência:** `docs/api-endpoints.md` (AwesomeAPI)

**Validações antes de executar:**

□ Tipos do schema.ts disponíveis
□ date-fns instalado (se necessário)

**Critérios de aceite:**

- [ ] cn() funciona corretamente
- [ ] Calculators retornam valores numéricos corretos
- [ ] Validators retornam {valid, errors}
- [ ] buscarCotacaoDolar() retorna número ou null
- [ ] Fórmulas conferem com docs/database-schema.md

---

### Prompt 0.3: Database Client Helpers

**Contexto:** Implementar helpers para queries comuns no banco de dados.

**Implementação:**

Criar arquivo `src/lib/db-client.ts` com funções helper:

1. **getProdutos(tipo: 'LAB' | 'PROD', includeDeleted = false)**
   - Retorna lista de produtos filtrados por tipo
   - Se includeDeleted false: WHERE deletedAt IS NULL
   - Ordenar por createdAt DESC

2. **getProdutoById(id: number)**
   - Retorna produto único ou null
   - Incluir produtos deletados também

3. **getCenariosByProdutoId(produtoId: number)**
   - Retorna lista de cenários do produto
   - Ordenar por createdAt DESC

4. **getVendas(filters?: { produtoId?: number, startDate?: Date, endDate?: Date })**
   - Retorna vendas com JOIN de produtos
   - Filtros opcionais por produto e data
   - Ordenar por data DESC

5. **getConfig()**
   - Retorna configuração global (singleton id=1)
   - Se não existir, criar com valores default

**Parâmetros:**

getProdutos:
- tipo: 'LAB' | 'PROD' (obrigatório)
- includeDeleted: boolean (opcional, default false)
- return: Promise<Produto[]>

getProdutoById:
- id: number
- return: Promise<Produto | null>

getCenariosByProdutoId:
- produtoId: number
- return: Promise<Cenario[]>

getVendas:
- filters: { produtoId?: number, startDate?: Date, endDate?: Date }
- return: Promise<(Venda & { produto: Produto })[]>

getConfig:
- return: Promise<Configuracao>

**Regras de Negócio:**

- Sempre filtrar deletedAt IS NULL por padrão (exceto quando includeDeleted=true)
- getConfig deve criar registro se não existir (singleton pattern)
- Usar Drizzle ORM queries (eq, and, isNull, gte, lte, desc)

**NÃO IMPLEMENTE:**

❌ Mutations (create/update/delete) - serão nas API routes
❌ Validações de dados - já estão em validators.ts
❌ Cálculos - já estão em calculators.ts

**Arquivos:**

- **Criar:** `src/lib/db-client.ts`
- **Usar:** `src/db/index.ts` (db e schema)
- **Usar:** `src/db/schema.ts` (tipos)
- **Referência:** `docs/database-schema.md` (queries comuns)

**Validações antes de executar:**

□ Database setup concluído (Prompt 0.1)
□ Schema e conexão funcionando

**Critérios de aceite:**

- [ ] getProdutos retorna array filtrado corretamente
- [ ] getProdutoById retorna produto ou null
- [ ] getCenariosByProdutoId retorna array
- [ ] getVendas aceita filtros opcionais
- [ ] getConfig retorna ou cria configuração

---

### Prompt 0.4: Layout e Estilos Globais

**Contexto:** Implementar layout raiz Next.js e estilos globais shadcn/ui.

**Implementação:**

1. **src/app/layout.tsx:**
   - Importar Inter font do next/font/google
   - Definir metadata: title "Sistema Gestão ML", description do escopo
   - Estrutura HTML com lang="pt-BR"
   - Aplicar className com font
   - Renderizar {children}
   - Adicionar <Toaster /> do shadcn/ui (será instalado depois)

2. **src/app/globals.css:**
   - Tailwind directives: @tailwind base, components, utilities
   - CSS Variables shadcn/ui (--background, --foreground, --card, --card-foreground, etc)
   - Usar tema padrão slate do shadcn/ui
   - Variáveis para light e dark mode (.dark)

3. **src/app/page.tsx:**
   - Página inicial temporária com título "Sistema Gestão ML"
   - Breve descrição
   - Lista de links para futuras páginas:
     - /produtos
     - /vendas
     - /simulacao
     - /lixeira
     - /configuracoes
   - Usar componentes HTML simples (não shadcn ainda)

**Regras de Negócio:**

- Usar fonte Inter (Google Fonts)
- Tema baseColor: slate (configurado em components.json)
- cssVariables: true para customização

**NÃO IMPLEMENTE:**

❌ Navbar completa (será em Prompt 1.1)
❌ Componentes shadcn/ui (instalar antes com CLI)
❌ Lógica de autenticação (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/layout.tsx`
- **Criar:** `src/app/globals.css`
- **Criar:** `src/app/page.tsx`
- **Referência:** `tailwind.config.ts` (já configurado)

**Validações antes de executar:**

□ tailwind.config.ts existe
□ postcss.config.js existe
□ pnpm dev funciona

**Critérios de aceite:**

- [ ] pnpm dev inicia sem erros
- [ ] Página abre em http://localhost:3000
- [ ] Estilos Tailwind funcionam
- [ ] Font Inter carrega
- [ ] Links são clicáveis (mesmo sem destino ainda)

---

## PHASE 1: SETUP INICIAL E CADASTRO

### Prompt 1.1: Navbar e Navegação

**Contexto:** Criar barra de navegação principal com links para todas as páginas.

**Implementação:**

Criar componente `src/components/Navbar.tsx`:

- Logo/Título "Sistema ML" à esquerda
- Links de navegação:
  - Dashboard (/)
  - Produtos (/produtos)
  - Vendas (/vendas)
  - Simulação (/simulacao)
  - Lixeira (/lixeira)
  - Configurações (/configuracoes)
- Destacar link ativo usando usePathname()
- Responsivo: menu hambúrguer em mobile
- Usar componentes HTML + Tailwind (ou shadcn/ui NavigationMenu se instalado)

Integrar no `src/app/layout.tsx`:
- Importar e renderizar <Navbar /> antes de {children}

**Props/Parâmetros:**

Navbar (sem props):
- Componente client-side ("use client")
- Usar next/link para navegação
- usePathname() para link ativo

**Regras de Negócio:**

- Link ativo deve ter visual diferenciado
- Mobile: menu collapse em telas < 768px

**NÃO IMPLEMENTE:**

❌ Dropdown de usuário (não há auth)
❌ Notificações (não está no escopo)
❌ Breadcrumbs (desnecessário para app simples)

**Arquivos:**

- **Criar:** `src/components/Navbar.tsx`
- **Modificar:** `src/app/layout.tsx` (adicionar <Navbar />)

**Validações antes de executar:**

□ Layout base existe (Prompt 0.4)
□ Links funcionam com next/link

**Critérios de aceite:**

- [ ] Navbar renderiza em todas as páginas
- [ ] Links navegam corretamente
- [ ] Link ativo destacado
- [ ] Responsivo em mobile

---

### Prompt 1.2: API Route - Produtos (GET/POST)

**Contexto:** Implementar endpoints para listar e criar produtos.

**Implementação:**

Criar `src/app/api/produtos/route.ts`:

**GET /api/produtos:**
- Query params: ?tipo=LAB ou ?tipo=PROD (obrigatório)
- Chamar getProdutos(tipo) do db-client
- Retornar JSON array de produtos

**POST /api/produtos:**
- Body: NovoProduto (nome, precoUSD, cotacao, freteTotal, quantidade, fornecedor?, tipo)
- Validar com validarProduto() do validators
- Se inválido: retornar 400 com errors
- Inserir no banco usando db.insert(produtos).values(data)
- Retornar 201 com produto criado

**Parâmetros:**

GET:
- query.tipo: 'LAB' | 'PROD' (obrigatório)
- return: 200 { produtos: Produto[] }

POST:
- body: NovoProduto
- return: 201 { produto: Produto } ou 400 { errors: string[] }

**Regras de Negócio:**

- tipo default é 'LAB' se não especificado no POST
- Todos campos numéricos devem ser > 0 exceto fornecedor (opcional)
- Auto-generate timestamps: createdAt, updatedAt

**NÃO IMPLEMENTE:**

❌ Atualização de produtos (será no Prompt 1.4)
❌ Soft delete (será no Prompt 1.6)
❌ Paginação (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/api/produtos/route.ts`
- **Usar:** `src/lib/db-client.ts` (getProdutos)
- **Usar:** `src/lib/validators.ts` (validarProduto)
- **Usar:** `src/db/index.ts` (db, schema)

**Validações antes de executar:**

□ db-client.ts implementado (Prompt 0.3)
□ validators.ts implementado (Prompt 0.2)
□ Database setup concluído (Prompt 0.1)

**Critérios de aceite:**

- [ ] GET /api/produtos?tipo=LAB retorna array
- [ ] POST /api/produtos cria produto
- [ ] Validações retornam 400 em caso de erro
- [ ] Timestamps são gerados automaticamente

---

### Prompt 1.3: Página Lista de Produtos

**Contexto:** Criar página para listar produtos LAB/PROD com filtros.

**Implementação:**

Criar `src/app/produtos/page.tsx`:

- Estado para tipo: 'LAB' | 'PROD' (default 'LAB')
- useEffect para fetch produtos via GET /api/produtos?tipo={tipo}
- Renderizar FilterTabs (componente a criar) para alternar LAB/PROD
- Listar produtos usando ProdutoCard (componente a criar)
- Botão "Novo Produto" que navega para /produtos/novo
- Loading state enquanto carrega
- Empty state se lista vazia

Criar `src/components/FilterTabs.tsx`:
- Dois tabs: "Simulação (LAB)" e "Produção (PROD)"
- Usar shadcn/ui Tabs se instalado, senão HTML + Tailwind
- onChange callback retorna tipo selecionado

Criar `src/components/ProdutoCard.tsx`:
- Exibir: nome, quantidade, precoUSD, cotação, badge LAB/PROD
- Botão "Editar" (navega para /produtos/[id])
- Botão "Deletar" (confirmar antes - será implementado depois)
- Botão "Migrar para PROD" (apenas se tipo=LAB, será implementado depois)
- Card visual com shadcn/ui Card ou Tailwind

**Props/Parâmetros:**

FilterTabs:
- value: 'LAB' | 'PROD' (controlled)
- onChange: (tipo: 'LAB' | 'PROD') => void

ProdutoCard:
- produto: Produto
- onEdit?: () => void
- onDelete?: () => void
- onMigrate?: () => void (opcional, só LAB)

**Regras de Negócio:**

- Lista sempre filtrada por tipo (LAB ou PROD)
- Produtos deletados não aparecem (deletedAt IS NULL no backend)
- Badge LAB = azul, PROD = verde

**NÃO IMPLEMENTE:**

❌ Funcionalidade de deletar (será Prompt 1.6)
❌ Funcionalidade de migrar (será Prompt 1.5)
❌ Paginação ou busca (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/produtos/page.tsx`
- **Criar:** `src/components/FilterTabs.tsx`
- **Criar:** `src/components/ProdutoCard.tsx`
- **Usar:** API GET /api/produtos (Prompt 1.2)

**Validações antes de executar:**

□ API /api/produtos funciona (Prompt 1.2)
□ Navbar existe (Prompt 1.1)
□ shadcn/ui instalado (ou usar Tailwind puro)

**Critérios de aceite:**

- [ ] Página /produtos renderiza
- [ ] Tabs LAB/PROD funcionam
- [ ] Lista produtos corretamente
- [ ] Cards exibem informações
- [ ] Loading state visível
- [ ] Empty state se lista vazia

---

### Prompt 1.4: Formulário de Cadastro de Produto

**Contexto:** Criar página e componente para cadastrar novo produto.

**Implementação:**

Criar `src/app/produtos/novo/page.tsx`:
- Renderizar <ProdutoForm />
- Ao submeter: POST /api/produtos
- Em sucesso: toast "Produto criado!" e redirect para /produtos
- Em erro: toast com mensagens de erro

Criar `src/components/ProdutoForm.tsx`:
- Campos:
  - nome: text, required, min 3 chars
  - precoUSD: number, required, min 0.01
  - cotacao: number, required, min 0.01 + botão "Buscar Cotação" (chama API AwesomeAPI)
  - freteTotal: number, required, min 0
  - quantidade: integer, required, min 1
  - fornecedor: text, optional
  - tipo: select 'LAB' | 'PROD', default 'LAB'
- Validação client-side antes de submit
- Usar shadcn/ui Form components (Input, Label, Button, Select) ou HTML
- Botão "Buscar Cotação" chama GET /api/cotacao e preenche campo

**Campos/Props:**

ProdutoForm:
- initialData?: Produto (para edição, opcional)
- onSubmit: (data: NovoProduto) => void
- isLoading: boolean (estado de submit)

Campos do form:
- nome: string, required, min 3, error "Nome obrigatório (mín 3 caracteres)"
- precoUSD: number, required, min 0.01, error "Preço deve ser maior que 0"
- cotacao: number, required, min 0.01, error "Cotação deve ser maior que 0"
- freteTotal: number, required, min 0, error "Frete inválido"
- quantidade: number, required, min 1, error "Quantidade deve ser maior que 0"
- fornecedor: string, optional
- tipo: 'LAB' | 'PROD', required, default 'LAB'

**Regras de Negócio:**

- Botão "Buscar Cotação" chama API AwesomeAPI e atualiza campo cotacao
- Se API falhar, permitir input manual
- Validar todos campos antes de submit

**NÃO IMPLEMENTE:**

❌ Edição de produto (será Prompt 1.7)
❌ Upload de imagens (não está no escopo)
❌ Cálculo automático de lucro (será em cenários)

**Arquivos:**

- **Criar:** `src/app/produtos/novo/page.tsx`
- **Criar:** `src/components/ProdutoForm.tsx`
- **Criar:** `src/app/api/cotacao/route.ts` (GET que chama buscarCotacaoDolar)
- **Usar:** POST /api/produtos (Prompt 1.2)
- **Usar:** `src/lib/cotacao.ts` (buscarCotacaoDolar)

**Validações antes de executar:**

□ API POST /api/produtos funciona
□ cotacao.ts implementado (Prompt 0.2)
□ shadcn/ui toast instalado

**Critérios de aceite:**

- [ ] Formulário renderiza com todos os campos
- [ ] Validações client-side funcionam
- [ ] Botão "Buscar Cotação" preenche campo
- [ ] Submit cria produto via API
- [ ] Toast de sucesso exibido
- [ ] Redirect para /produtos após sucesso

---

### Prompt 1.5: API Route - Migrar Produto LAB → PROD

**Contexto:** Implementar endpoint para copiar produto LAB para PROD.

**Implementação:**

Criar `src/app/api/produtos/migrate/route.ts`:

**POST /api/produtos/migrate:**
- Body: { produtoId: number }
- Buscar produto original (getProdutoById)
- Validar que produto é tipo='LAB' e não está deletado
- Se PROD ou deletado: retornar 400 com erro
- Criar NOVO produto com:
  - Todos dados do original
  - tipo = 'PROD'
  - id = auto increment (undefined)
  - createdAt, updatedAt = new Date()
- Produto original permanece em LAB intacto
- Retornar 201 com novo produto PROD

**Parâmetros:**

POST:
- body: { produtoId: number }
- return: 201 { produto: Produto } ou 400 { error: string }

**Regras de Negócio:**

- REGRA 1 do escopo: Produto só pode ser migrado LAB → PROD via ação explícita
- Migração é CÓPIA, não move (original permanece LAB)
- Apenas produtos ativos (deletedAt IS NULL) podem ser migrados
- Validar campos obrigatórios antes de migrar

**NÃO IMPLEMENTE:**

❌ Migração PROD → LAB (não faz sentido)
❌ Mover cenários junto (cenários ficam em LAB)
❌ Atualização em massa (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/api/produtos/migrate/route.ts`
- **Usar:** `src/lib/db-client.ts` (getProdutoById)
- **Usar:** `src/db/index.ts` (db.insert)

**Validações antes de executar:**

□ API GET/POST produtos funcionam (Prompt 1.2)
□ Validação de campos implementada

**Critérios de aceite:**

- [ ] POST /api/produtos/migrate copia produto LAB → PROD
- [ ] Original permanece em LAB
- [ ] Novo produto tem tipo='PROD'
- [ ] Erro 400 se produto não é LAB
- [ ] Timestamps são renovados

---

### Prompt 1.6: Botão Migrar e Soft Delete

**Contexto:** Adicionar funcionalidade de migrar produto e soft delete na lista.

**Implementação:**

Atualizar `src/components/ProdutoCard.tsx`:
- Adicionar onClick para onMigrate (se tipo LAB)
- Adicionar onClick para onDelete

Atualizar `src/app/produtos/page.tsx`:
- Implementar handleMigrate(produtoId):
  - Confirmar com dialog "Migrar produto para PROD?"
  - POST /api/produtos/migrate com { produtoId }
  - Toast de sucesso/erro
  - Recarregar lista (refetch)
- Implementar handleDelete(produtoId):
  - Usar componente DeleteConfirmDialog
  - PATCH /api/produtos/[id] com { deletedAt: new Date() }
  - Toast "Produto movido para lixeira"
  - Recarregar lista

Criar `src/components/DeleteConfirmDialog.tsx`:
- Props: isOpen, onConfirm, onCancel, title, description
- Usar shadcn/ui AlertDialog
- Botões: Cancelar (secondary) e Deletar (destructive)

Criar `src/app/api/produtos/[id]/route.ts`:
- PATCH /api/produtos/[id]: atualizar produto (incluindo soft delete)
- GET /api/produtos/[id]: buscar produto por ID

**Props/Parâmetros:**

DeleteConfirmDialog:
- isOpen: boolean
- onConfirm: () => void
- onCancel: () => void
- title: string (ex: "Tem certeza?")
- description: string (ex: "Produto será movido para lixeira")

PATCH /api/produtos/[id]:
- params: { id: string }
- body: Partial<Produto>
- return: 200 { produto: Produto } ou 404

**Regras de Negócio:**

- REGRA 1: Migração copia produto LAB → PROD
- REGRA 5: Soft delete (deletedAt = timestamp)
- Confirmar antes de deletar (dialog)
- Recarregar lista após ações

**NÃO IMPLEMENTE:**

❌ Delete permanente (apenas soft delete)
❌ Migração em massa (não está no escopo)
❌ Undo de ações (não está no escopo)

**Arquivos:**

- **Modificar:** `src/components/ProdutoCard.tsx`
- **Modificar:** `src/app/produtos/page.tsx`
- **Criar:** `src/components/DeleteConfirmDialog.tsx`
- **Criar:** `src/app/api/produtos/[id]/route.ts`
- **Usar:** POST /api/produtos/migrate (Prompt 1.5)

**Validações antes de executar:**

□ API migrate implementada (Prompt 1.5)
□ shadcn/ui AlertDialog instalado

**Critérios de aceite:**

- [ ] Botão "Migrar" aparece apenas em LAB
- [ ] Dialog de confirmação funciona
- [ ] Migração cria novo PROD e mantém LAB
- [ ] Soft delete move para lixeira
- [ ] Lista recarrega após ações
- [ ] Toasts informativos exibidos

---

### Prompt 1.7: Edição de Produto

**Contexto:** Implementar página de edição de produto existente.

**Implementação:**

Criar `src/app/produtos/[id]/page.tsx`:
- useParams para obter id
- useEffect para fetch produto via GET /api/produtos/[id]
- Renderizar <ProdutoForm initialData={produto} />
- Ao submeter: PATCH /api/produtos/[id]
- Em sucesso: toast "Produto atualizado!" e redirect para /produtos
- Em erro: toast com erro

Atualizar `src/components/ProdutoForm.tsx`:
- Se initialData fornecido: preencher campos
- Botão "Salvar" (se edit) ou "Criar" (se new)
- Manter validações

Completar `src/app/api/produtos/[id]/route.ts`:
- GET: retornar produto por ID (já iniciado no Prompt 1.6)
- PATCH: atualizar campos fornecidos (partial update)
- Validar dados antes de atualizar
- Atualizar updatedAt automaticamente

**Parâmetros:**

GET /api/produtos/[id]:
- params: { id: string }
- return: 200 { produto: Produto } ou 404

PATCH /api/produtos/[id]:
- params: { id: string }
- body: Partial<NovoProduto>
- return: 200 { produto: Produto } ou 400/404

**Regras de Negócio:**

- Não permitir editar campo tipo (LAB/PROD) após criação
- Validar campos editados
- Atualizar updatedAt automaticamente

**NÃO IMPLEMENTE:**

❌ Histórico de edições (não está no escopo)
❌ Controle de versão (não está no escopo)
❌ Edição em massa (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/produtos/[id]/page.tsx`
- **Modificar:** `src/components/ProdutoForm.tsx` (suportar initialData)
- **Completar:** `src/app/api/produtos/[id]/route.ts`

**Validações antes de executar:**

□ ProdutoForm existe (Prompt 1.4)
□ API PATCH iniciada (Prompt 1.6)

**Critérios de aceite:**

- [ ] Página /produtos/[id] carrega produto
- [ ] Formulário preenche com dados existentes
- [ ] Edição salva via PATCH
- [ ] updatedAt atualizado
- [ ] Redirect após sucesso
- [ ] Validações funcionam

---

### Prompt 1.8: Página Lixeira e Restauração

**Contexto:** Implementar página de lixeira com produtos deletados e restauração.

**Implementação:**

Criar `src/app/lixeira/page.tsx`:
- Fetch produtos deletados via GET /api/produtos/lixeira
- Renderizar <LixeiraList produtos={produtos} />
- Empty state se lista vazia ("Lixeira vazia")

Criar `src/components/LixeiraList.tsx`:
- Tabela com colunas: Nome, Tipo, Deletado em, Ações
- Botão "Restaurar" por linha
- Botão "Deletar Permanente" por linha (confirmar antes)
- Usar shadcn/ui Table

Criar `src/app/api/produtos/lixeira/route.ts`:
- GET /api/produtos/lixeira: retorna produtos com deletedAt NOT NULL
- Ordenar por deletedAt DESC

Criar `src/app/api/produtos/restore/route.ts`:
- POST /api/produtos/restore: restaurar produto
- Body: { produtoId: number }
- Se tipo='LAB': deletedAt = null (restaura em LAB)
- Se tipo='PROD': deletedAt = null E tipo = 'LAB' (move para LAB)
- Retornar 200 com produto restaurado

**Campos/Props:**

LixeiraList:
- produtos: Produto[]
- onRestore: (produtoId: number) => void
- onDeletePermanent: (produtoId: number) => void

POST /api/produtos/restore:
- body: { produtoId: number }
- return: 200 { produto: Produto } ou 404

**Regras de Negócio:**

- REGRA 5: LAB restaurado = LAB, PROD restaurado = LAB
- Soft delete permite restauração
- Delete permanente requer confirmação dupla
- Lixeira mostra timestamp de quando foi deletado

**NÃO IMPLEMENTE:**

❌ Limpeza automática da lixeira (não está no escopo)
❌ Restauração em massa (não está no escopo)
❌ Limite de tempo para restauração (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/lixeira/page.tsx`
- **Criar:** `src/components/LixeiraList.tsx`
- **Criar:** `src/app/api/produtos/lixeira/route.ts`
- **Criar:** `src/app/api/produtos/restore/route.ts`

**Validações antes de executar:**

□ Soft delete funcionando (Prompt 1.6)
□ shadcn/ui Table instalado

**Critérios de aceite:**

- [ ] Página /lixeira lista produtos deletados
- [ ] Botão "Restaurar" funciona (LAB → LAB, PROD → LAB)
- [ ] Timestamp de deleção exibido
- [ ] Empty state se lista vazia
- [ ] Confirmação antes de delete permanente

---

## PHASE 2: SIMULAÇÃO DE CENÁRIOS

### Prompt 2.1: API Routes - Cenários

**Contexto:** Implementar endpoints para criar e gerenciar cenários de simulação.

**Implementação:**

Criar `src/app/api/cenarios/route.ts`:

**GET /api/cenarios:**
- Query: ?produtoId=X (obrigatório)
- Chamar getCenariosByProdutoId(produtoId)
- Retornar array de cenários

**POST /api/cenarios:**
- Body: NovoCenario (sem lucros calculados)
- Buscar produto para obter custoTotal
- Calcular lucroClassico usando calculators.ts
- Calcular lucroPremium usando calculators.ts
- Validar com validarCenario()
- Inserir cenário com lucros calculados
- Retornar 201 com cenário criado

Criar `src/app/api/cenarios/[id]/route.ts`:

**PATCH /api/cenarios/[id]:**
- Body: Partial<Cenario>
- Recalcular lucros se preços mudaram
- Atualizar no banco
- Retornar 200 com cenário atualizado

**DELETE /api/cenarios/[id]:**
- Deletar cenário permanente (não soft delete)
- Retornar 204

**Parâmetros:**

GET /api/cenarios:
- query.produtoId: number (obrigatório)
- return: 200 { cenarios: Cenario[] }

POST /api/cenarios:
- body: Omit<NovoCenario, 'lucroClassico' | 'lucroPremium'>
- return: 201 { cenario: Cenario }

**Regras de Negócio:**

- REGRA 3: Produto pode ter múltiplos cenários
- Lucros calculados automaticamente no backend
- Fórmulas:
  - custoTotal do produto
  - taxaClassico = precoVendaClassico * (taxaClassico %)
  - taxaPremium = precoVendaPremium * (taxaPremium %)
  - lucroClassico = precoVendaClassico + freteCobrado - custoTotal - taxaClassico
  - lucroPremium = precoVendaPremium + freteCobrado - custoTotal - taxaPremium

**NÃO IMPLEMENTE:**

❌ Cenários para produtos PROD (apenas LAB)
❌ Comparação entre cenários (pode ser UI depois)
❌ Exportação de cenários (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/api/cenarios/route.ts`
- **Criar:** `src/app/api/cenarios/[id]/route.ts`
- **Usar:** `src/lib/calculators.ts` (calcularLucro, calcularTaxaML)
- **Usar:** `src/lib/db-client.ts` (getCenariosByProdutoId)

**Validações antes de executar:**

□ calculators.ts implementado (Prompt 0.2)
□ validators.ts implementado (Prompt 0.2)
□ Database schema tem tabela cenarios

**Critérios de aceite:**

- [ ] GET /api/cenarios?produtoId=X retorna array
- [ ] POST /api/cenarios cria e calcula lucros
- [ ] PATCH recalcula lucros se necessário
- [ ] DELETE remove cenário
- [ ] Fórmulas de lucro corretas

---

### Prompt 2.2: Página Simulação de Cenários

**Contexto:** Criar página para visualizar e gerenciar cenários de produtos LAB.

**Implementação:**

Criar `src/app/simulacao/page.tsx`:
- Select para escolher produto LAB (fetch via GET /api/produtos?tipo=LAB)
- Ao selecionar produto: fetch cenários via GET /api/cenarios?produtoId=X
- Renderizar lista de <CenarioCard /> (colapsados por padrão)
- Botão "Novo Cenário" abre modal/form
- Empty state se nenhum produto selecionado ou sem cenários

Criar `src/components/CenarioCard.tsx`:
- Collapsible card (usar shadcn/ui Collapsible)
- Header: nome do cenário (colapsado)
- Content (expandido):
  - Preço Clássico, Taxa, Lucro
  - Preço Premium, Taxa, Lucro
  - Frete cobrado
  - Botão "Editar"
  - Botão "Deletar"
- Cores: lucro positivo = verde, negativo = vermelho

Criar `src/components/CenarioForm.tsx`:
- Campos:
  - nome: text, required
  - precoVendaClassico: number, required, > 0
  - precoVendaPremium: number, required, > 0
  - freteCobrado: number, default 0
- Calcular lucros em tempo real (onChange)
- Submit via POST /api/cenarios ou PATCH
- Usar taxas do config global

**Props/Parâmetros:**

CenarioCard:
- cenario: Cenario
- onEdit: (cenarioId: number) => void
- onDelete: (cenarioId: number) => void

CenarioForm:
- produtoId: number (required)
- initialData?: Cenario (para edição)
- onSubmit: (data) => void
- onCancel: () => void

**Regras de Negócio:**

- REGRA 3: Múltiplos cenários por produto
- REGRA 4: Taxas ML editáveis (buscar de config)
- Cenários colapsados por padrão
- Cálculo de lucro em tempo real

**NÃO IMPLEMENTE:**

❌ Cenários para PROD (apenas LAB)
❌ Comparação visual de cenários (não essencial)
❌ Gráficos (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/simulacao/page.tsx`
- **Criar:** `src/components/CenarioCard.tsx`
- **Criar:** `src/components/CenarioForm.tsx`
- **Usar:** GET /api/cenarios (Prompt 2.1)
- **Usar:** POST/PATCH/DELETE /api/cenarios (Prompt 2.1)

**Validações antes de executar:**

□ API cenarios implementada (Prompt 2.1)
□ shadcn/ui Collapsible instalado
□ Config global existe no banco

**Critérios de aceite:**

- [ ] Select produto LAB funciona
- [ ] Lista cenários carrega
- [ ] Cards colapsam/expandem
- [ ] Cálculo de lucro em tempo real
- [ ] Criar/editar/deletar cenários funciona
- [ ] Cores de lucro corretas (verde/vermelho)

---

## PHASE 3: GESTÃO MANUAL DE VENDAS

### Prompt 3.1: API Routes - Vendas

**Contexto:** Implementar endpoints para registrar vendas e deduzir estoque.

**Implementação:**

Criar `src/app/api/vendas/route.ts`:

**GET /api/vendas:**
- Query opcional: ?produtoId=X, ?startDate=Y, ?endDate=Z
- Chamar getVendas(filters) com join de produtos
- Retornar array de vendas com produto

**POST /api/vendas:**
- Body: NovaVenda (produtoId, quantidadeVendida, precoVenda, tipoAnuncio, freteCobrado, data)
- Buscar produto via getProdutoById
- Validar estoque: quantidade >= quantidadeVendida
- Buscar config para obter taxa (taxaClassico ou taxaPremium)
- Calcular taxaML usando calculators
- Calcular custoTotal do produto
- Calcular lucroLiquido usando calculators
- **TRANSACTION:**
  - Inserir venda com taxaML e lucroLiquido calculados
  - Atualizar estoque: UPDATE produtos SET quantidade = quantidade - quantidadeVendida
- Retornar 201 com venda criada

**Parâmetros:**

GET /api/vendas:
- query: { produtoId?: number, startDate?: string, endDate?: string }
- return: 200 { vendas: (Venda & { produto: Produto })[] }

POST /api/vendas:
- body: Omit<NovaVenda, 'taxaML' | 'lucroLiquido'>
- return: 201 { venda: Venda } ou 400/404

**Regras de Negócio:**

- REGRA 2: Venda deduz estoque automaticamente
- Validar estoque suficiente (não pode ficar negativo)
- Apenas produtos PROD podem ter vendas
- Usar TRANSACTION para garantir atomicidade
- Fórmulas:
  - custoTotal do produto
  - taxaML = precoVenda * (taxa %)
  - lucroLiquido = (precoVenda * quantidadeVendida) + freteCobrado - (custoTotal * quantidadeVendida) - taxaML

**NÃO IMPLEMENTE:**

❌ Vendas para produtos LAB (apenas PROD)
❌ Cancelamento de vendas (não está no escopo)
❌ Integração automática ML (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/api/vendas/route.ts`
- **Usar:** `src/lib/db-client.ts` (getVendas, getProdutoById)
- **Usar:** `src/lib/calculators.ts` (calcularTaxaML, calcularLucro)
- **Usar:** `src/lib/validators.ts` (validarVenda)

**Validações antes de executar:**

□ calculators.ts implementado
□ validators.ts com validarVenda
□ Config global existe no banco

**Critérios de aceite:**

- [ ] GET /api/vendas retorna array com produtos
- [ ] POST /api/vendas cria venda e deduz estoque
- [ ] Erro 400 se estoque insuficiente
- [ ] Transaction garante atomicidade
- [ ] Fórmulas de lucro corretas

---

### Prompt 3.2: Página Registro de Vendas

**Contexto:** Criar página para registrar vendas manualmente e listar histórico.

**Implementação:**

Criar `src/app/vendas/page.tsx`:
- Fetch vendas via GET /api/vendas
- Renderizar <VendaList vendas={vendas} />
- Botão "Registrar Venda" navega para /vendas/novo
- Mostrar totais: soma de vendas, soma de lucros
- Filtros opcionais: produto, data range (se tempo permitir)

Criar `src/app/vendas/novo/page.tsx`:
- Renderizar <VendaForm />
- Ao submeter: POST /api/vendas
- Em sucesso: toast "Venda registrada!" e redirect para /vendas
- Em erro: toast com erro

Criar `src/components/VendaForm.tsx`:
- Campos:
  - produtoId: select (apenas PROD com estoque > 0)
  - quantidadeVendida: number, required, min 1, max estoque do produto
  - precoVenda: number, required, > 0
  - tipoAnuncio: select ['CLASSICO', 'PREMIUM']
  - freteCobrado: number, default 0
  - data: date picker, default hoje
- Calcular taxaML e lucroLiquido em tempo real (onChange)
- Exibir preview de lucro antes de submit
- Validar estoque suficiente

Criar `src/components/VendaList.tsx`:
- Tabela com colunas: Data, Produto, Qtd, Preço, Tipo, Taxa ML, Lucro, Ações (se implementar edit)
- Ordenar por data DESC
- Usar shadcn/ui Table
- Formatação: moeda BRL, data DD/MM/YYYY

**Props/Parâmetros:**

VendaForm:
- produtos: Produto[] (lista PROD)
- onSubmit: (data: NovaVenda) => void

VendaList:
- vendas: (Venda & { produto: Produto })[]

**Regras de Negócio:**

- Apenas produtos PROD com estoque > 0
- Validar quantidade <= estoque
- Buscar taxas de config global
- Cálculo de lucro em tempo real

**NÃO IMPLEMENTE:**

❌ Edição de vendas (não está no escopo)
❌ Cancelamento de vendas (não está no escopo)
❌ Gráficos de vendas (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/vendas/page.tsx`
- **Criar:** `src/app/vendas/novo/page.tsx`
- **Criar:** `src/components/VendaForm.tsx`
- **Criar:** `src/components/VendaList.tsx`
- **Usar:** GET/POST /api/vendas (Prompt 3.1)

**Validações antes de executar:**

□ API vendas implementada (Prompt 3.1)
□ shadcn/ui Table e DatePicker instalados
□ Produtos PROD existem no banco

**Critérios de aceite:**

- [ ] Página /vendas lista vendas com produtos
- [ ] Formulário calcula lucro em tempo real
- [ ] Select mostra apenas PROD com estoque
- [ ] Validação de estoque funciona
- [ ] Venda registra e deduz estoque
- [ ] Totais exibidos corretamente
- [ ] Formatação de moeda e data corretas

---

### Prompt 3.3: Configurações Globais

**Contexto:** Criar página para editar taxas ML e cotação do dólar.

**Implementação:**

Criar `src/app/configuracoes/page.tsx`:
- Fetch config via GET /api/configuracoes
- Renderizar <ConfigForm config={config} />
- Ao submeter: PATCH /api/configuracoes
- Toast "Configurações atualizadas!"

Criar `src/components/ConfigForm.tsx`:
- Campos:
  - taxaClassico: number, required, min 0, max 100, default 11
  - taxaPremium: number, required, min 0, max 100, default 16
  - cotacaoDolar: number, optional, > 0
- Botão "Atualizar Cotação" chama GET /api/cotacao
- Exibir timestamp de última atualização da cotação
- Permitir input manual de cotação

Completar `src/app/api/configuracoes/route.ts`:
- GET /api/configuracoes: retornar config global (id=1)
- PATCH /api/configuracoes: atualizar taxas e/ou cotação
- Atualizar updatedAt automaticamente

**Props/Parâmetros:**

ConfigForm:
- config: Configuracao
- onSubmit: (data: Partial<Configuracao>) => void

GET /api/configuracoes:
- return: 200 { config: Configuracao }

PATCH /api/configuracoes:
- body: Partial<Configuracao>
- return: 200 { config: Configuracao }

**Regras de Negócio:**

- REGRA 4: Taxas ML editáveis (default 11% e 16%)
- Cotação pode ser manual ou via API
- Singleton pattern: sempre id=1
- Taxas entre 0-100%

**NÃO IMPLEMENTE:**

❌ Múltiplas configurações (singleton apenas)
❌ Histórico de taxas (não está no escopo)
❌ Atualização automática de cotação (manual apenas)

**Arquivos:**

- **Criar:** `src/app/configuracoes/page.tsx`
- **Criar:** `src/components/ConfigForm.tsx`
- **Completar:** `src/app/api/configuracoes/route.ts`
- **Usar:** GET /api/cotacao (Prompt 1.4)

**Validações antes de executar:**

□ API cotacao implementada (Prompt 1.4)
□ Config seed existe no banco (Prompt 0.1)

**Critérios de aceite:**

- [ ] Página /configuracoes carrega config
- [ ] Formulário permite editar taxas
- [ ] Botão "Atualizar Cotação" preenche campo
- [ ] Input manual de cotação funciona
- [ ] Validações de range (0-100%) funcionam
- [ ] Timestamp de atualização exibido
- [ ] Toast de sucesso após salvar

---

## PHASE FINAL: POLISH & VALIDAÇÃO

### Prompt 4.1: Error Handling Global

**Contexto:** Adicionar tratamento consistente de erros em toda aplicação.

**Implementação:**

1. Criar `src/app/error.tsx`:
   - Error boundary do Next.js
   - Exibir mensagem amigável
   - Botão "Tentar Novamente"
   - Log erro no console (dev)

2. Atualizar todas API routes:
   - Wrap em try/catch
   - Retornar status HTTP corretos: 400, 404, 500
   - Mensagens de erro descritivas
   - Log erros no servidor

3. Atualizar componentes de formulário:
   - Exibir erros de validação inline
   - Toast de erro em caso de falha de API
   - Disable botões durante submit (loading)

**Regras de Negócio:**

- Nunca expor stack trace para usuário (apenas dev)
- Mensagens de erro em português
- HTTP status apropriados

**NÃO IMPLEMENTE:**

❌ Logging externo (Sentry, etc)
❌ Retry automático (não está no escopo)
❌ Relatórios de erro (não está no escopo)

**Arquivos:**

- **Criar:** `src/app/error.tsx`
- **Modificar:** Todas API routes (adicionar try/catch)
- **Modificar:** Componentes de formulário (error states)

**Critérios de aceite:**

- [ ] Error boundary captura erros
- [ ] API routes retornam status corretos
- [ ] Mensagens de erro descritivas
- [ ] Loading states em formulários
- [ ] Toasts de erro funcionam

---

### Prompt 4.2: Loading States

**Contexto:** Adicionar estados de loading em todas operações assíncronas.

**Implementação:**

1. Criar `src/app/loading.tsx`:
   - Loading skeleton global (opcional)
   - Ou spinner simples

2. Atualizar páginas de lista:
   - Estado isLoading durante fetch
   - Skeleton cards ou spinner
   - Mensagem "Carregando..."

3. Atualizar formulários:
   - Botão submit com loading (disabled + spinner)
   - Texto "Salvando..." ou "Criando..."

4. Criar `src/components/LoadingSpinner.tsx`:
   - Componente reutilizável
   - Usar lucide-react Loader2 icon

**Props/Parâmetros:**

LoadingSpinner:
- size?: 'sm' | 'md' | 'lg' (default 'md')
- className?: string

**NÃO IMPLEMENTE:**

❌ Progress bar (não está no escopo)
❌ Skeleton screens complexos (manter simples)
❌ Animações elaboradas (spinner básico ok)

**Arquivos:**

- **Criar:** `src/components/LoadingSpinner.tsx`
- **Modificar:** Todas páginas de lista (loading state)
- **Modificar:** Todos formulários (submit loading)
- **Opcional:** `src/app/loading.tsx`

**Critérios de aceite:**

- [ ] Spinner exibido durante fetch
- [ ] Botões desabilitados durante submit
- [ ] Texto "Carregando..." visível
- [ ] Loading não bloqueia UI desnecessariamente

---

### Prompt 4.3: Empty States

**Contexto:** Adicionar empty states em listas vazias.

**Implementação:**

Criar componente `src/components/EmptyState.tsx`:
- Props: title, description, icon?, action?
- Visual amigável (ícone, texto centralizado)
- Botão de ação opcional (ex: "Criar Produto")

Atualizar páginas de lista:
- `/produtos`: "Nenhum produto cadastrado. Crie seu primeiro produto!"
- `/vendas`: "Nenhuma venda registrada ainda."
- `/simulacao`: "Selecione um produto para ver cenários."
- `/lixeira`: "A lixeira está vazia."

**Props/Parâmetros:**

EmptyState:
- title: string
- description: string
- icon?: React.ReactNode (lucide-react icon)
- action?: { label: string, onClick: () => void }

**NÃO IMPLEMENTE:**

❌ Onboarding complexo (manter simples)
❌ Tutorial interativo (não está no escopo)
❌ Animações elaboradas (manter clean)

**Arquivos:**

- **Criar:** `src/components/EmptyState.tsx`
- **Modificar:** Todas páginas de lista (empty states)

**Critérios de aceite:**

- [ ] Empty state visível quando lista vazia
- [ ] Mensagens descritivas e amigáveis
- [ ] Botão de ação funciona (se aplicável)
- [ ] Visual limpo e centralizado

---

### Prompt 4.4: Validação Final e Testes Manuais

**Contexto:** Verificar todos critérios de aceite do escopo.md e testar fluxos principais.

**Checklist de Funcionalidades:**

- [ ] Cadastro de produto funcionando
- [ ] Auto-refresh após criar/editar/deletar
- [ ] Soft delete e restauração funcionando
- [ ] Migração LAB→PROD copia produto (mantém original)
- [ ] Simulação de cenários testável
- [ ] Registro de venda deduz estoque
- [ ] Todos campos obrigatórios validados
- [ ] Mensagens de erro adequadas

**Checklist de UX:**

- [ ] Interface intuitiva
- [ ] Responsivo em mobile
- [ ] Loading states visíveis
- [ ] Empty states funcionando
- [ ] Operações rápidas (<200ms no local)

**Checklist Técnico:**

- [ ] Código sem erros TypeScript
- [ ] Drizzle ORM funcionando corretamente
- [ ] Banco SQLite criado e populado
- [ ] Sistema funciona 100% offline (após setup)
- [ ] pnpm dev inicia sem erros
- [ ] pnpm build completa sem erros

**Fluxos de Teste Manual:**

1. **Fluxo Produto LAB → PROD:**
   - Criar produto LAB
   - Criar cenários para produto
   - Migrar para PROD
   - Verificar que LAB permanece intacto
   - Registrar venda do produto PROD
   - Verificar dedução de estoque

2. **Fluxo Lixeira:**
   - Deletar produto LAB
   - Verificar na lixeira
   - Restaurar produto (deve voltar como LAB)
   - Deletar produto PROD
   - Restaurar produto (deve voltar como LAB)

3. **Fluxo Configurações:**
   - Atualizar taxas ML
   - Atualizar cotação via API
   - Criar produto com nova cotação
   - Verificar cálculos usam taxas atualizadas

**Correções:**

Se encontrar bugs durante testes:
- Documentar o bug
- Corrigir antes de prosseguir
- Re-testar fluxo completo

**NÃO IMPLEMENTE:**

❌ Testes automatizados (não está no escopo)
❌ CI/CD (não está no escopo)
❌ Deploy em produção (app desktop local)

**Arquivos:**

- **Verificar:** Todos arquivos criados
- **Testar:** Todas features implementadas

**Critérios de aceite:**

- [ ] Todos checkboxes do escopo marcados
- [ ] Fluxos principais testados manualmente
- [ ] Sem erros TypeScript
- [ ] Build de produção funciona
- [ ] Performance adequada (<200ms)

---

## RESUMO DA EXECUÇÃO

**Total de prompts gerados:** 18  
**Fases:** 4 (Setup Base, Cadastro, Simulação, Vendas, Polish)  
**Features implementadas:** 9 principais

**Ordem de execução:**
1. Execute prompts em ordem numérica (0.1 → 4.4)
2. Valide cada um antes de avançar (checklist de critérios)
3. Se encontrar erro, corrija antes de prosseguir
4. Mantenha Cursor Rules ativas durante toda execução
5. Faça commits git após cada fase concluída

**Dependências de instalação shadcn/ui:**
Antes de iniciar, instale os componentes necessários:
```bash
npx shadcn@latest add button input label card dialog select table tabs toast
```

**Estimativa de tempo:**
- Phase 0: 2-3 horas
- Phase 1: 6-8 horas
- Phase 2: 3-4 horas
- Phase 3: 4-5 horas
- Phase Final: 2-3 horas
**Total:** 17-23 horas (~3-4 dias)

**Próximos passos após conclusão:**
1. Teste completo do sistema
2. Ajustes de UX/polimento
3. Documentação de uso (README)
4. Preparar para instalação local

---

**FIM DOS MICRO-PROMPTS**
