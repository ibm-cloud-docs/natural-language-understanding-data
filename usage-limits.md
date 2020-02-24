---

copyright:
  years: 2019
lastupdated: "2019-06-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Usage limits
{: #usage-limits}

The following usage limits and restrictions apply to {{site.data.keyword.nlushort}} service instances.
{: shortdesc}

## Analyzed text limit
{: #analyzed-text}

{{site.data.keyword.nlushort}} truncates analyzed text that contains more than 50,000 single-byte or multibyte characters. To view the text that counts toward this limit in your requests, set the `return_analyzed_text` parameter to `true`.

You can set a smaller character limit with the `limit_text_characters` parameter.

Example parameters object:
```json
{
  "text": "example text",
  "limit_text_characters": 10000,
  "return_analyzed_text": true,
  "features": {
    "concepts": {}
  }
}
```

## Language support
{: #language-support}

Different language restrictions apply depending on how you use the service. For details, see the [Language support](/docs/natural-language-understanding-data?topic=natural-language-understanding-data-language-support) page.


