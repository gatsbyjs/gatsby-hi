---
title: Gatsby में स्टाइलिंग का परिचय
typora-copy-images-to: ./
disableTableOfContents: true
---

<!-- Idea: Create a glossary to refer to. A lot of these terms get jumbled -->

<!--
  - Global styles
  - Component css
  - CSS-in-JS
  - CSS Modules

-->

Gatsby ट्यूटोरियल के भाग दो में आपका स्वागत है!

## इस ट्यूटोरियल में क्या है?

इस भाग में आप Gatsby वेबसाइट की स्टाइलिंग के ओप्शंस के बारे में जानेंगे और साइट बनाने में React कौम्पोनॅन्ट के इस्तेमाल के बारे में और गहराई से जानेंगे।

## ग्लोबल स्टाइल्स का उपयोग करना

प्रत्येक साइट में किसी न किसी प्रकार की ग्लोबल स्टाइल्स होती है। इसमें साइट की टीपोग्राफी और बॅकग्राउंड कलर जैसी चीजें शामिल हैं। ये स्टाइल्स साइट के समग्र अनुभव को निर्धारित करती हैं - जैसे दीवार का रंग और बनावट कमरे के समग्र अनुभव को निर्धारित करता है।

### स्टॅंडर्ड स्टाइल्स फाइलों के साथ ग्लोबल सीएसएस का निर्माण

किसी साइट पर ग्लोबल स्टाइल्स को जोड़ने के सबसे सरल तरीकों में से एक ग्लोबल `.css` स्टाइलशीट का उपयोग करना है।

#### ✋ एक नई Gatsby साइट बनाएँ

एक नई Gatsby साइट बनाना शुरू करें। यह सबसे अच्छा हो सकता है (विशेषकर यदि आप कमांड लाइन में नए हैं) की आप टर्मिनल विंडो को बंद कर दे जिसे आपने [भाग एक] (/tutorial/part-one/) मे उपयोग किया था और भाग दो के लिए एक नया टर्मिनल सेशन शुरू करे।

एक नई टर्मिनल विंडो खोलें, एक नया "हैलो वर्ल्ड" Gatsby साइट `tutorial-part-two` नामक डायरेक्टरी में बनाएं, और फिर इस डायरेक्टरी में जाएं:

```shell
gatsby new tutorial-part-two https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-two
```

अब आपके पास एक नई Gatsby साइट (Gatsby "हैलो वर्ल्ड" स्टार्टर के आधार पर) निम्नलिखित स्ट्रक्चर के साथ है:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
```

#### ✋ सीएसएस फाइल मे स्टाइल्स डालना

1. अपने नए प्रोजेक्ट में एक .css फ़ाइल बनाएँ:

```shell
cd src
mkdir styles
cd styles
touch global.css
```

> नोट: आप चाहें तो आप अपने मनपसंद कोड एडिटर का उपयोग करके इन फ़ोल्डर और फ़ाइलों को बना सकते है।

अब आपके पास इस तरह का स्ट्रक्चर होना चाहिए:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
```

2. `global.css` फ़ाइल में कुछ सीएसएस स्टाइल्स को डिफाइन करें:

```css:title=src/styles/global.css
html {
  background-color: lavenderblush;
}
```

> नोट: उदाहरण लिए सीएसएस फ़ाइल का प्लेसमेंट `/src/styles/` फ़ोल्डर में मनमाना है।

#### ✋ `gatsby-browser.js` में स्टाइलशीट को शामिल करें

1. एक नयी फाइल `gatsby-browser.js` बनाएँ

```shell
cd ../..
touch gatsby-browser.js
```

आपके प्रोजेक्ट का फ़ाइल स्ट्रक्चर अब इस तरह दिखना चाहिए:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
├── gatsby-browser.js
```

> 💡 `gatsby-browser.js` क्या है? इस बारे में बहुत अधिक और अभी के लिए चिंता न करें, बस यह जान लें कि `gatsby-browser.js` उन मुट्ठी भर विशेष फ़ाइलों में से एक है, जो Gatsby सर्च करता है और उपयोग करता है (यदि वे मौजूद हैं)। यहां, फ़ाइल का नामकरण महत्वपूर्ण **है**। यदि आप अभी और ज्यादा एक्सप्लोर करना चाहते हैं, तो [डॉक्स](/docs/browser-apis/) देखें।

2. `gatsby-browser.js` फ़ाइल में अपनी हाल ही में बनाई गई स्टाइलशीट इम्पोर्ट करें:

```javascript:title=gatsby-browser.js
import "./src/styles/global.css"

