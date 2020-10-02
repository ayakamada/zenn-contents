---
title: "Gatsby.jsを使ってみる" 
emoji: "💬" 
type: "tech" # tech: 技術記事 / idea: アイデア記事
topics: ['gatsby', 'react'] 
published: true 
---

# 公式サイト
https://www.gatsbyjs.com/

# 環境構築
## インストール
```
npm install -g gatsby-cli
```

## テンプレートをつくる
```
gatsby new test-site

// スターターテーマを使うこともできる
gatsby new test-site https://github.com/gatsbyjs/gatsby-starter-hello-world
```

## ローカルサーバーをたちあげる
```
cd test-site
gatsby develop
```
http://localhost:8000 にアクセス
http://localhost:8000/___graphql にアクセスでGraphqlもみられる


## gatsbyコマンド
### プロダクションビルド
/public にコンパイルされたファイルが生成される
```
gatsby build
```

### プロダクションビルド＆ローカルサーバー立ち上げ
```
gatsby serve
```

--- 


# サイトフレームをつくってみる
```shell
-- src
|   |-- components //追加
|   |   |-- Layout
|   |   |   |-- Footer.jsx
|   |   |   `-- Header.jsx
|   |   `-- layout.jsx
|   `-- pages
|       |-- about.jsx // 追加
|       `-- index.jsx
```

## Header.jsx
src/components/Layout/Header.jsx
```jsx
import React from "react"

const Header = ({ location }) => {
  return (
    <header>
      <h1>header</h1>
    </header>
  )
}

export default Header;
```


## Footer.jsx
src/components/Layout/Footer.jsx
```jsx
import React from "react"

const Footer = ({ location }) => {

  return (
    <footer>
      <h1>footer</h1>
    </footer>
  )
}

export default Footer;
```


## layout.jsx
src/components/layout.jsx
```jsx
import React from 'react';
import Header from './Layout/Header';
import Footer from './Layout/Footer';

const Layout = ({ children, location }) => {
// childrenは <Layout /> コンポーネント内の記述が展開される

  return (
    <>
      <div className="site-wrap">
        <Header location={location} />
        {children}
        <Footer location={location} />
      </div>
    </>
  )
}

export default Layout;
```

## index.jsx
src/pages/index.jsx
```jsx
import React from "react"
import { Link } from 'gatsby'
import Layout from '../components/layout'

class Home extends React.Component {

  render() {

    return (
      <Layout location={this.props.location}>
        <h1>index-page</h1>
        <Link to="/about">Aboutページ</Link>
      </Layout>
    );

  }
}

export default Home;
```

## about.jsx
src/pages/about.jsx
```jsx
import React from "react"
import { Link } from 'gatsby'
import Layout from '../components/layout'

class About extends React.Component {

  render() {

    return (
      <Layout location={this.props.location}>
        <h1>about-page</h1>
        <Link to="/">indexに戻る</Link>
      </Layout>
    );

  }
}

export default About;
```

---


# Graphqlを使ってみる

## gatsby-config.js
```js
module.exports = {
  /* Your site config here */
  siteMetadata: {
      siteName: `サイト名`,
      siteUrl: `https://hogehoge.net`,
      siteLogo: `/images/logo.png`,
      author: `author`,
    },
    /* plugins */
    plugins: [],
}
```

## GraphQl
ローカルサーバーを立ち上げている状態で、（`$gatsby develp`）
http://localhost:8000/___graphql にアクセス

Explorer枠（左カラム）で取得したいデータを選択して、
Execute（再生ボタン）をクリックすると、
Code Exporter枠（右カラム）に書き方が出力される

![](https://storage.googleapis.com/zenn-user-upload/xkmxjlbybsghegakq9llmgkmeedo)




## layout.jsx
src/components/layout.jsx
```jsx
import React from 'react';
import { useStaticQuery } from 'gatsby';
import Header from './Layout/Header';
import Footer from './Layout/Footer';

const Layout = ({ children, location }) => {

  // graphqlで調べた書き方でデータを取得
  const { site } = useStaticQuery(
    graphql `
      query {
        site {
          siteMetadata {
            siteUrl
            siteName
          }
        }
      }
    `
  )

  // サイト名が取得できる
  // console.log(site.siteMetadata.siteName);

  return (
    <>
      <div className="site-wrap">
        <Header location={location} />
        {children}
        <Footer location={location} />
      </div>
    </>
  )
}

export default Layout;
```

---

# propsを渡してみる

## layout.js
src/components/layout.jsx
```jsx

 return (
    <>
      <div className="site-wrap">
        <Header
          location={location}
          siteName={site.siteMetadata.siteName}
        />
        {children}
        <Footer location={location} />
      </div>
    </>
  )
 ```
 
 ## Header.js
src/components/Layout/Header.jsx
```jsx
import React from "react"

const Header = ({ location, siteName }) => {

  return (
    <header>
      {/* サイト名が表示される */}
      {siteName} 
      <h1>header</h1>
    </header>
  )
}

export default Header;
```
