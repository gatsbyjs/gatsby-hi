---
title: The gatsby-ssr.js API file
---

फ़ाइल `gatsby-ssr.js` आपको स्थिर HTML फ़ाइलों की सामग्री को बदलने देती है क्योंकि वे Gatsby और Node.js. द्वारा सर्वर-साइड रेंडर (SSR) की जा रही हैं। [Gatsby SSR APIs](/docs/ssr-apis/) का उपयोग करने के लिए, अपनी साइट की जड़ में gatsby-ssr.js नामक एक फ़ाइल बनाएँ। इस फ़ाइल में आपके द्वारा उपयोग किए जाने वाले किसी भी API को निर्यात करें।


APIs `wrapPageElement` और `wrapRootElement` दोनों SSR और [browser APIs](/docs/browser-apis) में मौजूद हैं।
यदि आप उनमें से एक का उपयोग करते हैं, तो विचार करें कि क्या आपको इसे `gatsby-ssr.js` और `gatsby-browser.js` दोनों में लागू करना चाहिए ताकि Node.js के साथ SSR के माध्यम से उत्पन्न पेजेज़ जावास्क्रिप्ट से [hydrated](/docs/glossary#hydration) होने के बाद समान हों।

```jsx:title=gatsby-ssr.js
const React = require("react")
const Layout = require("./src/components/layout")

// body element के लिए एक class name जोड़ता है
exports.onRenderBody = ({ setBodyAttributes }, pluginOptions) => {
  setBodyAttributes({
    className: "my-body-class",
  })
}

// प्रत्येक पृष्ठ को एक कौम्पोनॅन्टस में लपेटता है
exports.wrapPageElement = ({ element, props }) => {
  return <Layout {...props}>{element}</Layout>
}
```