// or:
// require('./src/styles/global.css')
```

> नोट: दोनों CommonJS (`require`) और ES मॉड्यूल (`import`) सिंटैक्स यहाँ काम करते हैं। यदि आप निश्चित नहीं हैं कि किसे चुनना है, तो `import` आमतौर पर एक अच्छा डिफ़ॉल्ट ओप्शंस है। केवल Node.js एन्वाइरन्मेंट में चलाई जाने वाली फ़ाइलों के साथ काम करने के लिए (जैसे `gatsby-node.js`), `require` का उपयोग करने की आवश्यकता होगी।

3. डेवेलपमेंट सर्वर शुरू करें:

```shell
gatsby develop
```

यदि आप ब्राउज़र में अपने प्रॉजेक्ट पर एक नज़र डालते हैं, तो आपको "हैलो वर्ल्ड" स्टार्टर पर लागू लैवेंडर बॅकग्राउंड दिखना चाहिए:

![Lavender Hello World!](global-css.png)

> नोट: ट्यूटोरियल के इस भाग मे सबसे तेज़ और सबसे सरल तरीके से Gatsby साइट को स्टाइलिंग करने पर ध्यान केंद्रित किया गया है — `gatsby-browser.js` को इस्तेमाल करके स्टैण्डर्ड सीएसएस फाइल को सीधा इम्पोर्ट कर सकते हैं।  ग्लोबल स्टाइल्स डालने का सबसे सही तरीका एक शेयर्ड लेआउट कौम्पोनॅन्ट इस्तेमाल करना है। [अधिक जानकारी के लिए डॉक्स](/docs/global-css/) देखें।

## कौम्पोनॅन्ट-स्कोप वाला सीएसएस का उपयोग करना

अब तक, हमने स्टॅंडर्ड सीएसएस स्टाइलशीट का उपयोग करने के अधिक पारंपरिक दृष्टिकोण के बारे में बात की है। अब, हम कौम्पोनॅन्ट-ओरियेनटेड तरीके से सीएसएस को संशोधित करने के विभिन्न तरीकों के बारे में बात करेंगे।

### सीएसएस मॉड्यूलस

आइए **सीएसएस मॉड्यूल** को एक्सप्लोर करें। [सीएसएस मॉड्यूल होमपेज](https://github.com/css-modules/css-modules) से:

> एक **सीएसएस मॉड्यूल** एक सीएसएस फ़ाइल है जिसमें सभी क्लास नेम्स और एनीमेशन नेम्स डिफ़ॉल्ट रूप से लोकल्ली स्कोप किए जाते हैं।

सीएसएस मॉड्यूल्स बहुत लोकप्रिय हैं क्योंकि वे आपको सीएसएस को सामान्य रूप से लिखने देते हैं लेकिन बहुत अधिक सुरक्षा के साथ। टूल्स ऑटोमेटिकली यूनीक क्लास नेम और एनीमेशन नेम जेनरेट करते हैं, इसलिए आपको सेलेक्टर नेम टकराव के बारे में चिंता करने की आवश्यकता नहीं है।

Gatsby सीएसएस मॉड्यूल के साथ बिना कुछ और सेटअप किये अपने आप काम करता है। यह दृष्टिकोण उन नए लोगों के लिए रेकमेंडेड है जो Gatsby (और सामान्य रूप से React) के साथ निर्माण करने में नये है।

#### ✋ सीएसएस मॉड्यूल का उपयोग करके एक नया पेज बनाएँ

इस अनुभाग में, आप एक नया पेज कौम्पोनॅन्ट बनाएंगे और उस पेज कौम्पोनॅन्ट को सीएसएस मॉड्यूल का उपयोग करके स्टाइल करेंगे।

सबसे पहले, एक नया 'Container' कौम्पोनॅन्ट बनाएं।

1. एक नया फोल्डर `src/components` बनाएँ और फिर, इस नये फोल्डर में, 'container.js` नाम की फ़ाइल बनाएँ और निम्नलिखित को पेस्ट करें:

