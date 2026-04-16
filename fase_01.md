# fase_01.md — Sobra
> Setup e Infraestrutura

---

## BLOCO_DE_CONTROLE_DE_EXECUCAO

- MODO_EXECUCAO: step-by-step
- NIVEL_COMPLEXIDADE: medio
- LIMITE_CONTEXTO: parar ao atingir 55-60% do contexto disponivel e emitir handoff estruturado
- POLITICA_HANDOFF:
  - registrar progresso por subtarefa (concluida / parcial / pendente)
  - listar arquivos criados ou modificados com caminho completo
  - listar comandos executados e status (sucesso / falha)
  - listar pendencias e riscos identificados
  - sugerir proximo passo exato antes de encerrar
- SAIDA_OBRIGATORIA:
  - resumo executivo da fase
  - arquivos criados/modificados
  - comandos executados
  - validacoes automaticas realizadas
  - pendencias e proximos passos

---

## PLANO_DE_FASES_DO_PROJETO

Gerado a partir da analise do escopo.md. Apresentado uma vez aqui como referencia.

- Fase 1: Setup e Infraestrutura (6 subtarefas) — projeto Next.js, Tailwind, shadcn/ui, Prisma, schema do banco, seed, CRON, deploy Railway
- Fase 2: Backend Core (5 subtarefas) — API routes, logica de calculo do saldo diario, acumulo CRON, pagamentos mensais, a receber
- Fase 3: Frontend — Dashboard e Fluxos Principais (5 subtarefas) — dashboard com numero principal, modal de gasto, pagamentos do mes, a receber, saldos por banco
- Fase 4: Frontend — Configuracoes e Polish (4 subtarefas) — CRUD de configuracoes, dark/light mode, loading states, mensagens de erro e validacoes visuais

Total: 4 fases, 20 subtarefas

IGNORADAS (sem detalhamento suficiente para implementacao neste ciclo):
- Upload PDF/CSV de faturas (Fase 2 do roadmap)
- Categorizacao automatica com aprendizado (Fase 2 do roadmap)
- Sistema de login (Fase 2 do roadmap — primeiro item pos-MVP)
- Graficos e comparativos (Fase 2 do roadmap)
- Alertas, historico, exportacao, Open Finance (Fase 3 do roadmap)

---

## OBJETIVO_DA_FASE

Criar a estrutura base do projeto Sobra: repositorio configurado, dependencias instaladas, banco de dados modelado via Prisma, seed com dados reais e deploy inicial funcionando no Railway.

Ao final desta fase, o projeto deve compilar sem erros, conectar ao PostgreSQL do Railway e ter o banco populado com dados reais prontos para as proximas fases.

---

## ESCOPO_IN

- Criacao do projeto Next.js 14 com App Router e TypeScript
- Configuracao de Tailwind CSS e shadcn/ui
- Configuracao do Prisma com PostgreSQL (Railway)
- Schema completo do banco de dados (todas as entidades do escopo.md, secao 4)
- Seed com dados reais (bancos, cartoes, contas fixas, parcelas futuras, valores a receber, configuracao inicial)
- Configuracao do CRON de acumulo diario (estrutura e job — sem logica de calculo, que pertence a Fase 2)
- Variaveis de ambiente (.env.example e .env local)
- Deploy inicial no Railway (app rodando, banco conectado, sem erros)

## ESCOPO_OUT

- Nenhuma API route de negocio (pertencem a Fase 2)
- Nenhum componente de interface (pertencem a Fase 3)
- Logica de calculo do saldo diario (pertence a Fase 2)
- Logica de execucao do CRON (pertence a Fase 2 — aqui apenas a estrutura do job)
- Sistema de autenticacao (pos-MVP)
- Upload de arquivos PDF/CSV (Fase 2 do roadmap)

---

## DEPENDENCIAS

- Conta no Railway com projeto criado e PostgreSQL provisionado
- Node.js 20.x instalado localmente
- npm disponivel
- Repositorio Git inicializado ou pronto para inicializar
- DATABASE_URL do PostgreSQL do Railway disponivel

---

## SUBTAREFAS_SEQUENCIAIS

---

### SUBTAREFA 1 — Criar projeto Next.js com TypeScript

**[PRE-REQUISITOS]**
- Node.js 20.x instalado
- npm disponivel
- Nenhum arquivo de projeto existente no diretorio alvo

**[COMANDOS_DE_INSTALACAO]**
```bash
npx create-next-app@latest sobra \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --no-src-dir \
  --import-alias "@/*"
cd sobra
```

**[CONTEXTO]**
Inicializar o projeto Next.js 14 com App Router, TypeScript, Tailwind CSS e ESLint configurados pelo scaffold oficial. O flag `--app` garante o uso do App Router conforme decisao tecnica.

