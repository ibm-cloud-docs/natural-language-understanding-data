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
        "https://{url}/v1/models/entities"
        ```
        {:pre}

6. To use your model, specify the `model` that you deployed in the
[entities ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-understanding-data#entities){: new_window} or
[relations ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-understanding-data#relations){: new_window} options of your API request:
    - Example curl request:

        ```bash
        curl -X POST \
        "{url}/v1/analyze" \
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
"{url}/v1/models/entities/{model_id}" \
--header "Authorization: Bearer {token}" \
```
{: pre}


## Language support for custom models
{: #language-support-for-custom-models}

Check *Custom model language support* on the [Language support](/docs/natural-language-understanding-data?topic=natural-language-understanding-data-language-support) page to see the languages supported for custom models.

### Targeted sentiment for custom model entities
{: #targeted-sentiment-for-custom-entities}

For English only, you can get sentiment scores for each custom model entity that is detected by the service by setting the `sentiment: true` option in the entities object. No other languages support targeted sentiment for custom model entities.
