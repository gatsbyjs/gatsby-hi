---
शीर्षक: विकास में एपीआई अनुरोधों को सम्‍मिलित करना
---

## साधन

यदि आप गैट्सबी के जीवनचक्र से परिचित नहीं हैं, तो अवलोकन देखें [गैट्सबी लाइफ़साइकल एपीआई](/docs/gatsby-lifecycle-apis/)

## विकास में एपीआई अनुरोधों का समर्थन करना

लोग अक्सर अपने बैकएंड कार्यान्वयन के रूप में उसी होस्ट और पोर्ट से फ्रंटएंड रिएक्ट ऐप की सेवा लेते हैं।

विकास सर्वर को किसी भी अज्ञात अनुरोधों को अपने एपीआई सर्वर के विकास में बताने के लिए, अपने `gatsby-config.js` के लिए एक `proxy` फ़ील्ड जोड़ें, उदाहरण के लिए:

```javascript:title=gatsby-config.js
module.exports = {
  proxy: {
    prefix: "/api",
    url: "http://dev-mysite.com",
  },
}
```

या:

```js:title=gatsby-config.js
module.exports = {
  proxy: [
    {
      prefix: "/api",
      url: "http://dev-mysite.com",
    },
    {
      prefix: "/api2",
      url: "http://dev2-mysite.com",
    },
  ],
}
```

इस तरह, जब आप विकास में `fetch('/api/todos')` करते हैं, तो विकास सर्वर यह पहचान लेगा कि यह स्थिर संपत्ति नहीं है, और आपके अनुरोध को `http://dev-mysite.com/api/todos` ले जाएगा गिरावट के रूप में।
 
ध्यान रखें कि `proxy` का केवल विकास में प्रभाव है (`gatsby develop` के साथ), और यह सुनिश्चित करना आप पर निर्भर करता है कि उत्पादन में सही जगह पर `/api/todos` जैसे URL मौजूद हैं या नहीं। 

## उन्नत समीपता

कभी-कभी आपको विकास सर्वर के लिए अधिक बारीक / लचीली पहुंच की आवश्यकता होती है।गैट्सबी आपकी साइट के `gatsby-config.js` के लिए [Express.js](https://expressjs.com/) विकास सर्वर को उजागर करता है जहाँ आप आवश्यकतानुसार एक्सप्रेस मिडलवेयर जोड़ सकते हैं।

```javascript:title=gatsby-config.js
const { createProxyMiddleware } = require("http-proxy-middleware") //v1.x.x
// Use implicit require for v0.x.x of 'http-proxy-middleware'
// const proxy = require('http-proxy-middleware')
// be sure to replace 'createProxyMiddleware' with 'proxy' where applicable

module.exports = {
  developMiddleware: app => {
    app.use(
      "/.netlify/functions/",
      createProxyMiddleware({
        target: "http://localhost:9000",
        pathRewrite: {
          "/.netlify/functions/": "",
        },
      })
    )
  },
}
```

ध्यान रखें कि मिडलवेयर का केवल विकास में प्रभाव होता है (`गैट्सबी डेवलप` के साथ)।

### स्व-हस्ताक्षरित प्रमाण पत्र

यदि आप स्व-हस्ताक्षरित प्रमाण पत्र के साथ स्थानीय एपीआई के लिए प्रॉक्सी करते हैं, तो विकल्प `secure` को `False` पर सेट करें।

```javascript:title=gatsby-config.js
const { createProxyMiddleware } = require("http-proxy-middleware") //v1.x.x
// Use implicit require for v0.x.x of 'http-proxy-middleware'
// const proxy = require('http-proxy-middleware')
// be sure to replace 'createProxyMiddleware' with 'proxy' where applicable

module.exports = {
  developMiddleware: app => {
    app.use(
      "/.netlify/functions/",
      createProxyMiddleware({
        target: "http://localhost:9000",
        secure: false, // Do not reject self-signed certificates.
        pathRewrite: {
          "/.netlify/functions/": "",
        },
      })
    )
  },
}
```
