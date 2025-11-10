# 01 - ESTRUTURA DE PASTAS

**COMO USAR:**
1. Abra Claude Web
2. Anexe seu `@escopo.md`
3. Cole este prompt completo
4. Claude gera 1 artifact com prompt para Cursor
5. Copie e cole no Cursor Chat
6. Valide com `tree` ou `ls -R`
7. Avance para `02-configuracoes.md`

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

Analise o @escopo.md e gere UM ÚNICO artifact contendo um prompt para criar a estrutura de pastas vazia.

ANÁLISE DO TECH STACK:
- Framework: [detectar do escopo]
- Tipo de projeto: [web/mobile/desktop/cli/backend]
- Estrutura adequada: [Next.js App Router / React SPA / Express API / etc]

REGRAS:
- Pastas VAZIAS apenas (sem arquivos ainda)
- Estrutura adequada ao tech stack detectado
- Incluir .cursor/rules/ (já criado no passo anterior)
- Incluir docs/ se houver database ou APIs externas

---

GERE O ARTIFACT:

Título: "Prompt para Cursor: Criar Estrutura de Pastas"

Conteúdo: Um prompt que cria toda estrutura de pastas usando comandos bash.

EXEMPLO DE ESTRUTURA (adaptar ao tech stack):

Para Next.js:
```
project-root/
├── .cursor/rules/     (já existe)
├── src/
│   ├── app/
│   ├── components/
│   ├── lib/
│   └── api/
├── docs/              (se aplicável)
└── public/
```

Para Express:
```
project-root/
├── .cursor/rules/     (já existe)
├── src/
│   ├── routes/
│   ├── controllers/
│   ├── models/
│   ├── middleware/
│   └── utils/
└── docs/              (se aplicável)
```

FORMATO DO PROMPT:
```
Crie a seguinte estrutura de pastas vazias:

mkdir -p src/app src/components src/lib
mkdir -p public docs
[... todos os comandos necessários]

VALIDAÇÃO:
tree -L 3
# ou
ls -R

Confirme que todas as pastas foram criadas.
```

O artifact deve ser executável diretamente no Cursor.
```
