---
शीर्षक: प्रोग्रामेटिक रूप से डेटा से पेज बनाना
typora-copy-images-to: ./
disableTableOfContents: true
---

> यह ट्यूटोरियल Gatsby के डेटा लेयर के बारे में एक श्रंखला का हिस्सा है। आगे बढ़ने से पहले सुनिश्चित करें कि आप इससे पहले [भाग 4](/tutorial/part-four/), [भाग 5](/tutorial/part-five/), और [भाग 6](/tutorial/part-six/) पढ़ चुके है।

## इस ट्यूटोरियल में क्या है?

पिछले ट्यूटोरियल में, आपने एक अच्छा इंडेक्स पेज बनाया था, जो मार्कडाउन फाइल्स को क्वेरी करता है
और ब्लॉग पोस्ट शीर्षक और अंशों की एक सूची तैयार करता है। लेकिन आप केवल अंश नहीं देखना चाहते हैं,आप मार्कडाउन फाइलें के लिए वास्तविक पेजेज़ चाहते हैं।

आप `src/pages` में React कौम्पोनॅन्टस को रखकर पेज बनाना जारी रख सकते हैं। हालाँकि, अब आप _प्रोग्रामेटिक_ रूप से _डेटा_ से पेज बनाना सीखेंगे। Gatsby स्टॅटिक साइट जनरेटर की तरह सिर्फ़ फ़ाइलों से पेजेज़ बनाने तक सीमित नही है। Gatsby GraphQL की मदद से _डेटा_ को क्वेरी करने देता है और बिल्ड टाइम मे क्वेरी रिज़ल्ट्स को पेजेज़ मे परिवर्तित कर देता है। यह वास्तव में शक्तिशाली विचार है। आप ट्यूटोरियल के इस भाग मे इसका उपयोग करने के तरीके सीखेंगे।

चलिए शुरू करें।

## पेजेज़ के लिए slugs का निर्माण करना

नए पेजेज़ बनाने के दो चरण हैं:

1.  पेज के लिए "path" या "slug" जेनरेट करें।
2.  पेज बनाएं।

_**नोट**: अक्सर डेटा सोर्स सीधे कॉंटेंट के लिए एक slug या pathname प्रदान करते है - जब उन सिस्टमों में से एक के साथ काम करते समय (जैसे कि एक CMS), आपको खुद से slugs बनाने की आवश्यकता नहीं है जैसा की आप मार्कडाउन फाइल के साथ करते हैं।_

