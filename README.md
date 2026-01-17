<div align="center">
<img src="/enter.png" alt="esse é apenas o primeiro passo" />
</div>

# Primeira etapa: liberdade de backend, sem retrabalho

Nesta primeira etapa, a ideia é não quebrar nada do que você já tem.
Você pode continuar usando Firebase normalmente, enquanto criamos uma réplica em tempo real dos dados.

A diferença é que, a partir daqui, você passa a ter liberdade total de infraestrutura:

seguir só com Firebase,

usar Postgres local,

ou rodar os dois em paralelo, sem mudar seu código de negócio.

Eu vou entregar uma biblioteca compatível com as rotas do Firebase, mas implementada sobre Postgres.
Na prática, isso significa: mesmas chamadas, mesmos contratos, outro backend.

> Vamos iniciar

```txt
Você é um agente de infraestrutura especializado em Supabase, Postgres e migração zero-loss.

Objetivo:
Copiar TODO o banco de dados de um projeto Supabase para um Postgres local
e reimplementar TODAS as Edge Functions como uma API HTTP local,
mantendo exatamente as mesmas rotas, contratos e comportamentos.

Contexto técnico obrigatório:
- Você tem acesso ao MCP do Supabase
- O Postgres local será o sistema de verdade após a migração
- A API local deve substituir completamente as Edge Functions
- Nenhuma rota pode mudar
- Nenhum contrato pode mudar
- Nenhum dado pode ser perdido
```

## PARTE 1 — Dump completo do Supabase

Usando o MCP do Supabase, faça:

1. Descobrir automaticamente:
   - Todos os schemas
   - Todas as tabelas
   - Views
   - Índices
   - Constraints
   - Triggers
   - Policies de RLS
   - Functions SQL
   - Extensions usadas

2. Exportar:
   - Estrutura completa (DDL)
   - Dados (DML)
   - Configurações críticas (timezone, encodings, extensions)

3. Gerar:
   - Um script SQL idempotente para recriar tudo no Postgres local
   - Um script separado apenas de dados (COPY ou INSERT otimizado)

⚠️ Regra:
Nada pode ser omitido.
Se algo não puder ser migrado automaticamente, liste explicitamente como BLOCKER.

## PARTE 2 — Importação no Postgres local

1. Criar instruções claras para:
   - Subir um Postgres local (Docker utilize a porta 4444)
   - Aplicar o schema
   - Aplicar os dados
   - Validar integridade referencial

2. Gerar comandos de verificação:
   - Contagem de linhas por tabela (Supabase vs local)
   - Hash ou checksum de amostras de dados
   - Verificação de funções e triggers

## PARTE 3 — Mapeamento das Edge Functions

```txt
Usando o MCP do Supabase:

1. Listar TODAS as Edge Functions:
   - Nome
   - Rota HTTP
   - Método (GET, POST, etc)
   - Headers esperados
   - Auth (JWT, anon, service role)
   - Variáveis de ambiente
   - Dependências externas

2. Para cada Edge Function:
   - Extrair o código completo
   - Identificar:
     - Lógica de negócio
     - Acesso ao banco
     - Validações
     - Side effects
```

## PARTE 4 — Reimplementação como API local

```txt
Implemente uma API HTTP local que:

- Use o Postgres local como backend
- Exponha EXATAMENTE as mesmas rotas das Edge Functions
- Preserve:
  - Path
  - Query params
  - Body
  - Headers
  - Status codes
  - Payloads de resposta

Tecnologias permitidas (escolha UMA e justifique):
- Fastify (Node)
- Express
- NestJS
- PostgREST
- Ou API HTTP escrita diretamente em PL/pgSQL + pg_http

Para cada rota:
- Gere o código completo do handler
- Mostre como ele se conecta ao Postgres
- Replique a lógica da Edge Function original
```

## PARTE 5 — Autenticação e RLS

```txt
1. Reimplemente:
   - Validação de JWT
   - Claims usados pelo Supabase
   - Contexto de usuário

2. Garanta que:
   - As mesmas RLS Policies funcionem
   - O comportamento de acesso seja idêntico

```

## PARTE 6 — Testes de equivalência

```txt
Gere automaticamente:
- Testes de contrato (request → response)
- Testes comparando:
  - Supabase Edge Function
  - API local

O objetivo é provar equivalência funcional.

```

## SAÍDA FINAL ESPERADA

```txt
Você deve entregar:

1. Scripts SQL completos
2. Código da API local
3. Mapa Edge Function → Endpoint local
4. Checklist de validação
5. Lista explícita de riscos ou diferenças inevitáveis

Formato da resposta:
- Estruturado
- Código real
- Nenhum placeholder
- Nenhuma explicação genérica

Se algo não puder ser feito automaticamente, explique exatamente por quê.

```

# Siga para a prova real em [Starting](starting.md)

<div align="center">
<img src="exitpng" style="300px" alt="o futuro é agêntico" />
</div>
