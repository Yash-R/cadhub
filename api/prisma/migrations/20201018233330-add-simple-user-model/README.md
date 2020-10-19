# Migration `20201018233330-add-simple-user-model`

This migration has been generated by Kurt Hutten at 10/19/2020, 10:33:30 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE "User" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "userName" TEXT NOT NULL,
    "email" TEXT NOT NULL,
    "issuer" TEXT NOT NULL,
    "createdAt" DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    "updatedAt" DATETIME NOT NULL,
    "image" TEXT,
    "bio" TEXT
)

CREATE UNIQUE INDEX "User.userName_unique" ON "User"("userName")

CREATE UNIQUE INDEX "User.email_unique" ON "User"("email")

CREATE UNIQUE INDEX "User.issuer_unique" ON "User"("issuer")
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201011095227-create-contact..20201018233330-add-simple-user-model
--- datamodel.dml
+++ datamodel.dml
@@ -1,9 +1,7 @@
 datasource DS {
-  // optionally set multiple providers
-  // example: provider = ["sqlite", "postgresql"]
-  provider = "sqlite"
-  url = "***"
+  provider = ["sqlite", "postgresql"]
+  url = "***"
 }
 generator client {
   provider      = "prisma-client-js"
@@ -34,4 +32,17 @@
   email     String
   message   String
   createdAt DateTime @default(now())
 }
+
+model User {
+  id       Int    @id @default(autoincrement())
+  userName String @unique
+  email    String @unique
+  issuer   String @unique
+
+  createdAt DateTime @default(now())
+  updatedAt DateTime @updatedAt
+
+  image String? // url maybe id or file storage service? cloudinary?
+  bio   String? //mark down
+}
```

