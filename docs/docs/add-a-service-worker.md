---
title: सर्विस वर्कर ऐड करना
---

## सर्विस वर्कर क्या है

सर्विस वर्कर एक स्क्रिप्ट है जो आपका ब्राउज़र बैकग्राउंड में एक वेब पेज से अलग चलता है, उन सुविधाओं के लिए द्वार खोलता है जिन्हें वेब पेज या उपयोगकर्ता इंटरैक्शन की आवश्यकता नहीं है। वे थोड़े ख़राब कनेक्शन में आपकी साइट की उपलब्धता बढ़ाते हैं, और एक अच्छा उपयोगकर्ता अनुभव बनाने के लिए आवश्यक हैं।

यह पुश नोटिफिकेशन और बैकग्राउंड सिंक जैसी सुविधाओं का समर्थन करता है।

## `gatsby-plugin-offline`के साथ Gatsby में service workers का उपयोग करना

Gatsby आपकी साइट [gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline) में एक सर्विस वर्कर बनाने और लोड करने के लिए अच्छा प्लगइन इंटरफ़ेस प्रदान करता है।

आप इस प्लगइन का उपयोग [मैनिफ़ेस्ट प्लगइन](https://www.npmjs.com/package/gatsby-plugin-manifest) साथ कर सकते हैं।(मैनिफ़ेस्ट प्लगइन के बाद ऑफ़लाइन प्लगइन को सूचीबद्ध करना न भूलें ताकि मेनिफ़ेस्ट फ़ाइल को service worker में शामिल किया जा सके)

##  `gatsby-plugin-offline` इनस्टॉल करना

`npm install --save gatsby-plugin-offline`

इस प्लगइन को अपने `gatsby-config.js` में ऐड करें

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-offline`]
```

## संदर्भ

- [सर्विस वर्कर: एक परिचय](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [सर्विस वर्कर API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
