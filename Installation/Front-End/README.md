# Welcome in the NEW CHAPTER Front-End Installation !

## Links

- [Full-Stack](./../Full-Stack/)
- [Front-End](./../Front-End/)
- [Root](https://github.com/LunashaGit/Javascript-TO-Typescript-skills-Power-Rangers-Group/)

### Websites

#### Librairies & Framework Installations in TypeScript (Front-End)

- [NEXTJS Full Stack Framework](#NEXT)
- [REACT Front-End Library](#REACT)
- [REACT-VITE Front-End Library](#REACT-VITE)
- [VUE Front-End Framework](#VUE)
- [Angular Front-End Framework](#ANGULAR)

- [EVERY NPM PACKAGE](#EVERY-NPM-PACKAGE)

#### Visual Studio Code Extensions

- [TypeScript Importer](https://marketplace.visualstudio.com/items?itemName=pmneo.tsimporter)
- [TypeScript Hero](https://marketplace.visualstudio.com/items?itemName=rbbit.typescript-hero)
- [TypeScript Explorer](https://marketplace.visualstudio.com/items?itemName=mxsdev.typescript-explorer)

## Disclaimer

You're not obliged to use VSCode & the extensions! For example, me i don't use some extensions, but i use VSCode!

## NEXT

![NEXTJS](./Images-FRONT-END/nextjs.jpeg)

### Installation FROM ZERO

```bash
npx create-next-app@latest --ts
# or
yarn create next-app --typescript
# or
pnpm create next-app --ts
```

### Existing Project

```bash
npm install --save-dev typescript @types/node
# &&
touch tsconfig.json
```

### Configuration

```js
// @ts-check

/**
 * @type {import('next').NextConfig}
 **/
const nextConfig = {
  /* config options here */
};

module.exports = nextConfig;
```

### LAUNCH THE SERVER

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

## REACT

![REACT](./Images-FRONT-END/react.png)

### Installation FROM ZERO

```bash
npx create-react-app my-app --template typescript
# or
yarn create react-app my-app --template typescript
```

### Existing Project

```bash
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
# &&
yarn add typescript @types/node @types/react @types/react-dom @types/jest
```

### Configuration

Rename JS, JSX files to TS, TSX

### LAUNCH THE SERVER

```bash
npm start
# or
yarn start
```

## REACT-VITE

### Installation FROM ZERO

![REACT-VITE](./Images-FRONT-END/react-vite.webp)

```bash
npm init vite@latest NAME -- --template react-ts
# or
yarn create vite NAME --template react-ts
```

### Existing Project

```bash
npm install --save-dev typescript @types/node
# &&
touch tsconfig.json
```

### LAUNCH THE SERVER

```bash
npm run dev
# or
yarn dev
```

## VUE

![VUE](./Images-FRONT-END/vue.jpeg)

### Installation

```bash
npx @vue/cli create typescript-app
```

### Configuration Installation

![Manual Configuration](./Images-FRONT-END/manual-configuration-typescript-vue.png)

### LAUNCH THE SERVER

```bash
npm run serve
# or
yarn serve
```

## ANGULAR

![VUE](./Images-FRONT-END/angular.png)

### Installation

```bash
npm install -g @angular/cli
# &&
ng new NAME
```

### LAUNCH THE SERVER

```bash
ng serve
```

## EVERY NPM PACKAGE

![EVERY NPM PACKAGE](./Images-FRONT-END/npm.png)

### Installation

```bash
# @types/NAME is the TypeScript definition file for the package NAME
npm install --save-dev typescript @types/node
```
