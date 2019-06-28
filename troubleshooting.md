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
{:download: .download}

# Troubleshooting
{: #troubleshooting}

If you have problems with {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}}, the following troubleshooting tips might help.
{:shortdesc}

## Incorrect language detection
{: #incorrect-language-detection}

The automatic language detection might not be accurate for text that contains fewer than 100 characters. If the service doesn't detect the correct language of your text, you can [override automatic language detection](/docs/services/natural-language-understanding-data?topic=natural-language-understanding--data-overriding-language-detection).

## Explanations for particular results
{: #explanations-for-results}

{{site.data.keyword.nlushort}} does not provide any diagnostic tools to explain why a particular request returns a particular result. The service is designed to provide accurate results for as many text samples as possible, but due to the nature of the machine learning models we use, there is no guarantee that any particular result will look correct from a human perspective.





