# Prepare a new NextJS project 🍵

### 🚀 Create a project with CLI

```bash
pnpm create next-app --use-pnpm --ts --eslint --src-dir --experimental-app
# or
npm create next-app --ts --eslint --src-dir --experimental-app
```

* Choose TypeScript and ESLint tools.
    
* If you set `--experimental-app` flag, you can meet the warning message below:
    

```plaintext
warn  - You have enabled experimental feature (appDir) in next.config.js.
warn  - Experimental features are not covered by semver, and may cause unexpected or broken application behavior. Use at your own risk.
```

### 🗻 Custom ESLint

This is the first look of default `.eslintrc.json`:

```json
{
  "extends": "next/core-web-vitals"
}
```

For React:

```bash
pnpm add -D eslint-plugin-react eslint-plugin-react-hooks
```

Add `@typescript-eslint/eslint-plugin` for TypeScript:

```bash
pnpm add -D @typescript-eslint/eslint-plugin
```

For prettier:

```bash
pnpm add -D eslint-plugin-prettier
```

For NextJS:

```bash
pnpm add -D eslint-plugin-next
```

`.eslintrc.json`:

```json
{
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "project": ["tsconfig.json"],
    "createDefaultProgram": true
  },
  "plugins": [
    "@typescript-eslint",
    "prettier"
  ],
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@next/next/recommended",
    "next/core-web-vitals",
    "prettier"
  ],
  "rules": {
    "@typescript-eslint/no-unused-vars": 2,
    "@typescript-eslint/no-explicit-any": 2,
    "id-length": [2, { "exceptions": ["i"] }],
    "@typescript-eslint/naming-convention": [
      2,
      {
        "selector": "interface",
        "format": ["PascalCase"],
        "custom": {
          "regex": "^I[A-Z]",
          "match": true
        }
      },
      {
        "selector": "variable",
        "format": ["camelCase", "UPPER_CASE"]
      },
      {
        "selector": "typeParameter",
        "format": ["PascalCase"],
        "prefix": ["T"]
      },
      {
        "selector": "variable",
        "format": ["PascalCase"],
        "types": ["boolean"],
        "prefix": ["is", "should", "has", "can", "did", "will", "was"]
      },
      {
        "selector": "enum",
        "format": ["PascalCase"]
      },
      {
        "selector": "enumMember",
        "format": ["PascalCase", "camelCase"]
      }
    ]
  }
}
```

### ✨ Add prettier

```bash
pnpm add -D prettier eslint-config-prettier
```

`.prettierrc.yaml`:

```yaml
singleQuote: true
printWidth: 80
```

Verify all settings above:

```bash
pnpm lint
```

Add formatting script in `package.json`:

```diff
--- a/package.json
+++ b/package.json
@@ -6,7 +6,8 @@
     "dev": "next dev",
     "build": "next build",
     "start": "next start",
-    "lint": "next lint"
+    "lint": "next lint",
+    "format": "prettier --write --cache src"
   },
```

```bash
pnpm format
```

### 🌸 Add spell-checking

Install `Code Spell Checker` extension for VS Code and create `cspell.json` file with blank content.

### 🍵 Create VS Code setting

Create recommendations VS Code extension:

1. `Ctrl` + `Shift` + `P`
    
2. Type "recom..." and `enter`
    

This will create a `.vscode/extensions.json` file.

`extensions.json`:

```json
{
	"recommendations": [
		"esbenp.prettier-vscode",
		"dbaeumer.vscode-eslint",
		"stylelint.vscode-stylelint",
		"mintlify.document",
		"streetsidesoftware.code-spell-checker",
		"DavidAnson.vscode-markdownlint",
		"Gruntfuggly.todo-tree",
		"mikestead.dotenv",
		"foxundermoon.next-js",
		"planbcoding.vscode-react-refactor"
	]
}
```

### Remove unused things

* Remove unused CSS in the `styles` folder
    
* Remove unused code in the `pages/index.tsx` folder
    

### 🍃 Other optional

`.markdownlint.yaml` for the Markdown file if needed:

```yaml
# Default state for all rules
default: true

line-length: false

# MD033/no-inline-html - Inline HTML
MD033:
  # Allowed elements
  allowed_elements: ["style"]
```

### Reference

* [https://paulintrognon.fr/blog/typescript-prettier-eslint-next-js](https://paulintrognon.fr/blog/typescript-prettier-eslint-next-js)
    
* [https://blog.logrocket.com/troubleshooting-next-js-app-eslint/](https://blog.logrocket.com/troubleshooting-next-js-app-eslint/)