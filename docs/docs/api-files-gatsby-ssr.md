---
title: gatsby-ssr.js एपीआई फ़ाइल
---

यह फ़ाइल `gatsby-ssr.js` आपको स्थिर HTML फ़ाइलों की सामग्री को बदलने की सुविधा देता है क्योंकि वे Gatsby और Node.js| द्वारा सर्वर-साइड रेंडर (SSR) की जा रही हैं। यह उपयोग करने के लिए [Gatsby SSR APIs](/docs/ssr-apis/), नामक एक फ़ाइल बनाएँ `gatsby-ssr.js` अपनी साइट की जड़ में। इस फ़ाइल में आपके द्वारा उपयोग किए जाने वाले किसी भी API को निर्यात करें।

एपीआई `wrapPageElement` और `wrapRootElement` SSR और दोनों में मौजूद हैं [browser APIs](/docs/browser-apis). यदि आप उनमें से एक का उपयोग करते हैं, तो विचार करें कि क्या आपको इसे दोनों में लागू करना चाहिए `gatsby-ssr.js` और `gatsby-browser.js` ताकि SSR के माध्यम से पेज उत्पन्न हों Node.js होने के बाद भी वही हैं [hydrated](/docs/glossary#hydration) ब्राउज़र जावास्क्रिप्ट के साथ।

```jsx:title=gatsby-ssr.js
const React = require("react")
const Layout = require("./src/components/layout")

// Adds a class name to the body element
exports.onRenderBody = ({ setBodyAttributes }, pluginOptions) => {
  setBodyAttributes({
    className: "my-body-class",
  })
}

// Wraps every page in a component
exports.wrapPageElement = ({ element, props }) => {
  return <Layout {...props}>{element}</Layout>
}
```
