---
title: 'React×TypeScriptでfower使うとき'
emoji: '🗂'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['react', 'typescript', 'fower']
published: true
---

## fower とは

Tailwind に対応した Next.js 作ってる Vercel が出したやつ

https://fower.vercel.app/

好きだ

## Component 化したい

Button という Component を作って,それを使うときに fower で margin とかを当てたい

```tsx
import {VFC} from 'react';
import {Box} from '@fower/react';
import {AtomicProps} from '@fower/types';

// AtomicPropsがスタイルの型と統合しておく
type ButtonProps = AtomicProps & {
  label: string;
  onClick?: () => void;
  color?: string; // これがないとTypeError
};

export const Button: VFC<ButtonProps> = ({label, onClick, color, ...props}) => {
  return (
    <Box
      as='button'
      fontBold // 共通するやつ適当に
      white
      bgBlack
      rounded-8
      px6
      onClick={onClick}
      {...props} // 親から受け取ったスタイルをここへ
    >
      {label}
    </Box>
  );
};
```

これで,使うときに

```jsx
<Button m-12 label='ボタン' onClick={() => {}} />
```

とかでいける.
なぜ color だけ別の型なのか不明...
