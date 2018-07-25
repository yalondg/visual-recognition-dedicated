---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Getting started tutorial

This tutorial guides you through how to use some built-in classifiers (also known as models) in {{site.data.keyword.visualrecognitionfull}} Dedicated to classify an image.
{: shortdesc}

## Before you begin
{: #prerequisites}

You create your service instance of the {{site.data.keyword.visualrecognitionshort}} Dedicated service through {{site.data.keyword.Bluemix}}, so you need a free {{site.data.keyword.Bluemix_dedicated_notm}} account to get started.

1.  Log into your {{site.data.keyword.Bluemix_dedicated_notm}} account.
1.  After you log in, create your service instance from the [{{site.data.keyword.visualrecognitionshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window} page in the Catalog.
1.  The API uses HTTP basic authentication. If you already know your credentials for the {{site.data.keyword.visualrecognitionshort}} service, skip this step. For details about how to find your service credentials, see [Service credentials for Watson services ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/watson/getting-started-credentials.html#getting-credentials-manually){: new_window}.

    **Note**: Service credentials (`username` and `password`) are different from your {{site.data.keyword.Bluemix_dedicated_notm}} account username and password.

## Step 1: Classify an image
{: #classify}

The endpoint used in this tutorial might not be your service endpoint. Check your endpoint URL on the **Service credentials** page in your instance of the {{site.data.keyword.visualrecognitionshort}} Dedicated service on {{site.data.keyword.Bluemix_dedicated_notm}}.
{: tip}

1.  Download the sample <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/fruitbowl.jpg" download="fruitbowl.jpg">fruitbowl.jpg <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> image.
1.  Issue the following command to upload the image and classify it against the General model:
    - Replace `{username}` and `{password}` with the service credentials you copied earlier.
    - Modify the location of the images\_file to point to where you saved the image.
    - Replace the `https . . .` endpoint with your endpoint URL

    ```bash
    curl -X POST -u "{username}:{password}" --form "images_file=@fruitbowl.jpg" \ "https://gateway.yourenvironment.watsonplatform.net/visual-recognition/api/v3/classify?version=2016-05-20"
    ```
    {: pre}

    The response includes the General model or classifier (which uses the `default` classifier_id), the classes identified in the image, and a score for each class.

    ```json
    {
      "images": [
        {
          "classifiers": [
            {
              "classifier_id": "default",
              "name": "default",
              "classes": [
                {
                  "class": "banana",
                  "score": 0.562,
                  "type_hierarchy": "/fruit/banana"
                },
                {
                  "class": "fruit",
                  "score": 0.788
                },
                {
                  "class": "diet (food)",
                  "score": 0.528,
                  "type_hierarchy": "/food/diet (food)"
                },
                {
                  "class": "food",
                  "score": 0.528
                },
                {
                  "class": "honeydew",
                  "score": 0.5,
                  "type_hierarchy": "/fruit/melon/honeydew"
                },
                {
                  "class": "melon",
                  "score": 0.501
                },
                {
                  "class": "olive color",
                  "score": 0.973
                },
                {
                  "class": "lemon yellow color",
                  "score": 0.789
                }
              ]
            }
          ],
          "image": "fruitbowl.jpg"
        }
      ],
      "images_processed": 1,
      "custom_classes": 0
    }
    ```
    {: codeblock}

    Confidence scores are in the range of 0 to 1, with a higher score indicating greater correlation. By default, the `/v3/classify` calls don't include classes with a score below `0.5`.

## Next steps

You have a basic understanding of how to use the built-in default classifier with {{site.data.keyword.visualrecognitionshort}} Dedicated. Now dive deeper:

- Learn more about how to [build a custom classifier](/docs/services/visual-recognition-dedicated/tutorial-custom-classifier.html).
- Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/762-visual-recognition-dedicated){: new_window}.

### Attributions
{: #attributions}

- [Fruit basket ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://flic.kr/p/JPHES){: new_window} by Flikr user [Ryan Edwards-Crewe ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.flickr.com/photos/ryanec/){: new_window} used under [Creative Commons Attribution 2.0 license ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://creativecommons.org/licenses/by/2.0/deed.en){: new_window}. No changes were made to this image.
