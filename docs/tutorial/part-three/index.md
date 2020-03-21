---
title: नेस्टेड लेआउट कौम्पोनॅन्टस बनाना
typora-copy-images-to: ./
disableTableOfContents: true
---

भाग तीन में आपका स्वागत है!

## इस ट्यूटोरियल में क्या है?

इस भाग में, आप Gatsby प्लगइन्स और "लेआउट" कौम्पोनॅन्टस बनाने के बारे में जानेंगे।

Gatsby प्लगइन्स जावास्क्रिप्ट पैकेज हैं जो एक Gatsby साइट में फ़ंक्शनैलिटी डालने में मदद करते हैं। Gatsby को एक्स्टेंसिबल रहने के लिए डिज़ाइन किया गया है, जिसका अर्थ है प्लगिन्स सब कुछ जो Gatsby करता है उसको एक्सटेंड और मॉडिफाई कर सकते है।

लेआउट कौम्पोनॅन्टस आपकी साइट के उन हिस्सों के लिए हैं जिन्हें आप कई पेजेज़ में शेयर करना चाहते हैं। उदाहरण के लिए, साइटों में आमतौर पर एक शेयर्ड हेडर और फुटर के साथ एक लेआउट कौम्पोनॅन्टस होगा। लेआउट में जोड़ने के लिए अन्य सामान्य चीजें एक साइडबार और / या नेविगेशन मेनू हैं। उदाहरण के लिए इस पेज पर, सबसे ऊपर का हेडर gatsbyjs.org के लेआउट कौम्पोनॅन्ट का हिस्सा है।

चलिए भाग तीन शुरू करते हैं।

## प्लगइन्स का उपयोग करना

आप शायद प्लगइन्स के विचार से परिचित हैं। कई सॉफ्टवेयर सिस्टम नई कार्यक्षमता ऐड करने या सॉफ़्टवेयर के मुख्य कामकाज को संशोधित करने के लिए कस्टम प्लगइन्स को ऐड करने का समर्थन करते हैं। Gatsby प्लगइन्स उसी तरह काम करते हैं।

समुदाय के सदस्य (आप की तरह!) प्लगइन्स (थोड़े से जावास्क्रिप्ट कोड) का योगदान कर सकते हैं जो अन्य लोग तब उपयोग कर सकते हैं जब Gatsby साइटों का निर्माण करते हैं।

> पहले से ही सैकड़ों प्लगइन्स हैं! गैट्सबी [प्लगइन लाइब्रेरी](/plugins/) को एक्स्प्लोर करें।

प्लगइन्स के साथ हमारा लक्ष्य उन्हें आसानी से इनस्टॉल और इस्तेमाल करने का है। आप संभवतः आपके द्वारा बनाए गए लगभग हर Gatsby साइट में प्लगइन्स का उपयोग कर रहे होंगे। बाकी ट्यूटोरियल के माध्यम से काम करते समय आपके पास प्लगइन्स को इनस्टॉल करने और उपयोग करने के कई अवसर हैं।

प्लगइन्स का उपयोग करने के लिए प्रारंभिक परिचय के लिए, हम टाइपोग्राफी के लिए Gatsby प्लगइन को इनस्टॉल और इम्प्लीमेंट करेंगे।

