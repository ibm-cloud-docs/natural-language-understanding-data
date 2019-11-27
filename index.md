---

copyright:
  years: 2019
lastupdated: "2019-06-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# About
{: #about}

With {{site.data.keyword.nlufull}} for {{site.data.keyword.icp4dfull}}, you can analyze text content for keywords and sentiment all from your own {{site.data.keyword.icp4dfull_notm}} installation. You can also use [custom models](/docs/services/natural-language-understanding-data?topic=natural-language-understanding-data-customizing) that you create in {{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}} to analyze text for entities and relations between entities.
{: shortdesc}

## Features
{: #features}

{{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}} supports a subset of the features of the public [{{site.data.keyword.nlushort}}](/docs/services/natural-language-understanding) service.

### Categories
{: #categories}

Categorize your content using a five-level classification hierarchy. View the complete list of categories [here](/docs/services/natural-language-understanding?topic=natural-language-understanding-categories-hierarchy). For example:

**Input**
> url: "www.cnn.com"

**Response**
> /news </br>
> /art and entertainment </br>
> /movies and tv/television </br>
> /news </br>
> /international news

### Entities
{: #entities}

In order to analyze entities with {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}}, you must create a [custom model](/docs/services/natural-language-understanding-data?topic=natural-language-understanding-data-customizing).
{: note}

Find people, places, events, and other types of entities mentioned in your content.

**Input**
> text: "IBM is an American multinational technology company headquartered in Armonk, New York, United States, with operations in over 170 countries."

**Response**
> IBM: Company </br>
> Armonk: Location </br>
> New York: Location </br>
> United States: Location

### Keywords
{: #keywords}

Search your content for relevant keywords. For example:

**Input**
>text: "IBM is an American multinational technology company headquartered in Armonk, New York, United States, with operations in over 170 countries."

**Response**
>American multinational technology company </br>
>United States </br>
>IBM

### Relations
{: #relations}

In order to analyze relations with {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}}, you must create a [custom model](/docs/services/natural-language-understanding-data?topic=natural-language-understanding-data-customizing).
{: note}

Recognize when two entities are related, and identify the type of relation. For example:

**Input**
>text: "The Nobel Prize in Physics 1921 was awarded to Albert Einstein."

**Response**
>"awardedTo" relation between "Noble Prize in Physics" and "Albert Einstein" </br>
>"timeOf" relation between "1921" and "awarded"

### Sentiment
{: #sentiment}

Analyze the sentiment toward specific target phrases and the sentiment of the document as a whole. You can also get sentiment information for detected entities and keywords by enabling the sentiment option for those features. For example:

**Input**
>text: "Thank you and have a nice day!"

**Response**
>Positive sentiment (score: 0.91)

## Supported languages
{: #supported-languages}

See the [Language support documentation](/docs/services/natural-language-understanding-data?topic=natural-language-understanding-data-language-support) for details about supported languages in {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull}}.

## FISMA support
{: #fisma-support}

Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.nlushort}} on {{site.data.keyword.icp4dfull_notm}} offerings purchased on or after August 30, 2019. FISMA support is also available to those who purchased the June 28, 2019 version and upgrade to the August 30, 2019 version. {{site.data.keyword.nlushort}} on {{site.data.keyword.icp4dfull_notm}} is FISMA High Ready.