```jsx:title=src/components/container.js
import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <div className={containerStyles.container}>{children}</div>
)
```

आप नोटिस करेंगे कि आपने एक कंटेनर मॉड्यूल फ़ाइल को इम्पोर्ट किया है, जिसका नाम `container.module.css` है। अब उस फाइल को बनाते हैं।

2. उसी फोल्डर (`src/components`) में, एक `container.module.css` फ़ाइल बनाएं और निम्नलिखित को कॉपी/पेस्ट करें:

```css:title=src/components/container.module.css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

आप देखेंगे कि फ़ाइल का नाम सामान्य के बजाय `.module.css` के साथ समाप्त होता है। इस तरह से आप Gatsby को बताते हैं कि इस सीएसएस फ़ाइल को सादे सीएसएस के बजाय सीएसएस मॉड्यूल के रूप में प्रोसेस्ड किया जाना चाहिए।

3. `src/pages/about-css-modules.js` पर एक फ़ाइल बनाकर एक नया पेज कौम्पोनॅन्ट बनाएँ

```jsx:title=src/pages/about-css-modules.js
import React from "react"

import Container from "../components/container"

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
)
```

अब, यदि आप `http://localhost:8000/about-css-modules/` पर जाते हैं, तो आपके पेज को कुछ इस तरह दिखना चाहिए:

![सीएसएस मॉड्यूल स्टाइल्स के साथ पेज](css-modules-basic.png)

#### ✋ सीएसएस मॉड्यूल का उपयोग करके कौम्पोनॅन्ट को स्टाइल करना

इस अनुभाग में, आप नाम, अवतार और छोटे लैटिन आत्मकथाओं वाले लोगों की एक सूची बनाएंगे। अब आप सीएसएस मॉड्यूल का उपयोग करके `<User />` कौम्पोनॅन्ट बनाएँ और उस कौम्पोनॅन्ट को स्टाइल करें।

1. सीएसएस के लिए एक नयी `src/pages/about-css-modules.module.css` फाइल बनाएँ।

2. नई फ़ाइल में निम्न पेस्ट करें:

```css:title=src/pages/about-css-modules.module.css
.user {
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
}

.user:last-child {
  margin-bottom: 0;
}

.avatar {
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
}

.description {
  flex: 1;
  margin-left: 18px;
  padding: 12px;
}

.username {
  margin: 0 0 12px 0;
  padding: 0;
}

.excerpt {
  margin: 0;
}
```

3. आपकी पहली बनाई हुई फाइल `about-css-modules.js` की शुरू की कुछ लाइन्स को एडिट करके नयी बनायीं फाइल `src/pages/about-css-modules.module.css` को इम्पोर्ट करें::

```javascript:title=src/pages/about-css-modules.js
import React from "react"
// highlight-next-line
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

// highlight-next-line
console.log(styles)
```

`console.log(styles)` कोड परिणामी इम्पोर्ट को लॉग करेगा ताकि आप अपने प्रोसेस्ड `about-css-modules.module.css` का परिणाम देख सके। यदि आप अपने ब्राउज़र में डेवलपर कंसोल (उदाहरण के लिए Firefox या Chrome के डेवलपर टूल का उपयोग करके) खोलते हैं, तो आप देखेंगे:

![कंसोल में CSS मॉड्यूल का इम्पोर्ट रिज़ल्ट](css-modules-console.png)

यदि आप अपनी सीएसएस फ़ाइल से तुलना करते हैं, आप देखेंगे की अब हर क्लास इम्पोर्टेड ऑब्जेक्ट में एक key है जो लॉन्ग स्ट्रिंग की तरफ इशारा कर रही है। उदाहरण के लिए `avatar` `src-pages----about-css-modules-module---avatar---2lRF7` की तरफ इशारा कर रहा है। सीएसएस मॉडल्स ये क्लास के नाम जनरेट करता है। वे आपकी साइट पर यूनीक होने की गारंटी देते हैं। और क्योंकि आपको क्लासस का उपयोग करने के लिए उन्हें इम्पोर्ट करना पड़ता है, इसलिए यहाँ कभी कोई सवाल नहीं है कि कुछ सीएसएस का उपयोग कहां किया जा रहा है।