**[IMPLEMENTACAO]**
Apos o scaffold, verificar e ajustar `next.config.ts` (ou `next.config.js`):

```ts
// next.config.ts
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  experimental: {
    // habilitar apenas quando necessario nas proximas fases
  },
};

export default nextConfig;
```

Verificar que `tsconfig.json` possui:
```json
{
  "compilerOptions": {
    "strict": true,
    "target": "ES2017",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "preserve",
    "baseUrl": ".",
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}
```

**[ARQUIVOS_ENVOLVIDOS]**
- Criar: estrutura completa do projeto via scaffold
- Modificar: `next.config.ts`, `tsconfig.json` se necessario

**[REGRAS_DE_NEGOCIO]**
- Nenhuma regra de negocio nesta subtarefa

**[NAO_IMPLEMENTE]**
- Nenhuma pagina de conteudo
- Nenhum componente de UI
- Nenhuma rota de API

---

### SUBTAREFA 2 — Configurar shadcn/ui

**[PRE-REQUISITOS]**
- Subtarefa 1 concluida
- Projeto Next.js com Tailwind configurado

**[COMANDOS_DE_INSTALACAO]**
```bash
npx shadcn@latest init
```

Responder ao CLI:
- Style: Default
- Base color: Slate
- CSS variables: Yes

Instalar os componentes que serao usados nas fases seguintes (instalar agora para evitar interrupcoes):
```bash
npx shadcn@latest add button
npx shadcn@latest add input
npx shadcn@latest add label
npx shadcn@latest add select
npx shadcn@latest add dialog
npx shadcn@latest add dropdown-menu
npx shadcn@latest add card
npx shadcn@latest add badge
npx shadcn@latest add separator
npx shadcn@latest add switch
npx shadcn@latest add textarea
npx shadcn@latest add toast
npx shadcn@latest add skeleton
```

**[CONTEXTO]**
Configurar shadcn/ui como biblioteca de componentes base. Instalar todos os componentes previstos no escopo de uma vez para evitar instalacoes parciais nas fases seguintes.

**[IMPLEMENTACAO]**
Apos o init, confirmar que `components/ui/` foi criado com os componentes instalados.

Ajustar `app/globals.css` para incluir a variavel de fonte que sera usada. A tipografia definitiva sera definida na Fase 3, mas ja reservar as variaveis CSS:

```css
/* app/globals.css — adicionar apos as diretivas do shadcn/ui */
:root {
  --font-display: 'a-definir';
  --font-body: 'a-definir';
}
```

**[ARQUIVOS_ENVOLVIDOS]**
- Criar: `components/ui/*` (via shadcn CLI)
- Modificar: `app/globals.css`, `tailwind.config.ts`, `components.json`

**[REGRAS_DE_NEGOCIO]**
- Nenhuma regra de negocio nesta subtarefa

**[NAO_IMPLEMENTE]**
- Nenhum componente customizado ainda
- Nenhuma pagina de conteudo
- Nenhuma tipografia definitiva (sera decidida na Fase 3)

---

### SUBTAREFA 3 — Configurar Prisma e variaveis de ambiente

**[PRE-REQUISITOS]**
- Subtarefa 1 concluida
- DATABASE_URL do PostgreSQL do Railway disponivel

**[COMANDOS_DE_INSTALACAO]**
```bash
npm install prisma --save-dev
npm install @prisma/client
npx prisma init --datasource-provider postgresql
```

**[CONTEXTO]**
Instalar e inicializar o Prisma com PostgreSQL. Configurar variaveis de ambiente para desenvolvimento local e producao no Railway. Tratar os tres estados possíveis da env: ausente, invalida e valida.

**[IMPLEMENTACAO]**

Criar `.env.example` com placeholders documentados:
```env
# .env.example
# Conexao com o PostgreSQL do Railway
# Formato: postgresql://USER:PASSWORD@HOST:PORT/DATABASE
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE?schema=public"

# URL base da aplicacao (usado em links e CRON)
NEXT_PUBLIC_APP_URL="http://localhost:3000"

# Secret para o endpoint do CRON (prevencao de chamadas nao autorizadas)
CRON_SECRET="trocar-por-string-aleatoria-em-producao"
```

Criar `.env` local com os valores reais (NAO commitar):
```env
DATABASE_URL="postgresql://SEU_USER:SUA_SENHA@SEU_HOST:SEU_PORT/SEU_DATABASE?schema=public"
NEXT_PUBLIC_APP_URL="http://localhost:3000"
CRON_SECRET="dev-secret-local"
```

Confirmar que `.gitignore` ja inclui `.env` (o scaffold do Next.js faz isso automaticamente — verificar).

