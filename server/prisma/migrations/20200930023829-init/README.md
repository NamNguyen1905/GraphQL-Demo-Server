# Migration `20200930023829-init`

This migration has been generated by Ben at 9/30/2020, 9:38:29 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE "public"."Author" (
"id" text   NOT NULL ,
"name" text   ,
"age" integer   NOT NULL ,
PRIMARY KEY ("id")
)

CREATE TABLE "public"."Book" (
"id" text   NOT NULL ,
"name" text   ,
"genre" text   ,
"authorId" text   NOT NULL ,
PRIMARY KEY ("id")
)

CREATE UNIQUE INDEX "Author.id_unique" ON "public"."Author"("id")

CREATE UNIQUE INDEX "Book.id_unique" ON "public"."Book"("id")

ALTER TABLE "public"."Book" ADD FOREIGN KEY ("authorId")REFERENCES "public"."Author"("id") ON DELETE CASCADE ON UPDATE CASCADE
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration ..20200930023829-init
--- datamodel.dml
+++ datamodel.dml
@@ -1,0 +1,26 @@
+// This is your Prisma schema file,
+// learn more about it in the docs: https://pris.ly/d/prisma-schema
+
+datasource db {
+    provider = "postgresql"
+    url = "***"
+}
+
+generator client {
+    provider = "prisma-client-js"
+}
+
+model Author {
+    id   String  @unique @id
+    name String?
+    age  Int
+	book Book[]
+}
+
+model Book {
+    id       String  @unique @id
+    name     String?
+    genre    String?
+    authorId String
+	author Author @relation(fields: [authorId], references:[id])
+}
```