[Typography.js](https://kyleamathews.github.io/typography.js/) एक जावास्क्रिप्ट लाइब्रेरी है जो आपकी साइट की टाइपोग्राफी के लिए वैश्विक बेस स्टाइल्स उत्पन्न करती है। लाइब्रेरी में एक Gatsby साइट का उपयोग करके इसे स्ट्रीमलाइन करने के लिए [संबंधित Gatsby प्लगइन](/packages/gatsby-plugin-typography/) है।

### ✋ एक नई गैट्सबी साइट बनाएँ

जैसा कि हमने उल्लेख किया है [भाग दो](/tutorial/part-two/) में, इस बिंदु पर टर्मिनल विंडो (एस) को बंद करना और ट्यूटोरियल के पिछले हिस्सों से परियोजना फाइलों को अपने काम पर रखने के लिए शायद एक अच्छा विचार है। इससे आप अपना डेस्कटॉप साफ़ रख सकते हैं। फिर एक नई टर्मिनल विंडो खोलें और `ट्यूटोरियल-पार्ट-थ्री` नामक एक निर्देशिका में एक नई गैट्सबी साइट बनाने के लिए निम्न कमांड चलाएं और फिर इस नई निर्देशिका में जाएं:

```shell
gatsby new tutorial-part-three https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-three
```

### ✋ `gatsby-plugin-typography` इनस्टॉल और कॉन्फ़िगर करें`

प्लगइन का उपयोग करने के दो मुख्य चरण हैं: इंस्टॉल करना और कॉन्फ़िगर करना।

1. `gatsby-plugin-typography` NPM पैकेज इंस्टॉल करें।

```shell
npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
```

> नोट: Typography.js को कुछ अतिरिक्त पैकेजों की आवश्यकता होती है, इसलिए उन्हें निर्देशों में शामिल किया जाता है। इस तरह की अतिरिक्त आवश्यकताएं प्रत्येक प्लगइन के "इंस्टॉल" निर्देशों में सूचीबद्ध होंगी।

2. निम्नलिखित के लिए अपनी परियोजना के रुट में फ़ाइल `gatsby-config.js` एडिट करें:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

`gatsby-config.js` एक और विशेष फ़ाइल है जिसे Gatsby अपने आप पहचान लेगा। यह वह जगह है जहां आप प्लगइन्स और अन्य साइट कॉन्फ़िगरेशन ऐड हैं।

> यदि आप चाहें, तो और पड़ने के लिए [doc on gatsby-config.js](/docs/gatsby-config/)  को देखें।

3. Typography.js को कॉन्फ़िगरेशन फ़ाइल की आवश्यकता होती है। `src` डायरेक्टरी में `utils` नामक एक नई डायरेक्टरी बनाएँ। फिर `typography.js` नामक एक नई फ़ाइल को `utils` में ऐड करें और फ़ाइल में निम्नलिखित को कॉपी करें:

```javascript:title=src/utils/typography.js
import Typography from "typography"
import fairyGateTheme from "typography-theme-fairy-gates"

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```

4. डेवलपमेंट सर्वर शुरू करें।

```shell
gatsby develop
```

एक बार साइट लोड करने के बाद, यदि आप Chrome डेवलपर टूल का उपयोग करके जेनरेट किए गए HTML का निरीक्षण करते हैं, तो आप देखेंगे कि टाइपोग्राफी प्लगइन ने `<style>` एलिमेंट को `<head>` एलिमेंट के साथ अपने जनरेटेड CSS में जोड़ा:

![typography-styles](typography-styles.png)

### ✋ कुछ कंटेंट और स्टाइल में बदलाव करें

निम्नलिखित को अपने `src/pages/index.js` में कॉपी करें ताकि आप देख सकें की
Typography.js द्वारा जनरेटेड CSS का प्रभाव बेहतर है।

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
)
```

आपकी साइट को अब इस तरह दिखना चाहिए:

![no-layout](no-layout.png)

चलिए कुछ छोटे सुधार करते हैं। कई साइटों के पेज के मध्य में केंद्रित पाठ का एक अकेला कॉलम होता है। इसे बनाने के लिए, निम्न शैलियों को ऐड करें
`src/pages/index.js` में `<div>`।

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  // highlight-next-line
  <div style={{ margin: `3rem auto`, maxWidth: 600 }}>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
)
```

![with-layout2](with-layout2.png)

बहुत बढ़िया। आपने अपना पहला Gatsby प्लगइन इनस्टॉल और कॉन्फ़िगर किया है!

## लेआउट कौम्पोनॅन्टस बनाना

अब लेआउट कौम्पोनॅन्टस के बारे में जानने के लिए आगे बढ़ते हैं। इस भाग के लिए तैयार होने के लिए, अपनी परियोजना में कुछ नए पेज जोड़ें: एक अबाउट पेज और संपर्क पेज।

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div>
    <h1>About me</h1>
    <p>I’m good enough, I’m smart enough, and gosh darn it, people like me!</p>
  </div>
)
```

```jsx:title=src/pages/contact.js
import React from "react"

