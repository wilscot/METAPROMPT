# 05 - MICRO-PROMPTS

**COMO USAR:**

1. Abra Claude Web

2. Anexe seu `@escopo.md`

3. Cole este prompt completo

4. Claude analisa o escopo, agrupa features em sub-fases e mostra o plano

5. Claude gera **1 artifact por fase** (nao tudo junto!)

6. **NAO copie tudo de uma vez!**

7. Copie **UM prompt por vez** (cada um esta em caixa unica copiavel)

8. Cole no Cursor Chat

9. Valide cada feature implementada antes de avancar

10. Repita ate completar todos os prompts da fase atual

11. Quando terminar uma fase, peca para Claude gerar a proxima fase

---

```

**PASSO 1: ANALISAR FASES AUTOMATICAMENTE**

REGRA DE AUTONOMIA: NAO pergunte ao usuario a menos que exista uma ambiguidade REAL no escopo.md que impeca voce de prosseguir (ex: duas secoes contraditorias, feature mencionada mas sem detalhamento nenhum). Se a informacao esta no escopo, mesmo que resumida, USE-A e tome a decisao voce mesmo. Nunca pergunte por "educacao" ou para "confirmar" algo que ja esta claro.

Analise o @escopo.md e determine voce mesmo a divisao em fases:

1. Leia a secao "Funcionalidades" (ou equivalente) do escopo
2. Identifique TODAS as features listadas
3. Agrupe-as em sub-fases logicas seguindo esta ordem:
   - Fase 1: Setup/Infra (banco, auth, config base, libs compartilhadas)
   - Fase 2: Core/Backend (models, API routes, logica de negocio)
   - Fase 3: Frontend (paginas, componentes, formularios)
   - Fase 4: Integracoes/Polish (APIs externas, otimizacoes, ajustes finais)
4. Se o escopo tiver apenas 1 fase (ex: MVP), DIVIDA as features em sub-fases conforme acima
5. Se o escopo ja tiver multiplas fases definidas, respeite a divisao do escopo e aplique a sub-divisao dentro de cada fase se necessario
6. Cada sub-fase deve ter no MAXIMO 4-6 prompts (se tiver mais, quebre em sub-fases menores)
7. Features do roadmap/futuro que NAO tenham detalhamento completo devem ser IGNORADAS (nao gere prompts para elas)

Apresente o plano de fases ANTES de gerar os prompts:

```
PLANO DE FASES IDENTIFICADO:
- Fase 1: [nome] ([N] prompts) - [lista resumida de features]
- Fase 2: [nome] ([N] prompts) - [lista resumida de features]
- Fase 3: [nome] ([N] prompts) - [lista resumida de features]
- ...
Total: [X] fases, [Y] prompts

