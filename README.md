# shopify-GA4-schema-Ecommerce-dataLayer
Shopify E-Commerce dataLayer for GA4 schema and GTM
Welcome to the dataLayer-shopify wiki!

# Definition
A data layer helps you collect more accurate analytics data, that in turn allows you to better understand what potential buyers are doing on your website and where you can make improvements. It also reduces the time to implement marketing tags on a website, and reduces the need for IT involvement, leaving them to get on with implementing new features and fixing bugs.

# Resources
https://help.shopify.com/themes/liquid/objects
http://www.datalayerdoctor.com/a-gentle-introduction-to-the-data-layer-for-digital-marketers/
http://www.simoahava.com/analytics/data-layer/

# Pages / Actions & Variables Guide
You can access the full Pages/Actions & Variables list here: https://docs.google.com/spreadsheets/d/1SB96_v8dwNMGy-GlVJ7DkrmXrezaBYI5V6MLmD-FF8Q/edit?usp=sharing


# Pages / Actions
The Page types and descriptions of the dataLayer will exist.

# Variables
All information the dataLayer is able to extract and the pages they can be extracted from.


# GTM Pages & Variables Import
If you are using GTM, you can import the GTM-InitialSetup.json container that sets up most of the GTM Triggers and Variables for you. This is constantly updated but if there are certain configurations that are not present please refer to the guide above and you should be able to set them up yourself. https://github.com/Niamul82773/dataLayer-shopify/blob/main/CAPI%20Shopify%20transaction%20data%20layer.json https://github.com/Niamul82773/dataLayer-shopify/blob/main/G%20ads%20E%20C%20%26%20Rmarketing%20transaction%20data%20layer.json https://github.com/Niamul82773/dataLayer-shopify/blob/main/GA4%20Ecommerce%20Tracking%20transaction%20data%20layer.json https://github.com/Niamul82773/dataLayer-shopify/blob/main/Shopify%20GA4%20GAds%20CAPI%20All%20.json https://github.com/Niamul82773/dataLayer-shopify/blob/main/SnapChat%20Pixel%20Brower%20sidetransaction%20data%20layer.json https://github.com/Niamul82773/dataLayer-shopify/blob/main/TikTok%20Event%20API%20Brower%20transaction%20data%20layer.json https://github.com/Niamul82773/dataLayer-shopify/blob/main/TikTok%20Event%20API%20Server%20transaction%20data%20layer.json https://github.com/Niamul82773/dataLayer-shopify/blob/main/Twitter%20Pixel%20Brower%20sidetransaction%20data%20layer.json To import the container in GTM navigate to Admin > Import Container. Under "Choose Container File", upload GTM-InitialSetup.json then choose whether to use a new or existing workspace. If you are unsure, it is always best to use a new workspace that can be merged into an existing workspace when you are satisfied. Next, you are 9 times out of 10 always going to use merge > Rename conflicting tags, triggers and variables ( always use Rename to be safe ). If you aren't sure why you should use Overwrite, then you most definitely shouldn't be using it. You can get more information on the changes by clicking on "View Detailed Changes". Anything that is renamed will have "import" appended to the title.

# Integration Instructions
Keep note that this is a base template that attempts to exploit Shopify’s data rendering capabilities and create an ease of integration for dataLayers that can be reused across all Shopify sites. Nonetheless, each site could carry variations that may not be completely compatible with this template. There may also be some areas of data we may have missed, may be a new configuration, or we wouldn’t know is necessary for your efforts. It is highly recommended to review the entire implementation and make your own configurations if needed.
Please let us know if you have any questions or concerns and we will be happy to follow up as soon as possible :)
There are 2 types of Installations provided below. Review each option and choose one.

# Installation Option 1:
If the Checkout page cannot be edited, use this option. ( Checkout page edits are only available on Shopify Plus. )
## Assets
<html>
<body>
<!--StartFragment--><b style="font-weight:normal;" id="docs-internal-guid-8375bad1-7fff-cce0-e86d-a51faed67867"><div dir="ltr" style="margin-left:0pt;" align="left">

Assets | Integration Type | Asset Type
-- | -- | --
theme.liquid ( or your primary theme template ) | Modification | Layout: Online Store > Themes > ... > Edit HTML/CSS > Layout > theme.liquid ( or primary theme template )
confirmation page | Modification | Admin Setting: Settings > Checkout > Order Processing > Additional Pixels & Scripts
dataLayer-allPages | Creation | Snippet: Online Store > Themes > ... > Edit HTML/CSS > Snippets > ( will create Snippet in instructions )
Google Tag Manager or any other Tag Manager Code | Creation or Modification | This can either be a Snippet ( unless adding to the confirmation page ) or added directly into your Layout

</div></b><!--EndFragment-->
</body>
</html>
GTM / Tag Manager Installation or Modification

* Within the theme.liquid layout, place the GTM / Tag Manager container ( snippet or actual code block ) directly below the opening <body> tag.
* Within the confirmation page the GTM / Tag Manager container ( actual code block ONLY ) should be placed above all additional scripts. Important Note: Snippets cannot be applied to the confirmation page, any scripts MUST be placed as an actual code block.

