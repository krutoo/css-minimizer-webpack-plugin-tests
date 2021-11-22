# Example of unexpected `css-minimizer-webpack-plugin` behavior

For reproduce problem with webpack plugin run `npm run test:plugin` and check dist folder

For reproduce problem with postcss+cssnano run `npm run test:cssnano` and check dist folder

## Details

After run cssnano, calculations lose the required parentheses in calc:

Before:

```css
html {
  --dot-size: 6;
}
body {
  transform: scale(calc(1 / (10 / var(--dot-size))));
}
```

After:

```css
/* ... */
body{transform: scale(calc(1/10/var(--dot-size)))}
```

Here the `calc` function has lost the necessary parentheses around the second division:

```
1 / (10 / 6) >>> 1 / 10 / 6
```
