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

### Mark failed migration as rolled back and re-deploy
```
$ npx prisma migrate resolve --rolled-back "20201127134938_added_bio_index"
$ npx prisma migrate deploy
```

### Deploy to server

```
$ npx prisma migrate deploy
```

### Reset database

```
$ npx prisma migrate reset
```
