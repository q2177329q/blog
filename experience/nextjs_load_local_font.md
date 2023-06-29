# Next.js 引入 TTF 字体文件方法

在 Next.js 中，为了保证页面渲染前加载完成字体文件，我们需要使用 `next/font/local` 加载本地字体文件。否则，可能会导致页面重绘闪烁。

以下是示例代码：

## font.ts

```typescript
import localFont from "next/font/local";

export const harmonyOS = localFont({
  src: [
    {
      path: '../../public/static/fonts/HarmonyOS_Sans/HarmonyOS_Sans_Regular.ttf',
      weight: '400',
      style: 'normal',
    },
  ],
  variable: "--font-harmony-os",
})

export const harmonyOSBold = localFont({
  src: [
    {
      path: '../../public/static/fonts/HarmonyOS_Sans/HarmonyOS_Sans_Bold.ttf',
      weight: '700',
      style: 'normal',
    },
  ],
});
```

## styles/global.ts

```typescript
import { harmonyOS, harmonyOSBold } from "../font"

export const defaultFontFamily = {
  fontFamilyNormal: harmonyOS?.style?.fontFamily,
  fontFamilyBold: harmonyOSBold?.style?.fontFamily,
}
```

## styles/theme.tsx

```typescript
import { ReactNode } from 'react'
import { ThemeProvider } from 'styled-components'
import { defaultTheme } from './globals'

export const Theme = (props: { children: ReactNode }) => {
  return (
    <ThemeProvider theme={defaultTheme}>
      {props.children}
    </ThemeProvider>
  )
}
```

## _app.tsx

```typescript
import { Theme } from '../styles/theme'

function MyApp({ Component, pageProps }: AppProps) {
  return (
    <Theme>
      <Component {...pageProps} />
    </Theme>
  )
}
```