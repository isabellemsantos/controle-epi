generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}

// ---------- Auth (Better Auth) ----------

model User {
  id            String    @id
  name          String
  email         String
  emailVerified Boolean
  image         String?
  role          String    @default("operador") // "admin" | "operador"
  createdAt     DateTime
  updatedAt     DateTime

  sessions      Session[]
  accounts      Account[]
  movimentacoes Movimentacao[]

  @@unique([email])
  @@map("user")
}

model Session {
  id        String   @id
  expiresAt DateTime
  token     String
  createdAt DateTime
  updatedAt DateTime
  ipAddress String?
  userAgent String?
  userId    String
  user      User     @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@unique([token])
  @@map("session")
}

model Account {
  id                    String    @id
  accountId             String
  providerId            String
  userId                String
  user                  User      @relation(fields: [userId], references: [id], onDelete: Cascade)
  accessToken           String?
  refreshToken          String?
  idToken               String?
  accessTokenExpiresAt  DateTime?
  refreshTokenExpiresAt DateTime?
  scope                 String?
  password              String?
  createdAt             DateTime
  updatedAt             DateTime

  @@map("account")
}

model Verification {
  id         String    @id
  identifier String
  value      String
  expiresAt  DateTime
  createdAt  DateTime?
  updatedAt  DateTime?

  @@map("verification")
}

// ---------- Domínio: EPIs ----------

model Epi {
  id            String   @id @default(cuid())
  codigo        String   // código interno do item (ex: 95.9008-55)
  nome          String
  ca            String   // Certificado de Aprovação
  validade      DateTime
  marca         String?
  unidade       String   @default("PC") // ex: PC, PR (par), CX...
  quantidade    Int      @default(0) // saldo atual em estoque
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt

  movimentacoes Movimentacao[]

  @@unique([codigo])
  @@index([ca])
}

model Funcionario {
  id            String   @id @default(cuid())
  nome          String
  setor         String
  matricula     String?
  ativo         Boolean  @default(true)
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt

  movimentacoes Movimentacao[]
}

enum TipoMovimentacao {
  ENTRADA
  SAIDA
}

model Movimentacao {
  id            String           @id @default(cuid())
  tipo          TipoMovimentacao
  quantidade    Int
  data          DateTime         @default(now())
  observacao    String?

  epiId         String
  epi           Epi              @relation(fields: [epiId], references: [id])

  funcionarioId String?          // null quando for ENTRADA
  funcionario   Funcionario?     @relation(fields: [funcionarioId], references: [id])

  registradoPorId String
  registradoPor   User           @relation(fields: [registradoPorId], references: [id])

  @@index([epiId])
  @@index([funcionarioId])
}
