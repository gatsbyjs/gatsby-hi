---
शीर्षक: पेजिनेशन जोड़ना
---

कॅन्टेन्ट की लिस्ट प्रदर्शित करने वाला पेज कॅन्टेन्ट की मात्रा बढ़ने पर अधिक लंबा हो जाता है।
पेजिनेशन उस सामग्री को कई पेजेज़ में फैलाने की तकनीक है।

पेजिनेशन का लक्ष्य कई पेजेज़ (एक सिंगल [टेम्पलेट](/docs/building-with-components/#page-template-components) से) बनाना है जो सीमित संख्या में आइटम्स दिखाते हैं।

प्रत्येक पेज में उन विशिष्ट आइटम्स के लिए [क्वेरी GraphQL](/docs/graphql-concepts/) होगा।

उन विशिष्ट आइटम्स (अर्थात [`limit`](/docs/graphql-reference/#limit) और [`skip`](/docs/graphql-reference/#skip) की वैल्यूस के लिए) की क्वेरी करने के लिए आवश्यक जानकारी [`context`](/docs/graphql-reference/#query-variables) से आ जाएगी जिसे तब जोड़ा जाता है जब `gatsby-node` में [पेज बना रहे हैं](/docs/creating-and-modifying-pages/#creating-pages-in-gatsby-nodejs) ।

## उदाहरण

```jsx:title=src/templates/blog-list-template.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default class BlogList extends React.Component {
  render() {
    const posts = this.props.data.allMarkdownRemark.edges
    return (
      <Layout>
        {posts.map(({ node }) => {
          const title = node.frontmatter.title || node.fields.slug
          return <div key={node.fields.slug}>{title}</div>
        })}
      </Layout>
    )
  }
}

export const blogListQuery = graphql`
// highlight-start
  query blogListQuery($skip: Int!, $limit: Int!) {
    allMarkdownRemark(
      sort: { fields: [frontmatter___date], order: DESC }
      limit: $limit
      skip: $skip
    ) {
// highlight-end
      edges {
        node {
          fields {
            slug
          }
          frontmatter {
            title
          }
        }
      }
    }
  }
`
```

```js:title=gatsby-node.js
const path = require("path")
const { createFilePath } = require("gatsby-source-filesystem")

exports.createPages = async ({ graphql, actions, reporter }) => {
  const { createPage } = actions

  const result = await graphql(
    `
      {
        allMarkdownRemark(
          sort: { fields: [frontmatter___date], order: DESC }
          limit: 1000
        ) {
          edges {
            node {
              fields {
                slug
              }
            }
          }
        }
      }
    `
  )

  if (result.errors) {
    reporter.panicOnBuild(`Error while running GraphQL query.`)
    return
  }

  // ...

  // ब्लॉग-लिस्ट पेजेज़ बनाएँ
  // हाइलाइट-शुरू
  const posts = result.data.allMarkdownRemark.edges
  const postsPerPage = 6
  const numPages = Math.ceil(posts.length / postsPerPage)

  Array.from({ length: numPages }).forEach((_, i) => {
    createPage({
      path: i === 0 ? `/blog` : `/blog/${i + 1}`,
      component: path.resolve("./src/templates/blog-list-template.js"),
      context: {
        limit: postsPerPage,
        skip: i * postsPerPage,
        numPages,
        currentPage: i + 1,
      },
    })
  })
  // हाइलाइट-समाप्त
}

exports.onCreateNode = ({ node, actions, getNode }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const value = createFilePath({ node, getNode })
    createNodeField({
      name: `slug`,
      node,
      value,
    })
  }
}
```

ऊपर दिया गया कोड उन पेजेज़ की मात्रा बनाएगा जो कुल पोस्ट्स की संख्या पर आधारित हैं। प्रत्येक पेज `postsPerPage` (6) पोस्ट्स को लिस्ट करेगा, जब तक कि `postsPerPage`(6) से कम पोस्ट्स न हों।
पहले पेज के लिए पथ `/blog` है, निम्न पेजेज़ का पथ इस रूप: `/blog/2`, `/blog/3`, आदि में होगा।

## अन्य संसाधन

- पिछले/अगले पेज और पेज के निचले भाग में पारंपरिक पेज-नेविगेशन के लिंक्स जोड़ने के लिए इस [चरण-दर-चरण ट्यूटोरियल](https://nickymeuleman.netlify.com/blog/gatsby-pagination/) का पालन करें।

- देखें आधिकारिक [gatsby-स्टार्टर-ब्लॉग] (https://github.com/gatsbyjs/gatsby-starter-blog) के स्थान पर इसका विस्तार  [Gatsby-पेजीनेटेड-ब्लॉग] (https://github.com/NickyMeuleman/gatsby-paginated-blog) [(डेमो)] (https://nickymeuleman.github.io/gatsby-paginated-blog/)  पेजिनेशन के साथ।