Criar `lib/env.ts` para validacao de env no startup:
```ts
// lib/env.ts
function getRequiredEnv(key: string): string {
  const value = process.env[key];
  if (!value || value.trim() === "") {
    const isProd = process.env.NODE_ENV === "production";
    if (isProd) {
      throw new Error(
        `[Sobra] Variavel de ambiente obrigatoria ausente ou vazia: ${key}. ` +
        `Configure esta variavel no Railway antes de fazer deploy.`
      );
    }
    console.warn(
      `[Sobra] AVISO: Variavel de ambiente ${key} ausente. ` +
      `Usando fallback de desenvolvimento — nao usar em producao.`
    );
    return "";
  }
  return value.trim();
}

export const env = {
  DATABASE_URL: getRequiredEnv("DATABASE_URL"),
  NEXT_PUBLIC_APP_URL: process.env.NEXT_PUBLIC_APP_URL ?? "http://localhost:3000",
  CRON_SECRET: getRequiredEnv("CRON_SECRET"),
};
```

Ajustar `prisma/schema.prisma` para apontar para a env correta:
```prisma
// prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

**[ARQUIVOS_ENVOLVIDOS]**
- Criar: `.env.example`, `lib/env.ts`, `prisma/schema.prisma` (via prisma init, ajustar)
- Modificar: `.gitignore` (verificar se `.env` ja esta ignorado)
- Nao commitar: `.env`

**[REGRAS_DE_NEGOCIO]**
- Em producao: falha imediata (throw) se DATABASE_URL ou CRON_SECRET ausentes
- Em desenvolvimento: warning no console, fallback vazio (permite rodar parcialmente)
- `.env` nunca deve ser commitado

**[NAO_IMPLEMENTE]**
- Schema do banco (proxima subtarefa)
- Nenhuma logica de negocio

---

### SUBTAREFA 4 — Criar schema completo do Prisma

**[PRE-REQUISITOS]**
- Subtarefa 3 concluida
- `prisma/schema.prisma` inicializado com datasource postgresql

**[CONTEXTO]**
Definir todas as entidades do modelo de dados conforme a Secao 4 do escopo.md. O schema deve ser completo para o MVP (Fase 1 do roadmap) e incluir as entidades de Fase 2 comentadas para referencia futura.

**[IMPLEMENTACAO]**

Substituir o conteudo de `prisma/schema.prisma` pelo schema completo abaixo:

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// ─────────────────────────────────────────────
// MVP — Fase 1
// ─────────────────────────────────────────────

model Banco {
  id           String       @id @default(cuid())
  nome         String
  saldoInicial Float        @default(0)
  cor          String
  ativo        Boolean      @default(true)
  createdAt    DateTime     @default(now())
  updatedAt    DateTime     @updatedAt

  transacoes   Transacao[]
  cartoes      Cartao[]
}

model Cartao {
  id             String          @id @default(cuid())
  nome           String
  bancoId        String
  diaVencimento  Int
  diaFechamento  Int
  cor            String
  ativo          Boolean         @default(true)
  createdAt      DateTime        @default(now())
  updatedAt      DateTime        @updatedAt

  banco          Banco           @relation(fields: [bancoId], references: [id])
  faturas        Fatura[]
  transacoes     Transacao[]
  parcelasFuturas ParcelaFutura[]
}

model Transacao {
  id         String          @id @default(cuid())
  tipo       TipoTransacao
  meio       MeioPagamento
  valor      Float
  descricao  String?
  categoria  String
  bancoId    String?
  cartaoId   String?
  data       DateTime        @default(now())
  createdAt  DateTime        @default(now())
  updatedAt  DateTime        @updatedAt

  banco      Banco?          @relation(fields: [bancoId], references: [id])
  cartao     Cartao?         @relation(fields: [cartaoId], references: [id])
}

model ContaFixa {
  id             String             @id @default(cuid())
  nome           String
  valorPadrao    Float
  diaVencimento  Int
  categoria      String
  ativo          Boolean            @default(true)
  createdAt      DateTime           @default(now())
  updatedAt      DateTime           @updatedAt

  pagamentos     PagamentoMensal[]
}

model PagamentoMensal {
  id             String     @id @default(cuid())
  contaFixaId    String
  mes            Int
  ano            Int
  valorReal      Float
  pago           Boolean    @default(false)
  dataPagamento  DateTime?
  observacao     String?
  createdAt      DateTime   @default(now())
  updatedAt      DateTime   @updatedAt

  contaFixa      ContaFixa  @relation(fields: [contaFixaId], references: [id])

  @@unique([contaFixaId, mes, ano])
}

model Fatura {
  id             String          @id @default(cuid())
  cartaoId       String
  mes            Int
  ano            Int
  pago           Boolean         @default(false)
  dataPagamento  DateTime?
  observacao     String?
  createdAt      DateTime        @default(now())
  updatedAt      DateTime        @updatedAt

  cartao         Cartao          @relation(fields: [cartaoId], references: [id])
  parcelasFuturas ParcelaFutura[]
  // lancamentos LancamentoFatura[] — habilitado na Fase 2

  @@unique([cartaoId, mes, ano])
}

model ParcelaFutura {
  id         String   @id @default(cuid())
  cartaoId   String
  descricao  String
  valor      Float
  mes        Int
  ano        Int
  faturaId   String?
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt

  cartao     Cartao   @relation(fields: [cartaoId], references: [id])
  fatura     Fatura?  @relation(fields: [faturaId], references: [id])
}

model ValorAReceber {
  id              String    @id @default(cuid())
  descricao       String
  valor           Float
  dataEsperada    DateTime
  recebido        Boolean   @default(false)
  dataRecebimento DateTime?
  observacao      String?
  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt
}

model AcumuloDiario {
  id              String   @id @default(cuid())
  data            DateTime @unique @db.Date
  limiteDia       Float
  gastoReal       Float
  acumuloGerado   Float
  createdAt       DateTime @default(now())
  updatedAt       DateTime @updatedAt
}

model ConfiguracaoApp {
  id             String  @id @default(cuid())
  reservaMinima  Float   @default(500)
  tema           Tema    @default(dark)
  createdAt      DateTime @default(now())
  updatedAt      DateTime @updatedAt
}

// ─────────────────────────────────────────────
// FASE 2 — NAO HABILITAR NO MVP
// Entidades comentadas para referencia futura:
//
// model LancamentoFatura { ... }
// model Categoria { ... }
// model PadraoCategoria { ... }
// ─────────────────────────────────────────────

enum TipoTransacao {
  GASTO
  ENTRADA
}

enum MeioPagamento {
  PIX
  CARTAO
  BOLETO
  DINHEIRO
}

enum Tema {
  dark
  light
}
```

