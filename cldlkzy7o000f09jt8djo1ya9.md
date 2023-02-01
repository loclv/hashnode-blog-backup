# TypeScript - client side - 📁 check if zip file is encrypted or protected by a password on browser

## 🍇 Problem

I want to check if the zip file is encrypted or protected by a password.

So, when I read that file, the error occurred. The error message should be exported from the library.

## 🦊 Solution

I searched for the solution and found this one: [https://stackoverflow.com/questions/28063494/extract-password-protected-zip-file-using-javascript-client-side](https://stackoverflow.com/questions/28063494/extract-password-protected-zip-file-using-javascript-client-side).

Then I just rewrite the code in TypeScript like this:

```typescript
import {
  ZipReader,
  BlobWriter,
  BlobReader,
  ERR_ENCRYPTED,
  ERR_INVALID_PASSWORD,
  ERR_EOCDR_NOT_FOUND,
} from '@zip.js/zip.js';

/**
 * Verify that using password.
 *
 * @param file - File
 * @param password - optional password
 * @returns true if using password
 */
export const isZipFileUsingPassword = async (
  file: Blob,
  password?: string
): Promise<boolean> => {
  let reader: undefined | ZipReader<Blob>;

  try {
    reader = new ZipReader(new BlobReader(file), { password });
    const entries = await reader.getEntries();

    for (const entry of entries) {
      try {
        await entry.getData(new BlobWriter());
        // eslint-disable-next-line @typescript-eslint/no-explicit-any
      } catch (entryError: any) {
        // importance logger
        console.log('zip - reader entry:', entryError.message);

        if (
          entryError.message === ERR_ENCRYPTED ||
          entryError.message === ERR_INVALID_PASSWORD
        ) {
          return true;
        }

        if (entryError.message === ERR_EOCDR_NOT_FOUND) {
          console.log('zip - reader: this is may not a zip file!');
          return false;
        }

        throw entryError;
      }
    }
    // eslint-disable-next-line @typescript-eslint/no-explicit-any
  } catch (err: any) {
    if (err.message === ERR_EOCDR_NOT_FOUND) {
      console.log('zip - reader: this is may not a zip file!');
      return false;
    }

    console.log('zip - reader:', err.message);
    return false;
  } finally {
    if (reader) await reader.close();
  }

  return false;
};
```

You need to add the `@zip.js/zip.js` module to your project first.

```typescript
pnpm add @zip.js/zip.js
```

Then use it like this in the handler:

```typescript
const handleFileSelected = async (event: {
  target: { files: FileList | null };
}) => {
  const files = event.target.files;
  if (!files) throw new Error('Files are not found!');

  console.log('🚀 ~ files', files);

  const firstFile = files[0];
  if (!firstFile) throw new Error('First file is not found!');

  const isUsingPass = await isZipFileUsingPassword(firstFile);
  console.log('🚀 ~ isUsingPass', isUsingPass);
};
```

Use `input` element to select the files and put them into the handler:

```xml
<input type="file" multiple onChange={handleFileSelected} />
```

Now, `isUsingPass` is true if the input zip file is using a password.