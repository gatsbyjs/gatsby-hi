---
title: Transformer plugins
typora-copy-images-to: ./
disableTableOfContents: true
---

> This tutorial is part of a series about Gatsby’s data layer. Make sure you’ve gone through [part 4](/tutorial/part-four/) and [part 5](/tutorial/part-five/) before continuing here.

## इस ट्यूटोरियल में क्या है?

पिछले ट्यूटोरियल मे आपने सीखा कि कैसे सोर्स प्लगइन डेटा को Gatsby के डेटा सिस्टम मे लाता हैं। इस ट्यूटोरियल में, आप सीखेंगे कि कैसे ट्रांसफॉर्मर प्लगइन्स अनिर्मित कॉंटेंट को सोर्स प्लगइन्स द्वारा बदलता है। सोर्स प्लगइन्स और ट्रांसफ़ॉर्मर प्लगइन्स का संयोजन सभी डेटा सोर्सिंग और डेटा ट्रांसफ़ॉर्मेशन को हैंडल कर सकता है, जो आपको Gatsby साइट बनाते समय चाहिए।

## ट्रांसफॉर्मर प्लगइन्स

अक्सर, सोर्स प्लगइन्स से प्राप्त डेटा का फार्मेट वह नहीं होता है जो आप अपनी वेबसाइट बनाने के लिए चाहते हैं। फ़ाइल सिस्टम सोर्स प्लगइन आपके फाइल्स को query करने देता है लेकिन क्या होगा यदि आप फ़ाइलों के अंदर query करना चाहते हैं?

इसे संभव बनाने के लिए Gatsby ट्रांसफार्मर प्लगइन्स का समर्थन करता है जो सोर्स प्लगइन्स से raw कॉंटेंट को अधिक उपयोगी मे बदल देता है।

उदाहरण के लिए मार्कडाउन फाइलें। मार्कडाउन लिखना अच्छा है, लेकिन जब आप पेज का निर्माण करते हैं, आप चाहेंगे की मार्कडाउन Html मे परिवर्तित हो जाए।

अपनी साइट पर एक मार्कडाउन फ़ाइल 
`src/pages/sweet-pandas-eating-sweets.md` ऐड करें (यह आपका पहला मार्कडाउन ब्लॉग पोस्ट बन जाएगा) और जानें कि कैसे ट्रांसफॉर्मर प्लगइन्स और Graphql का उपयोग करके HTML को _परिवर्तित_ किया जाता है।

```markdown:title=src/pages/sweet-pandas-eating-sweets.md
---
title: "Sweet Pandas Eating Sweets"
date: "2017-08-10"
---

Pandas are really sweet.

Here's a video of a panda eating sweets.

<iframe width="560" height="315" src="https://www.youtube.com/embed/4n0xNbfJLR8" frameborder="0" allowfullscreen></iframe>
```

फ़ाइल को सेव करने के बाद `/my-files/` को फिर से देखें - नई मार्कडाउन फ़ाइल टेबल के अंदर है। यह Gatsby की एक बहुत शक्तिशाली विशेषता है। पहले की तरह
`siteMetadata` उदाहरण, सोर्स प्लगइन्स डेटा को पुनः लोड कर सकते हैं।
`gatsby-source-filesystem` हमेशा नई फ़ाइलों को स्कैन करता रहता है और जब नयी फाइल्स ऐड हो जाती है, वे आपके queries को फिर से रन करता हैं।

एक ट्रांसफॉर्मर प्लगइन ऐड करें जो मार्कडाउन फ़ाइलों को बदल सकता है:

```shell
npm install --save gatsby-transformer-remark
```

