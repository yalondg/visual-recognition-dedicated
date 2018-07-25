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
{:note: .deprecated}

# About
{: #about}

The {{site.data.keyword.visualrecognitionfull}} Dedicated service uses deep learning algorithms to analyze images for scenes, objects, and other content. The response includes keywords that provide information about the content.
{: shortdesc}

##Available models
{: #models}

A set of built-in models (also known as classifiers) provides highly accurate results without training:

- [**General** model](/docs/services/visual-recognition-dedicated/customizing.html#default-classifiers): Default classification from thousands of classes.
- **Explicit** model (Beta): Whether an image is inappropriate for general use.
- **Food** model (Beta): Specifically for images of food items.

Use the beta [{{site.data.keyword.visualrecognitionshort}} tool ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://visual-recognition-tooling.sk.kr.bluemix.net/){: new_window} to create and manage your data.
{: tip}
{: download}

You can also train [custom models](/docs/services/visual-recognition-dedicated/tutorial-custom-classifier.html) to create specialized classes.

## How to use the service
{: #how-to-use}

The following image shows the process of creating and using {{site.data.keyword.visualrecognitionshort}}:

![Describes the flow of the {{site.data.keyword.visualrecognitionshort}} service, from preparing, training, and classifying images to viewing results.](images/visual-recognition-process-110717.png)

## Use cases

The {{site.data.keyword.visualrecognitionshort}} Dedicated service can be used for diverse applications and industries, such as:

- **Manufacturing:** Use images from a manufacturing setting to make sure products are being positioned correctly on an assembly line
- **Visual auditing:** Look for visual compliance or deterioration in a fleet of trucks, planes, or windmills out in the field, train custom models to understand what defects look like
- **Insurance:** Rapidly process claims by using images to classify claims into different categories
- **Social listening:** Use images from your product line or your logo to track buzz about your company on social media
- **Social commerce:** Use an image of a plated dish to find out which restaurant serves it and find reviews, use a travel photo to find vacation suggestions based on similar experiences
- **Retail:** Take a photo of a favorite outfit to find stores with those clothes in stock or on sale, use a travel image to find retail suggestions in that area
- **Education:** Create image-based applications to educate about taxonomies
