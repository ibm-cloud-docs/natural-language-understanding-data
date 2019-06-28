---

copyright:
  years: 2019
lastupdated: "2019-06-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:note: .note}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Overriding language detection
{: #overriding-language-detection}

To override automatic language detection in **Analyze text** requests, specify a [language code](#language-codes) with the `language` parameter.

__Example curl request__

```bash
curl -X POST \
"{url}/v1/analyze?version=2019-06-04" \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--data '{
  "text": "...X, Y, Z, now I know my A, B, Cs",
  "features": {
    "keywords": {}
  },
  "language": "en"
}'
```
{: pre}


## Language codes for supported languages
{: #language-codes}

To see the supported features and customization options for each language, see [Language support](/docs/services/natural-language-understanding-data?topic=natural-language-understanding-data-language-support).
{: note}

| Language | Language code |
| ---- | ----|
| Arabic | `ar` |
| Chinese (Simplified) | `zh` |
| Dutch | `nl` |
| English | `en` |
| French | `fr` |
| German | `de` |
| Italian | `it` |
| Japanese | `ja` |
| Korean | `ko` |
| Portuguese | `pt` |
| Russian | `ru` |
| Spanish | `es` |
| Swedish | `sv` |
