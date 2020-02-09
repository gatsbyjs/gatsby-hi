---
title: Adding a Service Worker
---

## service worker क्या है।

service worker एक स्क्रिप्ट है जो आपका ब्राउज़र पृष्ठभूमि में चलता है, एक वेब पेज से अलग होता है, उन सुविधाओं के लिए द्वार खोलता है जिन्हें वेब पेज या उपयोगकर्ता इंटरैक्शन की आवश्यकता नहीं है। वे धब्बेदार कनेक्शन में आपकी साइट की उपलब्धता बढ़ाते हैं, और एक अच्छा उपयोगकर्ता अनुभव बनाने के लिए आवश्यक हैं।

यह पुश नोटिफिकेशन और बैकग्राउंड सिंक जैसी सुविधाओं का समर्थन करता है।

## `gatsby-plugin-offline` साथ Gatsby में service workers का उपयोग करना।

Gatsby आपकी साइट में एक service worker बनाने और लोड करने के लिए अच्छा प्लगइन इंटरफ़ेस प्रदान करता है [gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

आप इस प्लगइन का उपयोग एक साथ कर सकते हैं [manifest plugin](https://www.npmjs.com/package/gatsby-plugin-manifest). (मैनिफ़ेस्ट प्लगइन के बाद ऑफ़लाइन प्लगइन को सूचीबद्ध करना न भूलें ताकि मेनिफ़ेस्ट फ़ाइल को service worker में शामिल किया जा सके ).

##  `gatsby-plugin-offline` को इंस्टॉल करने के लिये

`npm install --save gatsby-plugin-offline`

इस प्लगइन को अपने `gatsby-config.js`में जोड़ें

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-offline`]
```

## संदर्भ

- [Service Workers: an Introduction](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
