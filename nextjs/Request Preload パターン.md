# Request Preload パターン

例１

```typescript
// preload(あらかじめ非同期でフェッチ処理を行う)
const userPromise = getUser();
const productsPromise = getProducts();
const noticesPromise = getNotices();

export default async function Parent() {
  const user = await userPromise;
  return (
    <>
      <Child productsPromise={productsPromise} noticesPromise={noticesPromise} />
    </>
  );
}

function Child({ productsPromise, noticesPromise }) {
  // 子でawait
  const products = use(productsPromise);
  return (
    <>
      <GrandChild noticesPromise={noticesPromise} />
    </>
  );
}

function GrandChild({ noticesPromise }) {
  // 孫でawait
  const notices = use(noticesPromise);
  return <div>{/* ... */}</div>;
}
```

例２

```typescript
import "server-only";

export const preloadCurrentUser = () => {
  // preloadなので`await`しない
  void getCurrentUser();
};

export async function getCurrentUser() {
  const res = await fetch("https://dummyjson.com/user/me");
  return res.json() as User;
}
```

```typescript
export default function Page({ params }: { params: Promise<{ id: string }> }) {
  const { id } = await params;
  // `<Product>`や`<Comments>`のさらに子孫で`user`を利用するため、親コンポーネントでpreloadする
  preloadCurrentUser();

  return (
    <>
      <Product productId={id} />
      <Comments productId={id} />
    </>
  );
}
```

あらかじめ非同期でフェッチ処理を行うことで、子コンポーネントや孫コンポーネントでの待機時間を短縮し、全体のパフォーマンスを向上させることができる。
