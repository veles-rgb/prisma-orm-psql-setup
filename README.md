# prisma-orm-psql-setup
Simple guide to setting up Prisma ORM with PSQL in JS instead of TypeScript.

#
[Prisma ORM PSQL Quickstart Guide](https://www.prisma.io/docs/prisma-orm/quickstart/postgresql)

## Instructions

**Step 1**
```
npm install prisma --save-dev
npm install @prisma/client @prisma/adapter-pg pg dotenv
```

**Step 2**
```
npx prisma
```

**Step 3**
```
npx prisma init --datasource-provider postgresql --output ../generated/prisma --generator-provider prisma-client-js
```

**Step 4**
```
rename prisma.config.ts to prisma.config.js```
```

**Step 5**

Update your .env file with your PostgreSQL connection string:

```
DATABASE_URL="postgresql://johndoe:randompassword@localhost:5432/mydb?schema=public"
```

**Step 6**

Create your first migration to set up the database tables:

```
npx prisma migrate dev --name init
```
This command creates the database tables based on your schema.

**Step 7**

Now run the following command to generate the Prisma Client:
```
npx prisma generate
```

**Step 8**

Instead of lib/prisma.ts, create lib/prisma.js. You must also add the .js file extension when importing PrismaClient in that file:
```
import "dotenv/config";
import { PrismaPg } from "@prisma/adapter-pg";
import { PrismaClient } from '../generated/prisma/client.js';  // THIS LINE

const connectionString = `${process.env.DATABASE_URL}`;

const adapter = new PrismaPg({ connectionString });
const prisma = new PrismaClient({ adapter });

export { prisma };
```

**Step 9**

Explore your data with Prisma Studio
```
npx prisma studio --config ./prisma.config.js
```