4. एक नये `<User />` कौम्पोनॅन्ट  को `about-css-modules.js` पेज में इनलाइन बनाएँ। `about-css-modules.js` फाइल को एडिट करें ताकि यह निम्न की तरह दिखे:

```jsx:title=src/pages/about-css-modules.js
import React from "react"
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

console.log(styles)

// highlight-start
const User = props => (
  <div className={styles.user}>
    <img src={props.avatar} className={styles.avatar} alt="" />
    <div className={styles.description}>
      <h2 className={styles.username}>{props.username}</h2>
      <p className={styles.excerpt}>{props.excerpt}</p>
    </div>
  </div>
)
// highlight-end

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
    {/* highlight-start */}
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob Smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    {/* highlight-end */}
  </Container>
)
```

> टिप: आम तौर पर, यदि आप किसी साइट पर कई स्थानों पर एक कौम्पोनॅन्ट का उपयोग करते हैं, तो यह `components` फोल्डर में अपनी मॉड्यूल फ़ाइल में होना चाहिए। लेकिन, अगर यह केवल एक फ़ाइल में उपयोग किया जाता है, तो इसे इनलाइन बनाएं।

समाप्त पेज अब ऐसा दिखना चाहिए:

![सीएसएस मॉड्यूल के साथ उपयोगकर्ता सूची पेज](css-modules-userlist.png)

### CSS-in-JS

CSS-in-JS एक कौम्पोनॅन्ट-ओरियेनटेड स्टाइलिंग दृष्टिकोण है। ज्यादातर आम तौर पर, यह एक पैटर्न है जहां [सीएसएस जावास्क्रिप्ट का उपयोग करके इनलाइन बनाया जाता है](https://reactjs.org/docs/faq-styling.html#what-is-css-in-js)।

#### Gatsby के साथ CSS-in-JS का उपयोग करना

कई अलग-अलग CSS-in-JS लाइब्रेरीज़ हैं और उनमें से कई में पहले से ही Gatsby प्लगइन्स मौजूद हैं। हम इस प्रारंभिक ट्यूटोरियल में CSS-in-JS के एक उदाहरण को शामिल नहीं करेंगे, लेकिन हम आपको इस बात का [पता लगाने](/docs/styling/) के लिए प्रोत्साहित करते हैं कि ईकोसिस्टम के पास देने के लिए क्या है। दो लाइब्रेरीज़ के लिए मिनी-ट्यूटोरियल हैं, विशेष रूप से, [Emotion](/docs/emotion/) और [Styled Components](/docs/styled-components/)।

#### CSS-in-JS के बारे में पढ़ने के लिए सुझाव

यदि आप आगे पढ़ने में रुचि रखते हैं, तो [Christopher "vjeux" Chedeau की 2014 की प्रस्तुति देखें, जिसने इस आंदोलन को उकसाया](https://speakerdeck.com/vjeux/react-css-in-js) और साथ ही साथ [Mark Dalgleish का हाल ही का पोस्ट "A Unified Styling Language"](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660)।

### अन्य सीएसएस ऑप्शन

Gatsby लगभग हर संभव स्टाइलिंग ऑप्शन का समर्थन करता है (अगर आपके पसंदीदा सीएसएस विकल्प के लिए अभी तक कोई प्लगइन नहीं है, तो [कृपया योगदान दें!](/contributing/how-to-contribute/))

- [Typography.js](/packages/gatsby-plugin-typography/)
- [Sass](/packages/gatsby-plugin-sass/)
- [JSS](/packages/gatsby-plugin-jss/)
- [Stylus](/packages/gatsby-plugin-stylus/)
- [PostCSS](/packages/gatsby-plugin-postcss/)

और काफी सारे!

## आगे क्या आ रहा है?

अब जारी रखें [ट्यूटोरियल के भाग तीन](/tutorial/part-three/), जहां आप Gatsby प्लगइन्स और लेआउट कौम्पोनॅन्ट के बारे में जानेंगे।