[SE houver features ignoradas por falta de detalhamento:]
IGNORADAS (sem detalhamento suficiente): [lista]
```

Depois do plano, gere IMEDIATAMENTE o artifact da Fase 1. NAO espere confirmacao.

**PASSO 2: GERAR APENAS UMA FASE POR VEZ**

Gere APENAS os prompts da PRIMEIRA FASE no artifact.

**NAO gere todas as fases de uma vez!**

Apos o usuario completar todos os prompts da Fase 1, ele pedira para voce gerar a Fase 2, e assim por diante.

Isso evita artifacts gigantes que serao cortados pelo context window.

---

Analise o @escopo.md e gere UM artifact contendo APENAS os micro-prompts da FASE 1 (primeira fase), organizados conforme a secao "Funcionalidades" do escopo.

ANALISE DE IMPLEMENTACAO:

1. FASES DO PROJETO:
   - Extrair da secao "Funcionalidades" do escopo
   - Agrupar em sub-fases logicas (setup -> core -> frontend -> integracoes)
   - Identificar dependencias entre features
   - Ordenar logicamente (setup -> core -> advanced -> polish)
   - Cada sub-fase com no maximo 4-6 prompts

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

[PRE-REQUISITOS]
Verificar antes de executar:
- [ ] Prompt X.Y foi executado? (este prompt depende dele)
- [ ] Componente Z existe em src/components/ui/? Se nao: instalar via [COMANDOS DE INSTALACAO]
- [ ] Tabela W existe no schema? Se nao: executar Prompt X.Y primeiro
- [ ] Arquivo @caminho/arquivo.ts existe? Se nao: executar Prompt X.Y primeiro

[COMANDOS DE INSTALACAO]
Executar ANTES de implementar (se ainda nao foi feito):
- pnpm dlx shadcn@latest add [componente]
- pnpm add [dependencia]

Se comando ja foi executado em prompt anterior, pode ignorar.

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

[INSTRUCOES DE VALIDACAO PARA A IA]

Apos implementar, voce DEVE:

1. EXECUTAR AUTOMATICAMENTE (sem pedir ao usuario):
   - pnpm run build (ou npm run build)
   - Verificar se arquivos foram criados
   - Verificar erros TypeScript
   - Listar arquivos criados/modificados

2. REPORTAR RESULTADO neste formato:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PROMPT [N.X] EXECUTADO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

O QUE FOI FEITO:
[Resumo simples em linguagem nao-tecnica - 2-3 frases]
Exemplo: "Criei a pagina de produtos com formulario para cadastrar novos itens e lista para visualizar todos os produtos cadastrados."

VALIDACOES AUTOMATICAS (executadas pela IA):
[x] ou [ ] Codigo compilou sem erros (tudo funcionando)
[x] ou [ ] Arquivos criados corretamente
[x] ou [ ] Sem erros de codigo

Se alguma falhou, explicar de forma SIMPLES (sem termos tecnicos):
Exemplo: "Erro ao compilar: faltou instalar componente X. Execute: pnpm dlx shadcn@latest add X"

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TESTE MANUAL NECESSARIO (usuario deve fazer):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

TESTE 1 - [Nome do teste]:
1. Abra o navegador em http://localhost:3000/[rota]
2. [Acao especifica - ex: Clique no botao X]
3. [Acao especifica - ex: Preencha o campo Y com "teste"]
4. ESPERADO: [O que deve aparecer na tela - descricao visual clara]

TESTE 2 - [Nome do teste]:
1. [Passos especificos com URLs completas]
2. [Acoes visuais claras]
3. ESPERADO: [Resultado visual esperado]

[Se necessario, adicionar mais testes]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RESULTADO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

TUDO OK? → Pode enviar o proximo prompt
ALGO FALHOU? → Diga qual teste falhou e o que apareceu na tela

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIM DO PROMPT [N.X]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

**REGRAS PARA O RETORNO DA IA:**

1. **Resumo simples primeiro:**
   - Sempre comece com "O QUE FOI FEITO" em linguagem nao-tecnica
   - Use termos como "criei", "adicionei", "configurei" ao inves de "implementei", "instanciei"
   - Exemplo: "Criei a pagina de login com campos de email e senha" (nao "Implementei componente de autenticacao")

2. **Validacoes automaticas:**
   - Use linguagem simples: "Codigo compilou sem erros" (nao "Build passou")
   - Nao liste caminhos tecnicos de arquivos (@src/app/...) - apenas confirme que foram criados
   - Se erro, explique de forma SIMPLES com solucao clara

3. **Testes manuais:**
   - NUNCA usar curl (usuario nao sabe interpretar retorno)
   - NUNCA pedir para interpretar erros tecnicos (CORS, stack trace, etc)
   - SEMPRE dar URL completa (http://localhost:3000/pagina)
   - SEMPRE descrever o que clicar/preencher
   - SEMPRE dizer o que DEVE aparecer na tela (ESPERADO)

4. **Console do navegador - PODE pedir, mas com instrucoes claras:**
   - Explicar como abrir: "Aperte F12, clique na aba Console"
   - Pedir verificacao simples: "Tem alguma mensagem em VERMELHO?"
   - Se tiver erro, pedir para copiar: "Se tiver texto vermelho, copie e cole aqui"
   - NAO pedir interpretacao: usuario nao sabe o que e CORS, 500, stack trace

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
# MICRO-PROMPTS DE IMPLEMENTACAO - FASE 1 - [Nome do Projeto]

**INSTRUCOES CRITICAS:**
- Cole apenas **UM** prompt por vez no Cursor Chat
- Aguarde implementacao **completa** e validacao automatica pela IA
- **Valide** funcionamento manual seguindo os testes descritos
- **NAO** avance se houver erros
- Marque cada prompt como concluido apos validado
- Quando terminar TODOS os prompts desta fase, peca para gerar a proxima fase

**Fase atual:** 1 de [X]  
**Prompts nesta fase:** [Y]  
**Estimativa:** [Z horas/dias]  
**Complexidade:** [Small/Medium/Large]

---

## PHASE 1: [NOME DA FASE] (Prompts 1.1 - 1.X)

### Prompt 1.1: [Titulo]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[PRE-REQUISITOS]
[COMANDOS DE INSTALACAO]
[CONTEXTO]
[IMPLEMENTACAO]
[ARQUIVOS ENVOLVIDOS]
[REGRAS DE NEGOCIO]
[NAO IMPLEMENTE]
[INSTRUCOES DE VALIDACAO PARA A IA]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIM DO PROMPT [1.1]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

---

### Prompt 1.2: [Titulo]

[... continuar para todos os prompts da Fase 1]

---

## RESUMO DA FASE 1

**Total de prompts gerados:** [X]  
**Features implementadas:** [Z]

**Ordem de execucao:**
1. Execute prompts em ordem numerica (1.1, 1.2, 1.3...)
2. Valide cada um antes de avancar
3. Se erro, corrija antes de prosseguir
4. Marque como concluido apos validado

**Quando terminar esta fase:**
- Verifique se todos os prompts foram executados
- Valide se todas as funcionalidades da Fase 1 estao funcionando
- Peca para gerar os prompts da Fase 2
```

