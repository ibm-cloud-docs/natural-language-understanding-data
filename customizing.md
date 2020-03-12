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

# Customizing
{: #customizing}

With [{{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull_notm}}](docs/watson-knowledge-studio-data), you can
extend the {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}} add-on with custom models that identify
entities and relations unique to your domain.
{: shortdesc}

## Getting started with custom models
{: #getting-started-with-custom-models}

1. If you haven't done so already, [get started](/docs/natural-language-understanding-data?topic=natural-language-understanding-data-getting-started) with {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}}.
2. [Get started with {{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.icp4dfull_notm}}](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-wks_tutintro#wks_tutintro).
3. Create a custom model.
   1. To create a custom entities and relations model, see [Creating a machine learning model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-wks_tutml_intro) 
   2. You can also create a custom entities model with a rule based model. See [Creating a rule based model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-wks_tutrule_intro) for details.
4. [Export your model to {{site.data.keyword.nlushort}}](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-publish-ml#wks_manlu)
5. Use the **[Create entities model](https://{DomainName}/apidocs/natural-language-understanding-data#create-entities-model)** method to deploy the exported model to the service.
    - Example curl request:

        ```bash
        curl -X POST --header "Authorization: Bearer {token}" \ 
        --header "Content-Type: multipart/form-data" \ 
        --form "file=@custom_model.zip" \ 
        --form "name=MyEntitiesModel" \ 
        --form "version=1.0.1" \ 
        "https://{url}/v1/models/entities?version=2019-07-12"
        ```
        {:pre}

6. To use your model, specify the `model` that you deployed in the
[entities ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-understanding-data#entities){: new_window} or
[relations ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-understanding-data#relations){: new_window} options of your API request:
    - Example curl request:

        ```bash
        curl -X POST \
        "{url}/v1/analyze?version=2019-07-12" \
        --header "Authorization: Bearer {token}" \
        --header "Content-Type: application/json" \
        --data '{
          "text": "example text",
          "features": {
            "entities": {
              "model": "your-model-id-here"
            },
            "relations": {
              "model": "your-model-id-here"
            }
          }
        }'
        ```
        {: pre}

## Deleting a custom model
{: #deleting-a-custom-model}

To delete a model from the service, use the **[Delete entities model](https://{DomainName}/apidocs/natural-language-understanding-data#delete-entities-model)** method.

Example curl request:

```bash
curl -X DELETE \
"{url}/v1/models/entities/{model_id}?version=2019-07-12" \
--header "Authorization: Bearer {token}" \
```
{: pre}


## Language support for custom models
{: #language-support-for-custom-models}

Check *Custom model language support* on the [Language support](/docs/natural-language-understanding-data?topic=natural-language-understanding-data-language-support) page to see the languages supported for custom models.

### Targeted sentiment for custom model entities
{: #targeted-sentiment-for-custom-entities}

For English only, you can get sentiment scores for each custom model entity that is detected by the service by setting the `sentiment: true` option in the entities object. No other languages support targeted sentiment for custom model entities.


## Analyzing text with advanced rules
{: #advanced-rules}

The {{site.data.keyword.knowledgestudioshort}} advanced rules workspace allows you to create text extractors with deeper customization potential than what is offered in other custom models. To get started, see [Creating an advanced rules model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-create-advanced-rules-model).

### Uploading an advanced rules model
{: #uploading-an-advanced-rules-model}

1. Export your model from the advanced rules editor. See step 6 in [Creating an advanced rules model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-create-advanced-rules-model#create-advanced-rules-model-procedure).
    - If you plan to analyze HTML and want to extract spans over the original HTML content, check the **Enable Detagging** box before you export your model.
2. Use the **Create advanced rules model** method to upload your model to {{site.data.keyword.nlushort}}. Replace `{token}` and `{url}` with your service credentials, and replace `/Users/username/revenue_by_division_en.zip` with the path to your model file.

    ```bash
    curl -X POST --header "Authorization: Bearer {token}" \ 
    -H "Content-Type: multipart/form-data" \
    -F "name=MyAQLModel" \
    -F "language=en" \
    -F "description=Test AQL model" \
    -F "version=1.0.1" \
    -F "version_description=My version description" \
    -F "model=@/Users/username/revenue_by_division_en.zip;type=application/zip" \
    "{url}/v1/models/advanced_rules?version=2019-07-12"
    ```
    {: pre}

Use the `model_id` in the response to check the status of your model.

### Checking the status of advanced rules models
{: #checking-status-of-advanced-rules-models}

The following sample request for the **Get advanced rules model** method checks the status for the model with ID `e479adbb-8338-4d6d-973c-451548ccb08e`.

```bash
curl -X GET --header "Authorization: Bearer {token}" \
"{url}/v1/models/advanced_rules/e479adbb-8338-4d6d-973c-451548ccb08e?version=2019-07-12"
```
{: pre}

To get information for all advanced rules models deployed to your instance, use the **List advanced rules models** method.

```bash
curl -X GET --header "Authorization: Bearer {token}" \
"{url}/v1/models/advanced_rules?version=2019-07-12"
```
{: pre}

When the status is `available`, the model is ready to use.

The general **List models** method (`GET /v1/models`) does not return advanced rules models at this time.
{: note}


### Analyzing text with advanced rules models
{: #analyzing-text-with-advanced-rules}

After you've uploaded an advanced rules model and the status is `available`, you can use it with the **Analyze text** method.

- Example *parameters.json* file:

    ```json
    {
      "text": "IBM Watson",
      "features": {
        "advanced_rules": {
          "model": "e479adbb-8338-4d6d-973c-451548ccb08e"
        }
      }
    }
    ```
    {: codeblock}

- Example curl request:

    ```bash
    curl --user --header "Authorization: Bearer {token}" \
    "{url}/v1/analyze?version=2019-07-12" \
    --request POST \
    --header "Content-Type: application/json" \
    --data @parameters.json
    ```
    {: pre}

### Analyzing HTML with advanced rules models
{: #analyzing-html-with-advanced-rules-model}

{{site.data.keyword.nlushort}} removes HTML tags that are sent in the `html` or `url` parameters to focus analysis on the text content. In cases where you want the HTML tags to be processed by advanced rules models, you need to do the following.

1. When exporting your model from {{site.data.keyword.knowledgestudioshort}}, select the **Enable Detagging** button before you press **OK**.
2. Pass HTML content in the `text` field so that the service does not remove HTML tags before analysis.

    - Example *parameters.json* file:

        ```json
        {
          "text": "<html><body>IBM Watson</body></html>",
          "features": {
            "advanced_rules": {
              "model": "e479adbb-8338-4d6d-973c-451548ccb08e"
            }
          }
        }
        ```
        {: codeblock}

### Deleting an advanced rules model
{: #deleting-an-advanced-rules-model}

To delete an advanced rules model from your service instance, use the **Delete advanced rules model** method. Replace `{token}` and `{url}` with your service URL and API key, and replace `e479adbb-8338-4d6d-973c-451548ccb08e` with the model ID of the model you want to delete.

```bash
curl -X DELETE --header "Authorization: Bearer {token}" \
"{url}/v1/models/advanced_rules/e479adbb-8338-4d6d-973c-451548ccb08e?version=2019-07-12"
```
{: pre}

### Output format for advanced rules analysis
{: #advanced-rules-analysis-output}

The JSON output of an advanced rules analysis depends on the text extractor that you export from {{site.data.keyword.knowledgestudioshort}}.

- The response is a JSON object, where the keys are the names of the Annotation Query Language (AQL) output views.
- The tuples in an AQL view are represented as array of JSON objects, with one object for each tuple in the view.
- The keys in the JSON object are the names of the attributes in the view, while the values are the values of those attributes.

The following table describes how AQL data types are mapped to JSON.

| AQL Type | JSON Type | Example JSON |
| -------- | --------- | ----------- |
| `Integer` | `number` | `5` |
| `Float` | `number` | `4.13` |
| `Boolean` | `boolean` | `true` |
| `Text` | `string` | `"some string"` |
| `Span` | `object` of the form `{"text": String, "location": {"begin": Integer, "end": Integer}}` | `{ "text": "Jane", location": {"begin": 5, "end": 9} }`|
| Special case: `null` value | `null` | `null` |
| `List of Integer`| `array` of `number` | `[ 1, 2, 3, 4, 5]` |
| `List of Float`| `array` of `number` |  `[ 4.13, 4.5 ]` |
| `List of Boolean` | `array` of `boolean` |  `[ true, true, false]` |
| `List of Text` | `array` of `string` |  `[ "some string", "another string" ]` |
| `List of Span`  | `array` of `object` of the form `{"text":String, "location": {"begin": Integer, "end": Integer}}` | `[{ "text":"Jane", "location": {"begin": 5, "end": 9} }, { "text":"...", "location": {"begin": 15, "end": 40} }]` |
| Special case: empty `List` | `array` with 0 elements |  `[ ]` |
