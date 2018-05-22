---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-09"

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

The following new features and changes to the service are available.
{: shortdesc}

## Service API Versioning
{: version}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2016-05-20`.

## Beta features
{: #beta}

{{site.data.keyword.IBM_notm}} releases services, features, and language support for your evaluation that are classified as beta. These features might be unstable, might change frequently, and might be discontinued with short notice. Beta features also might not provide the same level of performance or compatibility that generally available features provide and are not intended for use in a production environment. Beta features are supported only on [developerWorks Answers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/visual-recognition.html){: new_window}.

## Changes
{: #changelog}

The following new features and changes to the service are available.

### 22 May 2018
{: #22May2018}

- **Information security**: The documentation includes some new details about data privacy. Read more in [Information security](information-security.html).

### 11 December 2017
{: #11december2017}

<ul>
  <li>
    <strong>Increased accuracy and output with the General model</strong>
      <p>
        The General model, which contains several thousand tags, now detects more secondary objects and has improved scene detection. These improvements help recognize the less prominent aspects of an image. In addition, the average number of tags returned per image has increased to 10.
      </p>
      <p>
        The following image shows an example of the tags returned before the update and the additional tags that are now returned.
      </p>
      <img src="images/tree-flower.jpg" alt="Photograph of azalea plant">
      <table>
        <tr>
          <th>Original tags</th>
          <th>Additional tags</th>
        </tr>
        <tr>
          <td></td>
          <td>
          Tag: tree<br/>
          Score: 0.799</td>
        </tr>
        <tr>
          <td></td>
          <td>
          Tag: flower<br/>
          Score: 0.792</td>
        </tr>
        <tr>
          <td>
          Tag: alpine azalea<br/>
          Score: 0.696</td>
          <td></td>
        </tr>
        <tr>
          <td>
          Tag: plant<br/>
          Score: 0.868</td>
          <td></td>
        </tr>
        <tr>
          <td>
          Tag: azalea<br/>
          Score: 0.617</td>
          <td></td>
        </tr>
        <tr>
          <td>
            Tag: swamp azalea<br/>
          Score: 0.5</td>
          </td>
          <td></td>
        <tr>
          <td>
            Tag: reddish orange color<br/>
          Score: 0.1</td>
          </td>
          <td></td>
        </tr>
      </table>
    <li>
      <strong>New Explicit model available in beta</strong>
      <p>
        The Explicit model, which launches in beta, classifies whether an image contains pornographic content and is inappropriate for general use. You can include the Explicit model with other models for combined analysis. For example, include both the `default` and `explicit` classifier IDs in your request to return image tags and whether the image contains explicit content.
      <p>
        For details about the API call, see the <strong>Classify images</strong> method in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/visual-recognition/api/v3/#classify_an_image), or try out the model in the [API explorer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-api-explorer.mybluemix.net/apis/visual-recognition-v3#!/Classify/classify).
      </p>
    </li>
    <li>
      <strong>Support for larger file sizes</strong>
      <p>
        The <strong>Classify images</strong> methods now support image files up to 10 MB and .zip files up to 100 MB.
    </li>
    <li>
      <strong>Array required when passing classifier IDs</strong>
      <p>
        The API now enforces an array when you pass in `classifier_ids` as part of the <strong>parameters</strong> object in the <strong>Classify images</strong> method. Previously, you could pass a classifier ID as a string. For more information, see the parameters description and example file in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/visual-recognition/api/v3/?curl#classify_an_image).
      </p>
    </li>
</ul>

### 30 June 2017
{: #30june2017}

- **Improved tagging**: We increased the number of training images for the default classifier. That increase improve the ability to recognize accurately the overall ‘scene’ of an image. For details, see [Further Enhancements for General Tagging Feature ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/07/watson-visual-recognition-sees-enhancements-general-tagging-feature/){: new_window}
- **Additional languages**: The **Classify images** method now supports Korean, Italian, and German in addition to English, Arabic, Spanish, and Japanese.

    For details about the API call, see the **Classify an image** method in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/762-visual-recognition-dedicated/#classify-an-image){: new_window} External link icon.

### 16 May 2017
{: #16may2017}

- **New food classifier is available: Beta**

    A new beta food recognition model provides enhanced specificity and accuracy for images of food items. The **Classify an image** method allows you to add this new classifier, "food", to the `classifier_ids` parameter.


### 21 April 2017
{: #21april2017}

This is the General Availability release of the {{site.data.keyword.visualrecognitionshort}} Dedicated service.

Any custom classifiers that were created while the service was in Beta must be recreated in a GA instance of the service.

Please be aware of the following items when using the {{site.data.keyword.visualrecognitionshort}} service:

- **Version date:** To utilize the features of this release, use `2016-05-17` as the value for the `version` parameter.
- **Classes and classifiers:** Single classifiers are called "classes". A group of classes is called a "classifier".
- **Classification:** Use the `POST` or `GET /v3/classify` methods to quickly and accurately identify a variety of subjects and scenes with default classes.
- **Multi-faceted custom classifiers:** You can create and train highly-specialized classifiers that are defined by several classes. For example, you can create a "new\_red\_car" classifier that is defined by the classes "new\_cars" and "red\_cars". To learn more about creating multi-faceted classifiers, see [Structure of the training data](/docs/services/visual-recognition-dedicated/customizing.html#structure).
- **Asynchronous training:** Training of custom classifiers is asynchronous, so training calls complete quickly while your custom classifier continues to learn in the background. To check on the training status of your custom classifier and find out when it is available for use, call the `GET /v3/classifiers/{classifier_id}` method and check the `status` response parameter.
- **`GET` calls for deleted classfiers:** Calling `GET /classifiers` to get a list of active custom classifiers can provide inaccurate results after classifiers have been deleted.  The list of classifiers in the response can include classifiers that have been deleted in the past, and repeated calls will return different results. To work around this issue, check each classifier in the response using `GET /classifiers/{classifier_id}` to learn which are available and which have been deleted.  Making this call for a classifier which has been deleted will result in an error message that the classifier is not found.
- **Repeated calls may stop training job:** Repeatedly calling `GET /classifiers` while training or retraining is in progress, in order to check status, can result in killing the training job. To work around this issue, poll a new classifier's status using `GET /classifiers/{classifier_id}`. In other words, use the classifier `GET` for a single classifier ID, rather than `GET /classifiers`, which gets all classifiers, and can trigger this issue. Note that `GET /classifiers/{classifier_id}` is also faster. You may also see this issue if you are repeatedly using `POST /classify` to classify new images while training is in progress; wait until training completes to classify new images using `POST /classify`.
