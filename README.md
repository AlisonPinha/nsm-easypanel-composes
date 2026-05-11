# nsm-easypanel-composes

Composes do easypanel da NSM para serviços standalone que precisam compartilhar networks com outros composes (ex.: Supabase self-hosted).

## metabase/

Metabase BI em frente ao Postgres do compose Supabase. Conecta-se via network externa `n8n_supabase_default` para alcançar o service `db` do compose Supabase.

### Como deployar no easypanel

1. No project `n8n`, criar service do tipo **compose**.
2. Source: git, repo `https://github.com/AlisonPinha/nsm-easypanel-composes.git`, branch `main`, root path `/metabase`, compose file `docker-compose.yml`.
3. Adicionar domain apontando para `metabase:3000`.
4. Deploy.

### Como apontar o Metabase para o Postgres do Supabase

Após o setup wizard inicial, adicionar Data Source PostgreSQL com:

- Host: `db`
- Port: `5432`
- Database: `postgres`
- Username: `postgres`
- Password: `<POSTGRES_PASSWORD do compose Supabase>`

A senha está no env do compose Supabase no easypanel (não comitar aqui).

### Metadata storage

O Metabase usa H2 local em `/metabase-data/metabase.db` (volume nomeado `metabase-data`). Suficiente para uso interno NSM; não recomendado para produção crítica.
