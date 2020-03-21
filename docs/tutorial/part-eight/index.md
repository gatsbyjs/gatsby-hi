---
title: साइट को लाइव करने के लिए तैयार करना 
typora-copy-images-to: ./
disableTableOfContents: true
---

वाह! आप बहुत दूर आ चुके है! आपने सीख लिया है की कैसे:

- एक नया Gatsby साइट बनाया जाए
- पेजेज और कौम्पोनॅन्टस बनाया जाए
- कौम्पोनॅन्टस को स्टाइल किया जाए 
- साइट मे प्लगिन्स ऐड किया जाए 
- डाटा को सोर्स और ट्रांसफॉर्म किया जाए
- GraphQL द्वारा पेजेज के लिए डाटा को क्वेरी किया जाए 
- प्रोग्राम द्वारा अपने डाटा के लिए पेजेज बनाया जाए

इस आखरी भाग में, आप साइट को तैयार करने के लिए कुछ सामान्य चरणों से गुजरने जा रहे हैं, आपको एक शक्तिशाली साइट डायग्नोस्टिक टूल से इंट्रोड्यूस करवाया जायेगा जिसका नाम [Lighthouse](https://developers.google.com/web/tools/lighthouse/) है। रास्ते में हम आपको कुछ और प्लगिन्स के साथ परिचित करवाएंगे जिनका आप अपने Gatsby साइट में कई बार इस्तेमाल करना चाहेंगे।

## Lighthouse के साथ ऑडिट करना

[Lighthouse वेबसाइट](https://developers.google.com/web/tools/lighthouse/) से कोट करते हुए:

> Lighthouse एक ओपन-सोर्स, ऑटोमेटेड टूल है जो आपको वेब पेजेज की गुणवत्ता बढ़ाने मैं मदद करती है। आप इसे किसी भी वेब पेज, पब्लिक या रिक्वायर्ड ऑथेंटिकेशन पर चला सकते हैं। इसमें परफॉरमेंस, अक्सेसिब्लिटी, प्रोग्रेसिव वेब अप्प्सस (PWAs), आदि के लिए ऑडिट्स है।

Lighthouse, Chrome DevTools मे शामिल है। इसकी ऑडिट चलाना -- और फिर इसके द्वारा पहचाने हुए एररस को ठीक करना और इसके द्वारा सुझाये गए सुधार को लागू करना -- एक बहुत सटीक तरीका है आपके साइट को लाइव लेजाने की तैयारी करने में। यह आपको यह विश्वास दिलाने में मदद करता है कि आपकी साइट जितना संभव हो उतना तेज़ और सुलभ है।

इसको इस्तेमाल करके देखें!

सबसे पहले, आपको अपने Gatsby साइट के लिए एक प्रोडक्शन बिल्ड बनाना पड़ेगा। Gatsby डेवलपमेंट सर्वर को आपका डेवलपमेंट तेज़ बनाने के लिए अनुकूलित किया गया है; लेकिन जो साइट ये जेनरेट करता है, वो बारीकी से एक प्रोडक्शन वर्शन जैसा दिखता है, पर उतना ऑप्टीमाइज़्ड नहीं होता है।

### ✋ एक प्रोडक्शन बिल्ड बनाइये

1.  डेवलपमेंट सर्वर को रोक दीजिये (अगर वह अब भी चल रहा है) फिर यह कमांड्स चलाइये:

```shell
gatsby build
```

> 💡 जैसा की आपने [भाग १](/tutorial/part-one/) मे सीखा, यह आपके साइट का प्रोडक्शन बिल्ड करता है और `public` डायरेक्टरी के अंदर बिल्ड स्टैटिक फाइल्स को आउटपुट करता है।

2.  लोकल्ली प्रोडक्शन साइट को देखने के लिए, चलाइये:

```shell
gatsby serve
```

इसके शुरू होने के बाद, आप अपनी साइट `http://localhost:9000` पर देख सकते है।

### एक Ligthouse ऑडिट रन करना:

अब आप अपना पहला Lighthouse टेस्ट करेंगे।

1.  अगर आपने यह पहले ही नहीं कर लिया है तोह, साइट को Chrome Incognito Mode मे खोलिये ताकि कोई भी एक्सटेंशन टेस्ट मे दखल न दे। फिर, Chrome DevTools को खोलिये।

2.  "Audits" टैब पर क्लिक कीजिये जहाँ पर आपको एक स्क्रीन दिखाई देगा जो ऐसा दिखेगा:

![Lighthouse ऑडिट स्टार्ट](./lighthouse-audit.png)

3.  "Perform an audit..." पर क्लिक करें (सभी उपलब्ध ऑडिट प्रकारों को डिफ़ॉल्ट रूप से चुना गया होगा)। उसके बाद "Run audit" पर क्लिक करें। (उसके बाद इसे २ से ३ मिनट लगेंगे ऑडिट को चलाने में)। एक बार ऑडिट पूरा हो जाये, आपके परिणाम कुछ ऐसा दिखना चाहिए:

![Lighthouse ऑडिट परिणाम](./lighthouse-audit-results.png)

जैसा की आप देख सकते हैं, Gatsby का परफॉरमेंस आउट ऑफ़ दी बॉक्स बहुत अच्छा है, लेकिन इसमें आप PWA, एक्सेसिबिलिटी, बेस्ट प्रैक्टिसेज और SEO को मिस कर रहे होंगे जो स्कोर्स को अच्छा करता है (और इस प्रक्रिया में आपकी साइट विज़िटर्स और सर्च इंजनों के लिए बहुत अधिक फ्रेंडली बनाएंगे)।

## मैनिफेस्ट फाइल ऐड करना

लगता है "Progressive Web App" केटेगरी में आपका स्कोर बहुत मंदा है। आइये उसके बारे बात करें।

लेकिन पहले, PWAs _है_ क्या चीज़?

यह मामूली वेबसाइट्स है जो आधुनिक ब्राउज़र की कार्यक्षमता का फायदा उठाकर वेब अनुभव को अप्प-लाइक विशेषतायें एवं फायदों के साथ ऑग्मेंट करता है। [Google का अवलोकन](https://developers.google.com/web/progressive-web-apps/) को देखिये जो यह दिखाता है की एक सही PWA अनुभव को क्या परिभाषित करता है।

एक वेब ऐप मैनिफ़ेस्ट का शामिल होना आम तौर पर स्वीकृत तीन [PWA की आधारभूत आवश्यकताओं](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1) में से एक है।

[Google](https://developers.google.com/web/fundamentals/web-app-manifest/) का उद्धरण करते हुए:

> वेब अप्प मैनिफेस्ट एक सरल JSON फाइल है जो ब्राउज़र को आपके वेब एप्लीकेशन के बारे में बताता है और यह भी बताता है की उसका व्यवहार कैसा होना चाहिए जब वह यूजर के मोबाइल डिवाइस या डेस्कटॉप पर इन्सटाल्ड हो।

[Gatsby की मैनिफेस्ट प्लगइन](/packages/gatsby-plugin-manifest/) हर साइट बिल्ड में Gatsby को कॉन्फ़िगर करके एक `manifest.webmanifest` फाइल बनाती है।

### ✋ `gatsby-plugin-manifest` का इस्तेमाल

1.  प्लगइन तो इनस्टॉल कीजिये:

```shell
npm install --save gatsby-plugin-manifest
```

2. `src/images/icon.png` के नीचे अपने अप्प के लिए एक फ़ेविकॉन डाले। इस ट्यूटोरियल के खातिर आप [यह उदहारण आइकॉन](https://raw.githubusercontent.com/gatsbyjs/gatsby/master/docs/tutorial/part-eight/icon.png) का इस्तेमाल कर सकते है, अगर आपके पास एक नहीं है तोह। यह आइकॉन मैनिफेस्ट के लिए सारे इमेजेज बनाने के लिए ज़रूरी है। और जानकारी के लिए, यह डॉक्स देखिये [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md)।

3. इस प्लगइन को `gatsby-config.js` फाइल के `plugins` array में दाल दीजिये।

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
  ]
}
```

बस आपको इतना ही चाहिए वेब मैनिफेस्ट को Gatsby साइट में डालने की शुरुआत करने के लिए। दिया गया उदाहरण एक बेस कॉन्फ़िगरेशन को दर्शाता हैं -- और विकल्पों के लिए [प्लगइन रेफरेन्स](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) को देखें।

## ऑफलाइन सपोर्ट ऐड करना

एक वेबसाइट को PWA के रूप में अर्हता प्राप्त करने के लिए और एक आवश्यकता की ज़रूरत है, जो है [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) का इस्तेमाल। एक सर्विस वर्कर पृष्ठभूमि मे चलता है, और कनेक्टिविटी के आधार पर यह निश्चित करता है की वह नेटवर्क या कैश्ड कंटेंट की सेवा करे, जो निर्बाध, मैनेज्ड ऑफलाइन अनुभव की अनुमति देता है।

[Gatsby की ऑफलाइन प्लगइन](/packages/gatsby-plugin-offline/) एक साइट को ऑफलाइन काम करने में और एक सर्विस वर्कर बनाकर उसे खराब नेटवर्क के खिलाफ प्रतिरोधित करता है।

### ✋`gatsby-plugin-offline` का इस्तेमाल

1.  प्लगइन को इनस्टॉल कीजिये:

```shell
npm install --save gatsby-plugin-offline
```

2.  प्लगइन को `gatsby-config.js` फाइल के `plugins` ऐरे में ऐड कीजिये:
```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    // highlight-next-line
    `gatsby-plugin-offline`,
  ]
}
```

Gatsby के सर्विस वर्कर्स से शुरुआत करने के लिए बस इतना ही चाहिए।

> 💡 ऑफलाइन प्लगइन को मैनिफेस्ट प्लगइन के बाद अंकित किया जाना चाहिए ताकि ऑफलाइन प्लगइन बनाये गए `manifest.webmanifest` को cache कर पाए।

## पेज मेटाडाटा ऐड करना

पेजेज मे मेटाडाटा डालना (जैसे एक शीर्षक या विवरण) जिससे Google जैसे सर्च इंजिन्स को आपका कंटेंट समझने मे और यह सुनिश्चित करने मे की उसे सर्च रिजल्ट्स मे कब दिखाया जाये।

[React Helmet](https://github.com/nfl/react-helmet) एक पैकेज है जो आपको React कौम्पोनॅन्ट इंटरफ़ेस प्रदान करता है जो आपको अपने [document head](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head) को सँभालने मे मदद करता है।

Gatsby की [React Helmet प्लगइन](/packages/gatsby-plugin-react-helmet/) आपको React Helmet द्वारा ऐड की हुई ड्राप-इन सपोर्ट प्रदान करती है ताकि आप सर्वर डेटा रेंडरिंग कर सकें। इस प्लगइन का इस्तेमाल करके, जो एट्रिब्यूट आप React Helmet मे डालते है वह Gatsby बिल्ड द्वारा बनाये जाने वाले स्टैटिक पेजेज मे भी दाल दिया जाता है।

### ✋ `React Helmet` और `gatsby-plugin-react-helmet` का इस्तेमाल

1.  बूथ पैकेजेस इनस्टॉल करना:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2.  सुनिश्चित कीजिये की आपके `siteMetadata` ऑब्जेक्ट के अंदर एक `description` और एक `author` कॉन्फ़िगर कर दिया गया है। साथ ही, आपके `gatsby-config.js` फाइल के अंदर `gatsby-plugin-react-helmet` प्लगइन को `plugins` ऐरे के अंदर ऐड कीजिये।

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
    // highlight-start
    description: `A simple description about pandas eating lots...`,
    author: `gatsbyjs`,
    // highlight-end
  },
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    `gatsby-plugin-offline`,
    // highlight-next-line
    `gatsby-plugin-react-helmet`,
  ],
}
```

3. `src/components` डायरेक्टरी के अंदर, `seo.js` नामक फाइल क्रिएट कीजिये और उसमे निचे दिया गया कोड डालिये:

```jsx:title=src/components/seo.js
import React from "react"
import PropTypes from "prop-types"
import Helmet from "react-helmet"
import { useStaticQuery, graphql } from "gatsby"

function SEO({ description, lang, meta, title }) {
  const { site } = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
            description
            author
          }
        }
      }
    `
  )

  const metaDescription = description || site.siteMetadata.description

  return (
    <Helmet
      htmlAttributes={{
        lang,
      }}
      title={title}
      titleTemplate={`%s | ${site.siteMetadata.title}`}
      meta={[
        {
          name: `description`,
          content: metaDescription,
        },
        {
          property: `og:title`,
          content: title,
        },
        {
          property: `og:description`,
          content: metaDescription,
        },
        {
          property: `og:type`,
          content: `website`,
        },
        {
          name: `twitter:card`,
          content: `summary`,
        },
        {
          name: `twitter:creator`,
          content: site.siteMetadata.author,
        },
        {
          name: `twitter:title`,
          content: title,
        },
        {
          name: `twitter:description`,
          content: metaDescription,
        },
      ].concat(meta)}
    />
  )
}