Apos criar o schema, criar a migration inicial:
```bash
npx prisma migrate dev --name init
```

Gerar o Prisma Client:
```bash
npx prisma generate
```

**[ARQUIVOS_ENVOLVIDOS]**
- Modificar: `prisma/schema.prisma`
- Criar: `prisma/migrations/` (gerado automaticamente pelo migrate)

**[REGRAS_DE_NEGOCIO]**
- `saldoInicial` em Banco: Float >= 0 (validado na API, nao no schema Prisma)
- `valor` em Transacao, ContaFixa, PagamentoMensal, ParcelaFutura, ValorAReceber: Float > 0 (validado na API)
- `diaVencimento` e `diaFechamento` em Cartao: Int entre 1 e 31 (validado na API)
- `mes` em PagamentoMensal, Fatura, ParcelaFutura: Int entre 1 e 12 (validado na API)
- `PagamentoMensal` tem constraint unique em [contaFixaId, mes, ano] — impede duplicata
- `Fatura` tem constraint unique em [cartaoId, mes, ano] — impede duplicata
- `AcumuloDiario` tem unique em `data` — apenas um registro por dia
- `valorTotal` de Fatura NAO existe como campo — calculado dinamicamente na API (soma ParcelaFutura do mes correspondente)
- `ConfiguracaoApp` deve ter exatamente um registro — garantido via seed (nao ha constraint no schema; verificar na API de leitura/escrita)

**[NAO_IMPLEMENTE]**
- Entidades de Fase 2 (LancamentoFatura, Categoria, PadraoCategoria)
- Nenhuma API route
- Nenhum componente de interface

---

### SUBTAREFA 5 — Criar seed com dados reais

**[PRE-REQUISITOS]**
- Subtarefa 4 concluida
- Migration `init` aplicada com sucesso
- Banco PostgreSQL acessivel via DATABASE_URL

**[CONTEXTO]**
Popular o banco com dados reais de uso imediato: bancos existentes, cartoes, contas fixas, parcelas futuras ate dezembro do ano corrente, valores a receber e configuracao inicial do app.

**[IMPLEMENTACAO]**

Criar `prisma/seed.ts`:

