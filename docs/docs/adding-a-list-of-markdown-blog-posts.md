---
title: मार्कडाउन ब्लॉग पोस्ट की लिस्ट जोड़ना
---

एक बार जब आप मार्कडाउन पेजिज़ को अपनी साइट पर जोड़ लेते हैं, तो आप एक समर्पित इंडेक्स पेज पर अपनी पोस्टों को सूचीबद्ध करने में सक्षम होने से बस एक कदम दूर होते हैं।

## पोस्ट बनाना

जैसा कि [यहाँ](adding-markdown-pages.md) बताया गया है, आपको मार्कडाउन फाइलों में अपनी पोस्ट बनानी होगी जो इस तरह दिखाई देगी:

```markdown
---
path: "/blog/my-first-post"
date: "2017-11-07"
title: "My first blog post"
---

Has anyone heard about GatsbyJS yet?
```

## पेज बनाना

पहला कदम उस पेज को बनाना होगा जो आपकी पोस्ट को `src/pages/` में प्रदर्शित करेगा। आप उदाहरण के लिए `index.js` का उपयोग कर सकते हैं।

```jsx:title=src/pages/index.js
import React from "react"
import PostLink from "../components/post-link"

const IndexPage = ({
  data: {
    allMarkdownRemark: { edges },
  },
}) => {
  const Posts = edges
    .filter(edge => !!edge.node.frontmatter.date) // You can filter your posts based on some criteria
    .map(edge => <PostLink key={edge.node.id} post={edge.node} />)

  return <div>{Posts}</div>
}

export default IndexPage
```

## GraphQL क्वेरी बनाना

दूसरा, आपको अपने कौम्पोनॅन्ट को GraphQL क्वेरी के साथ डेटा प्रदान करना होगा। इसे जोड़ें, ताकि `index.js` इस तरह दिखे:

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import PostLink from "../components/post-link"

const IndexPage = ({
  data: {
    allMarkdownRemark: { edges },
  },
}) => {
  const Posts = edges
    .filter(edge => !!edge.node.frontmatter.date) // You can filter your posts based on some criteria
    .map(edge => <PostLink key={edge.node.id} post={edge.node} />)

  return <div>{Posts}</div>
}

export default IndexPage

export const pageQuery = graphql`
  query {
    allMarkdownRemark(sort: { order: DESC, fields: [frontmatter___date] }) {
      edges {
        node {
          id
          excerpt(pruneLength: 250)
          frontmatter {
            date(formatString: "MMMM DD, YYYY")
            path
            title
          }
        }
      }
    }
  }
`
```

## `PostLink` कौम्पोनॅन्ट बनाना

केवल एक ही काम, `PostLink` कौम्पोनॅन्ट को जोड़ना रह गया है। `src/components/` में एक नई फ़ाइल `post-link.js` बनाएं और निम्नलिखित जोड़ें:

```jsx:title=src/components/post-link.js
import React from "react"
import { Link } from "gatsby"

const PostLink = ({ post }) => (
  <div>
    <Link to={post.frontmatter.path}>
      {post.frontmatter.title} ({post.frontmatter.date})
    </Link>
  </div>
)

export default PostLink
```

यह आपको एक पेज देना चाहिए जिसमें आपके पोस्ट्स अवरोही तिथि के अनुसार छांटे गए होंगे। आप अपने इच्छित प्रभावों को प्राप्त करने के लिए `frontmatter` और पेज और `PostLink` कौम्पोनॅन्टस के अंदर और अधिक बदलाव कर सकते हैं!
