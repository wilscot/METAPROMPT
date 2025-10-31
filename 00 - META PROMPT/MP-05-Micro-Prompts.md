# 05 - MICRO-PROMPTS

**COMO USAR:**
1. Abra Claude Web
2. Anexe seu `@escopo.md`
3. Cole este prompt completo
4. Claude gera 1 artifact com TODOS os micro-prompts numerados
5. **NÃO copie tudo de uma vez!**
6. Copie e cole **UM micro-prompt por vez** no Cursor Chat
7. Valide cada feature implementada antes de avançar
8. Repita até completar todos os prompts

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

GERE O ARTIFACT:

Título: "Micro-Prompts de Implementação (Cole 1 por vez no Cursor)"

ESTRUTURA:

```markdown
# MICRO-PROMPTS DE IMPLEMENTAÇÃO

**INSTRUÇÕES:**
- Cole apenas UM prompt por vez no Cursor Chat
- Aguarde implementação completa
- Valide funcionamento
- Só então avance para o próximo

Total de prompts: [X]
Estimativa: [Y horas/dias]

---

## PHASE 1: [NOME DA FASE]

### Prompt 1.1: [Nome Descritivo da Feature]

**Contexto:** [1 frase sobre o que vai ser construído]

**Implementação:**

[Especificação COMPLETA e DETALHADA:]
- O que criar
- Comportamentos esperados
- Validações necessárias
- Estados a gerenciar
- Integrações com outros arquivos

**Campos/Props/Parâmetros:**

[Para componentes:]
- prop1: tipo (propósito, valores válidos)
- prop2: tipo (comportamento, validação)

[Para funções:]
- param1: tipo (descrição, validação)
- return: tipo (formato esperado)

[Para forms/inputs:]
- field1: tipo, required, validation rules, error messages
- field2: tipo, optional, default value, format

**Regras de Negócio:**

[Listar regras específicas aplicáveis do escopo.md]
- Regra 1: [descrição]
- Regra 2: [fórmula ou lógica]
- Validação: [condições]

**NÃO IMPLEMENTE:**

❌ [Feature X - não foi pedida]
❌ [Funcionalidade Y - será feita no prompt 2.3]
❌ [Otimização Z - deixar para fase de polish]

[Previne feature creep e implementações fora de escopo]

**Arquivos:**

- **Criar:** `@src/components/NewComponent.tsx` (propósito específico)
- **Modificar:** `@src/app/page.tsx` (adicionar import e uso)
- **Usar:** `@src/lib/api.ts` (já existe, usar função X)

**Validações antes de executar:**

□ Confirmar que arquivos mencionados em "Usar" existem
□ Verificar se dependências necessárias estão instaladas
□ Revisar regras de negócio aplicáveis

**Critérios de aceite:**

- [ ] [Comportamento 1 funciona corretamente]
- [ ] [Validação 2 está ativa]
- [ ] [UI 3 renderiza como esperado]
- [ ] [Erro 4 é tratado adequadamente]

---

### Prompt 1.2: [Próxima Feature]

[Mesma estrutura]

---

## PHASE 2: [NOME DA FASE]

### Prompt 2.1: [Feature]

[Mesma estrutura]

---

## PHASE 3: [NOME DA FASE]

[Continue para todas as fases]

---

## PHASE FINAL: POLISH & VALIDAÇÃO

### Prompt X.1: Error Handling Completo

**Contexto:** Adicionar tratamento de erro consistente em todo o app

**Implementação:**
[...]

### Prompt X.2: Loading States

**Contexto:** Adicionar estados de loading em operações assíncronas

**Implementação:**
[...]

### Prompt X.3: Validação Final

**Contexto:** Verificar critérios de aceite do escopo.md

**Checklist:**
- [ ] [Critério 1 da seção 11 do escopo]
- [ ] [Critério 2 da seção 11 do escopo]
- [ ] [Todos os checkboxes do escopo verificados]

---

## RESUMO DA EXECUÇÃO

Total de prompts gerados: [X]
Fases: [Y]
Features implementadas: [Z]

**Ordem de execução:**
1. Execute prompts em ordem numérica
2. Valide cada um antes de avançar
3. Se encontrar erro, corrija antes de prosseguir
4. Mantenha Cursor Rules ativas durante toda execução
```

REGRAS PARA CADA MICRO-PROMPT:

1. **Auto-contido:** Toda informação necessária dentro do prompt
2. **Específico:** Detalhes técnicos completos, não genéricos
3. **Validável:** Critérios claros de sucesso
4. **Limitado:** Escopo bem definido, lista o que NÃO fazer
5. **Referências:** Mencionar arquivos por @path quando necessário
6. **Sequencial:** Assumir que prompts anteriores foram completados

ADAPTAÇÃO AO ESCOPO:

- Extrair regras de negócio da seção 5 do escopo
- Usar estrutura de dados da seção 8 do escopo
- Mapear casos de uso da seção 9 do escopo
- Implementar validações da seção 10 do escopo
- Verificar critérios da seção 11 do escopo

QUALIDADE:

Cada prompt deve ser tão detalhado que:
- IA não precisa fazer perguntas
- IA não precisa explorar código
- IA não precisa deduzir comportamentos
- Resultado seja previsível e correto
```
