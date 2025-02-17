---
title: HTMLAnchorElement.password
slug: Web/API/HTMLAnchorElement/password
page-type: web-api-instance-property
tags:
  - API
  - HTMLAnchorElement
  - プロパティ
browser-compat: api.HTMLAnchorElement.password
translation_of: Web/API/HTMLAnchorElement/password
original_slug: Web/API/HTMLHyperlinkElementUtils/password
---
{{ApiRef("HTML DOM")}}

**`HTMLAnchorElement.password`** プロパティは、ドメイン名の前で指定されたパスワードが入った文字列です。

先に [`username`](/ja/docs/Web/API/HTMLAnchorElement/username) プロパティを設定せずに設定しようとすると、暗黙のうちに失敗します。

## 値

文字列です。

## 例

```js
// <a id="myAnchor" href="https://anonymous:flabada@developer.mozilla.org/en-US/HTMLAnchorElement"> 要素が文書にあったとします
const anchor = document.getElementByID("myAnchor");
anchor.password; // 'flabada' を返す
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- 所属先の {{domxref("HTMLAnchorElement")}} インターフェイス
