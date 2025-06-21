# Next.jsのApp RouterとPages Routerのコードの違い

```typescript
type ProductProps = {
  product: Product;
};

export const getServerSideProps = (async () => {
  const res = await fetch("https://dummyjson.com/products/1");
  const product = await res.json();
  return { props: { product } };
}) satisfies GetServerSideProps<ProductProps>;

export default function ProductPage({
  product,
}: InferGetServerSidePropsType<typeof getServerSideProps>) {
  return (
    <ProductLayout>
      <ProductContents product={product} />
    </ProductLayout>
  );
}

function ProductContents({ product }: ProductProps) {
  return (
    <>
      <ProductHeader product={product} />
      <ProductDetail product={product} />
      <ProductFooter product={product} />
    </>
  );
}

// ...
```

```typescript
type ProductProps = {
  product: Product;
};

// <ProductLayout>は`layout.tsx`へ移動
export default function ProductPage() {
  return (
    <>
      <ProductHeader />
      <ProductDetail />
      <ProductFooter />
    </>
  );
}

async function ProductHeader() {
  const res = await fetchProduct();

  return <>...</>;
}

async function ProductDetail() {
  const res = await fetchProduct();

  return <>...</>;
}

// ...

async function fetchProduct() {
  // Request Memoizationにより、実際のデータフェッチは1回しか実行されない
  const res = await fetch("https://dummyjson.com/products/1");
  return res.json();
}
```
