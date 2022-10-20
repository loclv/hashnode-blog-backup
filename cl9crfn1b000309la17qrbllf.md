# Convert between SQL file and DBML formats file

## Introduce

[dbdiagram.io](https://dbdiagram.io/home) is a free, simple tool to draw ER diagrams by just writing code in a file.

And `.dbml` is the format of that file.

## Prepare

```bash
npm install -g @dbml/cli
# or
pnpm install -g @dbml/cli
```

## Convert a DBML file to SQL

Using `dbml2sql` command:

```bash
dbml2sql schema.dbml -o schema.sql
cat schema.sql
# output is not contain error
```

## Convert a SQL file to DBML

Using `sql2dbml` command:

```bash
sql2dbml schema.sql --mysql -o schema.dbml
# or
sql2dbml schema.sql --postgres -o schema.dbml

cat schema.dbml
# output is not contain error
```

## View the result

Use [dbdiagram.io](https://dbdiagram.io/) or [vscode - extention - dbml](https://marketplace.visualstudio.com/items?itemName=matt-meyers.vscode-dbml).

## Reference

- [DBML - CLI - documents](https://www.dbml.org/cli/#convert-a-dbml-file-to-sql)


