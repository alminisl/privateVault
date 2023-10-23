```
generator client {

provider = "prisma-client-js"

}

  

datasource db {

provider = "postgresql"

url = env("DATABASE_URL")

}

  

model Example {

id String @id @default(cuid())

}

  

model Account {

id String @id @default(cuid())

userId String

type String

provider String

providerAccountId String

refresh_token String?

access_token String?

expires_at Int?

token_type String?

scope String?

id_token String?

session_state String?

user User @relation(fields: [userId], references: [id], onDelete: Cascade)

  

@@unique([provider, providerAccountId])

}

  

model Session {

id String @id @default(cuid())

sessionToken String @unique

userId String

expires DateTime

user User @relation(fields: [userId], references: [id], onDelete: Cascade)

}

  

model User {

id String @id @default(cuid())

name String?

email String?

emailVerified DateTime?

image String?

rating Int @default(800)

accounts Account[]

lostmatches LostMatches[]

sessions Session[]

wongames WonMatches[]

sport Sport[]

Rating Rating[]

}

  

model Rating {

rating Int

user User @relation(fields: [userId], references: [id])

userId String

sport Sport @relation(fields: [sportId], references: [id])

sportId String

  

@@unique([userId, sportId])

}

  

model VerificationToken {

identifier String

token String @unique

expires DateTime

  

@@unique([identifier, token])

}

  

model Sport {

id String @id @default(cuid())

name String

createdAt DateTime @default(now())

updatedAt DateTime @updatedAt

match Match[]

users User[]

Rating Rating[]

}

  

model WonMatches {

matchId String

userId String

playedAt DateTime @default(now())

user User @relation(fields: [userId], references: [id])

match Match @relation(fields: [matchId], references: [id])

  

@@id([matchId, userId])

}

  

model LostMatches {

matchId String

userId String

playedAt DateTime @default(now())

user User @relation(fields: [userId], references: [id])

match Match @relation(fields: [matchId], references: [id])

  

@@id([matchId, userId])

}

  

model Match {

id String @id @default(cuid())

createdAt DateTime @default(now())

updatedAt DateTime @updatedAt

score String

userId String

loserId String

userBId String?

loserBId String?

userName String

loserName String

userBName String?

loserBName String?

sportId String

sport Sport @relation(fields: [sportId], references: [id])

lostMatches LostMatches[]

wonMatches WonMatches[]

}

  

model Pendingmatch {

id String @id @default(cuid())

createdAt DateTime @default(now())

updatedAt DateTime @updatedAt

score String

userId String

loserId String

userBId String?

loserBId String?

userName String

loserName String

userBName String?

loserBName String?

sportId String

confirmed Boolean @default(false)

}

  

model Log {

id String @id @default(cuid())

createdAt DateTime @default(now())

updatedAt DateTime @updatedAt

message String

type String

}
```