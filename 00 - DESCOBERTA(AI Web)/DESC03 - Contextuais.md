# DESC03: PERGUNTAS CONTEXTUAIS (UI, Dados, Identidade Visual)

**QUANDO USAR:**
1. Após completar DESC02 - Criticas.md
2. Abra NOVO chat no Claude (context limpo)
3. Anexe: Resumo DESC01 + JSON DESC02
4. Cole este prompt

**PRÉ-REQUISITOS:** 
- Resumo de contexto do DESC01
- JSON de decisões técnicas do DESC02

---

```
Você é uma IA especializada em design de interfaces e experiência de usuário.

Recebi o seguinte contexto do projeto:

[COLE AQUI O RESUMO DO DESC01]

E as decisões técnicas:

[COLE AQUI O JSON DO DESC02]

Agora preciso entender a INTERFACE, DADOS e IDENTIDADE VISUAL do sistema.

---

## INSTRUÇÕES PARA A IA:

### 1. INICIAR CONTEXTUALIZANDO

Diga ao usuário:

"""
Ótimo! Já sei a história e a arquitetura técnica.

Agora vou perguntar sobre a INTERFACE e DADOS do sistema.

Estas perguntas vão definir:
- Como as telas vão se parecer
- Que dados o usuário vai cadastrar
- Quais relatórios gerar
- Identidade visual (cores, logo)

Vou fazer 6 grupos de perguntas (o grupo 3 tem sub-perguntas sobre dados). Responda o que souber, posso sugerir com base no seu contexto.
"""

---

### 2. GRUPO 1 - DASHBOARD INICIAL

"""
**1. Dashboard Inicial (Tela Principal)**

Quando você abrir a aplicação, o que imagina ver na primeira tela?

Pense em:
- Números/métricas importantes que quer ver de relance
- Gráficos ou visualizações
- Atalhos para ações rápidas
- Avisos/notificações

Descreva livremente, pode ser bem visual:
"Quero ver um número grande mostrando X, embaixo uma lista de Y, 
e um botão para fazer Z rapidamente."

Se não tiver ideia clara, responda: "Sugira você baseado no contexto"
"""

---

### 3. GRUPO 2 - TELAS PRINCIPAIS

"""
**2. Telas/Páginas Principais**

Liste as principais seções ou páginas do sistema e descreva brevemente o que 
o usuário vai FAZER em cada uma.

Formato sugerido:
- **Tela 1 (Nome):** O que faz aqui? Ex: "Cadastrar novos produtos"
- **Tela 2 (Nome):** O que faz aqui? Ex: "Ver lista de vendas"
- **Tela 3 (Nome):** O que faz aqui? Ex: "Gerar relatórios"

Baseado no seu contexto [mencionar contexto do DESC01], imagino que precisa de:
[IA sugere 3-5 telas baseadas na história]

Concorda com estas? Quer adicionar, remover ou modificar alguma?
"""

---

### 4. GRUPO 3 - DADOS E ENTIDADES

"""
**3. Dados do Sistema**

Vou precisar entender TODOS os tipos de dados do sistema. 
Isso inclui dados digitados pelo usuário E dados que vêm de fora.

**3a. Dados que o usuário vai DIGITAR manualmente:**

Para cada tipo de dado, liste os campos principais:

Exemplo:
- **Produto:** nome, preço, estoque, fornecedor
- **Cliente:** nome, email, telefone, endereço

Liste os seus:
- **[Entidade 1]:** [campos]
- **[Entidade 2]:** [campos]

Se não souber todos os campos agora, liste apenas as entidades principais.

---

**3b. Dados que vêm de SISTEMAS EXTERNOS:**

Se o sistema integra com APIs/serviços externos (mencionado no DESC02):

- Que dados vêm do sistema externo?
- Em que formato chegam? (JSON, XML, CSV, etc)
- Algum campo vem em formato especial? (ex: datas em UTC, valores em centavos)
- Algum campo pode vir VAZIO ou inconsistente às vezes?

Exemplo:
- "Da API do vCenter vêm eventos com campos: tipo, VM, usuário, data"
- "O campo detail_before às vezes vem vazio"
- "Datas vêm em UTC, preciso converter para horário local"

---

**3c. Campos especiais:**

Alguma entidade tem campos que armazenam dados complexos?
- Campos JSON (guardam objeto inteiro, ex: detail_before, configurações)
- Campos de controle (is_active, is_primary, is_admin)
- Campos criptografados (senhas, tokens)
- Campos calculados (total = preço x quantidade)
- Campos enum (status: ativo/inativo/pendente, tipo: A/B/C)

Exemplo:
- "Evento tem campo raw_data que guarda o JSON inteiro do evento original"
- "vCenter tem campo encrypted_password"
- "Evento tem campo event_type que é enum (DiskExpand, PowerOn, etc)"

---

**3d. Relacionamentos entre entidades:**

Quais entidades se conectam com quais?

Exemplo:
- "Venda pertence a um Cliente (1 cliente tem N vendas)"
- "Evento pertence a um vCenter (1 vCenter tem N eventos)"

Liste os seus:
- [Entidade A] → [Entidade B]: [tipo de relação]
"""

---

### 5. GRUPO 4 - RELATÓRIOS

"""
**4. Relatórios e Exportações**

Precisa de relatórios nessa primeira fase (MVP)?

Se SIM, para cada relatório descreva:
- **Nome do relatório:** [ex: "Vendas do Mês"]
- **Que dados mostra:** [ex: "Lista de todas vendas com total"]
- **Formato:** [Tela / PDF / Excel / Gráfico]
- **Filtros:** [ex: "Por período, por produto"]

Exemplos:
- Relatório "Estoque Baixo": Lista produtos com estoque < 10, Tela, Filtro por categoria
- Relatório "Vendas Mensais": Gráfico de barras, exporta Excel, Filtro por mês

Liste os seus:
1. [Relatório 1]
2. [Relatório 2]

OU responda: "Não preciso de relatórios agora" / "Sugira você"
"""

---

### 6. GRUPO 5 - IDENTIDADE VISUAL

"""
**5. Identidade Visual e Paleta de Cores**

Agora sobre a APARÊNCIA do sistema:

**a) Marca/Logo:**
- Você já tem uma marca/logo existente que devemos usar?
  - Sim, tenho logo (pode anexar depois ou descrever)
  - Não, pode criar algo simples
  - Não precisa de logo, apenas nome do sistema

**b) Paleta de Cores:**
- Tem preferência de cores? Pense em:
  - Cor principal (botões, destaques)
  - Cor de fundo (claro, escuro)
  - Estilo geral (minimalista, colorido, corporativo)

Opções:
1. "Tenho preferência": [descrever cores, ex: azul marinho e laranja]
2. "Sugira cores profissionais baseado no contexto"
3. "Deixe padrão (azul/cinza neutro)"

**c) Estilo Visual:**
- Minimalista (clean, muito branco, poucos elementos)
- Corporativo (formal, sério, azul/cinza)
- Colorido/Criativo (vibrante, cards coloridos)
- Moderno/Tech (gradientes, dark mode)
- Outro: [descrever]

**d) Preferência Dark/Light:**
- Apenas light (fundo claro)
- Apenas dark (fundo escuro)
- Ambos (usuário escolhe)
- Tanto faz

Responda a, b, c, d.
"""

---

### 7. GRUPO 6 - WORKFLOWS

"""
**6. Fluxos de Trabalho (Workflows)**

Descreva um fluxo TÍPICO de uso do sistema, do início ao fim.

Formato sugerido:
1. Usuário abre sistema
2. Usuário faz X
3. Sistema mostra Y
4. Usuário clica em Z
5. Sistema salva e exibe confirmação

Exemplo (sistema de estoque):
1. Gerente abre dashboard, vê aviso "5 produtos com estoque baixo"
2. Clica em "Ver Produtos", lista aparece
3. Seleciona produto "Caneta Azul"
4. Clica "Adicionar Estoque", digita quantidade 100
5. Sistema atualiza, mostra toast "Estoque atualizado!"

Descreva o SEU fluxo principal:
[usuário descreve]

Se não tiver certeza, descreva o cenário que você imaginou no DESC01 
quando disse "dia perfeito usando a ferramenta".
"""

---

### 8. ANALISAR RESPOSTAS E GERAR RESUMO

Após receber as 6 respostas, ANALISE e gere resumo estruturado:

"""
RESUMO CONTEXTUAL CAPTURADO:

**Dashboard Inicial:**
[Resumir o que vai na tela principal]

**Telas Principais:**
1. [Tela 1 - Nome]: [O que faz]
2. [Tela 2 - Nome]: [O que faz]
3. [Tela 3 - Nome]: [O que faz]

**Entidades de Dados:**
- [Entidade 1]: [campos principais]
- [Entidade 2]: [campos principais]

**Relatórios:**
- [Relatório 1]: [formato, filtros]
- [Relatório 2]: [formato, filtros]

**Identidade Visual:**
- Logo: [Sim/Não/Criar]
- Paleta: [Cores escolhidas ou sugeridas]
- Estilo: [Minimalista/Corporativo/etc]
- Tema: [Light/Dark/Ambos]

**Fluxo Principal:**
[Descrever workflow típico em 3-5 passos]

---

SUGESTÕES DE UX/UI:

Baseado nas suas respostas e no contexto do projeto, sugiro:

[IA analisa e sugere melhorias de UX]

Exemplos de sugestões:
- "Adicionar botão flutuante '+' para cadastro rápido"
- "Dashboard com cards coloridos por status (verde=ok, vermelho=crítico)"
- "Breadcrumbs para navegação (já que tem múltiplas telas)"
- "Filtros rápidos na lista principal"

---

JSON ATUALIZADO:

Vou adicionar estas informações ao JSON do DESC02:

```json
{
  "projeto": {
    "nome": "[nome]",
    "contexto": "[resumo]"
  },
  "decisoes_tecnicas": {
    // ... (mantém da Parte 1)
  },
  "interface": {
    "dashboard": {
      "metricas": ["[metrica1]", "[metrica2]"],
      "acoes_rapidas": ["[acao1]", "[acao2]"],
      "descricao": "[texto livre do usuário]"
    },
    "telas": [
      {
        "nome": "[nome tela]",
        "proposito": "[o que faz]",
        "elementos": ["lista", "formulario", "graficos"]
      }
    ]
  },
  "dados": {
    "entidades": [
      {
        "nome": "[Produto]",
        "campos": ["nome", "preco", "estoque"],
        "campos_especiais": {
          "json_blobs": [],
          "criptografados": [],
          "enums": ["status (ativo/inativo)"],
          "flags": ["is_active"]
        },
        "origem": "manual",
        "relacionamentos": [
          {"com": "[Categoria]", "tipo": "many-to-one"}
        ]
      }
    ],
    "dados_externos": [
      {
        "origem": "[nome da API/serviço]",
        "formato": "[JSON/XML/CSV]",
        "campos_recebidos": ["campo1", "campo2"],
        "campos_instáveis": ["campo que pode vir vazio"],
        "observacoes": "[ex: datas em UTC, IDs com prefixo]"
      }
    ]
  },
  "relatorios": [
    {
      "nome": "[Vendas Mensais]",
      "tipo": "[grafico/lista/pdf]",
      "filtros": ["periodo", "produto"]
    }
  ],
  "identidade_visual": {
    "logo": {
      "existe": true/false,
      "descricao": "[arquivo ou criar]"
    },
    "paleta": {
      "cor_primaria": "[hex ou nome]",
      "cor_secundaria": "[hex ou nome]",
      "background": "light/dark",
      "estilo": "minimalista/corporativo/colorido"
    },
    "tema": "light/dark/both"
  },
  "workflows": [
    {
      "nome": "Workflow Principal",
      "passos": [
        "Passo 1: [descrição]",
        "Passo 2: [descrição]"
      ]
    }
  ]
}
```

---

PRÓXIMO PASSO:

Salve este JSON COMPLETO (com tudo do DESC02 + DESC03).

Depois, abra um NOVO chat no Claude e cole o prompt:
**DESC04 - Conflitos-e-Roadmap.md**

Anexe:
1. Resumo de contexto do DESC01
2. JSON completo (DESC02 + DESC03)

Lá vamos detectar conflitos técnicos e gerar o roadmap pós-MVP.
"""

---

## EXEMPLO DE SUGESTÃO DE CORES

**Se usuário disse:** "Sugira cores profissionais baseado no contexto"

**IA analisa contexto da Parte 0:**
- Projeto: Sistema de estoque
- Público: Gerente de loja
- Tom: Profissional, confiável

**IA sugere:**
"""
SUGESTÃO DE PALETA:

Baseado no contexto (sistema profissional de gestão), sugiro:

**Paleta Corporativa Moderna:**
- Primária: Azul Profundo (#1E3A8A) - Confiança e estabilidade
- Secundária: Verde Sucesso (#10B981) - Para alertas positivos
- Background: Cinza Claro (#F9FAFB) - Clean e profissional
- Texto: Cinza Escuro (#1F2937)
- Alerta Crítico: Vermelho (#EF4444) - Estoque baixo

**Tema:** Light (pode adicionar dark depois se quiser)

**Estilo:** Minimalista Corporativo
- Cards com sombra sutil
- Bordas arredondadas (8px)
- Espaçamento generoso
- Tipografia clara (Inter ou Roboto)

Concorda? Quer ajustar alguma cor?
"""

---

## VALIDAÇÃO

Após executar este prompt, você deve ter:
- Dashboard descrito
- Telas principais listadas
- Entidades de dados mapeadas (com campos especiais, enums, flags)
- Dados externos documentados (formato, campos instáveis)
- Relacionamentos entre entidades definidos
- Relatórios definidos (ou "não precisa")
- Identidade visual decidida
- Workflow principal descrito
- JSON completo (DESC02 + DESC03)

Se algo ficou vago, peça para IA sugerir baseado no contexto.
```
