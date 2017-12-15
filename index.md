---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Getting started tutorial
{: #getting-started}

The {{site.data.keyword.visualrecognitionfull}} Dedicated service allows you to use default classifiers to classify images.
{: shortdesc}

## Step 1: Log in, create the service, and get your credentials
{: #create-service}

You create your free instance of the {{site.data.keyword.visualrecognitionshort}} service through {{site.data.keyword.Bluemix}}, so you need a free {{site.data.keyword.Bluemix_notm}} account to get started.

The API uses HTTP basic authentication. If you already know your credentials for the {{site.data.keyword.visualrecognitionshort}} service, skip this step.
{: tip}

1.  Log into your {{site.data.keyword.Bluemix_notm}} account.
1.  After you log in, in the {{site.data.keyword.visualrecognitionshort}} Dedicated service page, enter a name in the **Service name** field to identify your instance of the service and click **Create**.
1.  Copy your credentials:
    1.  Click **Service Credentials**.
    1.  Copy the `username` and `password` that are associated with the instance.
    **Note**: Service credentials (`username` and `password`) are different from your {{site.data.keyword.Bluemix_notm}} account username and password.

## Step 2: Classifying an image
{: #classify}

The endpoint used in this tutorial might not be your service endpoint. Check your endpoint URL on the **Service Credentials** page in your instance of the {{site.data.keyword.visualrecognitionshort}} Dedicated service on {{site.data.keyword.Bluemix_notm}}.
{: tip}

1.  Download the sample [fruitbowl.jpg ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/fruitbowl.jpg){:new_window} image.
1.  Issue the following cURL command to upload the image and classify it against all built-in classifiers:
    - Replace `{username}` and `{password}` with the service credentials you copied earlier.
    - Modify the location of the `images\_file` to point to where you saved the image.
    - Replace the `https . . .` endpoint with your endpoint URL

    ```bash
    curl -X POST -u "{username}:{password}" -F "images_file=@fruitbowl.jpg" "https://gateway.yourenvironment.watsonplatform.net/visual-recognition/api/v3/classify?version=2016-05-17"
    ```
    {: pre}

  The response includes the default classifier, the classes identified in the image, and a score for each class.

    ```json
    {
      "custom_classes": 0,
      "images": [
        {
          "classifiers": [
            {
              "classes": [
                {
                  "class": "banana",
                  "score": 0.81,
                  "type_hierarchy": "/fruit/banana"
                },
                {
                  "class": "fruit",
                  "score": 0.922
                },
                {
                  "class": "mango",
                  "score": 0.554,
                  "type_hierarchy": "/fruit/mango"
                },
                {
                  "class": "olive color",
                  "score": 0.951
                },
                {
                  "class": "olive green color",
                  "score": 0.747
                }
              ],
              "classifier_id": "default",
              "name": "default"
            }
          ],
          "image": "fruitbowl.jpg"
        }
      ],
      "images_processed": 1
    }
    ```
    {: screen}

  Scores range from 0-1, with a higher score indicating greater correlation. The `/v3/classify` calls don't include low-scoring classes by default.

## Next steps

Learn how to [build a custom classifier](/docs/services/visual-recognition-dedicated/tutorial-custom-classifier.html).

## Attributions
{: #attributions notoc}

- "[Fruit basket ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://flic.kr/p/JPHES "Fruit basket"){:new_window} by Flikr user [Ryan Edwards-Crewe ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.flickr.com/photos/ryanec/){:new_window} used under [Creative Commons Attribution 2.0 license ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://creativecommons.org/licenses/by/2.0/deed.en){:new_window}. No changes were made to this image.
