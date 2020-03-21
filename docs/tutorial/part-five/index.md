---
title: सोर्स प्लगइन्स
typora-copy-images-to: ./
disableTableOfContents: true
---

> यह ट्यूटोरियल Gatsby के डेटा लेयर के बारे में एक श्रंखला का हिस्सा है। यहां जारी रखने से पहले सुनिश्चित करें कि आप [भाग 4] (/tutorial/part-four/) से गुजर चुके हैं।

## इस ट्यूटोरियल में क्या है?

इस ट्यूटोरियल में, आप GraphQL और सोर्स प्लगइन्स का उपयोग करके अपने Gatsby साइट में डेटा को कैसे पुल करना सीख सकते हैं। इससे पहले कि आप इन प्लगइन्स के बारे में जानें, आप यह जानना चाहेंगे कि GraphQL नामक एक चीज़ का उपयोग कैसे किया जाए, जो कि आपके क्वेरीज़ को सही ढंग से बनाने में मदद करता है।

## GraphiQL से परिचय

GraphiQL, GraphQL एकीकृत डेवलपमेंट एनवीरोनमेंट (आईडीई) है। यह एक शक्तिशाली (और हर तरह से बहुत बढ़िया) टूल है जिसका उपयोग आप अक्सर Gatsby वेबसाइटों के निर्माण के दौरान करेंगे।

जब आपकी साइट का डेवलपमेंट सर्वर सामान्य रूप से चल रहा हो तो आप इसे यहाँ पर `http://localhost:8000/___graphql` एक्सेस कर सकते हैं।

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="/graphiql-explore.mp4"></source>
  <p>Your browser does not support the video element.</p>
</video>

`Site` के बिल्ट-इन "type" को खोजें और देखें कि उस पर कौन से फ़ील्ड उपलब्ध हैं - `siteMetadata` ऑब्जेक्ट के साथ जो आपने पहले क्वेरी किये थे। GraphiQL को खोल के और अपने डेटा के साथ खेल के देखें। ऑटोकम्पलीट विंडो लाने के लिए  <kbd>Ctrl + Space</kbd> को दबाएं (या <kbd>Shift + Space</kbd> का इस्तेमाल करें अल्टेरनाते कीबोर्ड शॉर्टकट के रूप में) और  <kbd>Ctrl + Enter</kbd> GraphQL क्वेरी रन  करने के लिए। बाकि के बचे हुए ट्यूटोरियल से बहुत अधिक GraphiQL का उपयोग करेंगे।

## GraphiQL एक्सप्लोरर का उपयोग करना

GraphiQL एक्सप्लोरर आपको इन क्वेरीज़ को हाथ से टाइप करने की दोहराव प्रक्रिया के बिना उपलब्ध फ़ील्ड और इनपुट के माध्यम से क्लिक करके इंटरएक्टिव तरीके से पूर्ण क्वेरी बनाने में सक्षम बनाता है।

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-build-a-graphql-query-using-gatsby-s-graphiql-explorer"
  lessonTitle="Build a GraphQL Query using Gatsby’s GraphiQL Explorer"
/>

## सोर्स प्लगइन्स

Gatsby साइटों में डेटा कहीं से भी आ सकता है: APIs, डेटाबेस, CMSs, लोकल फाइलें, आदि।

सोर्स प्लगइन्स अपने सोर्स से डेटा प्राप्त करते हैं। जैसे फाइल सिस्टम सोर्स प्लगइन फाइल सिस्टम से डेटा प्राप्त करना जानता है। Wordpess प्लगइन Wordpress API से डेटा प्राप्त करना जानता है।

