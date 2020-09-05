# शैली गाइड

अनुवाद के लिए भाषा-विशिष्ट शैली के नियमों के लिए इस फ़ाइल का उपयोग करें।

## नियम

### कोड ब्लॉक में टेक्स्ट

टिप्पणियों को छोड़कर कोड ब्लॉक में टेक्स्ट का अनुवाद न करें। आप वैकल्पिक रूप से स्ट्रिंग में टेक्स्ट का अनुवाद कर सकते हैं, लेकिन कोड का संदर्भ देने वाले टेक्स्ट का अनुवाद न करने के लिए सावधान रहें!

उदाहरण:

```js
// उदाहरण
import React from "react"
export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>हैलो Gatsby!</div>
)
```

✅ सही:

```js
// उदाहरण
import React from "react"
export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
)
```

✅ यह भी सही:

```js
// उदाहरण
import React from "react"
export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>हैलो Gatsby!</div>
)
```

❌ गलत:

```js
// उदाहरण
import React from "react"
export default () => (
  // 'purple' एक CSS कीवर्ड है
  <div style={{ color: `बैंगनी`, fontSize: `72px` }}>हैलो Gatsby!</div>
)
```

❌ निश्चित रूप से गलत:

```js
React मे से "React" इम्पोर्ट करो
एक्स्पोर्ट डिफ़ॉल्ट () => (
   <div अंदाज = {{color: `बैंगनी`, fontSize:` 72px`}}> हैलो Gatsby! </div>
)
```

### बाहरी लिंक

यदि किसी लेख में बाहरी लिंक [MDN] या [विकिपीडिया] की तरह है, और उस लेख का एक संस्करण आपकी भाषा में मौजूद है, जो सभ्य गुणवत्ता का है, तो फिर इसके बजाय उस संस्करण से लिंक करने पर विचार करें।

[mdn]: https://developer.mozilla.org/en-US/
[विकिपीडिया]: https://en.wikipedia.org/wiki/Main_Page

उदाहरण:

```md
[React](https://en.wikipedia.org/wiki/React_(web_framework)) elements are immutable.
```

✅ सही:

```md
[React](https://hi.wikipedia.org/wiki/रियेक्ट) एलिमेन्ट्स इम्मुटेबल होते हैं।
```

ऐसे लिंक जिनके लिए कोई समतुल्य नहीं है (स्टैक ओवरफ़्लो, YouTube वीडियो आदि), उनके लिए अंग्रेज़ी लिंक का उपयोग करें।

## शब्दकोष

सामान्य तकनीकी शब्दावली का अनुवाद कैसे किया जाना चाहिए, यह जानने के लिए इस अनुभाग का उपयोग करें।

| Term   | Translation |
| :---: | :---: |
| Abstract | एबसट्रैक्ट |
| Additional | एडिशनल |
| App | एप्प |
| Apps | ऍप्स |
| Components | कौम्पोनॅन्टस |
| Deploy | डेप्लॉय |
| Directories | डायरेक्ट्रीज |
| Execute | एग्ज़ीक्यूट |
| Footer | फुटर |
| Functionality | फ़ंक्शनैलिटी |
| Javascript | जावास्क्रिप्ट |
| Locally | लोकल्ली |
| Markdown | मार्कडाउन |
| Menu | मेनू |
| Options | ओप्शंस |
| Optional | ऑप्शनल |
| Pages | पेजेज़ |
| Plugin | प्लगइन |
| Professionally | प्रोफेशनली |
| Programmatically | प्रोग्रमैटिकली |
| Projects | प्रोजेक्टस |
| Pull | पुल्ल |
| Query | क्वेरी |
| Repository | रिपॉज़िटरी |
| Resolve | रीसोलव |
| Reviewer | रीवीउअर |
| Review | रीव्यु |
| Shared | शेयर्ड |
| Static | इसटैटिक |
| Source | सोर्स |
| Text | टेक्स्ट |
| Tool | टूल |
| Theme  | थीम |
| Tutorial | ट्यूटोरियल |
| Value | वैल्यू  |
| View | व्यू |

ऐसी शब्द जिसका अनुवाद करने की आवश्यकता नहीं है:

| अनुवाद की आवश्यकता नहीं है |
| :-----: |
| API |
| array |
| class |
| constructor |
| context |
| CDN |
| fork |
| Gatsby |
| Github |
| HTML |
| props |
| React |
| strings |
| UI |
| key |