```ts
// prisma/seed.ts
import { PrismaClient, MeioPagamento, TipoTransacao } from "@prisma/client";

const prisma = new PrismaClient();

async function main() {
  console.log("Iniciando seed...");

  // ── Limpar dados existentes (ordem importa por FKs) ──────────────────
  await prisma.acumuloDiario.deleteMany();
  await prisma.transacao.deleteMany();
  await prisma.parcelaFutura.deleteMany();
  await prisma.fatura.deleteMany();
  await prisma.pagamentoMensal.deleteMany();
  await prisma.contaFixa.deleteMany();
  await prisma.valorAReceber.deleteMany();
  await prisma.cartao.deleteMany();
  await prisma.banco.deleteMany();
  await prisma.configuracaoApp.deleteMany();

  // ── ConfiguracaoApp ──────────────────────────────────────────────────
  await prisma.configuracaoApp.create({
    data: {
      reservaMinima: 500,
      tema: "dark",
    },
  });

  // ── Bancos ───────────────────────────────────────────────────────────
  // INSTRUCAO: Substituir saldoInicial pelos valores reais pos-salario
  // no momento da primeira execucao do seed.

  const nubank = await prisma.banco.create({
    data: {
      nome: "Nubank",
      saldoInicial: 0, // SUBSTITUIR pelo saldo real
      cor: "#820AD1",
    },
  });

  const c6 = await prisma.banco.create({
    data: {
      nome: "C6 Bank",
      saldoInicial: 0, // SUBSTITUIR pelo saldo real
      cor: "#000000",
    },
  });

  const bradesco = await prisma.banco.create({
    data: {
      nome: "Bradesco",
      saldoInicial: 0, // SUBSTITUIR pelo saldo real
      cor: "#CC0000",
    },
  });

  const mercadoPago = await prisma.banco.create({
    data: {
      nome: "Mercado Pago",
      saldoInicial: 0, // SUBSTITUIR pelo saldo disponivel (nao o a liberar)
      cor: "#009EE3",
    },
  });

  // ── Cartoes ───────────────────────────────────────────────────────────
  // INSTRUCAO: Confirmar diaVencimento e diaFechamento para cada cartao.

  const cartaoNubank = await prisma.cartao.create({
    data: {
      nome: "Nubank Credito",
      bancoId: nubank.id,
      diaVencimento: 10, // CONFIRMAR
      diaFechamento: 3,  // CONFIRMAR
      cor: "#820AD1",
    },
  });

  const cartaoC6 = await prisma.cartao.create({
    data: {
      nome: "C6 Bank Credito",
      bancoId: c6.id,
      diaVencimento: 10, // CONFIRMAR
      diaFechamento: 3,  // CONFIRMAR
      cor: "#000000",
    },
  });

  const cartaoBradesco = await prisma.cartao.create({
    data: {
      nome: "Bradesco Credito",
      bancoId: bradesco.id,
      diaVencimento: 10, // CONFIRMAR
      diaFechamento: 3,  // CONFIRMAR
      cor: "#CC0000",
    },
  });

  const cartaoMercadoPago = await prisma.cartao.create({
    data: {
      nome: "Mercado Pago Credito",
      bancoId: mercadoPago.id,
      diaVencimento: 10, // CONFIRMAR
      diaFechamento: 3,  // CONFIRMAR
      cor: "#009EE3",
    },
  });

  // ── Contas Fixas ──────────────────────────────────────────────────────
  // INSTRUCAO: Ajustar nomes, valores e dias de vencimento conforme realidade.

  const contasFixas = await Promise.all([
    prisma.contaFixa.create({
      data: {
        nome: "Aluguel",
        valorPadrao: 0, // SUBSTITUIR
        diaVencimento: 10,
        categoria: "Moradia",
      },
    }),
    prisma.contaFixa.create({
      data: {
        nome: "Energisa",
        valorPadrao: 0, // SUBSTITUIR — oscila, valorReal sera editado mensalmente
        diaVencimento: 15,
        categoria: "Moradia",
      },
    }),
    prisma.contaFixa.create({
      data: {
        nome: "Internet",
        valorPadrao: 0, // SUBSTITUIR
        diaVencimento: 20,
        categoria: "Moradia",
      },
    }),
  ]);

  // ── PagamentoMensal do mes corrente para cada ContaFixa ───────────────
  const agora = new Date();
  const mesAtual = agora.getMonth() + 1;
  const anoAtual = agora.getFullYear();

  for (const conta of contasFixas) {
    await prisma.pagamentoMensal.create({
      data: {
        contaFixaId: conta.id,
        mes: mesAtual,
        ano: anoAtual,
        valorReal: conta.valorPadrao,
        pago: false,
      },
    });
  }

  // ── Faturas dos cartoes para o mes corrente ────────────────────────────
  const cartoes = [cartaoNubank, cartaoC6, cartaoBradesco, cartaoMercadoPago];
  const faturas: Record<string, { id: string }> = {};

  for (const cartao of cartoes) {
    const fatura = await prisma.fatura.create({
      data: {
        cartaoId: cartao.id,
        mes: mesAtual,
        ano: anoAtual,
        pago: false,
      },
    });
    faturas[cartao.id] = fatura;
  }

  // ── Parcelas Futuras ──────────────────────────────────────────────────
  // INSTRUCAO: Adicionar todas as parcelas futuras conhecidas ate dezembro.
  // Exemplo de estrutura (descomentar e preencher com dados reais):
  //
  // await prisma.parcelaFutura.create({
  //   data: {
  //     cartaoId: cartaoNubank.id,
  //     descricao: "Nome da compra parcelada",
  //     valor: 0, // valor de CADA parcela
  //     mes: 4,
  //     ano: anoAtual,
  //   },
  // });

  // ── Valores a Receber ─────────────────────────────────────────────────
  // INSTRUCAO: Adicionar valores esperados com datas previstas.
  // Mercado Pago "a liberar" tambem entra aqui como ValorAReceber.
  //
  // Exemplo:
  // await prisma.valorAReceber.create({
  //   data: {
  //     descricao: "Venda XYZ",
  //     valor: 0, // SUBSTITUIR
  //     dataEsperada: new Date("2025-04-15"),
  //   },
  // });

  console.log("Seed concluido.");
  console.log("ATENCAO: Revise os valores marcados com 'SUBSTITUIR' antes de usar o app em producao.");
}

main()
  .catch((e) => {
    console.error("Erro no seed:", e);
    process.exit(1);
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
```

