# DESC04: DETECÇÃO DE CONFLITOS E ROADMAP

**QUANDO USAR:**
1. Após completar MP-00-Parte2-Contextuais.md
2. Abra NOVO chat no Claude (context limpo)
3. Anexe: Resumo Parte 0 + JSON completo (Partes 1+2)
4. Cole este prompt

**PRÉ-REQUISITOS:**
- Resumo de contexto da Parte 0
- JSON completo com decisões técnicas (Parte 1) e interface (Parte 2)

**ESTE É O PROMPT FINAL DA DESCOBERTA GUIADA**

---

```
Você é uma IA especializada em arquitetura de software e planejamento de projetos.

Recebi o seguinte contexto do projeto:

[COLE AQUI O RESUMO DA PARTE 0]

E o JSON completo com todas as decisões:

[COLE AQUI O JSON COMPLETO DAS PARTES 1 + 2]

Agora preciso:
1. DETECTAR conflitos técnicos entre as decisões
2. GERAR JSON final consolidado
3. CRIAR roadmap pós-MVP (fases 2, 3, etc)

---

## INSTRUÇÕES PARA A IA:

### 1. INICIAR CONTEXTUALIZANDO

Diga ao usuário:

"""
Perfeito! Tenho todas as informações necessárias.

Agora vou:
1. Analisar se existe algum CONFLITO técnico entre suas escolhas
2. Consolidar tudo em um JSON final
3. Criar um ROADMAP para desenvolvimento pós-MVP

Isso garante que vamos construir o sistema na ordem correta e sem surpresas técnicas.
"""

---

### 2. DETECÇÃO DE CONFLITOS

Analise o JSON completo e detecte conflitos comuns:

**Conflitos de Deploy:**
- SQLite + Railway = dados perdidos (filesystem efêmero)
- Uploads + Railway sem cloud storage = arquivos perdidos
- CRON jobs + Vercel free = (Vercel cobra por CRON)
- 24/7 + local deploy = (computador precisa ficar ligado)

**Conflitos de Database:**
- Multiuser + File system (JSON) = race conditions
- >10k registros + SQLite = (pode ficar lento)
- Offline required + Cloud database only = incompatível

**Conflitos de Volume:**
- >1000 ops/dia + free tier = pode atingir limites
- Uploads grandes (>10MB) + free storage = quota

**Conflitos de Dependências Nativas:**
- Railway + bcrypt/sharp/better-sqlite3 = compilação lenta
  -> Sugerir alternativas JS puras (bcryptjs, jimp, @libsql/client)

**Conflitos de Features:**
- Login com roles + "só eu uso" = roles são necessários?
- Automação diária + "não urgente" = realmente precisa de CRON?

---

### 3. APRESENTAR CONFLITOS DETECTADOS

Se detectou conflitos, PARE e apresente:

"""
CONFLITOS TÉCNICOS DETECTADOS:

Encontrei [N] incompatibilidades entre suas escolhas:

---

**Conflito 1: [Título]**
Problema: [Descrição clara do problema]

Exemplo:
Você escolheu: Railway deploy + SQLite database
Conflito: Railway tem filesystem efêmero - SQLite perde dados a cada deploy

Soluções:
A) Mudar database para PostgreSQL (Railway tem free tier)
   Prós: Persiste dados, escala melhor
   Contras: Setup um pouco mais complexo

B) Mudar deploy para Local only
   Prós: SQLite funciona perfeitamente
   Contras: Precisa deixar computador ligado

C) Usar Turso (LibSQL cloud)
   Prós: SQLite compatível + cloud persistence
   Contras: Serviço externo, precisa conta

Qual solução prefere? (A / B / C)

---

**Conflito 2: [Título]**
[Mesma estrutura]

---

POR FAVOR, escolha uma solução para CADA conflito antes de prosseguir.
"""

**AGUARDAR resposta do usuário para cada conflito.**

---

### 4. APÓS RESOLVER CONFLITOS - GERAR JSON FINAL

Quando todos conflitos estiverem resolvidos:

"""
CONFLITOS RESOLVIDOS!

Gerando JSON final consolidado...

```json
{
  "projeto": {
    "nome": "[nome do projeto]",
    "descricao_curta": "[1 frase - problema que resolve]",
    "contexto_completo": "[resumo da história da Parte 0]",
    "definicao_sucesso": "[métricas de sucesso da Parte 0]",
    "urgencia": "[timeline da Parte 0]",
    "complexidade_estimada": "small/medium/large"
  },
  
  "tech_stack": {
    "backend": {
      "framework": "[Next.js API Routes / Express / FastAPI]",
      "linguagem": "[TypeScript / JavaScript / Python]",
      "justificativa": "[por que esta escolha]"
    },
    "frontend": {
      "framework": "[Next.js / React / Vue]",
      "linguagem": "[TypeScript / JavaScript]",
      "styling": "[Tailwind CSS / CSS Modules]",
      "ui_components": "[shadcn/ui / Material-UI / Custom]"
    },
    "database": {
      "tipo": "[postgresql / mysql / sqlite / mongodb / filesystem]",
      "orm": "[Prisma / Drizzle / Mongoose / fs/promises]",
      "volume_estimado": "[numero de registros]",
      "offline_required": true/false,
      "multiuser": true/false,
      "justificativa": "[por que esta escolha - APÓS resolver conflitos]"
    },
    "infraestrutura": {
      "deploy": "[railway / vercel / local / outro]",
      "node_version": "[20.x / 18.x]",
      "package_manager": "[npm / yarn / pnpm]",
      "disponibilidade": "[24-7 / best-effort]",
      "budget": "[free / paid]",
      "justificativa": "[por que esta escolha - APÓS resolver conflitos]"
    }
  },
  
  "features": {
    "uploads": {
      "necessario": true/false,
      "tipos_arquivo": ["imagem", "pdf"],
      "tamanho_max_mb": "[numero]",
      "storage": "[local / cloudinary / s3]"
    },
    "automacao": {
      "necessaria": true/false,
      "tarefas": [
        {
          "descricao": "[o que automatizar]",
          "frequencia": "[daily / hourly / weekly]",
          "timezone": "[America/Sao_Paulo / UTC / etc]"
        }
      ]
    },
    "autenticacao": {
      "necessaria": true/false,
      "tipo": "[email-senha / oauth / outro]",
      "usuarios_simultaneos": "[numero]",
      "roles": true/false,
      "roles_lista": ["admin", "usuario"]
    },
    "integracoes_externas": [
      {
        "nome": "[Stripe / SendGrid / etc]",
        "proposito": "[para que serve]",
        "api_key_disponivel": true/false
      }
    ]
  },
  
  "interface": {
    "dashboard": {
      "metricas": ["[metrica1]", "[metrica2]"],
      "acoes_rapidas": ["[acao1]", "[acao2]"],
      "descricao": "[texto livre]"
    },
    "telas": [
      {
        "nome": "[nome tela]",
        "rota": "[/dashboard, /produtos, etc]",
        "proposito": "[o que faz]",
        "componentes": ["lista", "formulario", "graficos"]
      }
    ],
    "identidade_visual": {
      "logo": {
        "existe": true/false,
        "arquivo": "[caminho ou 'criar simples']"
      },
      "paleta": {
        "primaria": "[#hex ou nome]",
        "secundaria": "[#hex ou nome]",
        "background": "light/dark",
        "estilo": "minimalista/corporativo/colorido/moderno"
      },
      "tema": "light/dark/both",
      "tipografia": "[Inter / Roboto / Outro]"
    }
  },
  
  "dados": {
    "entidades": [
      {
        "nome": "[Produto]",
        "descricao": "[para que serve]",
        "campos": [
          {
            "nome": "nome",
            "tipo": "string",
            "obrigatorio": true,
            "validacao": "[min 3 chars / etc]"
          },
          {
            "nome": "preco",
            "tipo": "number",
            "obrigatorio": true,
            "validacao": "> 0"
          }
        ],
        "relacionamentos": [
          {
            "com": "[Cliente]",
            "tipo": "many-to-one",
            "descricao": "[produto pertence a cliente]"
          }
        ]
      }
    ]
  },
  
  "relatorios": [
    {
      "nome": "[Vendas Mensais]",
      "descricao": "[o que mostra]",
      "tipo": "grafico/lista/pdf",
      "dados": ["campo1", "campo2"],
      "filtros": ["periodo", "categoria"],
      "exportavel": true/false
    }
  ],
  
  "performance": {
    "operacoes_dia": "[numero]",
    "tempo_resposta_esperado": "fast/normal/slow",
    "picos_esperados": "[horarios de maior uso]"
  },
  
  "limitacoes": {
    "sistema_operacional": "[windows/mac/linux/todos]",
    "navegadores": "[chrome/firefox/todos]",
    "restricoes_tecnicas": ["[restricao1]", "[restricao2]"],
    "dependencias_evitar": ["[tech1]", "[tech2]"]
  },
  
  "alertas_tecnicos": [
    "[Alerta 1 - ex: Railway filesystem efêmero]",
    "[Alerta 2 - ex: Dependência nativa bcrypt]"
  ]
}
```

---

VALIDAÇÃO DO JSON:

Verifique se está completo:
- Projeto (nome, descrição, contexto)
- Tech stack (backend, frontend, database, infra)
- Features (uploads, automação, auth, integrações)
- Interface (dashboard, telas, identidade visual)
- Dados (entidades com campos e relacionamentos)
- Relatórios (se aplicável)
- Performance e limitações
- Alertas técnicos

Se algo estiver "null" ou vazio sem motivo, preencha agora.
"""

---

### 5. GERAR ROADMAP PÓS-MVP

Após JSON final estar completo:

"""
ROADMAP DE DESENVOLVIMENTO

Vou dividir o projeto em FASES:

**MVP (Minimum Viable Product) - FASE 1**
Objetivo: Validar a ideia com funcionalidades CORE

**Pós-MVP - FASES 2, 3, etc**
Objetivo: Expandir após validação com usuários reais

---

## FASE 1: MVP (Semanas 1-2)

**Escopo MÍNIMO para validar o conceito:**

### Setup Inicial:
- [ ] Estrutura de pastas
- [ ] Configurações (package.json, tsconfig, etc)
- [ ] Database schema básico
- [ ] Autenticação (se necessária)

### Features Core (baseadas na história da Parte 0):
[IA analisa contexto e lista 3-5 features ESSENCIAIS]

Exemplo (sistema de estoque):
- [ ] CRUD Produtos (cadastrar, listar, editar, deletar)
- [ ] Atualização automática estoque (ao vender)
- [ ] Dashboard com alerta de estoque baixo
- [ ] Relatório simples de vendas

### O que NÃO entra no MVP:
- [Feature não essencial 1]
- [Feature não essencial 2]
- [Otimizações prematuras]
- [Integrações complexas]

**Critérios de Conclusão MVP:**
- [ ] Usuário consegue [ação core 1]
- [ ] Usuário consegue [ação core 2]
- [ ] Sistema resolve [problema principal da Parte 0]
- [ ] Zero bugs críticos (que impedem uso)
- [ ] Deploy funcionando (se aplicável)

**Estimativa:** [X] horas de desenvolvimento

---

## FASE 2: Validação e Melhorias (Semanas 3-4)

**CONDIÇÃO PARA INICIAR:**
- MVP usado por pelo menos [N] usuários reais
- Feedback coletado e analisado
- Bugs críticos do MVP corrigidos

**Prioridade ALTA (baseado em feedback esperado):**
[IA sugere 3-5 features de Fase 2]

Exemplo:
- [ ] Filtros avançados nas listas
- [ ] Exportação de relatórios para Excel
- [ ] Notificações por email
- [ ] Histórico de alterações (auditoria)

**Prioridade MÉDIA:**
- [ ] [Feature nice-to-have 1]
- [ ] [Feature nice-to-have 2]

**O que ainda NÃO entra:**
- [Features avançadas que podem esperar]

**Critérios para Fase 3:**
- [ ] Fase 2 features validadas
- [ ] Métricas de sucesso atingidas: [definir da Parte 0]
- [ ] Performance adequada (tempo resposta < 3s)
- [ ] Sem bugs médios/altos

---

## FASE 3: Expansão (Mês 2+)

**CONDIÇÃO PARA INICIAR:**
- Sistema em uso regular (diário/semanal)
- Fase 2 estável
- Usuários solicitaram próximas features

**Features de Expansão:**
[IA sugere features avançadas]

Exemplo:
- [ ] Integração com sistema X
- [ ] Módulo de relatórios avançados (gráficos)
- [ ] API para integrações externas
- [ ] App mobile (se fizer sentido)
- [ ] Multi-tenancy (se crescer muito)

**Otimizações:**
- [ ] Cache de queries frequentes
- [ ] Indexação de database
- [ ] Code splitting (frontend)

---

## FASE 4+: Futuros Possíveis

**Ideias para considerar MUITO depois:**
[IA sugere features "sonho grande"]

Exemplo:
- Marketplace de plugins
- White-label para outros clientes
- IA integrada (se fizer sentido)
- Versão enterprise

**REGRA DE OURO:**

NÃO avançar para próxima fase sem:
1. Fase atual 100% estável
2. Usuários usando regularmente
3. Feedback positivo coletado
4. Métricas de sucesso atingidas

**Evitar "feature creep":**
Se surgir ideia nova durante desenvolvimento:
-> Anote no "Backlog Futuro"
-> NÃO implemente imediatamente
-> Valide necessidade com usuários ANTES

---

RESUMO EXECUTIVO:

**MVP (Fase 1):** [X] features core -> [Y] horas
**Validação (Fase 2):** Após feedback -> [Z] features
**Expansão (Fase 3):** Após estabilidade -> crescimento

**Prioridade MÁXIMA:** Fazer MVP funcionar e validar com usuários REAIS.
"""

---

### 6. GERAR PRÓXIMO PASSO

"""
DESCOBERTA GUIADA COMPLETA!

Você agora tem:
- JSON completo com todas decisões técnicas
- Conflitos resolvidos
- Roadmap de desenvolvimento (Fases 1, 2, 3+)

---

SALVAR ARQUIVOS:

1. **decisoes-tecnicas.json**
   Salve o JSON completo em arquivo local.

2. **roadmap.md**
   Copie o roadmap e salve separadamente.

---

PRÓXIMO PASSO:

Abra um NOVO chat no Claude e cole o prompt:
**MP-01-Gerar-Escopo.md**

Anexe naquele chat:
1. O JSON completo (decisoes-tecnicas.json)
2. O roadmap (roadmap.md)

MP-01 vai gerar o arquivo `escopo.md` completo, pronto para usar nos 
Meta-Prompts de desenvolvimento (MP-02 a MP-06).

PARABÉNS! A descoberta guiada está concluída.
"""

---

## EXEMPLO DE CONFLITO E RESOLUÇÃO

**Conflito detectado:**
```
CONFLITO 1: Deploy vs Database

