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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Creating a custom model

After you analyze an image in the "Getting started tutorial," you are ready to train and create a custom model. With a custom model (also known as a custom classifier), you can train the {{site.data.keyword.visualrecognitionshort}} Dedicated service to classify images to suit your business needs.
{: shortdesc}

## Step 1:  Copy your credentials
{: #copy-credentials}

Use the credentials that you copied in "Getting started tutorial." If you didn't create a service instance, run through those steps in the [Before you begin](/docs/services/visual-recognition-dedicated/index.html#prerequisites) section.

## Step 2: Creating a custom model
{: #create-custom-class}

{{site.data.keyword.visualrecognitionshort}} Dedicated can learn from example images you upload to create a new, multi-faceted model. Each example file is trained against the other files in that call, and positive examples are stored as classes. These classes are grouped to define a single model, and return their own scores. Negative example files are not stored as classes.

1.  Download the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/beagle.zip" download="beagle.zip">beagle.zip <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/husky.zip" download="husky.zip">husky.zip <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/golden-retriever.zip" download="golden-retriever.zip">golden-retriever.zip <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>, and <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/cats.zip" download="cats.zip">cats.zip <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> example training files.
1.  Call the `POST /v3/classifiers` method with the following command, which uploads the training data and creates a `dogs` custom model:
    - Replace `{username}` and `{password}` with the service credentials you copied in the first step.
    - Modify the location of the `{class}_positive_examples` to point to where you saved the .zip files.
    - Replace the `https . . .` endpoint with your endpoint URL

    ```bash
    curl -X POST -u "{username}:{password}" \
    --form "beagle_positive_examples=@beagle.zip" \
    --form "husky_positive_examples=@husky.zip" \
    --form "goldenretriever_positive_examples=@golden-retriever.zip" \
    --form "negative_examples=@cats.zip" \
    --form "name=dogs" \
    "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers?version=2016-05-20"
    ```
    {: pre}

    Positive example filenames require the suffix `_positive_examples`. In this example, the filenames are `beagle_positive_examples`, `goldenretriever_positive_examples`, and `husky_positive_examples`. The prefix (beagle, goldenretriever, and husky) is returned as the name of class.
    {:tip }

    The response includes a new classifier ID and status, for example:

    ```json
    {
      "classifier_id": "dogs_1941945966",
      "name": "dogs",
      "status": "training",
      "owner": "xxxx-xxxxx-xxx-xxxx",
      "created": "2018-03-17T19:01:30.536Z",
      "classes": [
        {
          "class": "husky"
        },
        {
          "class": "goldenretriever"
        },
        {
          "class": "beagle"
        }
      ],
    }
    ```
    {: codeblock}

1.  Check the training status periodically until you see a status of `ready`. Training begins immediately and must finish before you can query the model. Replace `{username}`, `{password}`, `{classifier_id}`, and the `https . . .` endpoint with your information:

    ```bash
    curl -X GET -u "{username}:{password}" \
    "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers/{classifier_id}?version=2016-05-17"
    ```
    {: pre}

## Step 3: Updating an existing custom model
{: #update-custom-class}

You can update a custom model either by adding classes to the model or by adding images to an existing class. Here, you improve the model that you created in Step 2 by adding a *Dalmatian* class to the types of dogs that can be classified. You also add images of cats to the negative example set for the "dogs" custom model.

1.  Download the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/dalmatian.zip" download="dalmatian.zip">dalmatian.zip <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> and <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/more-cats.zip" download="more-cats.zip">more-cats.zip <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> sample training files.
1.  Call the `POST /v3/classifiers/{classifier_id}` method with the following cURL command, which uploads the training data and updates the classifier "dogs\_1941945966":
    - Replace `{username}` and `{password}` with the service credentials you copied in the first step.
    - Replace `{classifier_id}` with the ID of the custom model you want to update.
    - Modify the location of the `{class}_positive_examples` to point to where you saved the .zip files.
    - Replace the `https . . .` endpoint with your endpoint URL

    ```bash
    curl -X POST -u "{username}:{password}" \
    --form "dalmatian_positive_examples=@dalmatian.zip" \
    --form "negative_examples=@more-cats.zip" \
    "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers/{classifier_id}?version=2016-05-20"
    ```
    {: pre}

    The existing "dogs" custom model is replaced by the retrained one with the same classifier_id. The response lists the new set of classes and the current status. For example:

    ```json
    {
      "classifier_id": "dogs_1941945966",
      "name": "dogs",
      "status": "retraining",
      "owner": "xxxx-xxxxx-xxx-xxxx",
      "created": "2018-03-17T19:01:30.536Z",
      "classes": [
        {
          "class": "husky"
        },
        {
          "class": "goldenretriever"
        },
        {
          "class": "beagle"
        },
        {
          "class": "dalmatian"
        }
      ],
    }
    ```
    {: codeblock}

    Training begins immediately. When the new one is available, the status changes to `ready`.

    Don't issue another retraining request until after the current status `ready` state. Multiple requests to retrain a model result in a single retraining taking effect. If you call the `/classify` method while the model is retraining, the old definition of the model is used.
    {: tip}
1.  Check the training status periodically until you see a status of `ready`. Replace `{username}`, `{password}`, `{classifier_id}`, and the `https . . .` endpoint with your information:

    ```bash
    curl -X GET -u "{username}:{password}" \
    "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers/{classifier_id}?version=2016-05-20"
    ```
    {: pre}

## Step 4: Classifying an image with a custom model
{: #classify-custom-class}

When the new model is ready, call it to see how it performs.

1.  Download the <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/raw/master/visual-recognition/dogs.jpg" download>dogs.jpg <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a>.
1.  Use the `POST /v3/classify` method to test your custom model. The following example classifies the `dogs.jpg` image against both the "dogs\_1941945966" custom model and the built-in `default` General model:
    - Replace `{username}` and `{password}` with the service credentials you copied in the first step.
    - Replace the `https . . .` endpoint with your endpoint URL

    ```bash
    curl -X POST -u "{username}:{password}" \
    --form "images_file=@dogs.jpg" \
    --form "classifier_ids=dogs__1941945966,default" \
    "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2016-05-20"
    ```
    {: pre}

    To classify against only the built-in General model, omit the `classifier_ids` parameter.
    {: tip}

    The response includes classifiers (models), their classes, and a score for each class. Scores range from 0-1, with a higher score indicating greater correlation. The `/v3/classify` calls omit low-scoring classes by default if high-scoring classes are identified. You can set a minimum score to display by specifying a floating point value for the `threshold` parameter in your call.

    ```json
    {
      "images": [
        {
          "classifiers": [
            {
              "classifier_id": "dogs_1941945966",
              "name": "dogs",
              "classes": [
                {
                  "class": "goldenretriever",
                  "score": 0.513638
                }
              ]
            },
            {
              "classifier_id": "default",
              "name": "default",
              "classes": [
                {
                  "class": "guide dog",
                  "score": 0.86,
                  "type_hierarchy": "/animal/domestic animal/dog/guide dog"
                },
                {
                  "class": "dog",
                  "score": 0.927
                },
                {
                  "class": "domestic animal",
                  "score": 0.927
                },
                {
                  "class": "animal",
                  "score": 0.927
                },
                {
                  "class": "beagling (dog)",
                  "score": 0.508,
                  "type_hierarchy": "/animal/domestic animal/dog/beagling (dog)"
                },
                {
                  "class": "golden retriever dog",
                  "score": 0.5,
                  "type_hierarchy": "/animal/domestic animal/dog/retriever dog/golden retriever dog"
                },
                {
                  "class": "retriever dog",
                  "score": 0.572
                },
                {
                  "class": "light brown color",
                  "score": 0.982
                }
              ]
            }
          ],
          "image": "dogs.jpg"
        }
      ],
      "images_processed": 1,
      "custom_classes": 1
    }
    ```
    {: codeblock}

1.  Review your results.

You're done! You created, trained, and queried a custom model with {{site.data.keyword.visualrecognitionshort}}.

### Deleting your custom model
{: #delete-class}

You might want to delete your custom model to begin developing your application with a clean instance.

To delete the model, call the `DELETE /v3/classifiers/{classifier_id}` method.
- Replace `{username}`, `{password}`, and the `https . . .` endpoint with your information.
- Include the `classifier_id` for the classifier you want to delete:

```bash
curl -X DELETE -u "{username}:{password}" \
"https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers/{classifier_id}?version=2016-05-20"
```
{: pre}

## Next steps

Now that you have a basic understanding of how to use custom models, you can dive deeper:

- Learn more about [Best practices for custom classifiers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2016/10/watson-visual-recognition-training-best-practices/){: new_window}.
- Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/762-visual-recognition-dedicated){: new_window}.

### Attributions
{: #attributions}

All images used on this page are from Flikr and used under [Creative Commons Attribution 2.0 license ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://creativecommons.org/licenses/by/2.0/deed.en){: new_window}. No changes were made to these images.
