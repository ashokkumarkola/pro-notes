# Workspace Settings

## 1️⃣ Create a folder:

```bash
mkdir .vscode
```

## 2️⃣ Create the file:

```bash
touch .vscode/settings.json
```

## 3️⃣ Paste it:

```json
{
  "editor.rulers": [80],
  "files.exclude": {
    "**/.git": true,
    "**/node_modules": true,
    "**/build": true
  },
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "flow.useNPMPackagedFlow": true,
  "javascript.validate.enable": false,
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ],
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

## 4️⃣ Make sure you have ESLint configured

```bash
npm install --save-dev eslint typescript
```

## 5️⃣ Restart VS Code

— your settings apply immediately.
