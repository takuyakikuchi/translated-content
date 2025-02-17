---
title: URL.toString()
slug: Web/API/URL/toString
page-type: web-api-instance-method
tags:
  - API
  - Method
  - Reference
  - Stringifier
  - URL
  - URL API
browser-compat: api.URL.toString
---

{{ApiRef("URL API")}}

O método **`URL.toString()`** {{Glossary("stringifier")}} retorna a {{domxref("USVString")}} contendo toda a URL. Efetivamente esta é a versão read-only de {{domxref("URL.href")}}.

{{AvailableInWorkers}}

## Sintaxe

```js
const href = url.toString();
```

### Retorna o valor

Uma {{domxref("USVString")}}.

## Exemplos

```js
const url = new URL(
  "https://developer.mozilla.org/en-US/docs/Web/API/URL/toString"
);
url.toString(); // deve rerornar a URL como string
```

## Especificações

{{Specifications}}

## Compatibilidade de browser

{{Compat}}

## Veja também

- A interface {{domxref("URL")}} a quem pertence.
