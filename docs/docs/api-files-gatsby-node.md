---
title: gatsby-node.js API फ़ाइल
---

फ़ाइल में कोड `gatsby-node.js` आपकी साइट के निर्माण की प्रक्रिया में एक बार चलाया जाता है। आप इसका उपयोग गतिशील रूप से पेजस बनाने के लिए, GraphQL में नोड्स जोड़ने के लिए या बिल्ड लाइफसाइकिल के दौरान घटनाओं पर प्रतिक्रिया देने के लिए कर सकते हैं। [Gatsby Node APIs] (/docs/node-apis/) का उपयोग करने के लिए, अपनी साइट के रूट में `gatsby-node.js` नामक फ़ाइल बनाएं। इस फ़ाइल में आपके द्वारा उपयोग किए जाने वाले किसी भी API को एक्सपोर्ट करें।

हर Gatsby नोड API एक [नोड एपीआई सहायकों का एक सेट] पास करता है (/docs/node-api-helpers/)। ये आपको कई तरीकों तक पहुँचने देते हैं जैसे रिपोर्टिंग, नए पेज बनाने जैसे कार्य करने देता है ।

```js:title=gatsby-node.js
const path = require(`path`)
// बिल्ड होने के बाद जानकारी लॉग आउट करें
exports.onPostBuild = ({ reporter }) => {
  reporter.info(`Your Gatsby site has been built!`)
}
// ब्लॉग पेज गतिशील रूप से बनाएं
exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions
  const blogPostTemplate = path.resolve(`src/templates/blog-post.js`)
  const result = await graphql(`
    query {
      allSamplePages {
        edges {
          node {
            slug
            title
          }
        }
      }
    }
  `)
  result.data.allSamplePages.edges.forEach(edge => {
    createPage({
      path: `${edge.node.slug}`,
      component: blogPostTemplate,
      context: {
        title: edge.node.title,
      },
    })
  })
}
```