Adicionar configuracao do seed no `package.json`:
```json
{
  "prisma": {
    "seed": "ts-node --compiler-options {\"module\":\"CommonJS\"} prisma/seed.ts"
  }
}
```

Instalar dependencia de execucao do seed:
```bash
npm install --save-dev ts-node
```

Executar o seed:
```bash
npx prisma db seed
```

**[ARQUIVOS_ENVOLVIDOS]**
- Criar: `prisma/seed.ts`
- Modificar: `package.json` (adicionar bloco `prisma.seed`)

**[REGRAS_DE_NEGOCIO]**
- `saldoInicial` dos bancos representa o saldo pos-salario no momento do cadastro — o sistema nao recalcula entradas de salario automaticamente
- Saldo disponivel do Mercado Pago entra em `saldoInicial`; saldo a liberar entra como `ValorAReceber` com `dataEsperada`
- `ConfiguracaoApp` deve ter exatamente um registro — o seed deleta tudo antes de inserir, garantindo isso
- Parcelas futuras: cadastrar uma entrada por mes/cartao ate dezembro do ano corrente
- `PagamentoMensal` gerado com `valorReal = valorPadrao` — editavel mensalmente sem alterar historico

**[NAO_IMPLEMENTE]**
- Dados de usuarios (sem autenticacao no MVP)
- Dados de LancamentoFatura, Categoria, PadraoCategoria (Fase 2)
- Logica de calculo no seed (apenas insercao de dados)

---

### SUBTAREFA 6 — Configurar CRON e fazer deploy no Railway

**[PRE-REQUISITOS]**
- Subtarefas 1 a 5 concluidas
- Banco populado com seed
- Conta no Railway com projeto configurado
- Variaveis de ambiente configuradas no Railway (DATABASE_URL, CRON_SECRET, NEXT_PUBLIC_APP_URL)

**[COMANDOS_DE_INSTALACAO]**
```bash
npm install node-cron
npm install --save-dev @types/node-cron
```

**[CONTEXTO]**
Criar a estrutura do job CRON que rodara todo dia as 00:01. Nesta fase, apenas o esqueleto do job e a rota de API que o dispara. A logica de calculo do acumulo sera implementada na Fase 2.

**[IMPLEMENTACAO]**

Criar a rota de API para o CRON (chamada pelo Railway Cron ou por chamada HTTP autenticada):

```ts
// app/api/cron/acumulo-diario/route.ts
import { NextRequest, NextResponse } from "next/server";
import { env } from "@/lib/env";

export async function POST(request: NextRequest) {
  const secret = request.headers.get("x-cron-secret");

  if (secret !== env.CRON_SECRET) {
    return NextResponse.json({ error: "Unauthorized" }, { status: 401 });
  }

  try {
    // TODO (Fase 2): implementar logica de calculo do acumulo diario
    // 1. Buscar transacoes do dia anterior
    // 2. Calcular gastoReal
    // 3. Calcular limiteDia
    // 4. Calcular acumuloGerado = max(0, limiteDia - gastoReal)
    // 5. Verificar soma dos acumulos dos ultimos 3 dias (teto)
    // 6. Persistir em AcumuloDiario

    console.log(`[CRON] acumulo-diario executado em ${new Date().toISOString()} — logica pendente (Fase 2)`);

    return NextResponse.json({
      success: true,
      message: "CRON registrado. Logica de calculo sera implementada na Fase 2.",
      executedAt: new Date().toISOString(),
    });
  } catch (error) {
    console.error("[CRON] Erro ao executar acumulo-diario:", error);
    return NextResponse.json(
      { error: "Erro interno no CRON" },
      { status: 500 }
    );
  }
}
```

