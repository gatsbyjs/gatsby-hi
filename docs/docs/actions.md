---
title: एक्शन्स
description: एक्शन्स पर प्रलेखन और वे आपको Gatsby के भीतर स्टेट में हेरफेर करने में कैसे मदद करते हैं
jsdoc:
  - "gatsby/src/redux/actions/public.js"
  - "gatsby/src/redux/actions/restricted.js"
contentsHeading: Functions
---

Gatsby स्टेट का प्रबंधन करने के लिए आंतरिक रूप से [Redux](http://redux.js.org) का उपयोग करता है। जब आप एक Gatsby API कार्यान्वित करते हैं, तो आपको क्रियाओं का एक संग्रह  (equivalent to actions bound with [bindActionCreators](https://redux.js.org/api/bindactioncreators/) in Redux) जिसका उपयोग आप स्टेट में हेरफेर करने के लिए कर सकते हैं आपकी साइट पर ।

ऑब्जेक्ट `actions` में फ़ंक्शंस होते हैं और इन्हें ES6 ऑब्जेक्ट destructing का उपयोग करके व्यक्तिगत रूप से निकाला जा सकता है।

```javascript
// For function createNodeField
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
}
```
