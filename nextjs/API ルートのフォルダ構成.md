# API ルートのフォルダ構成

app/products/fetcher.ts
→ 小規模なプロジェクトや単純な API の場合は、1 つのファイルにまとめることができる。

```typescript
// 商品一覧取得
export async function getProducts() {
  const res = await fetch('https://dummyjson.com/products');
  if (!res.ok) throw new Error('商品一覧の取得に失敗しました');
  return res.json();
}

// 商品詳細取得
export async function getProduct(id: string) {
  const res = await fetch(`https://dummyjson.com/products/${id}`);
  if (!res.ok) throw new Error('商品詳細の取得に失敗しました');
  return res.json();
}

// カテゴリ一覧取得
export async function getCategories() {
  const res = await fetch('https://dummyjson.com/products/categories');
  if (!res.ok) throw new Error('カテゴリ一覧の取得に失敗しました');
  return res.json();
}
```

利用例（商品一覧ページ）

```typescript
import { getProducts, getCategories } from './fetcher';

export default async function ProductsPage() {
  const [products, categories] = await Promise.all([
    getProducts(),
    getCategories(),
  ]);

  return (
    <div>
      <h1>商品一覧</h1>
      <ul>
        {products.products.map((p: any) => (
          <li key={p.id}>{p.title}</li>
        ))}
      </ul>
      <h2>カテゴリ</h2>
      <ul>
        {categories.map((c: string) => (
          <li key={c}>{c}</li>
        ))}
      </ul>
    </div>
  );
}
```

app/products/_lib/fetcher.ts
→ より大規模なプロジェクトや複数の API エンドポイントがある場合は、`_lib` フォルダを作成し、その中に各 API のフェッチャーを配置することができる。

```bash
app/
├── layout.tsx
├── page.tsx
└── products/
    ├── page.tsx                  // 商品一覧ページ
    ├── [id]/
    │   └── page.tsx              // 商品詳細ページ
    └── _lib/
        ├── fetcher.ts            // データ取得のエントリーポイント
        ├── productFetcher.ts     // 商品関連API
        └── categoryFetcher.ts    // カテゴリ関連API
```

productFetcher.ts

```typescript
export async function getProducts() {
  const res = await fetch('https://dummyjson.com/products');
  if (!res.ok) throw new Error('商品一覧の取得に失敗しました');
  return res.json();
}

export async function getProduct(id: string) {
  const res = await fetch(`https://dummyjson.com/products/${id}`);
  if (!res.ok) throw new Error('商品詳細の取得に失敗しました');
  return res.json();
}
```

categoryFetcher.ts

```typescript
export async function getCategories() {
  const res = await fetch('https://dummyjson.com/products/categories');
  if (!res.ok) throw new Error('カテゴリ一覧の取得に失敗しました');
  return res.json();
}
```

fetcher.ts

```typescript
export * from './productFetcher';
export * from './categoryFetcher';
```

商品一覧ページでの利用例

```typescript
import { getProducts, getCategories } from './_lib/fetcher';

export default async function ProductsPage() {
  const [products, categories] = await Promise.all([
    getProducts(),
    getCategories(),
  ]);

  return (
    <div>
      <h1>商品一覧</h1>
      <ul>
        {products.products.map((p: any) => (
          <li key={p.id}>{p.title}</li>
        ))}
      </ul>
      <h2>カテゴリ</h2>
      <ul>
        {categories.map((c: string) => (
          <li key={c}>{c}</li>
        ))}
      </ul>
    </div>
  );
}
```

app/products/_lib/fetcher/product.ts
→　さらに細分化が必要な場合は、`_lib` フォルダ内に各 API エンドポイントごとにサブフォルダを作成し、その中にフェッチャーを配置することができる。

```bash
app/
└── products/
    └── _lib/
        └── fetcher/
            ├── product.ts      // 商品データ取得
            └── category.ts     // カテゴリデータ取得
```

product.ts

```typescript
export async function getProducts() {
  const res = await fetch('https://dummyjson.com/products');
  if (!res.ok) throw new Error('商品一覧の取得に失敗しました');
  return res.json();
}
export async function getProduct(id: string) {
  const res = await fetch(`https://dummyjson.com/products/${id}`);
  if (!res.ok) throw new Error('商品詳細の取得に失敗しました');
  return res.json();
}
```

category.ts

```typescript
export async function getCategories() {
  const res = await fetch('https://dummyjson.com/products/categories');
  if (!res.ok) throw new Error('カテゴリ一覧の取得に失敗しました');
  return res.json();
}
```

```typescript
import { getProducts } from './_lib/fetcher/product';

export default async function ProductsPage() {
  const products = await getProducts();
  return (
    <div>
      <h1>商品一覧</h1>
      <ul>
        {products.products.map((p: any) => (
          <li key={p.id}>{p.title}</li>
        ))}
      </ul>
    </div>
  );
}
```
