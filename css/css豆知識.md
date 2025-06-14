:root と html 要素の違い

下のように設定すると特定性の高い :root の設定が優先される。

```css
:root {
  color: red
}
html {
  color: green;
}
```