---

EXEMPLO DE PROMPT BEM FORMATADO:

```
### Prompt 2.3: API Route + Pagina - Produtos LAB

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COPIE DAQUI PARA BAIXO E COLE NO CURSOR (PROMPT COMPLETO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[PRE-REQUISITOS]
Verificar antes de executar:
- [ ] Prompt 2.2 foi executado? (API route /api/produtos deve existir)
- [ ] Prompt 1.3 foi executado? (shadcn/ui deve estar instalado)
- [ ] Prompt 1.5 foi executado? (calculators.ts e validators.ts devem existir)
- [ ] Componente Dialog existe em src/components/ui/? Se nao: instalar via [COMANDOS DE INSTALACAO]
- [ ] Componente Table existe em src/components/ui/? Se nao: instalar via [COMANDOS DE INSTALACAO]

[COMANDOS DE INSTALACAO]
Executar ANTES de implementar (se ainda nao foi feito):
- pnpm dlx shadcn@latest add dialog
- pnpm dlx shadcn@latest add table
- pnpm dlx shadcn@latest add button
- pnpm dlx shadcn@latest add input
- pnpm dlx shadcn@latest add form

Se comando ja foi executado em prompt anterior, pode ignorar.

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

[INSTRUCOES DE VALIDACAO PARA A IA]

Apos implementar, voce DEVE:

1. EXECUTAR AUTOMATICAMENTE (sem pedir ao usuario):
   - pnpm run build
   - Verificar se arquivos foram criados
   - Verificar erros TypeScript
   - Listar arquivos criados/modificados

2. REPORTAR RESULTADO neste formato:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PROMPT [2.3] EXECUTADO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

O QUE FOI FEITO:
Criei a pagina de produtos LAB com formulario para cadastrar/editar produtos e lista para visualizar todos os produtos. O formulario calcula automaticamente o custo unitario enquanto voce preenche os campos.

VALIDACOES AUTOMATICAS (executadas pela IA):
[x] Codigo compilou sem erros (tudo funcionando)
[x] Arquivos criados corretamente
[x] Sem erros de codigo

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TESTE MANUAL NECESSARIO (usuario deve fazer):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

TESTE 1 - Criar novo produto:
1. Abra o navegador em http://localhost:3000/lab/produtos
2. Clique no botao "+ Novo Produto LAB"
3. ESPERADO: Deve abrir um modal (caixa flutuante) com um formulario
4. Preencha o campo "Nome" com "Produto Teste"
5. Preencha o campo "Preco USD" com "10"
6. Preencha o campo "Cotacao" com "5.5"
7. Preencha o campo "Frete Total BRL" com "100"
8. ESPERADO: Deve aparecer um badge mostrando "Custo Unit.: R$ 155,00" (calculado automaticamente)
9. Clique no botao "Salvar"
10. ESPERADO: Modal deve fechar, deve aparecer uma mensagem verde de sucesso no canto da tela, e o produto "Produto Teste" deve aparecer na lista abaixo

TESTE 2 - Verificar calculo do custo unitario:
1. Na mesma pagina http://localhost:3000/lab/produtos
2. Na lista de produtos, encontre a coluna "Custo Unit."
3. ESPERADO: Deve mostrar "R$ 155,00" para o produto criado (calculado como: 10 x 5.5 + 100 = 155)

TESTE 3 - Editar produto:
1. Na lista de produtos, clique no botao de editar (icone de lapis) ao lado do produto "Produto Teste"
2. ESPERADO: Deve abrir o modal novamente com os campos preenchidos
3. Mude o campo "Preco USD" de "10" para "20"
4. ESPERADO: O badge "Custo Unit." deve atualizar automaticamente para "R$ 210,00"
5. Clique em "Salvar"
6. ESPERADO: Modal fecha, mensagem de sucesso aparece, e na lista o custo unitario deve estar atualizado para R$ 210,00

TESTE 4 - Deletar produto:
1. Na lista de produtos, clique no botao de deletar (icone de lixeira) ao lado do produto
2. ESPERADO: Deve aparecer uma caixa de confirmacao perguntando se quer deletar
3. Clique em "Confirmar" ou "Sim"
4. ESPERADO: Mensagem de sucesso aparece e o produto desaparece da lista

TESTE 5 - Validacao de formulario:
1. Clique em "+ Novo Produto LAB"
2. Tente salvar sem preencher nenhum campo obrigatorio
3. ESPERADO: Deve aparecer mensagens de erro em vermelho abaixo dos campos vazios
4. Preencha o campo "Nome" com apenas "AB" (menos de 3 caracteres)
5. Tente salvar
6. ESPERADO: Deve aparecer erro dizendo que nome precisa ter pelo menos 3 caracteres

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RESULTADO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

TUDO OK? → Pode enviar o proximo prompt
ALGO FALHOU? → Diga qual teste falhou e o que apareceu na tela

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIM DO PROMPT [2.3]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

CHECKLIST DE QUALIDADE DE CADA PROMPT:

Antes de gerar cada prompt, verificar:

- [ ] TUDO dentro de uma unica caixa copiavel (linhas inicio/fim)
- [ ] Secao [PRE-REQUISITOS] no inicio com checkboxes de dependencias
- [ ] Secao [COMANDOS DE INSTALACAO] antes da implementacao
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
- [ ] Secao [INSTRUCOES DE VALIDACAO PARA A IA] com formato padronizado
- [ ] Secao "O QUE FOI FEITO" com resumo simples e nao-tecnico
- [ ] Validacoes automaticas com linguagem simples ("Codigo compilou" ao inves de "Build passou")
- [ ] Testes manuais com URLs completas (http://localhost:3000/rota)
- [ ] Testes manuais com acoes visuais claras (clique, preencha, etc)
- [ ] Testes manuais com ESPERADO descrito visualmente
- [ ] NUNCA usar curl nos testes manuais
- [ ] NUNCA pedir interpretacao de erros tecnicos
- [ ] NUNCA listar caminhos tecnicos de arquivos no retorno ao usuario

---

IMPORTANTE:

- Cada prompt e INDEPENDENTE (pode ser executado sozinho)
- IA do Cursor deve conseguir implementar olhando APENAS o que esta na caixa
- Zero friccao: copiar -> colar -> executar
- Zero ambiguidade: tudo especificado
- **Gere APENAS os prompts da Fase 1 neste primeiro artifact**
- **Apos o usuario completar a Fase 1, ele pedira para voce gerar a Fase 2**

GERE O ARTIFACT DA FASE 1 seguindo estas regras rigorosamente.
```