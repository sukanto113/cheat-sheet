### Push schema to db without a migration

```
$ npx prisma db push
```

### Generate prisma client from schema

```
$ npx prisma generate
```

# Prisma cheat sheet

### Create a migration

```
$ npx prisma migrate dev --name init
```

### Deploy to server

```
$ npx prisma migrate deploy
```

### Reset database

```
$ npx prisma migrate reset
```
