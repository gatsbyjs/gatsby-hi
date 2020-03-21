---
title: Data in Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

ट्यूटोरियल के भाग चार में आपका स्वागत है! हम आधे रास्ते तक पहुच चुके है! आशा है की अब आपको चीज़ें काफी आरामदायक लग रही होंगी 😀

## ट्यूटोरियल के पहले हाफ का रिकैप

अब तक, आप सीख रहे थे कि React.js का उपयोग कैसे करें - 
वेबसाइटों के लिए कस्टम बिल्डिंग ब्लॉक के रूप में कार्य करने के लिए अपने कस्टम कौम्पोनॅन्टस को बनाने में सक्षम होना कितना शक्तिशाली है।

आपने CSS मॉड्यूल का उपयोग करके कौम्पोनॅन्टस की स्टाइलिंग करने की जानकारी भी प्राप्त की है।

## इस ट्यूटोरियल में क्या है?

ट्यूटोरियल के अगले चार भागों (इस एक सहित) में, आप Gatsby डेटा लेयर के बारे में जानेंगे, जो कि Gatsby की एक शक्तिशाली विशेषता है, जो आपको Markdown, WordPress, headless CMSs और अन्य डेटा सोर्स से आसानी से सभी प्रकार की साइटें बनाने देता है।

**नोट:** Gatsby की डेटा लेयर GraphQL द्वारा संचालित है। 
GraphQL के बारे में और गहराई से जानने के लिए [How to GraphQL](https://www.howtographql.com/) देखें।

## Gatsby में डेटा

एक वेबसाइट के चार भाग हैं: HTML, CSS, JS और डेटा। ट्यूटोरियल के पहले आधे भाग पहले तीन पर केंद्रित थे। अब हम Gatsby साइटों में डेटा का उपयोग करना सीखेंगे।

**डेटा क्या है?**

एक बहुत ही कंप्यूटर विज्ञान-नी उत्तर होगा: डेटा जैसे `"strings"`,
integers (`42`), objects (`{ pizza: true }`) आदि चीजें हैं।

हालांकि, Gatsby में काम करने के उद्देश्य से, एक अधिक उपयोगी उत्तर है "सब कुछ जो एक React कौम्पोनॅन्ट के बाहर रहता है"।

अब तक, आप कौम्पोनॅन्ट में टेक्स्ट लिख रहे थे और _डायरेक्टली_ इमेजस ऐड कर रहे थे जो की अनेक वेबसाइट बनाने का एक _एक्सीलेंट_ तरीका है। लेकिन, अक्सर आप डेटा कौम्पोनॅन्ट के _बाहर_ स्टोर करना चाहते हैं और फिर जरूरत पड़ने पर डेटा कौम्पोनॅन्ट के _अंदर_ लाते है।

यदि आप WordPress (ताकि अन्य योगदानकर्ताओं के लिए कॉंटेंट ऐड करने और बनाए रखने के लिए एक अच्छा इंटरफ़ेस हो) और Gatsby के साथ एक साइट का निर्माण कर रहे हैं, साइट के लिए (पेजेज और पोस्ट) _डेटा_ WordPress में हैं और आप जरूरत पड़ने पर डेटा को कौम्पोनॅन्ट मे _पुल_ करते है।

डेटा, Markdown, CSV जैसी फाइलों के साथ-साथ डेटाबेस और सभी प्रकार के APIs में भी रह सकता है।

**Gatsby की डेटा लेयर आपको इन (और किसी भी अन्य सोर्स) से सीधे अपने कौम्पोनॅन्ट में डेटा पुल करने देती है** - जिस आकार और रूप में आप चाहते हैं।

## अंस्ट्रक्चर्ड डेटा बनाम GraphQL का उपयोग करना

### क्या मुझे Gatsby साइटों में डेटा पुल करने के लिए GraphQL और सोर्स प्लगइन्स का उपयोग करना होगा?

बिलकुल नहीं! आप GraphQL डेटा लेयर के बजाय सीधे Gatsby पेजेज में असंरचित डेटा को पुल करने के लिए नोड `createPages` API का उपयोग कर सकते हैं। यह छोटी साइटों के लिए एक बढ़िया विकल्प है, जबकि GraphQL और सोर्स प्लगइन्स अधिक जटिल साइटों के लिए समय बचाने में मदद कर सकते हैं।

अपने Gatsby साइट में नोड `createPages` API का उपयोग करके डेटा को कैसे पुल करे और एक उदाहरण साइट देखने के लिए, [बिना GraphQL के Gatsby का उपयोग करना](/docs/using-gatsby-without-graphql/) देखें!

### मैं GraphQL बनाम असंरचित डेटा का उपयोग कब करूं?

यदि आप एक छोटी साइट का निर्माण कर रहे हैं, तो इसे बनाने के लिए एक कुशल तरीका है कि इस गाइड में उल्लिखित असंरचित डेटा को पुल करते हुए `createPages` API का उपयोग करके, और यदि बाद में साइट अधिक जटिल हो जाती है, आप अधिक जटिल साइटें का निर्माण करना चाहते है, या आप अपना डेटा बदलना चाहते हैं तो, इन स्टेप्स का अनुसरण करें:

1. [प्लगइन लाइब्रेरी](/plugins/) देखें ताकि आप यह जान पाए की जिस सोर्स प्लगइन्स और/या ट्रांसफॉर्मर प्लगइन्स का आप उपयोग करना चाहते हैं वो पहले से ही मौजूद हैं या नहीं।
2. यदि वे मौजूद नहीं हैं, तो [प्लगइन ऑथरिंग](/docs/creating-plugins/) गाइड पढ़ें और अपना स्वयं का निर्माण करने पर विचार करें!

### कैसे Gatsby डेटा लेयर कौम्पोनॅन्टस में डेटा पुल करने के लिए GraphQL का उपयोग करता है

React कौम्पोनॅन्टस में डेटा लोड करने के लिए कई विकल्प हैं। इनमें से सबसे ज्यादा लोकप्रिय और शक्तिशाली एक तकनीक है जिसे [GraphQL](http://graphql.org/) कहा जाता है।

GraphQL का आविष्कार फेसबुक द्वारा प्रोडक्ट इंजीनियरों को कौम्पोनॅन्टस के अंदर डाटा _पुल_ करने मे मदद करने के लिए किया गया था। 

GraphQL एक **q**uery **l**anguage (इसके नाम का _QL_ हिस्सा) है। अगर आप SQL से परिचित हो तो, यह समान तरीके से काम करता है। एक विशेष सिंटॅक्स का उपयोग करते हुए, आप डेटा का वर्णन करते हैं जो आप अपने कौम्पोनॅन्टस में चाहते हैं और फिर वह डेटा आप को दिया जाता है।

Gatsby GraphQL का उपयोग करता है ताकि कौम्पोनॅन्टस मे आवश्यक डेटा घोषित करने में सक्षम हो।

## एक नई example साइट बनाएँ

ट्यूटोरियल के इस भाग के लिए एक और नई साइट बनाएँ। आप एक Markdown ब्लॉग बनाने जा रहे हैं जिसका नाम "Pandas Eating Lots" है। यह बहुत सारे भोजन खाने वाले पांडा के सर्वोत्तम चित्रों और वीडियो को दिखाने के लिए समर्पित है। रास्ते में, आप GraphQL और Gatsby के मार्कडाउन सपोर्ट भी सीखेंगे।

एक नई टर्मिनल विंडो खोलें और `tutorial-part-four` नामक एक फोल्डर में एक नई Gatsby साइट बनाने के लिए निम्न कमांड चलाएं। फिर बनाये गए नये फोल्डर पर जाएँ:

```shell
gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-four
```

फिर प्रॉजेक्ट की रूट में कुछ अन्य आवश्यक dependencies इनस्टॉल करें। आप टाइपोग्राफी थीम "Kirkham" का उपयोग करेंगे, और आप CSS-in-JS लाइब्रेरी ["Emotion"](https://emotion.sh/) आज़माएँगे:

```shell
npm install --save gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/core
```

[भाग तीन](/tutorial/part-three) में आपके द्वारा बनाई गई साइट के समान साइट बनाए। इस साइट में एक लेआउट कौम्पोनॅन्ट और दो पेज कौम्पोनॅन्टस होंगे:

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
import { Link } from "gatsby"

import { rhythm } from "../utils/typography"

export default ({ children }) => (
  <div
    css={css`
      margin: 0 auto;
      max-width: 700px;
      padding: ${rhythm(2)};
      padding-top: ${rhythm(1.5)};
    `}
  >
    <Link to={`/`}>
      <h3
        css={css`
          margin-bottom: ${rhythm(2)};
          display: inline-block;
          font-style: normal;
        `}
      >
        Pandas Eating Lots
      </h3>
    </Link>
    <Link
      to={`/about/`}
      css={css`
        float: right;
      `}
    >
      About
    </Link>
    {children}
  </div>
)
```

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>Amazing Pandas Eating Things</h1>
    <div>
      <img
        src="https://2.bp.blogspot.com/-BMP2l6Hwvp4/TiAxeGx4CTI/AAAAAAAAD_M/XlC_mY3SoEw/s1600/panda-group-eating-bamboo.jpg"
        alt="Group of pandas eating bamboo"
      />
    </div>
  </Layout>
)
```

```jsx:title=src/pages/about.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>About Pandas Eating Lots</h1>
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)
```

```javascript:title=src/utils/typography.js
import Typography from "typography"
import kirkhamTheme from "typography-theme-kirkham"

const typography = new Typography(kirkhamTheme)

export default typography
export const rhythm = typography.rhythm
```

`gatsby-config.js` (आपके प्रोजेक्ट के रूट में होना चाहिए, src में नहीं)

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

उपयुर्क्त फ़ाइलों को ऐड करें और फिर सामान्य रूप से `gatsby develop` को चलाएं, और आपको निम्नलिखित दिखेगा:

![start](start.png)

आपके पास एक और छोटी साइट है जिसमें एक लेआउट और दो पेजेज हैं।

अब आप quering करना शुरू कर सकते हैं 😋

## आपकी पहली GraphQL query

साइटों का निर्माण करते समय, आप संभवतः डेटा का पुन: उपयोग करना चाहेंगे - उदाहरण के लिए _साइट शीर्षक_। `/about/` पेज देखें। आप देखेंगे कि आपके पास साइट शीर्षक (`Pandas Eating Lots`) लेआउट कौम्पोनॅन्ट (साइट हेडर) के साथ-साथ `about.js` पेज (पेज हेडर) के `<h1/>` दोनों में है।

लेकिन अगर आप भविष्य में साइट का शीर्षक बदलना चाहते हैं तो? आपको अपने सभी कौम्पोनॅन्टस में शीर्षक की खोज करनी होगी और प्रत्येक इंस्टैंस में बदलाव करना होगा। यह बोझिल और एरर-प्रोन दोनों है, विशेष रूप से बड़े, अधिक जटिल साइटों के लिए। इसके बजाय, आप शीर्षक को एक स्थान पर स्टोर कर सकते हैं और उस स्थान को अन्य फ़ाइलों से रिफरेन्स कर सकते हैं; शीर्षक को एक ही स्थान पर बदलें, और Gatsby आपके अपडेटेड शीर्षक को फ़ाइलों में _पुल_ करेगा जो इसे रिफरेन्स करता है।

सामान्य डेटा के लिए जगह `gatsby-config.js` फ़ाइल में `siteMetadata` ऑब्जेक् है। `gatsby-config.js` फ़ाइल में अपनी साइट का शीर्षक ऐड करें:

```javascript:title=gatsby-config.js
module.exports = {
  // highlight-start
  siteMetadata: {
    title: `Title from siteMetadata`,
  },
  // highlight-end
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

डेवेलपमेंट सर्वर को रीस्टार्ट करें:

### पेज query का उपयोग करना

अब साइट शीर्षक query करने के लिए उपलब्ध है; [page query](/docs/page-query) का उपयोग करके इसे `about.js` फ़ाइल में ऐड करें:

```jsx:title=src/pages/about.js
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Layout from "../components/layout"

// highlight-next-line
export default ({ data }) => (
  <Layout>
    <h1>About {data.site.siteMetadata.title}</h1> {/* highlight-line */}
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)

// highlight-start
export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end
```

यह काम कर गया! 🎉

![पेज शीर्षक siteMetadata से पुल कर रहे हैं](site-metadata-title.png)

मूल GraphQL query जो आपके `शीर्षक` को `about.js` मे पुनर्प्राप्त करती है:

```graphql:title=src/pages/about.js
{
  site {
    siteMetadata {
      title
    }
  }
}
```

> 💡 [भाग पांच](/tutorial/part-five/#introducing-graphiql) में, आप एक टूल के बारे मे जानेगे, जो हमें GraphQL के माध्यम से उपलब्ध डेटा का इंटरेक्टिव रूप से पता लगाने देता है, और ऊपर दिए गए queries को तैयार करने में मदद करता है।

पेज queries कौम्पोनॅन्ट परिभाषा के बाहर रहते हैं -- कन्वेंशन हिसाब से पेज कौम्पोनॅन्ट फ़ाइल के अंत में -- और केवल पेज कौम्पोनॅन्टस पर उपलब्ध हैं।

### StaticQuery का उपयोग करना


[StaticQuery](/docs/static-query/) Gatsby v2 में शुरू किया गया एक नया API है जो नॉन-पेज कौम्पोनॅन्टस (जैसे आपके `layout.js` कौम्पोनॅन्ट) को GraphQL queries के माध्यम से डेटा को पुनः प्राप्त करने की अनुमति देता है। आइए इसमें शुरू किए गए नए [`useStaticQuery`](/docs/use-static-query/) hook version का उपयोग करें।

चलिए `src/components/layout.js` फ़ाइल में  `useStaticQuery` hook का उपयोग करते हुए कुछ परिवर्तन करें और `{data.site.siteMetadata.title}` का रिफरेन्स करे। जब यह पूरा हो जायेगा, तो आपकी फ़ाइल इस तरह दिखाई देगी:


```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
// highlight-next-line
import { useStaticQuery, Link, graphql } from "gatsby"

import { rhythm } from "../utils/typography"
// highlight-start
export default ({ children }) => {
  const data = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `
  )
  return (
    // highlight-end
    <div
      css={css`
        margin: 0 auto;
        max-width: 700px;
        padding: ${rhythm(2)};
        padding-top: ${rhythm(1.5)};
      `}
    >
      <Link to={`/`}>
        <h3
          css={css`
            margin-bottom: ${rhythm(2)};
            display: inline-block;
            font-style: normal;
          `}
        >
          {data.site.siteMetadata.title} {/* highlight-line */}
        </h3>
      </Link>
      <Link
        to={`/about/`}
        css={css`
          float: right;
        `}
      >
        About
      </Link>
      {children}
    </div>
    // highlight-start
  )
}
// highlight-end
```

एक और सफलता! 🎉

![पेज शीर्षक और लेआउट शीर्षक दोनों siteMetadata से पुल कर रहे हैं](site-metadata-two-titles.png)

यहां दो अलग-अलग queries का उपयोग क्यों करें? ये उदाहरण query टाइप्स के छोटे से परिचय के लिए थे, उन्हें कैसे फॉर्मेट किया जाता है, और कहाँ उनका उपयोग किया जा सकता है। अभी के लिए ध्यान रखें कि केवल पेज queries बना सकते हैं। नॉन-पेज कौम्पोनॅन्टस, जैसे कि लेआउट, StaticQuery का उपयोग कर सकते हैं। [भाग 7](/tutorial/part-seven/) ट्यूटोरियल मे इसकी गहराई से अधिक व्याख्या की गयी है।

लेकिन वास्तविक शीर्षक को रिस्टोर करते हैं।

Gatsby के मुख्य सिद्धांतों में से एक यह है कि _creators को तत्काल कनेक्शन की आवश्यकता होती है कि वे क्या बना रहे हैं_ ([hat tip to Bret Victor](http://blog.ezyang.com/2012/02/transcript-of-inventing-on-principle/))। दूसरे शब्दों में, जब आप कोड में कोई बदलाव करते हैं तो आपको तुरंत उस बदलाव का प्रभाव दिखना चाहिए। आप Gatsby के एक इनपुट में हेरफेर करते हैं और आपको स्क्रीन पर नया आउटपुट दिखता हैं।

लगभग हर जगह, आपके द्वारा किए गए परिवर्तन तुरंत प्रभावी होंगे। `gatsby-config.js` फ़ाइल को फिर से एडिट करें, इस बार `शीर्षक` को बदलकर "Pandas Eating Lots" कर दें। परिवर्तन आपके साइट पेजेज में बहुत तेज़ी से दिखना चाहिए।

![Both titles say Pandas Eating Lots](pandas-eating-lots-titles.png)

## आगे क्या आ रहा है?

अब, आप ट्यूटोरियल के [भाग पांच](tutorial/part-five) में Gatsby साइट में Graphql के साथ सोर्स प्लगइन् का उपयोग करके डेटा पुल करने के बारे में सीखेंगे।
