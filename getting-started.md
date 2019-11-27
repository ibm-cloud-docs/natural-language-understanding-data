---

copyright:
  years: 2019
lastupdated: "2019-06-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:go: .ph data-hd-programlang='go'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# Getting started tutorial
{: #getting-started}

This short tutorial introduces the {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull}} API with example requests and links to additional resources.
{:shortdesc}

## Before you begin
{: #before-you-begin}

1.  Provision the instance of the {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}}. For more information about provisioning, see [Installing](/docs/services/natural-language-understanding-data?topic=natural-language-understanding-data-install).
2.  From the {{site.data.keyword.icp4dfull_notm}} web client menu, choose **My Instances**.
3.  Click the {{site.data.keyword.nlushort}} instance to open the overview page. Copy the `{token}` and `{url}` credential values.
4.  Make sure that you have the `curl` command.
    - Test whether `curl` is installed. Run the following command on the command line. If the output lists the `curl` version with SSL support, you are set for the tutorial.

        ```bash
        curl -V
        ```
        {: pre}

    - If necessary, install a version with SSL enabled from [curl.haxx.se](https://curl.haxx.se/){: external}.


This tutorial shows you how to use the {{site.data.keyword.nlushort}} API from a command-line interface. To download client libraries for various programming languages, check out the [Watson SDKs](/docs/services/natural-language-understanding-data?topic=watson-using-sdks#using-sdks).
{:tip}

## Step 1: Analyze text
{: #analyze-sample}

Run the following command to analyze text to get sentiment and keywords. <span class="hide-dashboard">Replace `{token}` and `{url}` with your service credentials.</span>


{:note}

```bash
curl -X POST \
"{url}/v1/analyze" \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--data '{
  "text": "IBM is an American multinational information technology company headquartered in Armonk, New York, with operations in over 170 countries",
  "features": {
    "categories": {},
    "entities": {},
    "sentiment": {},
    "keywords": {}
  }
}'
```
{:pre}

The next step demonstrates how to specify options that customize the analysis for each feature.

## Step 2: Analyze target phrases and keywords
{: #analyze-phrase}

{{site.data.keyword.nlushort}} can analyze target phrases in context of the surrounding text for focused sentiment and emotion results. The **targets** option for sentiment in the following example tells the service to search for the targets "apples", "oranges", and "broccoli". Since "apples" and "oranges" are located in the text, sentiment scores are returned for those targets.

You can also get sentiment and emotion results for entities and keywords that are detected in your text. In the example, the **emotion** option for keywords tells the service to analyze each detected keyword for emotion results.

```bash
curl -X POST \
"{url}/v1/analyze" \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--data '{
  "text": "I love apples! I do not like oranges.",
  "features": {
    "sentiment": {
      "targets": [
        "apples",
        "oranges",
        "broccoli"
      ]
    },
    "keywords": {
      "emotion": true
    }
  }
}'
```
{:pre}

## Next steps
{: #next-steps}

- View the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-understanding-data){: new_window}.
- Learn how to identify [custom entities and relations](/docs/services/natural-language-understanding-data?topic=natural-language-understanding-data-customizing).