Create the dataLayer-allPages snippet ( use exact naming and casing! )

* Create a snippet called dataLayer-allPages and copy over the provided [dataLayer-allPages.js](https://github.com/Niamul82773/dataLayer-shopify/blob/main/dataLayer-allPages.js) in the newly created snippet. In the code, navigate to the “Dynamic Dependencies” section and make any necessary changes.
`````/**********************`````
`````* DYNAMIC DEPENDENCIES`````
`````***********************/`````
        
 `````__DL__ = {`````
    `````dynamicCart: true,  // if cart is dynamic (meaning no refresh on cart add) set to true`````
    `````debug: true, // if true, console messages will be displayed`````
    `````cart: null,`````
    `````wishlist: null,`````
    `````removeCart: null`````
`````};`````
        
`````customBindings = {`````
    `````cartTriggers: [],`````
    `````viewCart: [],`````
    `````removeCartTrigger: [],`````
    `````cartVisableSelector: [],`````
    `````promoSubscriptionsSelectors: [],`````
    `````promoSuccess: [],`````
    `````ctaSelectors: [],`````
    `````newsletterSelectors: [],`````
    `````newsletterSuccess: [],`````
    `````searchPage: [],`````
    `````wishlistSelector: [],`````
    `````removeWishlist: [],`````
    `````wishlistPage: [],`````
    `````searchTermQuery: [getURLParams('q')], // replace var with correct query`````
`````};`````
        
Add the code to the layouts
* Within the theme.liquid layout, place this include snippet {% include 'dataLayer-allPages' %} right before the closing </head> tag
* Within the confirmation page admin settings, copy over the provided [dataLayer-allPages.js](https://github.com/TechnicalWebAnalytics/dataLayer-shopify/blob/master/dataLayer-allPages.js) code directly above the GTM code block. ( Remember, snippets cannot be used in this section so the actual code block must be added )

Prerequisite Library
* These are already included in the dataLayer build.
Review, Test, Done :)



***
# Installation Option 2:
      If the Checkout page can be edited, use this option.
## Assets
<html>
<body>
<!--StartFragment--><b style="font-weight:normal;" id="docs-internal-guid-b204e398-7fff-5d91-24e9-4ea6da5b819e"><h4 dir="ltr" style="line-height:1.2;margin-left: -15pt;background-color:#ffffff;margin-top:0pt;margin-bottom:12pt;padding:6pt 0pt 0pt 0pt;"></h4><div dir="ltr" style="margin-left:0pt;" align="left">

Assets | Integration Type | Asset Type
-- | -- | --
theme.liquid ( or your primary theme template ) | Modification | Layout: Online Store > Themes > ... > Edit HTML/CSS > Layout > theme.liquid ( or primary theme template )
checkout.liquid | Modification | Layout: Online Store > Themes > ... > Edit HTML/CSS > Layout > checkout.liquid
dataLayer-allPages | Creation | Snippet: Online Store > Themes > ... > Edit HTML/CSS > Snippets > ( will create Snippet in instructions )
Google Tag Manager or any other Tag Manager Code | Creation or Modification | This can either be a Snippet or added directly into your Layout

</div></b><!--EndFragment-->
</body>
</html>

**Instructions ( Option 2 )**
GTM / Tag Manager Installation or Modification
* Within the theme.liquid & checkout.liquid layout, place the GTM / Tag Manager container ( snippet or actual code block ) directly below the opening <body> tag.

Create the dataLayer-allPages Snippet ( use exact naming and casing! )
* Create a snippet called dataLayer-allPages and copy over the provided [dataLayer-allPages.js](https://github.com/TechnicalWebAnalytics/dataLayer-shopify/blob/master/dataLayer-allPages.js) in the newly created snippet. In the code, navigate to the “Dynamic Dependencies” section and make any necessary changes.

```/**********************```
```* DYNAMIC DEPENDENCIES```
```***********************/```
      
```__DL__ = {```
  ```dynamicCart: true,  // if cart is dynamic (meaning no refresh on cart add) set to true```
  ```debug: true, // if true, console messages will be displayed```
  ```cart: null,```
  ```wishlist: null,```
  ```removeCart: null```
```};```
      
```customBindings = {```
  ```cartTriggers: [],```
  ```viewCart: [],```
  ```removeCartTrigger: [],```
  ```cartVisableSelector: [],```
  ```promoSubscriptionsSelectors: [],```
  ```promoSuccess: [],```
  ```ctaSelectors: [],```
  ```newsletterSelectors: [],```
  ```newsletterSuccess: [],```
  ```searchPage: [],```
  ```wishlistSelector: [],```
  ```removeWishlist: [],```
  ```wishlistPage: [],```
  ```searchTermQuery: [getURLParams('q')], // replace var with correct query```
```};```

Add the code to the layouts

* Within the theme.liquid layout, place this include snippet {% include 'dataLayer-allPages' %} right before the closing </head> tag
* Within the checkout.liquid layout, place this include snippet {% include 'dataLayer-allPages' %} right before the closing </head> tag

Prerequisite Library
**These are already included in the dataLayer build.**
5.Review, Test, Done :)
