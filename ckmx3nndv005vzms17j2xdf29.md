## Converts flat list to tree 🌲 with Typescript and no any type


Flat list is an array of items that has no children with ids and parent ids.

## Purpose

- Converts flat list to tree with Typescript in strict-mode (no `any` type).
- Focus in type checking.
- Runs in browsers and Node.js.
- Choose best algorithm from [stackoverflow's answer for build-tree-array-from-flat-array-in-javascript](https://stackoverflow.com/questions/18017869/build-tree-array-from-flat-array-in-javascript).
- You can use open-source library like [performant-array-to-tree](https://github.com/philipstanislaus/performant-array-to-tree) but if you want to reduce web bundle size and a customable function.

## Example

### Input

```typescript
export interface IFolder {
  folderId: number;
  folderParentId: number;
  name: string;
}

const folderArr = [
  { folderId: 1, folderParentId: 0, name: 'root' },
  { folderId: 2, folderParentId: 1, name: 'A' },
  { folderId: 3, folderParentId: 1, name: 'B' },
  { folderId: 4, folderParentId: 3, name: 'C' },
];
```

### Output

```typescript
const folderTree = [
  {
    folderId: 1,
    folderParentId: 0,
    name: 'root',

    children: [
      {
        folderId: 2,
        folderParentId: 1,
        name: 'A',

        children: [],
      },
      {
        folderId: 3,
        folderParentId: 1,
        name: 'B',

        children: [
          {
            folderId: 4,
            folderParentId: 3,
            name: 'C',
            children: [],
          },
        ],
      },
    ],
  },
];

```

## Tree model for type checking

```typescript
/**
 * like `interface` prefix, `type` prefix is `T`
 */
export type TTree<T> = {
  children?: TTree<T>[];
} & T;
```

## Converts

```typescript
import { TTree } from '@model';

/**
 * flat list to tree
 *
 * @param list - a flat list
 * @param params - `{ id, parentId }`: id name and parentId name
 *
 * @example `arrayToTree<IFolder>(
 *   folderArr, { id: 'folderId', parentId: 'folderParentId' });`
 *
 * @returns `TTree`
 */
export const arrayToTree = <T>(
  list: T[],
  { id, parentId }: { id: string; parentId: string }
): TTree<T>[] | [] => {
  /** map between id and array position */
  const map: number[] = [];
  const treeList: TTree<T>[] = list as TTree<T>[];

  for (let i = 0; i < treeList.length; i += 1) {
    /** initialize the map */
    map[(treeList[i] as TTree<T> & { [id: string]: number })[id]] = i;
    /** initialize the children */
    treeList[i].children = [];
  }

  let node: TTree<T> & { [parentId: string]: number };
  /** return value */
  const roots: TTree<T>[] = [];

  for (const item of treeList) {
    node = item as TTree<T> & { [parentId: string]: number };
    if (node[parentId] !== 0) {
      if (treeList[map[node[parentId]]] !== undefined) {
        treeList[map[node[parentId]]].children?.push(node);
      }
    } else {
      roots.push(node);
    }
  }
  return roots;
};
```

## Demo

You can use [my demo in stackblitz](https://stackblitz.com/edit/typescript-flat-list-to-tree-demo?file=index.ts).

---

Photo by <a href="https://unsplash.com/@fabulu75?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Fabrice Villard</a> on <a href="https://unsplash.com/s/photos/tree?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