फिर इसे सामान्य की तरह `gatsby-config.js` में ऐड करें:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-transformer-remark`, // highlight-line
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

डेवेलपमेंट सर्वर को रीस्टार्ट करें, फिर GraphiQL को रेफ्रेश (या फिर से खोलें) करें और ऑटो-कंप्लीट को देखे:

![markdown-autocomplete](markdown-autocomplete.png)

`allMarkdownRemark` को फिर से सेलेक्ट करे और इसे रन करे जैसा आपने` allFile` के लिए रन किया था। आप हाल ही में आपके द्वारा ऐड किए गए मार्कडाउन फ़ाइल को देखेंगे। अब फीलड्स की छान-बीन करें जो `MarkdownRemark` नोड पर उपलब्ध है।

![markdown-query](markdown-query.png)

ठीक है! उम्मीद है, कुछ बेसिक बातें अब समझ मे आने लगी होंगी। सोर्स प्लगइन्स डेटा को Gatsby डेटा सिस्टम मे लाते हैं और _transformer_ प्लगइन्स raw कॉंटेंट को स्रोत प्लगइन्स द्वारा _परिवर्तित_ करते हैं। यह पैटर्न सभी डेटा सोर्सिंग और डेटा परिवर्तन को संभाल सकता है, एक Gatsby साइट का निर्माण करते समय आपको आवश्यकता हो सकती है।

## `src/pages/index.js` में अपनी साइट की मार्कडाउन फ़ाइलों की सूची बनाएँ

अब आपको फ्रंट पेज पर अपनी मार्कडाउन फाइलों की एक सूची बनानी होगी। अन्य के जैसे
ब्लॉग, आप प्रत्येक ब्लॉग पोस्टको इंगित करने वाले फ्रंट पेज पर लिंक की एक सूची के साथ समाप्त करना चाहते हैं। GraphQL से आप मार्कडाउन ब्लॉग पोस्ट की वर्तमान सूची के लिए _query_ कर सकते हैं इसलिए आपको मैन्युअल रूप से सूची बनाए रखने की आवश्यकता नहीं होगी।

जैसे `src/pages/my-files.js` पेज के साथ, `src/pages/index.js` को 
कुछ प्रारंभिक HTML और स्टाइलिंग के साथ Graphql query ऐड करने के लिए निम्नलिखित मे बदलें।

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import { css } from "@emotion/core"
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Amazing Pandas Eating Things
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
            <h3
              css={css`
                margin-bottom: ${rhythm(1 / 4)};
              `}
            >
              {node.frontmatter.title}{" "}
              <span
                css={css`
                  color: #bbb;
                `}
              >
                — {node.frontmatter.date}
              </span>
            </h3>
            <p>{node.excerpt}</p>
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

अब फ्रंट पेज कुछ इस तरह दिखना चाहिए:

![frontpage](frontpage.png)

लेकिन आपका ब्लॉग पोस्ट थोड़ा अकेला लग रहा है। तो चलिए एक और 
`src/pages/pandas-and-bananas.md` ऐड करते हैं

```markdown:title=src/pages/pandas-and-bananas.md
---
title: "Pandas and Bananas"
date: "2017-08-21"
---

Do Pandas eat bananas? Check out this short video that shows that yes! pandas do
seem to really enjoy bananas!

<iframe width="560" height="315" src="https://www.youtube.com/embed/4SZl1r2O_bY" frameborder="0" allowfullscreen></iframe>
```

![two-posts](two-posts.png)

अब बहुत अच्छा लग रहा है! सिवाय ... पोस्ट का क्रम गलत है।

लेकिन इसे ठीक करना बहुत ही आसान है। किसी प्रकार के कनेक्शन की query करते समय, आप GraphQL query को विभिन्न प्रकार के arguments पास कर सकते हैं। आप नोड को `sort` और `filter` कर सकते हैं, सेट करें कितने नोड्स को `skip` करना है, और कितने नोड्स को पुनः प्राप्त करने की` limit` भी सेलेक्ट कर सकते है। साथ में ऑपरेटरों का यह शक्तिशाली सेट, आप अपने इच्छित किसी भी डेटा का चयन कर सकते हैं जिस भी फॉर्मॅट मे आपको चाहिए।

अपने इंडेक्स पेज की GraphQL query में, `allMarkdownREDIA` को `allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC })` मे बदलें। _Note: `frontmatter` और `date` के बीच ३ अंडरस्कोर हैं। इसे सेव करे और sort का क्रम ठीक हो जाना चाहिए।

GraphiQL को खोले और विभिन्न प्रकार के विकल्पों के साथ खेलने का प्रयास करें। आप अन्य कनेक्शन के साथ `allFile` कनेक्शन को sort कर सकते हैं।

हमारे query ऑपरेटरों पर और अधिक डॉक्युमेंटेशन के लिए, हमारे [GraphQL संदर्भ गाइड](/docs/graphql-reference/) को देखे

## चुनौती

एक नया पोस्ट बनाने का प्रयास करें जिसमें ब्लॉग पोस्ट हो और देखें कि होमपेज पर ब्लॉग पोस्ट की सूची में क्या होता है!

## आगे क्या आ रहा है?

यह भी खूब रही! आपने अभी एक अच्छा इंडेक्स पेज बनाया है जहाँ आप अपने मार्कडाउन फाइल्स को query कर रहे हैं और ब्लॉग पोस्ट शीर्षक और अंश की एक सूची का निर्माण कर रहे है। लेकिन आप केवल अंश नहीं देखना चाहते हैं, आप अपनी मार्कडाउन फ़ाइलों के लिए वास्तविक पेज बनाना चाहते हैं।

आप `src/pages` में React कौम्पोनॅन्टस को रखकर पेज बनाना जारी रख सकते हैं। हालाँकि, आगे आप सीखेंगे कि _programmatically_ _डेटा_ से पेजेज कैसे बनाएं। Gatsby सिर्फ़ static साइट जनरेटर, जैसे फ़ाइलों से पेज बनाने तक सीमित नही है। Gatsby GraphQL का उपयोग करके डेटा को query करने देता है और बिल्ड टाइम मे query रिज़ल्ट्स को पेजेज मे परिवर्तित कर देता है। यह वास्तव में शक्तिशाली विचार है। अगले ट्यूटोरियल में इसका उपयोग करने के तरीके सीखेंगे [डेटा से programmatically पेजेज बनाना](/tutorial/part-seven/)।