Criar `railway.json` na raiz do projeto para configurar o CRON no Railway:
```json
{
  "$schema": "https://railway.app/railway.schema.json",
  "build": {
    "builder": "NIXPACKS"
  },
  "deploy": {
    "startCommand": "npm run start",
    "restartPolicyType": "ON_FAILURE",
    "restartPolicyMaxRetries": 3
  }
}
```

Configurar o CRON no painel do Railway:
- Acesse o servico no Railway
- Va em Settings > Cron Jobs
- Adicione: `1 0 * * *` (todo dia as 00:01)
- Comando: `curl -X POST $NEXT_PUBLIC_APP_URL/api/cron/acumulo-diario -H "x-cron-secret: $CRON_SECRET"`

Criar `Procfile` como alternativa ao `railway.json` se o NIXPACKS nao reconhecer:
```
web: npm run start
```

Configurar o script de start no `package.json` (verificar se ja existe):
```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "typecheck": "tsc --noEmit"
  }
}
```

Commit e push para o repositorio vinculado ao Railway:
```bash
git add .
git commit -m "feat: setup inicial — Next.js, Prisma, schema, seed, CRON skeleton"
git push
```

Apos o deploy automatico do Railway, executar o seed em producao via Railway CLI ou pelo painel:
```bash
# Via Railway CLI (se instalado)
railway run npx prisma db seed

# Ou via painel: Railway > Service > Settings > Deploy > Run Command
# npx prisma db seed
```

**[ARQUIVOS_ENVOLVIDOS]**
- Criar: `app/api/cron/acumulo-diario/route.ts`, `railway.json`, `Procfile` (opcional)
- Modificar: `package.json` (scripts e bloco prisma.seed)

**[REGRAS_DE_NEGOCIO]**
- CRON executa todo dia as 00:01 (expressao cron: `1 0 * * *`)
- Autenticacao do endpoint CRON via header `x-cron-secret` — rejeitar com 401 se ausente ou invalido
- Logica de calculo permanece como TODO — nao implementar aqui (Fase 2)
- Limite maximo de 3 dias de acumulo — implementado na Fase 2

**[NAO_IMPLEMENTE]**
- Logica de calculo do acumulo (Fase 2)
- Nenhum componente de interface
- Nenhuma outra API route de negocio

---

## ARQUIVOS_ALVO

```
sobra/
├── app/
│   ├── api/
│   │   └── cron/
│   │       └── acumulo-diario/
│   │           └── route.ts
│   └── globals.css
├── components/
│   └── ui/           (gerado pelo shadcn CLI)
├── lib/
│   └── env.ts
├── prisma/
│   ├── migrations/   (gerado pelo prisma migrate)
│   ├── schema.prisma
│   └── seed.ts
├── .env              (nao commitar)
├── .env.example
├── .gitignore
├── next.config.ts
├── package.json
├── railway.json
├── tsconfig.json
└── Procfile          (opcional)
```

---

## REGRAS_DE_NEGOCIO

Resumo das regras aplicaveis a esta fase:

1. `saldoInicial` dos bancos e o saldo pos-salario — entradas de salario futuras sao registradas como Transacao (ENTRADA) ou ValorAReceber, nao recalculadas automaticamente
2. `valorTotal` de Fatura e calculado dinamicamente na API — nunca armazenar como campo estatico no banco
3. `ValorAReceber` nao entra no saldo disponivel ate `recebido = true` — validado no backend
4. `PagamentoMensal` tem unique constraint em [contaFixaId, mes, ano]
5. `Fatura` tem unique constraint em [cartaoId, mes, ano]
6. `AcumuloDiario` tem unique constraint em `data`
7. `ConfiguracaoApp` deve ter exatamente um registro no banco
8. CRON protegido por `x-cron-secret` — rejeitar requests sem header valido
9. Saldo a liberar do Mercado Pago modelado como `ValorAReceber` com `dataEsperada`

---

## NAO_IMPLEMENTE

- Nenhuma API route de negocio (Fase 2)
- Nenhum componente de interface ou pagina (Fase 3)
- Logica de calculo do saldo diario (Fase 2)
- Logica de execucao real do CRON (Fase 2 — apenas estrutura aqui)
- Sistema de autenticacao (pos-MVP)
- Entidades de Fase 2: LancamentoFatura, Categoria, PadraoCategoria
- Upload ou processamento de arquivos PDF/CSV
- Tipografia definitiva (Fase 3)