अपने मार्कडाउन पेज बनाने के लिए, आप दो Gatsby API का उपयोग करना सीखेंगे:
[`onCreateNode`](/docs/node-apis/#onCreateNode) और
[`createPages`](/docs/node-apis/#createPages)। 
ये दो वर्कहॉर्स APIs, आप कई साइटों और प्लगइन्स में उपयोग होते देखेंगे।

हम Gatsby API को सरल तरीके से इंप्लिमेंट करने की पूरी कोशिश करते हैं। एक API को इंप्लिमेंट करने के लिए, आप एक फ़ंक्शन नाम के साथ `gatsby-node.js` मे एक्सपोर्ट करते हैं 

यहाँ आप ऐसा करेंगे। अपनी साइट की रूट में, `gatsby-node.js` नाम की एक फ़ाइल बनाएँ। फिर निम्नलिखित ऐड करें।

```javascript:title=gatsby-node.js
exports.onCreateNode = ({ node }) => {
  console.log(node.internal.type)
}
```

जब भी एक नया नोड बनाया (या अपडेट) किया जाता है, तो यह `onCreateNode` फ़ंक्शन Gatsby द्वारा कॉल किया जाता है।

डेवेलपमेंट सर्वर को स्टॉप करें और फिर स्टार्ट करें। जैसा कि आप करते हैं, आप कुछ नये 
निर्मित नोड्स टर्मिनल कंसोल में लॉग होते देखेंगे।

अगले भाग में, आप इस API का उपयोग अपने मार्केडाउन पेजों के लिए slug को `MarkdownRemark` नोड्स में ऐड करेंगे।

अपने फ़ंक्शन को बदलें ताकि यह अब केवल `MarkdownRemark` नोड्स को लॉग करे।

```javascript:title=gatsby-node.js
exports.onCreateNode = ({ node }) => {
  // highlight-start
  if (node.internal.type === `MarkdownRemark`) {
    console.log(node.internal.type)
  }
  // highlight-end
}
```

आप प्रत्येक मार्कडाउन फ़ाइल नाम का उपयोग पेज slug बनाने के लिए करना चाहते हैं। इसलिए
`pandas-and-bananas.md` बनेंगे `/pandas-and-bananas/`। लेकिन आप `MarkdownRemark` नोड से फ़ाइल का नाम कैसे पाएँगे? इसे पाने के लिए, आपको "नोड ग्राफ" को इसके _parent_ `File` नोड के रूप में _traverse_ करने की आवश्यकता है, क्योंकि `File` नोड्स में डेटा होता है, जिस फ़ाइलों के लिए आपको आवश्यकता है। ऐसा करने के लिए, अपने फ़ंक्शन को फिर से संशोधित करें:

```javascript:title=gatsby-node.js
// highlight-next-line
exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    // highlight-start
    const fileNode = getNode(node.parent)
    console.log(`\n`, fileNode.relativePath)
    // highlight-end
  }
}
```

डेवेलपमेंट सर्वर को फिर से स्टार्ट करने के बाद, आपको अपने दो मार्कडाउन फाइल्स के लिए रिलेटिव path टर्मिनल स्क्रीन पर प्रिंट होते दिखनी चाहये।

![markdown-relative-path](markdown-relative-path.png)

अब आपको slugs बनाना होगा। जैसा कि फाइल्स के नामो से slug बनाने का तर्क मुश्किल हो सकता है, slug बनाने के लिए `gatsby-source-filesystem` प्लगइन के साथ फ़ंक्शन आता है। चलिए इसका उपयोग करते है।

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`) // highlight-line

exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(createFilePath({ node, getNode, basePath: `pages` })) // highlight-line
  }
}
```

फ़ंक्शन slug बनाने के साथ-साथ पैरेंट `File` नोड को खोजने का काम करता है। डेवेलपमेंट सर्वर को फिर से स्टार्ट करें और आपको टर्मिनल पर दो slug लॉग होते दिखने चाहिए, प्रत्येक मार्कडाउन फ़ाइल के लिए एक।

अब आप अपने नए slug को सीधे `MarkdownRemark` नोड पर ऐड सकते हैं। ये शक्तिशाली है, जैसा कि आप किसी भी डेटा को नोड में ऐड करते हैं, बाद में GraphQL के साथ क्वेरी करने के लिए उपलब्ध होता है।
इसलिए समय आने पर पेजेज़ बनाने के लिए slug प्राप्त करना आसान होगा।

ऐसा करने के लिए, आप API इंप्लिमेंटेशन मे [`CreateNodeField`](/docs/actions/#createNodeField) फ़ंक्शन का उपयोग करेंगे। यह फ़ंक्शन आपको अन्य प्लगइन्स द्वारा बनाए गए नोड्स पर अतिरिक्त फ़ील्ड बनाने की अनुमति देता है। केवल नोड के मूल निर्माता सीधे नोड को संशोधित कर सकते हैं - अन्य सभी प्लगइन्स
(अपने `gatsby-node.js` सहित) अतिरिक्त फीलड्स बनाने के लिए इस फ़ंक्शन का उपयोग करें।

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)
// highlight-next-line
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions // highlight-line
  if (node.internal.type === `MarkdownRemark`) {
    // highlight-start
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
    // highlight-end
  }
}
```

डेवेलपमेंट सर्वर रिसटार्ट करें और GraphiQL खोले या रेफ्रेश करें। फिर अपने नए slug को देखने के लिए, निम्न GraphQL क्वेरी रन करें।

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        fields {
          slug
        }
      }
    }
  }
}
```

अब जब slugs बन गये हैं, तो आप पेजेज़ बना सकते हैं।

## पेजेज़ बनाना

उसी `gatsby-node.js` फ़ाइल में, निम्न ऐड करें।

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}

// highlight-start
exports.createPages = async ({ graphql, actions }) => {
  // **Note:** The graphql function call returns a Promise
  // see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise for more info
  const result = await graphql(`
    query {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `)

  console.log(JSON.stringify(result, null, 4))
}
// highlight-end
```

आपने [`createPages`](/docs/node-apis/#createPage) API का कार्यान्वयन ऐड किया है जिसे Gatsby कॉल करता है ताकि प्लगइन्स पेजेज़ को ऐड कर सकें।

जैसा कि ट्यूटोरियल के इस भाग के परिचय में बताया गया है, प्रोग्रमैटिकली पेजेज़ बनाने के लिए निम्नलिखित स्टेप्स हैं:

1.  GraphQL के साथ डेटा क्वेरी करें
2.  पेजेज़ पर क्वेरी परिणामों को मैप करें

उपरोक्त कोड आपके मार्कडाउन से पेज बनाने के लिए पहला कदम है, आपके द्वारा बनाए गए मार्कडाउन slug को क्वेरी करने के लिए `graphql` फ़ंक्शन का उपयोग करते है। फिर आप उस क्वेरी के परिणाम को लॉग कर रहे हैं जो इस तरह दिखना चाहिए:

![query-markdown-slugs](query-markdown-slugs.png)

पेज बनाने के लिए आपको slug से परे एक अतिरिक्त चीज़ की आवश्यकता है: एक पेज टेम्प्लेट
कौम्पोनॅन्ट। Gatsby में सब कुछ की तरह, प्रोग्रामेटिक पेज React द्वारा संचालित होते हैं। पेज बनाते समय, आपको यह निर्दिष्ट करना होगा कि किस कौम्पोनॅन्ट का उपयोग करना है।

`src/templates` पर एक फोल्डर बनाएँ, और फिर `src/templates/blog-post.js` फ़ाइल में निम्न जोड़ें।

```jsx:title=src/templates/blog-post.js
import React from "react"
import Layout from "../components/layout"