export default () => (
  <div>
    <h1>I'd love to talk! Email me at the address below</h1>
    <p>
      <a href="mailto:me@example.com">me@example.com</a>
    </p>
  </div>
)
```

आइए देखें कि अबाउट पेज में नया क्या दिखता है:

![about-uncentered](about-uncentered.png)

हम्। यह अच्छा होगा यदि दो नए पेजेज की कंटेंट index पेज की तरह केंद्रित हो। और किसी प्रकार का ग्लोबल नेविगेशन करना अच्छा होगा, ताकि वीजीटर्स को प्रत्येक उप-पेजेज को खोजने और देखने में आसानी हो।

आप अपना पहला लेआउट कौम्पोनॅन्टस बनाकर इन परिवर्तनों से निपटेंगे।

### ✋ अपना पहला लेआउट कौम्पोनॅन्टस बनाएँ

1. `src/components` पर एक नई डायरेक्टरी बनाएँ।

2. `src/components/layout.js` पर एक बहुत ही बेसिक लेआउट कौम्पोनॅन्ट बनाएँ:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

3. इस नए लेआउट कौम्पोनॅन्टस को अपने `src/pages/index.js` पेज कौम्पोनॅन्ट में import करें:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout" // highlight-line

export default () => (
  <Layout> {/* highlight-line */}
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </Layout> {/* highlight-line */}
)
```

![with-layout2](with-layout2.png)

बहुत बढ़िया, लेआउट काम कर रहा है! आपके index पेज का कंटेंट अभी भी केंद्रित है।

लेकिन `/about/`, या `/contact/` के लिए नेविगेट करने का प्रयास करें। उन पेजेज का कंटेंट अभी भी केंद्रित नहीं होगी।

4. लेआउट कौम्पोनॅन्टस को `about.js` और `contact.js` में import करें (जैसा कि आपने पिछले चरण में `index.js` के लिए किया था)।

एक अकेले शेयर्ड लेआउट कौम्पोनॅन्ट से तीनो पेजेज के कंटेंट सेण्टर में हो गए हैं!

### ✋ एक साइट शीर्षक जोड़ें

1. अपने नए लेआउट कौम्पोनॅन्टस में निम्न पंक्ति ऐड करें:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    <h3>MySweetSite</h3> {/* highlight-line */}
    {children}
  </div>
)
```

यदि आप अपने तीन पेजेज में से किसी पर जाते हैं, तो आप वही टाइटल उस पेज में ऐड देखेंगे उदाहरण, `/about/` पेज:

![with-title](with-title.png)

### ✋ पृष्ठों के बीच नेविगेशन लिंक ऐड करें

1. अपने लेआउट कौम्पोनॅन्टस फ़ाइल में निम्नलिखित को कॉपी करें:

```jsx:title=src/components/layout.js
import React from "react"
// highlight-start
import { Link } from "gatsby"

const ListLink = props => (
  <li style={{ display: `inline-block`, marginRight: `1rem` }}>
    <Link to={props.to}>{props.children}</Link>
  </li>
)
// highlight-end

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {/* highlight-start */}
    <header style={{ marginBottom: `1.5rem` }}>
      <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
        <h3 style={{ display: `inline` }}>MySweetSite</h3>
      </Link>
      <ul style={{ listStyle: `none`, float: `right` }}>
        <ListLink to="/">Home</ListLink>
        <ListLink to="/about/">About</ListLink>
        <ListLink to="/contact/">Contact</ListLink>
      </ul>
    </header>
    {/* highlight-end */}
    {children}
  </div>
)
```

![with-navigation2](with-navigation.png)

आखिर आपने इसे हासिल कर ही लिया है! बुनियादी ग्लोबल नेविगेशन के साथ एक तीन पेज की साइट।

_चुनौती:_ अपनी नई "लेआउट कौम्पोनॅन्टस" शक्तियों के साथ, अपने Gatsby साइटों पर हेडर, फुटर, ग्लोबल नेविगेशन, साइडबार आदि ऐड करने की कोशिश करें!

## आगे क्या आ रहा है?

[ट्यूटोरियल के भाग चार](/tutorial/part-four/) पर जारी रखें जहाँ आप Gatsby के डेटा लेयर और प्रोग्राम बनाने के बारे में सीखना शुरू करेंगे।
