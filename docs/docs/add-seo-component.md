---
title: "Adding an SEO Component"
---

वेब पर प्रत्येक साइट में उनके '<head>' तत्व में पृष्ठ का मूल शीर्षक, फेविकॉन या विवरण जैसे बुनियादी _meta-tags_ हैं। यह जानकारी ब्राउज़र में प्रदर्शित हो जाती है और इसका उपयोग तब किया जाता है जब कोई आपकी वेबसाइट को साझा करता है, उदा। ट्विटर पे। आप अपने उपयोगकर्ताओं और इन वेबसाइटों को अपनी वेबसाइट को अधिक डेटा के साथ एम्बेड करने के लिए अतिरिक्त डेटा दे सकते हैं - और यही वह स्थान है जहां एक एसईओ घटक के लिए यह गाइड आता है। अंत में आपके पास एक घटक होगा जो आप अपने लेआउट फ़ाइल में रख सकते हैं और समृद्ध पूर्वावलोकन कर सकते हैं। अन्य ग्राहकों, स्मार्टफोन उपयोगकर्ताओं और खोज इंजन के लिए।

_Note: यह घटक StaticQuery का उपयोग करेगा। यदि आप इससे अपरिचित हैं, तो [StaticQuery प्रलेखन] (/ डॉक्स / स्टैटिक-क्वेरी /) पर एक नज़र डालें। आपके पास `रिएक्शन-हेलमेट` भी होना चाहिए जिसके लिए आप [इस दस्तावेज़] (/ डॉक्स / ऐड-पेज-मेटाडेटा) पर एक नज़र डाल सकते हैं ।_

## gatsby-config.js

Gatsby सभी डेटा को आपके `gatsby-config` फ़ाइल के` siteMetadata` अनुभाग में ग्राफिंक में स्वचालित रूप से उपलब्ध कराता है और इसलिए यह आपकी जानकारी को वहाँ के घटक के लिए रखने का एक अच्छा विचार है।

```js:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: "Severus Snape",
    titleTemplate: "%s · The Real Hero",
    description:
      "Hogwarts Potions master, Head of Slytherin house and former Death Eater.",
    url: "https://www.doe.com", // No trailing slash allowed!
    image: "/images/snape.jpg", // Path to your image you placed in the 'static' folder
    twitterUsername: "@occlumency",
  },
}
```

## SEO अंग

इस प्रारंभिक बायलरप्लेट के साथ एक नया घटक बनाएँ:

```jsx:title=src/components/SEO.js
import React from "react"
import { Helmet } from "react-helmet"
import PropTypes from "prop-types"
import { StaticQuery, graphql } from "gatsby"

const SEO = ({ title, description, image, pathname, article }) => ()

export default SEO

SEO.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string,
  image: PropTypes.string,
  pathname: PropTypes.string,
  article: PropTypes.bool,
}

SEO.defaultProps = {
  title: null,
  description: null,
  image: null,
  pathname: null,
  article: false,
}
```

** ध्यान दें: ** `प्रोपटीपेस` इस ​​उदाहरण में शामिल हैं, जिससे आपको यह सुनिश्चित करने में मदद मिलेगी कि आपको घटक में आवश्यक सभी डेटा मिल रहे हैं, और उन प्रॉप्स को नष्ट / उपयोग करते समय एक गाइड के रूप में सेवा करने में मदद मिलेगी।

जैसा कि SEO घटक अन्य फ़ाइलों में भी प्रयोग करने योग्य होना चाहिए, उदा। एक टेम्प्लेट फ़ाइल, घटक उन गुणों को भी स्वीकार करता है जिनके लिए आप `SEO.defaultProps` अनुभाग में समझदार चूक सेट करते हैं। इस तरह से आप `siteMetadata` में दी गई जानकारी को हर बार उपयोग करते हैं जब तक कि आप स्पष्ट रूप से संपत्ति को परिभाषित नहीं करते हैं।
Now define the query and place it in the StaticQuery (you can also save the query in a constant). You can also alias query items, so `title` gets renamed to `defaultTitle`.

```jsx:title=src/components/SEO.js
const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery query={query} render={} />
)

export default SEO

const query = graphql`
  query SEO {
    site {
      siteMetadata {
        defaultTitle: title
        titleTemplate
        defaultDescription: description
        siteUrl: url
        defaultImage: image
        twitterUsername
      }
    }
  }
`
```

