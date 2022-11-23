# next.js - next/image - an example for migration a object-fit and fill Image to version 13

## Documents

Full change-log documents at:

- [messages/next-image-upgrade-to-13](https://nextjs.org/docs/messages/next-image-upgrade-to-13)
- [next/legacy/image](https://nextjs.org/docs/api-reference/next/legacy/image)
- [next/image](https://nextjs.org/docs/api-reference/next/image) - Version History

From type definition (node_modules/.pnpm/next@13.0.4_m5sxuueb27gk6ddc5gums6vtgq/node_modules/next/dist/client/image.d.ts) when you press `ctrl` and click on `Image` element from `'next/image'`:

```ts
export declare type ImageProps = Omit<JSX.IntrinsicElements['img'], 'src' | 'srcSet' | 'ref' | 'alt' | 'width' | 'height' | 'loading'> & {
    // other property
    fill?: boolean;
    loader?: ImageLoader;
    quality?: SafeNumber;
    priority?: boolean;
    loading?: LoadingValue;
    placeholder?: PlaceholderValue;
    blurDataURL?: string;
    unoptimized?: boolean;
    onLoadingComplete?: OnLoadingComplete;
    /**
     * @deprecated Use `fill` prop instead of `layout="fill"` or change import to `next/legacy/image`.
     * @see https://nextjs.org/docs/api-reference/next/legacy/image
     */
    layout?: string;
    /**
     * @deprecated Use `style` prop instead.
     */
    objectFit?: string;
    /**
     * @deprecated Use `style` prop instead.
     */
    objectPosition?: string;
    /**
     * @deprecated This prop does not do anything.
     */
    lazyBoundary?: string;
    /**
     * @deprecated This prop does not do anything.
     */
    lazyRoot?: string;
}
```

## An example for migration a object-fit and fill Image to version 13

From:

```tsx
<Image
  alt='Mountains'
  src="/images/mountains.png"
  priority={true}
  layout="fill"
  objectFit="contain"
/>
```

to:

```tsx
<Image
  alt="Mountains"
  src="/images/mountains.png"
  priority={true}
  fill
  style={{ objectFit: 'cover' }}
/>
```
