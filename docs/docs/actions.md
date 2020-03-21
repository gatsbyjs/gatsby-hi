---
title: एक्शन्स
description: एक्शन्स पर डॉक्यूमेंटेशन और वे आपको Gatsby के भीतर स्टेट में हेरफेर करने में कैसे मदद करते हैं
jsdoc:
  - "gatsby/src/redux/actions/public.js"
  - "gatsby/src/redux/actions/restricted.js"
contentsHeading: Functions
---

Gatsby स्टेट का प्रबंधन करने के लिए आंतरिक रूप से [Redux](http://redux.js.org) का उपयोग करता है। जब आप एक Gatsby API बनाते हैं, तो आप एक्शन्स का एक कलेक्शन (Redux में [bindActionCreators](https://redux.js.org/api/bindactioncreators/) से बंधे हुए एक्शन्स के बराबर) जिसका उपयोग आप आपकी साइट पर स्टेट में हेरफेर करने के लिए कर सकते हैं।

ऑब्जेक्ट `actions` में फ़ंक्शंस होते हैं और इन्हें ES6 ऑब्जेक्ट destructing का उपयोग करके अलग-अलग करके निकाला जा सकता है।

```javascript
// For function createNodeField
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
}
```
