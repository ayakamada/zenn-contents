---
title: "Gatsby.jsのかるいまとめ" # 記事のタイトル
emoji: "💬" 
type: "tech" # tech: 技術記事 / idea: アイデア記事
topics: ['gatsby', 'react'] 
published: true 
---

# gatsby.jsとは
Reactベースの静的サイトジェネレーター
SSG（Static Site Generator）
https://www.gatsbyjs.com/

> Webサイトの公開・構築に良く使われるWordPressなどのCMSは、記事の「閲覧時」に動的にサイト内容が生成されるが、静的サイトジェネレータは閲覧時ではなく「ビルド時」にHTMLやCSSなどがあらかじめ生成されていることが特徴。



# なぜgatsby.js
以前に[React-Static](https://github.com/react-static/react-static)でサイトを作っていて、とにかくはやい＆なんとなくでそれなりに形になったのでSSGを使いたいと思っていた。
ドキュメントが少なくて初心者にはとっつきにくい部分があったので、別のフレームを調べていたところ発見。

- Next.jsの方がいろいろできそうだったが、今回は小規模サイトなのでgatsbyで機能的に十分
- Tutorialなどドキュメントが充実している
- Qiitaなどでまとめ記事が多かったのでハマりどころの解決策がみつけやすい

### 参考にしたサイト
[Reactの最強フレームワークGatsby.jsの良さを伝えたい！！](https://qiita.com/hppRC/items/00739eaf9ae7fc95c1ca)



# gatsby.jsの特徴

## スターターテーマがある
https://www.gatsbyjs.com/starters/?v=2

これだけで、開発環境が整う。
webpackの設定が必要ない
```
gatsby new my-gatsby-project https://github.com/gatsbyjs/gatsby-starter-blog
```


## プラグインが豊富
https://www.gatsbyjs.com/plugins/

- sassコンパイルの設定はこれでOK
https://www.gatsbyjs.com/plugins/gatsby-plugin-sass/?=

- 画像最適化を自動で行ってくれる、gatsby-image
https://www.gatsbyjs.com/plugins/gatsby-image/

### gatsby-image
[公式サイト](https://using-gatsby-image.gatsbyjs.org/)
> - デバイスと画像サイズにあった画像を読み込む
> - 読み込み中に画像ポジションを維持するので、読み込み中にページが動かない
> - blur-upエフェクトを使用して、フルサイズ読み込み中は、小さい画像を読み込んで表示する
> - トレースされたプレースホルダーSVG画像を提供
> - lazyloadを使用して、初期読み込み時間を短縮
> - ブラウザがWebpをサポートしていたらWebp画像を使用する


## データまわりは、Graphql
http://localhost:8000/__graphql

`gatsy-config.js`やmarkdownで設定したtitle,slugなどはすべてgraphqlを介して取得できる


## その他

- src/pagesの中のファイルは、各々一つのページとして作成される
src/pages/about.jsxというファイルがあると、/aboutになる



## showcase
https://www.gatsbyjs.com/showcase/