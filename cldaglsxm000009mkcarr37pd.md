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

`package.json` :

```json
{
  "scripts": {
    "lint:ts:fix": "eslint . --fix --ext .js,.ts,.tsx"
  }
}
```

### `✨` Add prettier

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

## 🍇 Add SASS

```bash
pnpm add -D sass
```

## 🌻 Add `stylelint`

```bash
pnpm add -D stylelint stylelint-checkstyle-formatter stylelint-config-recommended-scss stylelint-config-standard stylelint-scss
```

`package.json`:

```json
{
  "scripts": {
    "lint:css": "stylelint --cache **/*.{scss,css}",
    "lint:css:fix": "stylelint --cache --fix **/*.{scss,css}"
  }
}
```

`.stylelintignore` :

```yaml
# testing
/coverage

# next.js
/.next/
/out/

# production
/build
```

`.stylelintrc` :

```json
{
  "extends": "stylelint-config-recommended-scss",
  "formatter": "stylelint-checkstyle-formatter",
  "plugins": ["stylelint-scss"],
  "rules": {
    "string-quotes": "single",
    "color-hex-length": "long",
    "color-function-notation": "modern",
    "import-notation": "string"
  }
}
```

To verify the configuration above, run:

```bash
pnpm lint:css
pnpm lint:css:fix
```

## ☕ Config the NodeJS version to develop

Add `.nvmrc` file with the content below or your own configuration:

```yaml
v16.18.1
```

For example, use that configuration by using `fnm`:

```bash
fnm use
```

We can also use the `package.json` to verify the configuration above.

```json
{
  "engines": {
    "node": ">=16",
    "pnpm": ">=7.26.0"
  }
}
```

## 🌒 Add environment variable for development and production

`.env.development` file's content:

```yaml
# dev | test | prod
ENV=dev
```

Setup the runtime environment variables:

```bash
cp .env.development .env.local
```

## ☄️ Add the hook when committing the code

```bash
pnpm add -D husky lint-staged
pnpm husky install
touch .husky/pre-commit
chmod +x .husky/pre-commit

# lint the commit message
pnpm add -D @commitlint/cli @commitlint/config-conventional
pnpm husky add .husky/commit-msg  'pnpm --no -- commitlint --edit ${1}'
```

`pre-commit` :

```bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

pnpm lint-staged
```

`commit-msg` :

```bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

pnpm commitlint --edit ${1}
```

`.lintstagedrc.js` :

```javascript
const path = require('path');

const buildEslintCommand = (filenames) =>
  `next lint --fix --file ${filenames
    .map((f) => path.relative(process.cwd(), f))
    .join(' --file ')}`;

const buildStyleLintCommand = (filenames) =>
  `stylelint --cache ${filenames
    .map((f) => path.relative(process.cwd(), f))
    .join(' ')}`;

module.exports = {
  '*.{js,ts,tsx}': [buildEslintCommand],
  '*.{css,scss}': [buildStyleLintCommand],
};
```

`commitlint.config.js` :

```javascript
module.exports = {
  extends: ['@commitlint/config-conventional'],
};
```

To verify the code above:

```bash
git commit -m "refactor: add pre-commit hook"
```

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

## 🍂 Remove unused things

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

### 🌾 Reference

* [https://paulintrognon.fr/blog/typescript-prettier-eslint-next-js](https://paulintrognon.fr/blog/typescript-prettier-eslint-next-js)
    
* [https://blog.logrocket.com/troubleshooting-next-js-app-eslint/](https://blog.logrocket.com/troubleshooting-next-js-app-eslint/)
    
* [https://amanhimself.dev/blog/setup-nextjs-project-with-eslint-prettier-husky-lint-staged/](https://amanhimself.dev/blog/setup-nextjs-project-with-eslint-prettier-husky-lint-staged/)