# 04 - ESTRUTURA DE CÓDIGO

**COMO USAR:**
1. Abra Claude Web
2. Anexe seu `@escopo.md`
3. Cole este prompt completo
4. Claude gera 1 artifact com prompt para Cursor
5. Copie e cole no Cursor Chat
6. Valide contando arquivos criados: `find src -name "*.tsx" -o -name "*.ts" | wc -l`
7. Avance para `05-micro-prompts.md`

---

```
Analise o @escopo.md e gere UM ÚNICO artifact contendo um prompt para criar todos os arquivos de código VAZIOS (apenas com comentários TODO).

ANÁLISE DE ARQUIVOS NECESSÁRIOS:

Baseado em:
- Tech stack (React/Next.js/Express/etc)
- Features listadas no escopo
- Estrutura de dados
- Casos de uso

Determinar:
- Quantos componentes UI necessários
- Quantas rotas/páginas necessárias
- Quantos arquivos de lógica/utils necessários
- Quantos arquivos de tipos/interfaces necessários

IMPORTANTE:
- Arquivos VAZIOS (só comentários TODO)
- NÃO implementar código ainda
- Propósito: criar skeleton para preencher depois
- Comentários TODO devem indicar o que vai no arquivo

---

GERE O ARTIFACT:

Título: "Prompt para Cursor: Criar Estrutura de Código (arquivos vazios)"

ESTRUTURA DO PROMPT:

```
Crie os seguintes arquivos com comentários TODO (SEM implementação):

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: src/app/layout.tsx

// TODO: Root layout component
// - Configure metadata
// - Import globals.css
// - Setup providers if needed

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: src/app/page.tsx

// TODO: Main landing page
// - Import Hero component
// - Import FeatureList component
// - Handle initial state

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: src/components/Hero.tsx

// TODO: Hero section component
// - Accept title and subtitle props
// - Render CTA button
// - Responsive design

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: src/lib/api.ts

// TODO: API client functions
// - fetchUsers()
// - createUser(data)
// - updateUser(id, data)
// - Handle errors

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: src/types/user.ts

// TODO: User type definitions
// - User interface
// - CreateUserDTO
// - UpdateUserDTO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[... continuar para TODOS os arquivos necessários baseados no escopo]

VALIDAÇÃO:
find src -name "*.tsx" -o -name "*.ts" | wc -l
# Expected: [X] files

cat src/app/layout.tsx
# Should show TODO comment, no implementation

ls src/components/
# Should list all component files

Confirme que todos os arquivos foram criados vazios.
```

REGRAS PARA GERAÇÃO:
- Mapear TODAS as features do escopo em arquivos
- Um arquivo por componente/função principal
- Seguir convenções do framework (Next.js App Router, etc)
- Incluir arquivos de tipos se TypeScript
- Incluir arquivos de estilos se necessário (globals.css, etc)

GRANULARIDADE:
- Componentes UI: 1 arquivo por componente
- Pages/Routes: 1 arquivo por rota
- API: 1 arquivo por grupo de endpoints relacionados
- Utils: 1 arquivo por categoria de helpers
- Types: 1 arquivo por domínio/entidade
```
