# Welcome in the NEW CHAPTER Back-End Installation !

## Links

### Github

- [Full-Stack](./../Full-Stack/)
- [Front-End](./../Front-End/)
- [Root](https://github.com/LunashaGit/Javascript-TO-Typescript-skills-Power-Rangers-Group/)

### Websites

#### Librairies & Framework Installations in TypeScript (Back-End)

- [EXPRESSJS Back-End Framework](#EXPRESS)

- [EVERY NPM PACKAGE](#EVERY-NPM-PACKAGE)

#### Visual Studio Code Extensions

- [TypeScript Importer](https://marketplace.visualstudio.com/items?itemName=pmneo.tsimporter)
- [TypeScript Hero](https://marketplace.visualstudio.com/items?itemName=rbbit.typescript-hero)
- [TypeScript Explorer](https://marketplace.visualstudio.com/items?itemName=mxsdev.typescript-explorer)

## Disclaimer

You're not obliged to use VSCode & the extensions! For example, me i don't use some extensions, but i use VSCode!

## EXPRESS

![EXPRESS](./Images-BACK-END/EXPRESS.png)

### Installation

```bash
npm init -y
# &&
npm install express
# &&
npm install -D typescript @types/node @types/express
# &&
npx tsc --init
# &&
npm i -g tsx
```

### Configuration

```bash
touch tsconfig.json
```

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "ES5",
    "lib": ["dom", "dom.iterable"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noEmit": true,
    "esModuleInterop": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}
```

### LAUNCH THE SERVER

```json
{
  "scripts": {
    "backend": "tsx watch ./index.tsx"
  }
}
```

## EVERY NPM PACKAGE

![EVERY NPM PACKAGE](./Images-BACK-END/npm.png)

### Installation

```bash
# @types/NAME is the TypeScript definition file for the package NAME
npm install --save-dev typescript @types/node
```
