---
title: "Use Drizzle ORM 💦 and PostgresJS 🐘 step by step with Bun"
seoTitle: "Use Drizzle ORM and PostgresJS step by step with Bun"
seoDescription: "Use Drizzle ORM and PostgresJS step by step with Bun"
datePublished: Sun Jan 28 2024 19:25:26 GMT+0000 (Coordinated Universal Time)
cuid: clrxw4u6c000008ji5ngg5ukj
slug: use-drizzle-orm-and-postgresjs-step-by-step-with-bun
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/YN0HJB0qoys/upload/26260d1e0f24130c2fe748f69dd85a89.jpeg
tags: drizzleorm

---

## Installation

```bash
bun add drizzle-orm postgres
bun add -D drizzle-kit
```

## Define the schema

```bash
cd src
mkdir db
cd db
mkdir schema
cd schema
touch products.ts
```

`products.ts`:

```ts
import { pgTable, serial, text, integer } from 'drizzle-orm/pg-core'

export const products = pgTable('products', {
  id: serial('id').primaryKey(),
  name: text('name').notNull(),
  description: text('description'),
  price: integer('price'),
})

```

Back to the project root directory:

```bash
touch drizzle.config.ts
```

`drizzle.config.ts`:

```ts
import type { Config } from 'drizzle-kit'

export default {
  schema: './src/db/schema/products.ts',
  out: './drizzle',
} satisfies Config

```

Add the script to the `package.json`:

```json
{
  "scripts": {
    "gen": "drizzle-kit generate:pg"
  }
}
```

To generate the SQL migration files:

```bash
bun gen
```

Generated command's output is below.

>[✓] Your SQL migration file ➜ drizzle/0000_talented_smasher.sql 🚀

### Troubleshooting when generating the SQL migration

If you have an error when generating the SQL migration:

```text
Error: Cannot find module 'node:process'
Require stack:
- ~/bun-monorepo/node_modules/drizzle-kit/bin.cjs
```

Please use the latest version of the Node.js:

```bash
fnm use 20
```

## Migration

In your project's root directory, create environment variables file:

```bash
cp .env.example .env
```

`.env.example`:

```conf
# DEV | PROD | STG
ENV=
DATABASE_URL=
```

We need to specify the database connection URL for the development.

For example, if you run PostgreSQL server on localhost using the `brew` command:

```bash
brew services start postgresql
# => Successfully started `postgresql@14`
```

PostgreSQL URL's format is:

>postgres://{user}:{password}@{hostname}:{port}/{database-name}

In this case, hostname and port are `localhost:5432`.

```bash
bun run env | grep ENV
bun run env | grep DATABASE
```

In your project's root directory, create a `migrate.ts` file:

```bash
touch migrate.ts
```

```ts
import { migrate } from 'drizzle-orm/postgres-js/migrator'
import postgres from 'postgres'
import { drizzle } from 'drizzle-orm/postgres-js'

console.log('Start migration! 🍀')

if (!process.env.DATABASE_URL) {
  throw new Error('Please specify a DATABASE_URL environment variable! 🚧')
}

const databaseUrl = drizzle(
  postgres(`${process.env.DATABASE_URL}`, {
    ssl: process.env.ENV === 'PROD' || process.env.ENV === 'STG' ? 'require' : false,
    max: 1,
  }),
)

const main = async () => {
  try {
    await migrate(databaseUrl, { migrationsFolder: 'drizzle' })
    console.log('Migration complete! 🌟')
  } catch (error) {
    console.log('🚫 Err: ', error)
  }

  process.exit(0)
}

main()

```

Add migration scripts to your `package.json`:

```json
{
  "scripts": {
    "migrate": "bun run migrate.ts"
  }
}
```

To run migrations:

```bash
bun migrate
```

### Troubleshooting when running migration

If you have an error when running migration:

```text
Start migration! 🍀
🚫 Err:  ECONNREFUSED: Failed to connect
 syscall: "connect"
```

May be you need to start the PostgreSQL server:

```bash
# MacOS:
brew services start postgresql
# ==> Successfully started `postgresql@14` (label: homebrew.mxcl.postgresql@14)
```

## Create a DB instance for query purposes

```bash
cd src/db
touch index.ts
```

`src/db/index.ts`:

```ts
import { drizzle } from 'drizzle-orm/postgres-js'
import postgres from 'postgres'

if (!process.env.DATABASE_URL) {
  throw new Error('Please specify a DATABASE_URL environment variable! 🚧')
}

/**
 * for query purposes
 */
const queryClient = postgres(process.env.DATABASE_URL)
export const db = drizzle(queryClient)

```

## Seed

Now that we have a database, let's add some data to it. Create a `seed.ts` file with the following contents.

```bash
touch seed.ts
```

```ts
import { db } from './src/db'
import { products } from './src/db/schema/products'

await db.insert(products).values([
  {
    id: 1,
    name: 'Product A',
    description: 'A description',
    price: 11,
  },
  {
    id: 2,
    name: 'Product B',
    description: 'B description',
    price: 11,
  },
  {
    id: 3,
    name: 'Product C',
    description: 'C description',
    price: 11,
  },
])

console.log('Seeding complete. 🌟')

// DONE
process.exit(0)

```

To run seeding:

```bash
bun seed
```

## Commands Summary

```bash
bun gen
bun migrate
bun seed
```

### Troubleshooting

When you see an error about `tsconfig.json`, you can use the configuration below:

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "ESNext",
    "lib": ["DOM"],
    "composite": false,
    "declaration": true,
    "declarationMap": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "inlineSources": false,
    "isolatedModules": true,
    "moduleResolution": "node",
    "noUnusedLocals": false,
    "noUnusedParameters": false,
    "preserveWatchOutput": true,
    "skipLibCheck": true,
    "strict": true
  },
  "include": ["."],
  "exclude": ["dist", "build", "node_modules"]
}
```

You also can use the runnable project: <https://github.com/loclv/bun-monorepo>.

## References

- <https://orm.drizzle.team/docs/get-started-postgresql>
- <https://neon.tech/blog/api-cf-drizzle-neon>
- <https://bun.sh/guides/ecosystem/drizzle>
- <https://bun.sh/guides/runtime/set-env>
- <https://stackoverflow.com/questions/3582552/what-is-the-format-for-the-postgresql-connection-string-url>
