# ESC02 - GERAR ESCOPO (PARTE 2)

**QUANDO USAR:**
1. Apos completar MP-01-Gerar-Escopo-Parte1.md
2. Ter o escopo.md com secoes 1-4 geradas
3. Abra NOVO chat no Claude (context limpo)
4. Anexe o JSON da descoberta + escopo.md da Parte 1
5. Cole este prompt

**PRE-REQUISITOS:** 
- JSON completo da descoberta guiada
- escopo.md com secoes 1-4 (gerado na Parte 1)

**OUTPUT:** escopo.md completo (secoes 5-9 adicionadas)

---

```
Voce e uma IA especializada em gerar documentacao de escopo de software.

Recebi o seguinte JSON da descoberta guiada:

[COLE AQUI O JSON COMPLETO DA DESCOBERTA]

E o escopo.md parcial (secoes 1-4):

[COLE AQUI O ESCOPO.MD DA PARTE 1]

Sua tarefa: CONTINUAR o arquivo escopo.md adicionando as secoes 5 a 9.

NAO reescreva as secoes 1-4, apenas ADICIONE as novas secoes ao final.

---

## INSTRUCOES PARA A IA:

### 1. VERIFICACAO INICIAL

Confirme que o escopo.md da Parte 1 tem:
- [ ] Secao 1 - Visao Geral
- [ ] Secao 2 - Tech Stack
- [ ] Secao 3 - Interface e Identidade Visual
- [ ] Secao 4 - Estrutura de Dados

Se alguma estiver faltando, PARE e informe o usuario.

Confirme que o JSON tem:
- [ ] dados.entidades (com campos e validacoes)
- [ ] features ou funcionalidades MVP
- [ ] limitacoes ou "o que nao fazer"
- [ ] roadmap ou fases futuras
- [ ] alertas_tecnicos

---

### 2. GERAR SECAO 5 - REGRAS DE NEGOCIO E VALIDACOES

Extraia do JSON:
- Regras de negocio (se existirem no contexto)
- Validacoes de campos (de dados.entidades[].campos[].validacao)

Formato:
"""
## 5. REGRAS DE NEGOCIO E VALIDACOES

### Regras de Negocio

[Se o JSON ou contexto mencionar regras de negocio, listar:]

**Regra 1 - [Nome inferido]:**
- Descricao: [O que a regra define]
- Formula/Logica: [Se aplicavel]
- Excecoes: [Casos especiais]

[Se nao houver regras explicitas, escrever:]
**Nenhuma regra de negocio complexa identificada na descoberta.**
As validacoes de campo abaixo cobrem as restricoes do sistema.

---

### Validacoes de Campo

[Agrupar por entidade/formulario:]

**Formulario: [Entidade 1]**

| Campo | Tipo | Obrigatorio | Validacao | Mensagem Erro |
|-------|------|-------------|-----------|---------------|
[Para cada campo da entidade, preencher linha]

**Formulario: [Entidade 2]**

| Campo | Tipo | Obrigatorio | Validacao | Mensagem Erro |
|-------|------|-------------|-----------|---------------|
[Para cada campo da entidade, preencher linha]
"""

---

### 3. GERAR SECAO 6 - FUNCIONALIDADES MVP

Extraia do JSON:
- Features da Fase 1 / MVP
- Criterios de conclusao

Formato:
"""
## 6. FUNCIONALIDADES MVP (Fase 1)

### Setup Inicial
- [ ] Estrutura de pastas
- [ ] Configuracoes (package.json, tsconfig, etc)
- [ ] Database schema basico
- [ ] Autenticacao (se necessaria)

### Features Core

[Para cada feature do MVP no JSON:]

**Feature [N] - [nome]:**
- Descricao: [o que faz]
- Prioridade: [Alta / Media]
- Criterio de Aceite: [como saber que esta pronto]

---

### Criterios de Conclusao MVP

**Funcional:**
[Extrair de criterios de conclusao ou gerar baseado nas features:]
- [ ] Usuario consegue [acao principal 1]
- [ ] Usuario consegue [acao principal 2]
- [ ] Sistema resolve [problema da Visao Geral]

**Tecnico:**
- [ ] Codigo sem erros TypeScript
- [ ] Sem warnings no console
- [ ] Persistencia funcionando
- [ ] Deploy funcionando (se aplicavel)

**UX:**
- [ ] Interface intuitiva
- [ ] Loading states visiveis
- [ ] Mensagens de erro claras
- [ ] Responsivo (se aplicavel)
"""

---

### 4. GERAR SECAO 7 - O QUE NAO FAZER

Extraia do JSON:
- limitacoes.dependencias_evitar
- Features excluidas do MVP
- Preferencias negativas

Formato:
"""
## 7. O QUE NAO FAZER

### Funcionalidades Excluidas do MVP
[Listar features que foram para Fase 2+ ou backlog:]
- [Feature 1 que nao entra agora]
- [Feature 2 que nao entra agora]
- [Feature 3 que nao entra agora]

### Preferencias de Implementacao
[Se houver no JSON:]
- [Abordagem a evitar - preferir alternativa]
- [Padrao a nao seguir]

### Tecnologias a Evitar
[De limitacoes.dependencias_evitar:]
- [Tech 1 - motivo se houver]
- [Tech 2 - motivo se houver]

[Se nao houver nada especifico:]
**Nenhuma restricao adicional alem das ja definidas no Tech Stack.**
"""

---

### 5. GERAR SECAO 8 - ROADMAP

Extraia do JSON:
- Fases 2, 3+ do roadmap
- Backlog futuro

Formato:
"""
## 8. ROADMAP (Fases Futuras)

### Fase 2 - Validacao e Melhorias

**Condicao para iniciar:**
- MVP usado por usuarios reais
- Feedback coletado
- Bugs criticos corrigidos

**Features planejadas:**
[Extrair features da Fase 2:]
- [ ] [Feature 1]
- [ ] [Feature 2]
- [ ] [Feature 3]

---

### Fase 3 - Expansao

**Condicao para iniciar:**
- Fase 2 estavel
- Usuarios solicitaram proximas features

**Features planejadas:**
[Extrair features da Fase 3:]
- [ ] [Feature 1]
- [ ] [Feature 2]
- [ ] [Integracoes avancadas]

---

### Backlog Futuro (apos Fase 3)
[Extrair ideias de longo prazo:]
- [Ideia 1]
- [Ideia 2]
- [Ideia 3]

**Regra:** NAO implementar nada do backlog sem validar necessidade com usuarios.
"""

---

### 6. GERAR SECAO 9 - ALERTAS TECNICOS

Extraia do JSON:
- alertas_tecnicos
- Conflitos resolvidos
- Dependencias especiais

Formato:
"""
## 9. ALERTAS TECNICOS

### Conflitos Resolvidos na Descoberta

[Para cada alerta/conflito no JSON:]

**[Titulo do Conflito]:**
- Problema original: [Descrever o que foi detectado]
- Solucao escolhida: [O que foi decidido]
- Justificativa: [Por que essa escolha]

---

### Dependencias com Requisitos Especiais

[Se houver dependencias nativas mencionadas:]

| Biblioteca | Proposito | Requisito | Alternativa JS |
|------------|-----------|-----------|----------------|
| [lib] | [para que] | [o que precisa] | [alternativa] |

[Se nao houver:]
**Nenhuma dependencia nativa identificada. Projeto usa apenas bibliotecas JavaScript puras.**

---

### Lembretes Importantes

[Extrair lembretes relevantes dos alertas:]
- [Lembrete 1 - ex: Railway filesystem e efemero]
- [Lembrete 2 - ex: Usar cloud storage para uploads]
- [Lembrete 3]

[Se nao houver alertas especificos:]
- Seguir Tech Stack definido na Secao 2
- Usar ferramentas pre-aprovadas quando possivel
"""

---

### 7. ADICIONAR CHECKLIST FINAL

Apos as 9 secoes, adicionar:

"""
---

## CHECKLIST DE VALIDACAO

**Antes de usar nos Meta-Prompts, verificar:**

- [ ] Secao 1 (Visao Geral) completa
- [ ] Secao 2 (Tech Stack) com todas decisoes
- [ ] Secao 3 (Interface) com telas e identidade visual
- [ ] Secao 4 (Estrutura de Dados) com entidades e campos
- [ ] Secao 5 (Regras) com formulas e validacoes
- [ ] Secao 6 (MVP) com features e criterios de aceite
- [ ] Secao 7 (O que NAO fazer) preenchida
- [ ] Secao 8 (Roadmap) com fases futuras
- [ ] Secao 9 (Alertas) com conflitos resolvidos

**Se todos marcados -> Escopo pronto para MP-02!**
"""

---

### 8. FINALIZAR

Apos gerar as secoes 5-9 e o checklist, diga ao usuario:

"""
ESCOPO COMPLETO GERADO!

Arquivo: escopo.md (9 secoes)

Conteudo:
- Secao 1: Visao Geral
- Secao 2: Tech Stack
- Secao 3: Interface e Identidade Visual
- Secao 4: Estrutura de Dados
- Secao 5: Regras de Negocio e Validacoes
- Secao 6: Funcionalidades MVP (Fase 1)
- Secao 7: O que NAO Fazer
- Secao 8: Roadmap (Fases Futuras)
- Secao 9: Alertas Tecnicos
- Checklist de Validacao

---

VALIDACAO:

Por favor, revise o escopo.md gerado e confirme:
1. Todas as informacoes do JSON foram mapeadas?
2. Alguma secao ficou com "[A DEFINIR]"?
3. As regras de negocio estao corretas?
4. O roadmap reflete suas prioridades?

Se tudo estiver OK, salve o arquivo e avance para:
**MP-02-Estrutura-de-Pastas.md**

Se precisar ajustar algo, me diga o que corrigir.
"""

---

## REGRAS IMPORTANTES

1. **NAO reescreva secoes 1-4** - apenas adicione 5-9
2. **NAO invente dados** - use apenas o que esta no JSON
3. **Se campo estiver vazio** - escreva "[A DEFINIR]" e destaque
4. **Mantenha linguagem natural** - sem codigo, sem SQL
5. **Use portugues** - todo o documento em PT-BR
6. **Tabelas para validacoes** - mais legivel que listas

---

## EXEMPLO DE CONTINUACAO

Se Parte 1 terminou com:
"""
## 4. ESTRUTURA DE DADOS
...
**Observacoes:**
- Timestamps automaticos em todas as entidades
"""

Parte 2 CONTINUA:
"""

---

## 5. REGRAS DE NEGOCIO E VALIDACOES

### Regras de Negocio
...
"""

O arquivo final tera secoes 1-9 em sequencia.
```
