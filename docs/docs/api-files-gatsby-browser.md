---
title: The gatsby-browser.js API फाइल
---

`gatsby-browser.js` आपको ब्राउज़र के भीतर क्रएक्शन्स का जवाब देने देता है, और आपकी साइट को अतिरिक्त कॉम्पोनेंट्स में  रैप करता है। [Gatsby Browser API](/docs/browser-apis) आपको Gatsby के [क्लाइंट-साइड](/docs/glossary#client-side) के साथ बातचीत करने के लिए कई विकल्प देता है।

APIs `wrapPageElement` और` wrapRootElement` दोनों ब्राउज़र और [सर्वर-साइड रेंडरिंग (SSR) API](/docs/ssr-apis) में मौजूद हैं। यदि आप उनमें से एक का उपयोग करते हैं, तो विचार करें कि क्या आपको इसे `gatsby-ssr.js` और `gatsby-browser.js` दोनों में लागू करना चाहिए, ताकि Node.js के साथ SSR के माध्यम से उत्पन्न पेजेज [हाइड्रेटेड](/docs/glossary#hydration) होने के बाद समान हों ब्राउज़र जावास्क्रिप्ट के साथ।

ब्राउज़र API का उपयोग करने के लिए, `gatsby-browser.js` पर अपनी साइट की रुट में एक फ़ाइल बनाएँ। इस फ़ाइल से उपयोग करने के लिए प्रत्येक API को एक्सपोर्ट करें।

```jsx:title=gatsby-browser.js
const React = require("react")
const Layout = require("./src/components/layout")

// लॉग जब क्लाइंट रूट बदलता है
exports.onRouteUpdate = ({ location, prevLocation }) => {
  console.log("new pathname", location.pathname)
  console.log("old pathname", prevLocation ? prevLocation.pathname : null)
}

// एक कॉम्पोनेन्ट में हर पेज को रैप करता है
exports.wrapPageElement = ({ element, props }) => {
  return <Layout {...props}>{element}</Layout>
}
```
