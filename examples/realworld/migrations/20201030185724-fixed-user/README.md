# Migration `20201030185724-fixed-user`

This migration has been generated by Martin Sosic at 10/30/2020, 7:57:24 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;
CREATE TABLE "new_User" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "username" TEXT NOT NULL,
    "email" TEXT NOT NULL,
    "password" TEXT NOT NULL
);
INSERT INTO "new_User" ("id") SELECT "id" FROM "User";
DROP TABLE "User";
ALTER TABLE "new_User" RENAME TO "User";
CREATE UNIQUE INDEX "User.username_unique" ON "User"("username");
CREATE UNIQUE INDEX "User.email_unique" ON "User"("email");
PRAGMA foreign_key_check;
PRAGMA foreign_keys=ON
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201030161549-user..20201030185724-fixed-user
--- datamodel.dml
+++ datamodel.dml
@@ -1,8 +1,8 @@
 datasource db {
   provider = "sqlite"
-  url = "***"
+  url = "***"
 }
 generator client {
   provider = "prisma-client-js"
@@ -10,8 +10,9 @@
 }
 model User {
     id          Int     @id @default(autoincrement())
-    description String
-    isDone      Boolean @default(false)
+    username    String  @unique
+    email       String  @unique
+    password    String
 }
```


