# Request Memoizationのメモ

App Router の RSC では、同じリクエストを投げると、最初のリクエストのキャッシュが返却される。

例えば、RSC の親コンポーネントで API A を実行して、その後孫コンポーネントで API A を実行したら一番最初に実行した内容がキャッシュとして返却される。

これは 1 回の HTTP リクエストでの話で、パスが変わった後に同じ API を実行してもキャッシュされた値が返却されるわけではない。

[Request Memoization](https://nextjs.org/docs/app/guides/caching#request-memoization)
