---
title: gatsby-node.js API फ़ाइल
---

`gatsby-node.js` फ़ाइल में कोड आपकी साइट के निर्माण की प्रक्रिया में एक बार चलाया जाता है। आप इसका उपयोग गतिशील रूप से पृष्ठ बनाने के लिए, GraphQL में नोड्स जोड़ने के लिए या बिल्ड जीवनचक्र के दौरान घटनाओं पर प्रतिक्रिया देने के लिए कर सकते हैं। [Gatsby Node APIs] (/docs/node-apis/) का उपयोग करने के लिए, अपनी साइट के रूट में `gatsby-node.js` नामक फ़ाइल बनाएं। इस फ़ाइल में आपके द्वारा उपयोग किए जाने वाले किसी भी API को निर्यात करें।

हर गैट्सबी नोड एपीआई  [set of Node API helpers](/docs/node-api-helpers/) पास करता है। ये आपको रिपोर्टिंग जैसे कई तरीकों का उपयोग करने देता हैं, या नए पेज बनाने देता है।

```js:title=gatsby-node.js
const path = require(`path`)
// Log out information after a build is done
exports.onPostBuild = ({ reporter }) => {
  reporter.info(`Your Gatsby site has been built!`)
}
// Create blog pages dynamically
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