Você escolheu:
- Deploy: Railway (free tier, 24/7)
- Database: SQLite
- Upload: Sim (imagens)

Problema:
Railway tem filesystem EFÊMERO - a cada deploy:
- SQLite perde TODOS os dados
- Imagens enviadas são DELETADAS

Isso significa que seu sistema vai "esquecer" tudo periodicamente.

Soluções:

A) Mudar database para PostgreSQL
   Railway tem PostgreSQL grátis (500MB)
   Prós: Persiste dados
   Prós: Melhor para multiuser
   Contras: Setup +2 comandos

B) Mudar deploy para Local only
   Rodar no seu computador
   Prós: SQLite funciona perfeitamente
   Contras: Precisa deixar PC ligado 24/7

C) Usar Turso (LibSQL cloud) + Cloudinary (imagens)
   Prós: SQLite compatível
   Prós: Cloud persistence
   Contras: Precisa criar conta (grátis)

Qual solução prefere? (A / B / C)
```

**Usuário responde:** "A - PostgreSQL"

**IA atualiza JSON:**
```json
{
  "database": {
    "tipo": "postgresql",
    "orm": "prisma",
    "justificativa": "Railway deploy + necessidade de persistência"
  },
  "alertas_tecnicos": [
    "PostgreSQL requer Railway database (já configurado no setup)",
    "Migrar schema SQLite -> PostgreSQL é simples (Prisma handled)"
  ]
}
```

---

## VALIDAÇÃO FINAL

Após executar este prompt, você deve ter:
- Conflitos detectados e resolvidos
- JSON final completo e validado
- Roadmap com Fases 1, 2, 3+
- Critérios de conclusão de cada fase
- Direcionamento para MP-01

**Este é o FINAL da descoberta guiada.**

**Próximo:** MP-01 gera escopo.md baseado neste JSON.
```
