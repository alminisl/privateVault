I have created a nextAuth.ts file. This file contains a basic "config" for the oAuth provider. 

currently looks like this: 

```ts
import NextAuth, { type NextAuthOptions } from "next-auth";  
import GoogleProvider from "next-auth/providers/google";  
  
// Prisma adapter for NextAuth, optional and can be removed  
import { PrismaAdapter } from "@next-auth/prisma-adapter";  
import { prisma } from "../../../server/db/client";  
import { env } from "../../../env/server.mjs";  
  
export const authOptions: NextAuthOptions = {  
  // Include user.id on session  
  callbacks: {  
    session({ session, user }) {  
      if (session.user) {  
        session.user.id = user.id;  
      }  
      return session;  
    },  
  },  
  // Configure one or more authentication providers  
  adapter: PrismaAdapter(prisma),  
  providers: [  
    GoogleProvider({  
      clientId: "909061897263-0onph1qdjnmnfua4hfb5kh7v29et5bik.apps.googleusercontent.com",  
      clientSecret: "tkq23g-bUiuo6phyQLz3-neh",  
    }),  
    // ...add more providers here  
  ],  
};  
  
export default NextAuth(authOptions);
```


- I've installed a google Auth provider
- I've added my google account `clientID` and `clientSecret` 
- session provider
```tsx
<SessionProvider session={session}>  
  <Component {...pageProps} />  
</SessionProvider>
```
