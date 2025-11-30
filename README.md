# Project setup command

## Create a Next.js Project (with pnpm)

Use this command to install nextjs application

```pnpm
pnpm create next-app@latest
```

After runnin this command install all node modules. Then setup basic page.tsx and layout.tsx file.

### page.tsx

```tsx
export default function Home() {
  return (
    <div className="flex min-h-screen items-center justify-center">
      Home Page
    </div>
  );
}
```

### layout.tsx

```tsx
import type { Metadata } from "next";
import { Inter } from "next/font/google";
import "./globals.css";

const inter = Inter({
  variable: "--font-geist-sans",
  subsets: ["latin"],
});

export const metadata: Metadata = {
  title: "Finac Shortner",
  description: "Finac Shortner is a tool that allows you to shorten long URLs.",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en" suppressHydrationWarning>
      <body className={`${inter.className} antialiased`}>
        <main className="container mx-auto p-4">{children}</main>
      </body>
    </html>
  );
}
```

Inside global.css file remove tw-animate-css as shown below

![Removed tw-animate-css](./public/screenshot/02-remvoe-tw-file.png)

## Add Shadcn

Install shadcn using below command

```pnpm
pnpm dlx shadcn@latest init
```

To add shadcn component use below command.

```pnpm
pnpm dlx shadcn@latest add button label input card select
```

## Init Github

Initialize git then commit all changes and create new repo. Then add repo and its name then push the changes to github.

## Project Structure

After doing all above changes our project structure will look like this.

![Project Structure](./public/screenshot/01-project-structure.png)

## Setup Prisma with Postgress

This will install prisma and prims client to project.

```pnpm
pnpm add -D prisma
pnpm add @prisma/client
```

### Initialize prisma

This creates:

- prisma/schema.prisma
- .env (update DATABASE_URL here)

```pnpm
pnpm prisma init
```

After running above command we will get below schema.prisma file. Change output to **output = "../lib/generated/prisma"**

```prisma
// This is your Prisma schema file,
// learn more about it in the docs: https://pris.ly/d/prisma-schema

// Looking for ways to speed up your queries, or scale easily with your serverless or edge functions?
// Try Prisma Accelerate: https://pris.ly/cli/accelerate-init

generator client {
  provider = "prisma-client"
  output   = "../lib/generated/prisma"
}

datasource db {
  provider = "postgresql"
}
```

we have to install **dotenv** package to our project.

```pnpm
pnpm add -D prisma dotenv
```

## Create Prisma Schema

Now create basic prisma schema to migrate.

```prisma
model Testing {
  id           String   @id @default(uuid())
  testName     String
  descriptions String

  @@map("testings")
}
```

After adding sample prisma model our schema.prisma file will look like this.

```schema.prisma
// This is your Prisma schema file,
// learn more about it in the docs: https://pris.ly/d/prisma-schema

// Looking for ways to speed up your queries, or scale easily with your serverless or edge functions?
// Try Prisma Accelerate: https://pris.ly/cli/accelerate-init

generator client {
  provider = "prisma-client"
  output   = "../lib/generated/prisma"
}

datasource db {
  provider = "postgresql"
}

// sample schema
model Testing {
  id           String @id @default(uuid())
  testName     String
  descriptions String

  @@map("testings")
}
```
