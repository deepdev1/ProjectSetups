# Node-Express-Typescript Project Setup

```
- Latest NodeJS LTS version
- New directory without space or special characters
```

1. Initialize the node project `package.json`
   ```bash
   npx init --yes
   ```

2. Install `express` and `dotenv` dependencies
   ```bash
   npm i express dotenv
   ```

3. Install `typescript` and type declarations of respective libraries
   ```bash
   npm i -D typescript @types/express @types/dotenv
   ```

4. Configure typescript compiler
   - Generate `tsconfig.json` file
     ```bash
     npx tsc --init
     ```

   - Add the `outDir` path in `tsconfig.json`:
     ```bash
     {
        "compilerOptions": {
            "outDir": "./dist"

            // rest options remain same
        }
     }
     ```

5. Create `index.ts` with the following content:
   ```typescript
    import express, { Express, Request, Response } from 'express';
    import dotenv from 'dotenv';

    dotenv.config();

    const app: Express = express();
    const port = process.env.PORT;

    app.get('/', (req: Request, res: Response) => {
        res.send('Express + TypeScript Server');
    });

    app.listen(port, () => {
        console.log(`⚡️[server]: Server is running at https://localhost:${port}`);
    });
   ```

   ```bash
   #.env file
   PORT=8000
   ```

6. Watching files and build directory using `concurrently` and `nodemon`
    - Install the dev dependencies
      ```bash
      npm install -D concurrently nodemon
      ```

    - Add the following in the scripts section of `package.json`
      ```json
      {
          "scripts": {
              "build": "npx tsc",
              "start": "node dist/index.js",
              "dev": "concurrently \"npx tsc --watch\" \"nodemon -q dist/index.js\""
          }
      }
      ```

7. Build and start the dev server
   ```bash
   npm run build
   npm run dev
   ```
