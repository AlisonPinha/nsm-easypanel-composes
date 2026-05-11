# nsm-easypanel-composes

Forks de composes do easypanel.io para a NSM, com customizações específicas.

## supabase/

Fork de `easypanel-io/compose@19-01-2026/supabase`. Mudança: adicionado service `metabase` (Metabase v0.58.7) ao docker-compose.yml para que ele compartilhe a network do compose Supabase e consiga conectar diretamente ao Postgres `db` interno.

### Customizações vs. upstream

- `code/docker-compose.yml` — adicionado service `metabase` no final + volume nomeado `metabase-data`.

### Como apontar o easypanel

Trocar source git do service `supabase` do project `n8n` para:

- repo: `https://github.com/AlisonPinha/nsm-easypanel-composes.git`
- ref: `main`
- rootPath: `/supabase/code`
- composeFile: `docker-compose.yml`

### Como apontar Metabase para o Postgres do Supabase

Após o setup wizard inicial, adicionar Data Source PostgreSQL com:

- Host: `db`
- Port: `5432`
- Database: `postgres`
- Username: `postgres`
- Password: `<POSTGRES_PASSWORD do env do compose Supabase>`

### Rollback

Para reverter, apontar o source git do service `supabase` de volta para:

- repo: `https://github.com/easypanel-io/compose.git`
- ref: `19-01-2026`
- rootPath: `/supabase/code`
- composeFile: `docker-compose.yml`

Volumes nomeados (incluindo `db-config` do Postgres) persistem em ambas as direções.