अगला कदम क्वेरी से डेटा को नष्ट करना है और एक ऑब्जेक्ट बनाना है जो यह जांचता है कि क्या प्रॉप्स का उपयोग किया गया था - यदि डिफ़ॉल्ट मानों का उपयोग नहीं किया गया है। अलियासिंग नाम यहाँ काम आता है: यह नाम टकराव से बचा जाता है।

```jsx:title=src/components/SEO.js
const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery
    query={query}
    render={({
      site: {
        siteMetadata: {
          defaultTitle,
          titleTemplate,
          defaultDescription,
          siteUrl,
          defaultImage,
          twitterUsername,
        }
      }
    }) => {
      const seo = {
        title: title || defaultTitle,
        description: description || defaultDescription,
        image: `${siteUrl}${image || defaultImage}`,
        url: `${siteUrl}${pathname || '/'}`,
      }

      return ()
    }}
  />
)

export default SEO
```

अंतिम चरण `हेलमेट` की मदद से इस डेटा को वापस करना है। आपका पूरा एसईओ घटक जैसा दिखना चाहिए:

```jsx:title=src/components/SEO.js
import React from "react"
import { Helmet } from "react-helmet"
import PropTypes from "prop-types"
import { StaticQuery, graphql } from "gatsby"

const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery
    query={query}
    render={({
      site: {
        siteMetadata: {
          defaultTitle,
          titleTemplate,
          defaultDescription,
          siteUrl,
          defaultImage,
          twitterUsername,
        },
      },
    }) => {
      const seo = {
        title: title || defaultTitle,
        description: description || defaultDescription,
        image: `${siteUrl}${image || defaultImage}`,
        url: `${siteUrl}${pathname || "/"}`,
      }

      return (
        <>
          <Helmet title={seo.title} titleTemplate={titleTemplate}>
            <meta name="description" content={seo.description} />
            <meta name="image" content={seo.image} />
            {seo.url && <meta property="og:url" content={seo.url} />}
            {(article ? true : null) && (
              <meta property="og:type" content="article" />
            )}
            {seo.title && <meta property="og:title" content={seo.title} />}
            {seo.description && (
              <meta property="og:description" content={seo.description} />
            )}
            {seo.image && <meta property="og:image" content={seo.image} />}
            <meta name="twitter:card" content="summary_large_image" />
            {twitterUsername && (
              <meta name="twitter:creator" content={twitterUsername} />
            )}
            {seo.title && <meta name="twitter:title" content={seo.title} />}
            {seo.description && (
              <meta name="twitter:description" content={seo.description} />
            )}
            {seo.image && <meta name="twitter:image" content={seo.image} />}
          </Helmet>
        </>
      )
    }}
  />
)

export default SEO

SEO.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string,
  image: PropTypes.string,
  pathname: PropTypes.string,
  article: PropTypes.bool,
}

SEO.defaultProps = {
  title: null,
  description: null,
  image: null,
  pathname: null,
  article: false,
}

const query = graphql`
  query SEO {
    site {
      siteMetadata {
        defaultTitle: title
        titleTemplate
        defaultDescription: description
        siteUrl: url
        defaultImage: image
        twitterUsername
      }
    }
  }
`
```

## उदाहरण

आप फेसबुक और ट्विटर मेटा-टैग को अपने घटकों में भी डाल सकते हैं, अपने पसंदीदा स्टैविक फोन्स को अपने `स्थिर` फ़ोल्डर में जोड़ सकते हैं, और [schema.org] (https://schema.org/) डेटा (Google का उपयोग करेंगे) उनके [संरचित डेटा] (https://developers.google.com/search/docs/guides/intro-structured-data)) के लिए। यह देखने के लिए कि कैसे काम करता है आप इन दो उदाहरणों पर एक नज़र डाल सकते हैं:

- [marisamorby.com](https://github.com/marisamorby/marisamorby.com/blob/master/packages/gatsby-theme-blog-sanity/src/components/seo.js)
- [gatsby-starter-prismic](https://github.com/LeKoArts/gatsby-starter-prismic/blob/master/src/components/SEO/SEO.jsx)

जैसा कि शुरुआत में बताया गया है कि आप टेम्प्लेट में घटक का उपयोग करने में सक्षम हैं, जैसे कि [this example](https://github.com/jlengstorf/marisamorby.com/blob/6e86f845185f9650ff95316d3475bb8ac86b15bf/src/templates/post.js#L12-L18).