---

## TESTES_AUTOMATIZADOS_OBRIGATORIOS

### 1. Typecheck

```bash
npm run typecheck
```

Aprovado: zero erros TypeScript.
Reprovado: qualquer erro de tipo. Corrigir antes de prosseguir.

### 2. Build de producao

```bash
npm run build
```

Aprovado: build finaliza sem erros (`✓ Compiled successfully`).
Reprovado: qualquer erro de compilacao. Corrigir antes de prosseguir.

### 3. Lint

```bash
npm run lint
```

Aprovado: zero erros de lint (warnings sao aceitaveis nesta fase).
Reprovado: erros que bloqueiam o build. Corrigir antes de prosseguir.

### 4. Conexao com banco (smoke test)

```bash
npx prisma db pull
```

Aprovado: schema refletido sem erros — confirma que a conexao com o PostgreSQL esta funcionando.
Reprovado: erro de conexao. Verificar DATABASE_URL e status do servico no Railway.

### 5. Validacao do schema

```bash
npx prisma validate
```

Aprovado: `The schema at prisma/schema.prisma is valid`.
Reprovado: erros de schema. Corrigir antes de continuar.

### 6. Verificacao do seed

```bash
npx prisma studio
```

Abrir no navegador e verificar:
- Tabela `Banco`: registros presentes
- Tabela `ConfiguracaoApp`: exatamente 1 registro
- Tabela `PagamentoMensal`: registros do mes corrente presentes
- Tabela `Fatura`: registros do mes corrente presentes

Aprovado: todas as tabelas acima com dados conforme o seed.
Reprovado: tabelas vazias ou ausentes. Reexecutar `npx prisma db seed`.

### 7. Smoke test do endpoint CRON

```bash
# Com o servidor rodando localmente (npm run dev):
curl -X POST http://localhost:3000/api/cron/acumulo-diario \
  -H "x-cron-secret: dev-secret-local" \
  -H "Content-Type: application/json"
```

Aprovado: resposta HTTP 200 com `{ "success": true }`.
Reprovado: erro 401 (secret errado — verificar .env), erro 500 (erro interno — verificar logs).

```bash
# Testar rejeicao de request sem secret:
curl -X POST http://localhost:3000/api/cron/acumulo-diario
```

Aprovado: resposta HTTP 401.
Reprovado: qualquer outra resposta.

---

## VALIDACAO_MANUAL_OPCIONAL

Nao aplicavel nesta fase — sem UI/UX para validar.

---

## CRITERIO_DE_CONCLUSAO

- [ ] Projeto Next.js criado e rodando localmente com `npm run dev`
- [ ] shadcn/ui configurado e componentes base instalados em `components/ui/`
- [ ] Prisma configurado com PostgreSQL Railway
- [ ] `npx prisma validate` sem erros
- [ ] Migration `init` aplicada com sucesso (`prisma/migrations/` criada)
- [ ] Seed executado sem erros — dados visiveis no Prisma Studio
- [ ] `ConfiguracaoApp` com exatamente 1 registro no banco
- [ ] `npm run typecheck` sem erros
- [ ] `npm run build` sem erros
- [ ] `npm run lint` sem erros bloqueantes
- [ ] Endpoint `POST /api/cron/acumulo-diario` retorna 200 com secret correto
- [ ] Endpoint `POST /api/cron/acumulo-diario` retorna 401 sem secret
- [ ] Deploy no Railway funcionando (app acessivel via URL do Railway)
- [ ] CRON configurado no Railway (`1 0 * * *`)
- [ ] Nenhum item de `NAO_IMPLEMENTE` foi implementado

---

## FORMATO_DE_HANDOFF

Se o limite de contexto for atingido antes da conclusao, emitir:

```
## HANDOFF — fase_01.md

PROGRESSO:
- Subtarefa 1 (Criar projeto): [concluida | parcial | pendente]
- Subtarefa 2 (shadcn/ui): [concluida | parcial | pendente]
- Subtarefa 3 (Prisma + env): [concluida | parcial | pendente]
- Subtarefa 4 (Schema): [concluida | parcial | pendente]
- Subtarefa 5 (Seed): [concluida | parcial | pendente]
- Subtarefa 6 (CRON + deploy): [concluida | parcial | pendente]

ARQUIVOS_ALTERADOS: [lista com caminhos completos]

COMANDOS_EXECUTADOS: [lista com status de cada comando]

TESTES_EXECUTADOS: [lista com aprovado/reprovado]

PENDENCIAS: [lista]

RISCOS: [lista]

PROXIMO_PASSO_EXATO: [acao objetiva e especifica]
```
