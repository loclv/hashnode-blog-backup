---
title: "Creating a simple functional logger in Node.js from scratch can write log file in localhost 🦮"
seoTitle: "Creating a simple functional logger in Node.js from scratch"
seoDescription: "Creating a simple functional logger in Node.js from scratch can write log file in localhost"
datePublished: Sat Feb 03 2024 16:23:36 GMT+0000 (Coordinated Universal Time)
cuid: cls6aa3s600040ajmd96k3cny
slug: creating-a-simple-functional-logger-in-nodejs-from-scratch-can-write-log-file-in-localhost
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/73pyV0JJOmE/upload/881dcd9bd735d747ba81a47577eab2e1.jpeg
tags: nodejs, logging, scratch, logger, nodejs-logger

---

## Ask ChatGPT first

Question:

>create a simple functional logger in Node.js from scratch can write log file in localhost

The answer is described a `class Logger` to do what we expected.

But what I want to create is `functional` logger, not `class` logger.

Let's create a simple functional logger from scratch.

## Create a log file to store the log on localhost

```ts
import fs from 'fs'
import { createReadableTime, startTime } from './time'

const startTimeStr = createReadableTime(startTime)

/**
 * From first parameter of Node.js CLI command line.
 */
const fileName = process.argv[2] ?? 'log'
/**
 * Do not replace the old log file, so we create a new one with
 * different file name by timestamp.
 */
const fullFileName = `${fileName}-${startTimeStr}.log`

const logStream = fs.createWriteStream(fullFileName, { flags: 'a' })

const logToFile = (message: string) => {
  logStream.write(`${message}\n`)
}

process.on('exit', () => {
  logStream.end()
})

```

And this is `./time` utility functions:

```ts
export const startTime = new Date()

export const createReadableTime = (date: Date): string => {
  let month: number | string = date.getMonth() + 1
  let day: number | string = date.getDate()
  let hour: number | string = date.getHours()
  let min: number | string = date.getMinutes()
  let sec: number | string = date.getSeconds()

  month = `${month < 10 ? '0' : ''}${month}`
  day = `${day < 10 ? '0' : ''}${day}`
  hour = `${hour < 10 ? '0' : ''}${hour}`
  min = `${min < 10 ? '0' : ''}${min}`
  sec = `${sec < 10 ? '0' : ''}${sec}`

  const str = `${date.getFullYear()}-${month}-${day}-${hour}-${min}-${sec}`

  return str
}

```

Now, create a object called `logger`:

```ts
/**
 * Describes the log levels.
 */
const levelObj = {
  INFO: 'INFO',
  WARN: 'WARN',
  ERROR: 'ERROR',
} as const

/**
 * Whatever you want to log.
 */
type OtherInfoNotString = object | number | boolean | string

/**
 * Same as `console.log(message: string, param2)`.
 */
const addOtherInfoToLog = (
  level: keyof typeof levelObj,
  message: string,
  otherInfo?: OtherInfoNotString,
) => {
  let logMess = `[${level}] ${message}`

  if (typeof otherInfo === 'string') {
    logMess += ` ${otherInfo}`
  } else if (otherInfo !== undefined) {
    logMess += ` ${JSON.stringify(otherInfo)}`
  }
  return logToFile(logMess)
}

/**
 * Do the same thing with `console.log`, so we can
 * replace `console.log` with `logger.info`.
 *
 * @example
 * logger.info('Application started')
 * logger.warn('This could be risky')
 * logger.error('Something went wrong')
 *
 */
export const logger = {
  info: (message: string, otherInfo?: OtherInfoNotString) =>
    addOtherInfoToLog(levelObj.INFO, message, otherInfo),

  warn: (message: string, otherInfo?: OtherInfoNotString) =>
    addOtherInfoToLog(levelObj.WARN, message, otherInfo),

  error: (message: string, otherInfo?: OtherInfoNotString) =>
    addOtherInfoToLog(levelObj.ERROR, message, otherInfo),
}
```

Last, use `logger` in `main` function:

```ts
import { logger } from './utils/logger'

/**
 * Command:
 * pnpm do-something
 *
 */
const main = async () => {
  logger.info('🌱 Start script!', new Date().toISOString())

  try {
    const res = await doSomething()
    if (res !== null) {
      logger.info('Result:', res)
    } else {
      logger.warn('Result is null!')
    }
  } finally () {
    // do something
  }

  logger.info('🌳 End script!', new Date().toISOString())

main().catch((err) => {
  logger.error('error:', err)
  process.exit(1)
})
```

## Running the script

To test our logger, we need to run the script with the following `package.json` and `tsconfig.json`:

`package.json`:

```json
{
  "name": "sample-scripts",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "do-something": "tsx src/do-something.ts filename",
    "lint": "eslint --cache ./src/ --ext .ts",
    "lint:fix": "eslint --cache ./src/ --ext .ts --fix",
    "format": "prettier --write --cache src"
  },
  "private": true,
  "dependencies": {},
  "devDependencies": {
    "@types/node": "^20.11.6",
    "@typescript-eslint/eslint-plugin": "^6.19.1",
    "@typescript-eslint/parser": "^6.19.1",
    "eslint": "^8.56.0",
    "prettier": "^3.2.4",
    "tsx": "^4.7.0",
    "typescript": "^5.3.3"
  },
  "engines": {
    "node": ">=20.11",
    "npm": "Please use pnpm",
    "yarn": "Please use pnpm",
    "pnpm": ">=8.15.0",
    "bun": "Please use pnpm"
  }
}

```

- `src/do-something.ts` is TypeScript file contains the `main` function.

- `filename` in `tsx src/do-something.ts filename` is the name of the log file.

`tsconfig.json` (generated by <https://bun.sh/> CLI):

```json
{
  "compilerOptions": {
    "lib": ["ESNext"],
    "target": "ESNext",
    "module": "ESNext",
    "moduleDetection": "force",
    "esModuleInterop": true,
    "jsx": "react-jsx",
    "allowJs": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "verbatimModuleSyntax": true,
    "noEmit": true,

    /* Linting */
    "skipLibCheck": true,
    "strict": true,
    "noFallthroughCasesInSwitch": true,
    "forceConsistentCasingInFileNames": true
  }
}

```

Run the script from the command line:

```bash
pnpm do-something
```

After the script has been run, you can see the output of the script is `filename-2024-02-03-19-17-30.log`
on localhost, project root folder.

## References

- <https://www.digitalocean.com/community/tutorials/nodejs-command-line-arguments-node-scripts>
- <https://stackoverflow.com/questions/5416920/timestamp-to-human-readable-format>
- <https://www.frontendmag.com/tutorials/nodejs-logging-to-file/>
