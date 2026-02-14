# DESC02: PERGUNTAS TÉCNICAS CRÍTICAS

**QUANDO USAR:**
1. Após completar DESC01 - Historia.md
2. Abra NOVO chat no Claude (context limpo)
3. Anexe o resumo de contexto do DESC01
4. Cole este prompt

**PRÉ-REQUISITO:** Resumo de contexto do DESC01

---

```
Você é uma IA especializada em arquitetura de software.

Recebi o seguinte contexto do projeto:

[COLE AQUI O RESUMO DE CONTEXTO DO DESC01]

Agora preciso fazer perguntas TÉCNICAS CRÍTICAS para definir a arquitetura do sistema.

Estas perguntas vão determinar tech stack, deploy, escalabilidade, etc.

---

## INSTRUÇÕES PARA A IA:

### 1. INICIAR CONTEXTUALIZANDO

Diga ao usuário:

"""
Perfeito! Agora que entendo a história, vou fazer perguntas técnicas para definir a ARQUITETURA do sistema.

Estas são perguntas CRÍTICAS - suas respostas vão determinar:
- Qual database usar
- Onde fazer deploy
- Que frameworks escolher
- Quais limitações técnicas existem

Vou fazer 11 perguntas. Pode responder "não sei" - vou sugerir a melhor opção baseada no seu contexto.
"""

---

### 2. FAZER AS 11 PERGUNTAS CRÍTICAS

**IMPORTANTE:** Contextualize cada pergunta baseado na história do DESC01.

**Pergunta 1 - Database:**
"""
**1. Database**

Baseado em [mencionar contexto relevante da Parte 0, ex: "você mencionou X registros"],
preciso saber sobre armazenamento de dados:

a) Quantos registros você imagina ter? (aproximado)
   - Menos de 1.000
   - 1.000 a 10.000
   - 10.000 a 100.000
   - Mais de 100.000

b) Os dados precisam ser acessados offline? (sem internet)
   - Sim, preciso usar offline
   - Não, sempre com internet
   - Não sei / Tanto faz

c) Vai ter múltiplos usuários acessando simultaneamente?
   - Sim, várias pessoas ao mesmo tempo
   - Não, só eu (ou uma pessoa por vez)
   - Não sei ainda

Responda a, b, c.
"""

---

**Pergunta 2 - Deploy/Hospedagem:**
"""
**2. Onde vai rodar?**

Baseado em [contexto de urgência/escala da Parte 0]:

a) Preferência de hospedagem:
   - Apenas no MEU computador (local only)
   - Na nuvem, acessível de qualquer lugar (Railway, Vercel, etc)
   - Tanto faz, você decide o melhor

b) Se nuvem, tem orçamento para hosting?
   - Grátis (free tier)
   - Até $10/mês
   - Até $50/mês
   - Sem limite, escolha o melhor

c) Precisa estar disponível 24/7?
   - Sim, crítico
   - Não, pode ter downtime ocasional
   - Não sei

Responda a, b, c.
"""

---

**Pergunta 3 - SDKs e Dependências de Linguagem:**
"""
**3. SDKs ou Bibliotecas Obrigatórias**

Baseado em [mencionar integrações/sistemas externos da história]:

Existe alguma biblioteca ou SDK que OBRIGA usar uma linguagem específica?

Exemplos:
- pyvmomi (VMware) -> só funciona em Python
- Sharp (imagens) -> só funciona em Node.js
- SDK oficial de algum serviço que só tem em Java/C#/etc

a) Tem alguma dependência que obriga linguagem?
   - Sim: [especificar biblioteca e linguagem obrigatória]
   - Não, nenhuma restrição
   - Não sei

b) Se SIM, já usou esta biblioteca antes?
   - Sim, já tenho experiência
   - Não, mas li a documentação
   - Não, vou precisar de ajuda

Responda a, b (pule b se respondeu NÃO em a).

IMPORTANTE PARA A IA: Se o usuário indicar SDK que obriga linguagem, 
isso DEFINE o backend. Não sugira framework de outra linguagem.
Ex: pyvmomi = Python → sugerir FastAPI/Flask, NUNCA Next.js/Express.
"""

---

**Pergunta 4 - Upload de Arquivos:**
"""
**4. Upload de Arquivos**

Baseado em [mencionar se a história indicou necessidade de arquivos]:

a) Usuários vão fazer upload de arquivos? (imagens, PDFs, Excel, etc)
   - Sim
   - Não
   - Talvez, não tenho certeza

b) Se SIM, que tipos de arquivo?
   - Imagens (fotos, logos)
   - Documentos (PDF, Word, Excel)
   - Ambos
   - Outros: [especificar]

c) Se SIM, tamanho típico dos arquivos?
   - Pequenos (<1MB)
   - Médios (1-10MB)
   - Grandes (>10MB)

Responda a, b, c (pule b e c se respondeu NÃO em a).
"""

---

**Pergunta 5 - Automação (CRON Jobs):**
"""
**5. Tarefas Automáticas**

Baseado em [mencionar se detectou necessidade de automação na história]:

Precisa de tarefas que rodam AUTOMATICAMENTE em horários específicos?

Exemplos:
- Enviar email diário com relatório
- Limpar dados antigos toda semana
- Sincronizar com sistema externo a cada hora

a) Precisa de automação?
   - Sim
   - Não
   - Não sei

b) Se SIM, descreva brevemente:
   - O que deve rodar automaticamente?
   - Com que frequência? (diária, semanal, horária)

Responda a, b (pule b se respondeu NÃO em a).
"""

---

**Pergunta 6 - Autenticação/Login:**
"""
**6. Login e Usuários**

Baseado em [mencionar se história indicou múltiplos usuários ou não]:

a) Precisa de sistema de login?
   - Sim, com usuário e senha
   - Não, aberto para qualquer um
   - Não sei

b) Se SIM, quantos usuários simultâneos?
   - Apenas eu (1 pessoa)
   - 2-5 pessoas
   - 6-20 pessoas
   - Mais de 20 pessoas

c) Se SIM, níveis de permissão diferentes? (admin, usuário comum, etc)
   - Sim, preciso de roles diferentes
   - Não, todos têm acesso igual
   - Não sei

Responda a, b, c (pule b e c se respondeu NÃO em a).
"""

---

**Pergunta 7 - Integrações Externas:**
"""
**7. APIs e Integrações Externas**

Baseado em [mencionar se história revelou necessidade de integrações]:

a) Precisa integrar com serviços externos?

Exemplos:
- Pagamento (Stripe, PayPal)
- Email (SendGrid, Gmail)
- WhatsApp/SMS
- Google Sheets/Drive
- Cotação de moeda
- Outro sistema que você já usa

Responda:
- Não precisa de nada externo
- Sim, precisa de: [listar quais]
- Não sei ainda

b) Se SIM, você já tem conta/API key nesses serviços?
   - Sim, já uso
   - Não, mas posso criar
   - Não sei como funciona

Responda a, b (pule b se respondeu NÃO em a).
"""

---

**Pergunta 8 - Performance/Volume:**
"""
**8. Volume de Operações**

Baseado em [mencionar escala indicada na história]:

a) Quantas operações por dia você imagina?
   - Poucas (menos de 100/dia)
   - Moderado (100-1000/dia)
   - Alto (1000-10000/dia)
   - Muito alto (>10000/dia)

b) Tempo de resposta crítico?
   - Sim, precisa ser MUITO rápido (<1 segundo)
   - Normal, até 3 segundos está ok
   - Não importa, pode demorar um pouco

Responda a, b.
"""

---

**Pergunta 9 - Limitações Conhecidas:**
"""
**9. Restrições e Limitações**

a) Tem alguma limitação técnica conhecida?
   - Sistema operacional específico (Windows only, Mac only, etc)
   - Navegador específico
   - Sem acesso a internet em produção
   - Outra: [especificar]
   - Nenhuma limitação

b) Tem alguma tecnologia que você NÃO quer usar?
   - Nenhuma preferência
   - Evitar: [especificar tecnologias/frameworks]

Responda a, b.
"""

---

**Pergunta 10 - Ambiente de Desenvolvimento vs Produção:**
"""
**10. Ambientes Dev e Produção**

Desenvolvimento e produção vão rodar no mesmo ambiente?

a) Ambiente de DESENVOLVIMENTO (onde você vai codar):
   - Windows
   - Mac
   - Linux
   - Docker no Windows/Mac
   - Outro: [especificar]

b) Ambiente de PRODUÇÃO (onde o sistema vai rodar de verdade):
   - Mesmo que desenvolvimento
   - Linux (VM ou servidor)
   - Docker/Docker Compose
   - Cloud (Railway, Vercel, AWS, etc)
   - Outro: [especificar]

c) Se dev e prod são DIFERENTES, tem algo que funciona 
   diferente entre eles? (Ex: caminhos de arquivo, DNS, 
   certificados SSL, variáveis de ambiente)
   - Sim: [descrever]
   - Não sei
   - Não se aplica (mesmo ambiente)

Responda a, b, c.

IMPORTANTE PARA A IA: Se dev e prod são ambientes diferentes,
incluir nos alertas_tecnicos. Ex: "Testar no Linux antes de 
deploy - SSL e DNS podem divergir do Windows."
"""

---

**Pergunta 11 - Pegadinhas do Domínio:**
"""
**11. Pegadinhas Técnicas do Domínio**

Existe alguma pegadinha técnica no domínio deste projeto que eu deva saber?

Coisas que SÓ QUEM TRABALHA NA ÁREA sabe e que podem causar problemas:

Exemplos:
- "A API do vCenter perde logs após 30 dias"
- "O certificado SSL é auto-assinado, precisa de verify=False"
- "Alguns campos vêm vazios às vezes, precisa de fallback"
- "O endpoint muda entre versão 7 e 8 do produto"
- "Dados chegam em fuso horário UTC mas usuário espera local"

a) Tem pegadinhas técnicas que eu deva saber?
   - Sim: [listar todas que lembrar - quanto mais melhor]
   - Não, nenhuma que eu saiba
   - Não sei

IMPORTANTE PARA A IA: Estas pegadinhas são CRÍTICAS. Adicione 
TODAS ao campo alertas_tecnicos do JSON. Mesmo que pareçam 
óbvias para o usuário, a IA de desenvolvimento precisa saber.
"""

---

### 3. ANALISAR RESPOSTAS E GERAR JSON

Após receber as 11 respostas, ANALISE e gere um JSON estruturado:

"""
ANÁLISE DAS RESPOSTAS TÉCNICAS:

Baseado nas suas respostas, detectei:

**Database Recomendado:**
[SQLite / PostgreSQL / MongoDB / File system]
Motivo: [justificar baseado em volume, offline, custo]

**Deploy Recomendado:**
[Local only / Railway / Vercel / Outro]
Motivo: [justificar baseado em budget, 24/7, escala]

**Tech Stack Sugerido:**
- Backend: [Next.js API Routes / Express / FastAPI]
- Frontend: [Next.js / React]
- Database: [escolhido acima]
- ORM: [Prisma / Drizzle / Mongoose]

Motivo: [justificar escolhas baseado em contexto + respostas]

**Alertas Importantes:**
[Se detectou conflitos ou limitações, listar aqui]

Exemplo:
ALERTA: Você quer Railway deploy MAS mencionou usar SQLite
   -> SQLite não persiste em Railway (filesystem efêmero)
   -> Sugestão: mudar para PostgreSQL OU deploy local

---

JSON ESTRUTURADO:

```json
{
  "projeto": {
    "nome": "[extrair da Parte 0]",
    "contexto": "[resumo de 1 frase]"
  },
  "decisoes_tecnicas": {
    "sdk_obrigatorio": {
      "tem": true/false,
      "biblioteca": "[nome da biblioteca]",
      "linguagem_obrigatoria": "[python/node/java/etc]",
      "impacto": "[define backend framework]"
    },
    "database": {
      "tipo": "[sqlite/postgresql/mongodb/filesystem]",
      "volume_estimado": "[numero de registros]",
      "offline_required": true/false,
      "multiuser": true/false,
      "justificativa": "[motivo da escolha]"
    },
    "deploy": {
      "tipo": "[local/railway/vercel/docker-compose/outro]",
      "disponibilidade": "[24-7/best-effort]",
      "budget": "[free/paid]",
      "justificativa": "[motivo da escolha]"
    },
    "ambientes": {
      "desenvolvimento": "[windows/mac/linux/docker]",
      "producao": "[mesmo/linux/docker-compose/cloud]",
      "diferencas": "[descrever se dev != prod, ex: SSL, DNS, paths]"
    },
    "uploads": {
      "necessario": true/false,
      "tipos": ["imagem", "pdf"],
      "tamanho_max": "[MB]"
    },
    "automacao": {
      "necessaria": true/false,
      "descricao": "[o que automatizar]",
      "frequencia": "[daily/hourly/weekly]"
    },
    "autenticacao": {
      "necessaria": true/false,
      "usuarios_simultaneos": "[numero]",
      "roles": true/false
    },
    "integracoes": {
      "necessarias": true/false,
      "lista": ["stripe", "sendgrid"]
    },
    "performance": {
      "operacoes_dia": "[numero]",
      "tempo_resposta": "[fast/normal/slow]"
    }
  },
  "alertas_tecnicos": [
    "[conflito detectado 1]",
    "[conflito detectado 2]",
    "[pegadinha do dominio 1 - da pergunta 11]",
    "[pegadinha do dominio 2 - da pergunta 11]"
  ]
}
```

---

PRÓXIMO PASSO:

Salve este JSON em um arquivo local.

Depois, abra um NOVO chat no Claude e cole o prompt:
**DESC03 - Contextuais.md**

Anexe:
1. O resumo de contexto do DESC01
2. Este JSON do DESC02

Isso vai permitir perguntas contextualizadas sobre UI, telas e workflows.
"""

---

## EXEMPLO DE ANÁLISE

**Se usuário respondeu:**
1. Database: 5.000 registros, offline não, multiuser sim
2. Deploy: Railway free tier, 24/7 sim
3. Upload: Sim, imagens pequenas
4. Automação: Não
5. Login: Sim, 10 usuários, roles diferentes
6. Integração: Cotação moeda
7. Performance: 500 ops/dia, normal
8. Limitações: Nenhuma

**IA detecta conflito:**
ALERTA: Railway + arquivo uploads = problema (ephemeral filesystem)
-> Sugestão: usar cloud storage (Cloudinary/S3) OU deploy local

**IA gera JSON:**
```json
{
  "projeto": {
    "nome": "Sistema Estoque",
    "contexto": "Automatizar atualização de estoque"
  },
  "decisoes_tecnicas": {
    "database": {
      "tipo": "postgresql",
      "volume_estimado": "5000",
      "offline_required": false,
      "multiuser": true,
      "justificativa": "Multiuser + Railway = precisa PostgreSQL"
    },
    "deploy": {
      "tipo": "railway",
      "disponibilidade": "24-7",
      "budget": "free",
      "justificativa": "Free tier suficiente para 500 ops/dia"
    },
    "uploads": {
      "necessario": true,
      "tipos": ["imagem"],
      "tamanho_max": "1MB"
    }
  },
  "alertas": [
    "Railway filesystem é efêmero - usar Cloudinary para imagens"
  ]
}
```

---

## VALIDAÇÃO

Após executar este prompt, você deve ter:
- 11 perguntas respondidas
- JSON estruturado gerado
- Alertas de conflitos (se houver)
- Pegadinhas do domínio registradas
- Tech stack sugerido (respeitando SDK obrigatório se houver)
- Ambientes dev/prod documentados
- Direcionamento para DESC03

Se JSON está incompleto, peça para IA regenerar.
```