[`Gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) ऐड करें और जानें कि यह कैसे काम करता है।

सबसे पहले, प्रोजेक्ट की रुट में प्लगइन इंस्टॉल करें:

```shell
npm install --save gatsby-source-filesystem
```

फिर इसे अपने `gatsby-config.js` में ऐड करें:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    // highlight-start
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    // highlight-end
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

सेव करें और gatsby डेवलपमेंट सर्वर को पुनरारंभ करें। इसके बाद फिर से GraphiQL को खोलें।

एक्सप्लोरर पैन में, आप `allFile` और` file` सलेक्शनस के रूप में उपलब्ध देखेंगे:

![graphiql-filesystem](graphiql-filesystem.png)

`AllFile` ड्रॉपडाउन पर क्लिक करें। क्वेरी क्षेत्र में `allFile` के बाद अपना कर्सर रखें, और फिर टाइप करें <kbd>Ctrl + Enter</kbd>। यह प्रत्येक फ़ाइल के `आईडी` के लिए एक क्वेरी भर देगा। क्वेरी चलाने के लिए "Play" दबाएं:

![filesystem-query](filesystem-query.png)

एक्सप्लोरर पैन में, `id` फ़ील्ड को ऑटोमेटिकली चुना गया है। फ़ील्ड के संबंधित चेकबॉक्स की जाँच करके अधिक फ़ील्ड के लिए चयन करें। नए फ़ील्ड के साथ क्वेरी चलाने के लिए "Play" दबाएं:

![filesystem-explorer-options](filesystem-explorer-options.png)

वैकल्पिक रूप से, आप ऑटोकम्पलीट शॉर्टकट (<kbd>Ctrl + Space</kbd>) का उपयोग करके फ़ील्ड जोड़ सकते हैं। यह `File` नोड्स पर क्वेरी करने योग्य फ़ील्ड दिखाएगा।

![filesystem-autocomplete](filesystem-autocomplete.png)

अपनी क्वेरी में कई फ़ील्ड जोड़ने का प्रयास करें, <kbd>Ctrl + Enter</kbd> दबाएं
हर बार क्वेरी को फिर से चलाने के लिए। आपको अपडेट किए गए क्वेरी परिणाम दिखाई देंगे:

![allfile-query](allfile-query.png)

इसका रिजल्ट 'File` "nodes" का एक ऐरे है (नोड एक "graph" में एक ऑब्जेक्ट के लिए एक फैंसी नाम है)। 
प्रत्येक 'File' नोड ऑब्जेक्ट में आपके द्वारा क्वेरीड किए गए फ़ील्ड हैं।

## एक GraphQL क्वेरी के साथ एक पेज बनाएँ

Gatsby के साथ नए पेजेज़ का निर्माण अक्सर GraphiQL में शुरू होता है। पहले अाप डेटा क्वेरी
की रूपरेखा Graphiql को इस्तेमाल करके के बना लें उसके बाद UI का निर्माण शुरू करने के लिए इसको
कॉपी करके React पेज के कौम्पोनॅन्ट में डालें।

चलो इसे टराइ करके देखते हैं।

`src/pages/my-files.js` पर एक नयी फाइल बनाएं `allFile` GraphQL क्वेरी के साथ जो आपने अभी
बनाई थी:

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data) // highlight-line
  return (
    <Layout>
      <div>Hello world</div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

`console.log(data)` लाइन ऊपर हाइलाइटेड है। एक नया कौम्पोनॅन्ट बनाने में
GraphQL क्वेरी से मिला हुआ डाटा कंसोल में आउटपुट करने में मददगार होता है
इससे अाप UI बनाते समय अपने ब्राउज़र कंसोल में डेटा को देख और समझ सकते हैं।

यदि आप `/my-files/` पर नए पेज पर जाते हैं और अपने ब्राउज़र कंसोल को खोलते हैं
तो अापको उसमें कुछ ऐसा दिखेगा:

![data-in-console](data-in-console.png)

डेटा का आकार GraphQL क्वेरी के आकार से मेल खाता है।

फ़ाइल डेटा को प्रिंट करने के लिए अपने कौम्पोनॅन्ट में कुछ कोड लिखें।


```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>My Site's Files</h1>
        <table>
          <thead>
            <tr>
              <th>relativePath</th>
              <th>prettySize</th>
              <th>extension</th>
              <th>birthTime</th>
            </tr>
          </thead>
          <tbody>
            {data.allFile.edges.map(({ node }, index) => (
              <tr key={index}>
                <td>{node.relativePath}</td>
                <td>{node.prettySize}</td>
                <td>{node.extension}</td>
                <td>{node.birthTime}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {/* highlight-end */}
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

और अब `http://localhost:8000/my-files`… पर जाएँ। 😲

![my-files-page](my-files-page.png)

## आगे क्या आ रहा है?

अब आप जान गए हैं कि सोर्स प्लगइन से डेटा _into_ Gatsby डेटा सिस्टम में कैसे लाते हैं। अगले ट्यूटोरियल में, आप सीखेंगे कि ट्रांसफॉर्मर प्लगइन्स सोर्स प्लगइन्स द्वारा लाया गया रौ डेटा कैसे _transform_ करता है। सोर्स प्लगइन्स और ट्रांसफ़ॉर्मर प्लगइन्स का संयोजन सभी डेटा सोर्सिंग और डेटा ट्रांसफ़ॉर्मेशन को हैंडल कर सकता है जो आपको एक Gatsby साइट के निर्माण के समय की आवश्यकता हो सकती है। [ट्यूटोरियल के छठे भाग](/tutorial/part-six/) में ट्रांसफॉर्मर प्लगइन्स के बारे में और जानें।