export default () => {
  return (
    <Layout>
      <div>Hello blog post</div>
    </Layout>
  )
}
```

फिर `gatsby-node.js` अपडेट करें

```javascript:title=gatsby-node.js
const path = require(`path`) // highlight-line
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}

exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions // highlight-line
  const result = await graphql(`
    query {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `)

  // highlight-start
  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: path.resolve(`./src/templates/blog-post.js`),
      context: {
        // Data passed to context is available
        // in page queries as GraphQL variables.
        slug: node.fields.slug,
      },
    })
  })
  // highlight-end
}
```

डेवेलपमेंट सर्वर को रिसटार्ट करें और आपके पेजेज़ बन जाएंगे! डेवेलोप करते समय नई पेजेज़ को ढूंढ़ने का एक आसान तरीका यह है की किसी भी रैंडम पाथ पर जाएं Gatsby आपको साइट पर पेजेज़ की सूची दिखाने में मदद करेगा। अगर आप <http://localhost: 8000/sdf> पर जाएँगे, आपके द्वारा बनाए गए नए पेजेज़ दिखेंगे।

![new-pages](new-pages.png)

उनमें से एक पर जाएँ और आप देखें:

![hello-world-blog-post](hello-world-blog-post.png)

जो थोड़ा बोरिंग है और न कि आप जो चाहते हैं। अब आप अपने मार्कडाउन पोस्ट के डेटा को pull कर सकते हैं। `src/templates/blog-post.js` को परिवर्तित करें:

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Layout from "../components/layout"

// highlight-start
export default ({ data }) => {
  const post = data.markdownRemark
  // highlight-end
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
      {/* highlight-end */}
    </Layout>
  )
}

// highlight-start
export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`
// highlight-end
```

और…

![blog-post](blog-post.png)

बहुत अच्छे!

अंतिम चरण मे अपने नए पेजेज़ को इंडेक्स पेज से लिंक करना है।

`src/pages/index.js` पर लौटें, अपने मार्कडाउन slug के लिए क्वेरी करें, और लिंक बनाएं।

```jsx:title=src/pages/index.js
import React from "react"
import { css } from "@emotion/core"
import { Link, graphql } from "gatsby" // highlight-line
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default ({ data }) => {
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
            {/* highlight-start */}
            <Link
              to={node.fields.slug}
              css={css`
                text-decoration: none;
                color: inherit;
              `}
            >
              {/* highlight-end */}
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
            </Link> {/* highlight-line */}
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC }) {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          // highlight-start
          fields {
            slug
          }
          // highlight-end
          excerpt
        }
      }
    }
  }
`
```

और! एक वर्किंग यद्यपि छोटा, ब्लॉग!

## चुनौती

साइट के साथ खेलने का प्रयास करें। कुछ और मार्कडाउन फ़ाइलों को ऐड करने का प्रयास करें। `MarkdownRemark` नोड्स से अन्य डेटा को क्वेरी करें और फ्रंटपेज या ब्लॉग पोस्ट पेज ऐड करें।

ट्यूटोरियल के इस भाग में, आपने Gatsby की डेटा लेयर के साथ निर्माण की नींव के बारे में सीखा है। आपने सीखा कि कैसे _source_ और _transform_ डेटा का उपयोग किया जाता है प्लगइन्स के साथ, पेजेज़ पर डेटा _map_ करने के लिए GraphQL का उपयोग कैसे करें और फिर _page_ टेम्प्लेट कौम्पोनॅन्टस कैसे बनाएं जहां आप प्रत्येक पेज के डेटा के लिए क्वेरी करते हैं।

## आगे क्या आ रहा है?

अब जब आपने एक Gatsby साइट बना ली है, तो आप आगे क्या करने वाले है?

- Twitter पर अपनी Gatsby साइट शेयर करें और #gatsbytutorial सर्च करके देखें कि अन्य लोगों ने क्या बनाया है! अपने ट्वीट में @gatsbyjs का उल्लेख करना सुनिश्चित करें और हैशटैग #gatsbytutorial शामिल करें :)
- आप कुछ [उदाहरण साइटों](https://github.com/gatsbyjs/gatsby/tree/master/examples#gatsby-example-websites) पर एक नज़र डाल सकते हैं
- और ज्यादा खोजें [plugins](/docs/plugins/)
- देखें कि [अन्य लोग Gatsby के साथ क्या निर्माण कर रहे हैं](/showcase/)
- [Gatsby's APIs](/docs/api-specification/), [nodes](/docs/node-interface/), या [GraphQL](/docs/graphql-reference/) का डॉक्युमेंटेशन देखें
