---
title: "Bun/NodeJS - Example of using json-2-csv package and emptyFieldValue option"
datePublished: Fri Oct 18 2024 16:15:34 GMT+0000 (Coordinated Universal Time)
cuid: cm2exlkb4000109k1ch3l0z0p
slug: bunnodejs-example-of-using-json-2-csv-package-and-emptyfieldvalue-option
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/6T7kfc3VitU/upload/cb0a2330a3b99434b756242ddedff90d.jpeg
tags: nodejs, bun, json-2-csv

---

## Example

```ts
import fs from 'fs'
import { json2csv } from 'json-2-csv'

/**
 * Example of using 3rd party library json-2-csv.
 * json-2-csv: {@link https://www.npmjs.com/package/json-2-csv}
 */
const rows = [
  {
    name: 'Sato',
    age: 3,
    weight: 14.9,
    note: 'a baby',
    updatedAt: '2024-01-01T00:00:00.000Z',
  },
  {
    name: 'Jack',
    age: 4,
    weight: 15.333333333333334,
    note: '',
  },
  {
    name: 'Minh Tue',
    age: 5,
    weight: '(not set 🍎)',
    value4: 'mobile',
  },
]

const csv = json2csv(rows, {
  /**
   * Value that, if specified, will be substituted in for field values
   * that are undefined, null, or an empty string
   */
  emptyFieldValue: '-',
})

console.log('💚 ~ csv:', csv)

/**
 * bun src/test-json-2-csv.ts
 */
fs.writeFile('name.csv', csv, 'utf8', err => {
  if (err !== null) {
    console.error('🚨 CSV file writing error: ', err)

    return
  }

  console.info("💧 It's saved!")
})
```

## Output

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729268041643/b6b31c0b-95fb-4e6e-b283-eb05c70ff223.png align="center")