SEO.defaultProps = {
  lang: `en`,
  meta: [],
  description: ``,
}

SEO.propTypes = {
  description: PropTypes.string,
  lang: PropTypes.string,
  meta: PropTypes.arrayOf(PropTypes.object),
  title: PropTypes.string.isRequired,
}

export default SEO
```

उपयुर्क्त कोड आपके सबसे आम मेटाडाटा टैग्स के लिए डिफॉल्ट्स सेट अप करता है और आपको एक `<SEO>` कौम्पोनॅन्ट प्रदान करता है जो आपको बचे हुए प्रोजेक्ट मे काम करने मे मदद करेगी। बहुत अच्छा, हैना?

4.  अब, आप अपने टेम्पलेट्स और पेजेज मैं `<SEO>` कौम्पोनॅन्ट यूस कर सकते है और उसमे props पास कर सकते है। उदाहरण के लिए, अपने `blog-post.js` टेम्पलेट मे ऐड कीजिये इस तरह से:

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"
// highlight-next-line
import SEO from "../components/seo"

export default ({ data }) => {
  const post = data.markdownRemark
  return (
    <Layout>
      // highlight-start
      <SEO title={post.frontmatter.title} description={post.excerpt} />
      // highlight-end
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </Layout>
  )
}

export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
      // highlight-next-line
      excerpt
    }
  }
`
```

उपयुर्क्त उदहारण [Gatsby स्टार्टर ब्लॉग](/starters/gatsbyjs/gatsby-starter-blog/) पर आधारित है। अगर आप `<SEO>` कौम्पोनॅन्ट मे props पास करते है, तो आप डाईनामिकली एक पोस्ट की मेटाडाट को बदल सकते हैं। इस मामले में, `gatsby-config.js` फाइल मे डिफ़ॉल्ट `siteMetadata` प्रॉपर्टी के बदले ब्लॉग पोस्ट के `title` और `excerpt` का इस्तेमाल किया जायेगा (अगर वह ब्लॉग पोस्ट के अंदर मौजूद है तोह)।

अब, अगर आप उपयुर्क्त तरीके से Lighthouse ऑडिट को फिर से चलाते है, तो आपको 100 स्कोर या 100 स्कोर के बेहद करीब मिलेंगे!

> 💡 आगे पढ़ने के लिए और उदाहरणों के लिए, [SEO कौम्पोनॅन्ट ऐड करना](/docs/add-seo-component/) और [React Helmet डॉक्स](https://github.com/nfl/react-helmet#example) को देखिये!

## इसको बेहतर बनाते जाइये

इस भाग मे, हमने आपको कुछ Gatsby-स्पेसिफिक टूल्स दिखाए जो आपकी साइट की प्रदर्शन को बढ़ाता है और आपकी साइट को लाइव लेजाने मे आपकी मदद करता है। 

साइट मे सुधार लाने के लिए और सीखने के लिए Lighthouse एक बहुत उपयोगी साधन है -- इसमें बताये गए विस्तृत प्रतिक्रिया को देखना जारी रखिये और अपने साइट को बेहतर बनाते जाइये!

## अगले कदम

### आधिकारिक डॉक्यूमेंटेशन

- [आधिकारिक डॉक्यूमेंटेशन](https://www.gatsbyjs.org/docs/): हमारे आधिकारिक डॉक्यूमेंटेशन को देखिये _[जल्द शुरुआत](https://www.gatsbyjs.org/docs/quick-start/)_, _[विस्तृत गाइड्स](https://www.gatsbyjs.org/docs/preparing-your-environment/)_, _[API संधर्बे](https://www.gatsbyjs.org/docs/gatsby-link/)_, और बहुत कुछ।

### आधिकारिक प्लगिन्स

- [आधिकारिक प्लगिन्स](https://github.com/gatsbyjs/gatsby/tree/master/packages): Gatsby द्वारा मेन्टेन किये हुए सारे आधिकारिक प्लगिन्स की पूरी सूचि।

### आधिकारिक स्टार्टर्स

1.  [Gatsby का डिफ़ॉल्ट स्टार्टर](https://github.com/gatsbyjs/gatsby-starter-default): इस बॉयलरप्लेट के साथ अपने प्रोजेक्ट की शुरुआत कीजिये।
यह बैरबोनस स्टार्टर, Gatsby के मुख्य कॉन्फ़िगरेशन फाइल्स के साथ शिप किया जाता है जिसकी आपको ज़रूरत पड़ सकती है। _[काम करता हुआ उदाहरण](http://gatsbyjs.github.io/gatsby-starter-default/)_
2.  [Gatsby का ब्लॉग स्टार्टर](https://github.com/gatsbyjs/gatsby-starter-blog): मस्त और अधिक तेज़ ब्लॉग बनाने के लिए Gatsby का स्टार्टर। _[चलता हुआ उदाहरण](http://gatsbyjs.github.io/gatsby-starter-blog/)_
3.  [Gatsby का हेलो वर्ल्ड स्टार्टर](https://github.com/gatsbyjs/gatsby-starter-hello-world): Gatsby साइट बनाने के लिए अधिकतम काम ज़रूरतों वाला Gatsby का स्टार्टर।_[चलता हुआ उदाहरण](https://gatsby-starter-hello-world-demo.netlify.com/)_

## बस इतना ही, दोस्तों 

लेकिन बस इस ही टुटोरिअल के लिए। और भी गाइडेड यूस केसेस देखने के लिए [अतिरिक्त ट्यूटोरियल](/tutorial/additional-tutorials/) को देखिये।

यह तो बस शुरुआत है। बढ़ते जाइये!

- क्या आपने कुछ मस्त बनाया है? Twitter पर शेयर कीजिये, टैग [#buildwithgatsby](https://twitter.com/search?q=%23buildwithgatsby), और [@mention us](https://twitter.com/gatsbyjs) के साथ!
- क्या आपने जो सीखा उसके बारे में एक मस्त ब्लॉग पोस्ट लिखा है? उसको भी शेयर कीजिये!
- सहयोग दीजिये! Gatsby रेपो पर यह देखिये [खुले हुए मुद्दे](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) और [सहयोगी बनिए](/contributing/how-to-contribute/)।

और भी आइडियाज के लिए ["सहयोग कैसे दे"](/contributing/how-to-contribute/) देखिये।

हम बेताब है यह देखने के लिए की आप क्या करने वाले है 😄।
