---

copyright:
  years: 2019
lastupdated: "2019-08-30"

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

# Release notes
{: #release-notes}

The following new features and changes to the service are available.
{: shortdesc}

## Service API versioning
{: #service-api-versioning}

**Current API version**: 2019-06-04

API requests require a version parameter that takes the date in the format `version=YYYY-MM-DD`. Send the version parameter with every API request.

When we change the API in a backwards-incompatible way, we release a new minor version. To take advantage of the changes in a new version, change the value of the version parameter to the new date. If you're not ready to update to that version, don't change your version date.

### Active version dates
{: #active-version-dates}

The following table shows the service behavior changes for each version date. Switching to a later version date will activate all changes introduced in earlier versions.

|Version date|Changes summary|
|---|---|
|[`2019-06-04`](#4-june-2019)| <li>Fixed a bug that caused entities requests with custom models to ignore the `limit` option.</li><li>The default `limit` value for all entities requests is now 50 for all models.</li><li>The maximum `limit` value of 250 entities has been removed.</li>|
|[`2017-02-27`](#27-february-2017)| Base version.| 

## Version 1.0.1 (30 August 2019)
{: #30-august-2019}

- Expanded [language support](/docs/services/natural-language-understanding-data?topic=natural-language-understanding-data-language-support) for keywords to include Spanish, German, French, Italian, Brazilian Portuguese, and Japanese.
- Added support for installing on {{site.data.keyword.icp4dfull_notm}} with Red Hat OpenShift.
- Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}} offerings purchased on or after August 30, 2019. {{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}} is FISMA High Ready.

## Version 1.0.0 (28 June 2019)
{: #28-june-2019}

{{site.data.keyword.nlushort}} for {{site.data.keyword.icp4dfull_notm}} is now available as an add-on to the {{site.data.keyword.icpfull_notm}} platform.

