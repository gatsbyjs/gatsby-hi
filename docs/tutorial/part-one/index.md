---
title: Get to Know Gatsby Building Blocks
typora-copy-images-to: ./
disableTableOfContents: true
---

[**पिछले भाग**](/tutorial/part-zero/) में, आपने आवश्यक सॉफ़्टवेयर इनस्टॉल करके लोकल डेवेलपमेंट एन्वाइरन्मेंट तैयार किया और [**“hello world” स्टार्टर**](https://github.com/gatsbyjs/gatsby-starter-hello-world) का उपयोग करके अपना पहला Gatsby साइट बनाया। अब, उस स्टार्टर द्वारा जनरेटेड कोड के बारे में हम और गहराई से जानेंगे।

## Gatsby का उपयोग करना

[**ट्यूटोरियल के भाग शून्य**](/tutorial/part-zero/) में, आपने निम्नलिखित कमांड का उपयोग करके "hello world" स्टार्टर के आधार पर एक नई साइट बनाई थी:

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

एक नई Gatsby साइट बनाते समय, आप एक नई साइट बनाने के लिए किसी भी मौजूदा Gatsby स्टार्टर के आधार पर निम्न कमांड का उपयोग कर सकते हैं:

```shell
gatsby new [SITE_DIRECTORY_NAME] [URL_OF_STARTER_GITHUB_REPO]
```

यदि आप अंत से URL हटा देते हैं, तो Gatsby आपके लिए [**डिफ़ॉल्ट स्टार्टर**](https://github.com/gatsbyjs/gatsby-starter-default) के आधार पर ऑटोमॅटिकली आपके लिए एक साइट तैयार करेगा। ट्यूटोरियल के इस भाग के लिए, "hello world" साइट का ही प्रयोग करे जिसे आपने ट्यूटोरियल भाग शून्य में बनाया था। आप डॉक्स में [स्टार्टर मे बदलाव](/docs/modifying-a-starter) के बारे में अधिक जान सकते हैं।

### ✋ कोड खोलें

अपने कोड एडिटर में, अपने "hello world" साइट के लिए जनरेट किए गए कोड को खोलें और ‘hello-world’ फोल्डर्स में विभिन्न फोल्डर्स और फाइलों पर एक नज़र डालें। यह कुछ इस तरह दिखना चाहिए:

![Hello World project in VS Code](01-hello-world-vscode.png)

_नोट: फिर से, यहां दिखाया गया एडिटर Visual Studio Code है। यदि आप एक अलग एडिटर का उपयोग कर रहे हैं, तो यह थोड़ा अलग दिखेगा।_

आइए होमपेज के कोड पर एक नज़र डालें।

> 💡 यदि आपने पिछले खंड में `gatsby develop` को रन करने के बाद अपने डेवेलपमेंट सर्वर को स्टॉप कर दिया है, तो इसे अब फिर से स्टार्ट करें — अब hello-world साइट में कुछ बदलाव करने का समय है!

## Gatsby पेजेज के साथ परिचय

अपने कोड एडिटर में `/src` फोल्डर खोलें। उसमे एक सिंगल फोल्डर `/pages` मिलेगा।

अब `src/pages/index.js` फ़ाइल को खोलें। इस फ़ाइल में कोड एक कौम्पोनॅन्ट बनाता है जिसमें एक ही div और कुछ टेक्स्ट होता है - उचित रूप से, "Hello World!"

### ✋ “Hello World” होमपेज मे परिवर्तन करे

1. “Hello World!” टेक्स्ट को “Hello Gatsby!” में बदलें और फाइल को सेव करें। यदि आपके विंडोस अगल-बगल हैं, तो आप देख सकते हैं कि फ़ाइल को सेव करने के बाद आपके कोड और कॉंटेंट्स मे परिवर्तन लगभग तुरंत ही ब्राउज़र में दिखने लगते हैं।

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./02-demo-hot-reloading.mp4"></source>
  <p>Sorry! Your browser doesn't support this video.</p>
</video>

>💡 Gatsby आपके डेवेलपमेंट प्रोसेस को तेज करने के लिए **hot reloading** का उपयोग करता है। अनिवार्य रूप से, जब आप एक Gatsby डेवेलपमेंट सर्वर चला रहे हैं, तो Gatsby साइट फ़ाइलों को बॅकग्राउंड मे "watched" होती रहती है - जब भी आप किसी फ़ाइल को सेव करते हैं, तो आपके परिवर्तन तुरंत ब्राउज़र में दिखाई देंगे। आपको पेज को हार्ड रिफ्रेश करने या डेवेलपमेंट सर्वर को पुनः स्टार्ट करने की आवश्यकता नहीं है - आपके परिवर्तन तुरंत दिखाई देते हैं।

2. अब आप अपने बदलावों को थोड़ा और स्पष्ट कर सकते हैं। नीचे दिए गए कोड को `src/pages/index.js` में बदलने का प्रयास करें और फिर से सेव करें। आप टेक्स्ट में परिवर्तन देखेंगे - टेक्स्ट का कलर बैंगनी होगा और फ़ॉन्ट का आकार बड़ा होगा।

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
)
```

> 💡 हम ट्यूटोरियल के [**भाग दो**](/tutorial/part-two/) में Gatsby में स्टाइलिंग के बारे में अधिक जानकारी देंगे।

3. फ़ॉन्ट साइज़ स्टाइल को हटा दे, "Hello Gatsby!" टेक्स्ट को एक लेवेल वन हेडर में बदलें, और हेडर के नीचे एक पैराग्राफ डाले।


```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  {/* highlight-start */}
  <div style={{ color: `purple` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
  {/* highlight-end */}
  </div>
)
```

![More changes with hot reloading](03-more-hot-reloading.png)

4. एक इमेज डाले। (इस मामले में, Unsplash से एक रॅंडम इमेज)।

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
    {/* highlight-next-line */}
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

![Add image](04-add-image.png)

### रुकिए... हमारे Javascript में HTML?

_यदि आप React और JSX से परिचित हैं, तो इस अनुभाग को स्किप कर सकते है। यदि आपने पहले React फ्रेमवर्क के साथ काम नहीं किया है, तो आप सोच रहे होंगे कि HTML एक Javascript फ़ंक्शन में क्या कर रहा है। या हम पहली पंक्ति में `react` क्यों इम्पोर्ट कर रहे हैं, लेकिन कहीं भी इसका उपयोग नहीं कर रहे हैं। यह हाइब्रिड "HTML-in-JS" वास्तव में React के लिए Javascript का एक सिंटैक्स एक्सटेंशन है, जिसे JSX कहा जाता है। आप पूर्व अनुभव के बिना इस ट्यूटोरियल के साथ अनुसरण कर सकते हैं, लेकिन यदि आप उत्सुक हैं, तो यहां एक संक्षिप्त प्राइमर है…


आइए `src/pages/index.js` फ़ाइल की ओरिजिनल कॉंटेंट पर विचार करते है:

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

शुद्ध Javascript में, यह इस तरह दिखता है:

```javascript:title=src/pages/index.js
import React from "react"

export default () => React.createElement("div", null, "Hello world!")
```

अब आप `'react'` के इम्पोर्ट को पहचान सकते हैं! लेकिन रुकें। आप JSX लिख रहे हैं, शुद्ध HTML और Javascript नहीं। ब्राउज़र इसे कैसे पढ़ता है? संक्षिप्त उत्तर: यह नहीं पढ़ता है। Gatsby साइटें आपके सोर्स कोड को किसी ऐसी चीज़ में बदलने के लिए पहले से ही टूलिंग के साथ आती हैं, जो ब्राउज़र व्याख्या कर सकते हैं।

## कौम्पोनॅन्ट का निर्माण करना

होमपेज जो आप केवल एडिट कर रहे थे, उसे एक पेज कौम्पोनॅन्ट को परिभाषित करके बनाया गया था। वास्तव में “component” क्या है?

मोटे तौर पर परिभाषित करे तो, एक कौम्पोनॅन्ट आपकी साइट के लिए एक बिल्डिंग ब्लॉक है; यह एक सेल्फ़-कंटेंड कोड है जो UI(यूज़र इंटरफ़ेस) के एक भाग का वर्णन करता है।

Gatsby को React का उपयोग करके बनाया गया है। जब हम **कौम्पोनॅन्टस** का उपयोग करने और परिभाषित करने के बारे में बात करते हैं, तो हम वास्तव में **React कौम्पोनॅन्टस** के बारे में बात कर रहे हैं - कोड के सेल्फ़-कंटेंड टुकड़े (आमतौर पर JSX के साथ लिखे गए) जो इनपुट को स्वीकार करते हैं और UI के एक भाग का वर्णन करने वाले React एलिमेंट्स को रिटर्न करते हैं।

कौम्पोनॅन्ट का निर्माण शुरू करते समय आप जो बड़े मानसिक बदलाव करते हैं, उनमें से एक (यदि आप पहले से ही एक डेवलपर हैं) तो यह है कि अब आपके CSS, HTML, और Javascript टाइट्ली कपल्ड हैं और अक्सर एक ही फ़ाइल के भीतर ही रहते हैं।

एक साधारण बदलाव के साथ, इसमें वेबसाइटों के निर्माण के बारे में आपके विचार के गम्भीर प्रभाव हैं।

एक कस्टम बटन बनाने का उदाहरण लें। अतीत में, आप अपनी कस्टम स्टाइल्स के साथ CSS क्लास (शायद `.primary-button`) बनाएंगे और जब भी आप उन स्टाइल्स को अप्लाइ करना चाहते हैं, तब इसका उपयोग करें। उदाहरण के लिए:

```html
<button class="primary-button">Click me</button>
```

कौम्पोनॅन्ट की दुनिया में, आप अपनी बटन स्टाइल्स के साथ एक `PrimaryButton` कौम्पोनॅन्ट बनाते हैं और इसे अपनी साइट मे उपयोग करते हैं जैसे:

<!-- prettier-ignore -->
```jsx
<PrimaryButton>Click me</PrimaryButton>
```

कौम्पोनॅन्ट आपकी साइट के बेस बिल्डिंग ब्लॉक बन जाते हैं। बिल्डिंग ब्लॉक्स तक सीमित होने के बजाय ब्राउज़र जैसे `<button />` प्रदान करता है, आप आसानी से नए बिल्डिंग ब्लॉक बना सकते हैं, जो आपकी प्रॉजेक्ट्स की जरूरतों को पूरा करते हैं।

### ✋ पेज कौम्पोनॅन्ट का उपयोग करना

`src/pages/*.js` में परिभाषित कोई भी React कौम्पोनॅन्ट ऑटोमॅटिकली एक पेज बन जाएगा। आइए देखें।

आपके पास पहले से ही `src/pages/index.js` फ़ाइल है जो "Hello World" स्टार्टर के साथ आया था। चलिए about पेज बनाते है।

1. एक नई फ़ाइल `src/pages/about.js` बनाएँ, निम्न कोड को नई फ़ाइल में कॉपी करें, और सेव करें।

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div style={{ color: `teal` }}>
    <h1>About Gatsby</h1>
    <p>Such wow. Very React.</p>
  </div>
)
```

2. अब `http://localhost:8000/about/` पर जाए।

![New about page](05-about-page.png)

बस `src/Pages/about.js` फ़ाइल में एक React कौम्पोनॅन्ट डाल कर, अब आपके पास एक पेज `/about` उपलब्ध है।

### ✋ सब-कौम्पोनॅन्टस का उपयोग करना

मान लें कि होमपेज और about पेज दोनों काफी बड़े हो गए हैं और आप बहुत सारी चीजों को फिर से लिख रहे हैं। आप सब-कौम्पोनॅन्टस का उपयोग करके UI को रियूज़बल पीसस मे ब्रेक कर सकते हैं। आपके दोनों पेजेज में `<h1>` हेडर्स है - एक कौम्पोनॅन्ट बनाएं जो एक `Header`  का वर्णन करेगा।

1. `src/components` पर एक नया फोल्डर बनाएँ और उसमे एक नई फ़ाइल `header.js` बनाए।
2. निम्न कोड को नए `src/components/header.js` फ़ाइल में ऐड करें।

```jsx:title=src/components/header.js
import React from "react"

export default () => <h1>This is a header.</h1>
```

3. `about.js` फ़ाइल को एडिट करें और `Header` कौम्पोनॅन्ट को इम्पोर्ट करें। `h1` मार्कअप को `<Header />` से बदलें:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header" // highlight-line

export default () => (
  <div style={{ color: `teal` }}>
    <Header /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Adding Header component](06-header-component.png)

ब्राउज़र में, “About Gatsby” हेडर टेक्स्ट अब “This is a header.” के साथ बदल जाना चाहिए। लेकिन आप यह नहीं चाहते हैं कि “About” पेज पर “This is a header.” दिखे, आप चाहेंगे की इस पर “About Gatsby” दिखे।

4. वापस `src/components/header.js` मे जाए और निम्नलिखित परिवर्तन करें:

```jsx:title=src/components/header.js
import React from "react"

export default props => <h1>{props.headerText}</h1> {/* highlight-line */}
```

5. वापस `src/pages/about.js` मे जाए और निम्नलिखित परिवर्तन करें:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="About Gatsby" /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Passing data to header](07-pass-data-header.png)

अब आपको अपना “About Gatsby” हेडर टेक्स्ट फिर से दिखना चाहिए!

### “props” क्या है?

इससे पहले आपने React कौम्पोनॅन्ट को कोड के रियूज़बल पीसस के रूप में परिभाषित करते हुए UI के रूप मे वर्णन किया था। इन रियूज़बल पीसस को गतिशील बनाने के लिए आपको अलग-अलग डेटा के साथ सप्लाई करना होगा। आप ऐसा करते हैं "props" इनपुट के साथ। Props (उचित रूप से पर्याप्त) प्रॉपर्टीस है जिसे React कौम्पोनॅन्ट को सप्लाई की जाती है।

इम्पोर्टेड `Header` सब-कॉम्पोनेन्ट `about.js` में `headerText` prop `"About Gatsby"` वैल्यू के साथ पास किया था:

```jsx:title=src/pages/about.js
<Header headerText="About Gatsby" />
```

`header.js` में, हेडर कौम्पोनॅन्ट `headerText` prop को प्राप्त करने की उम्मीद करता है (क्योंकि आपने यह उम्मीद करने के लिए इसे लिखा है)। तो आप इसे इस तरह एक्सेस कर सकते हैं:

```jsx:title=src/components/header.js
<h1>{props.headerText}</h1>
```

> 💡 JSX में, आप किसी भी Javascript एक्सप्रेशन को `{}` के साथ रैप करके एम्बेड कर सकते हैं। इस प्रकार आप “props” ऑब्जेक्ट से `headerText` प्रॉपर्टी (या “prop!”) को एक्सेस कर सकते हैं।

यदि आपने अपने `<Header />` कौम्पोनॅन्ट मे एक और “prop” उपयोग किया है, तो...

```jsx:title=src/pages/about.js
<Header headerText="About Gatsby" arbitraryPhrase="is arbitrary" />
```

...आप `arbitraryPhrase` prop को एक्सेस कर सकते थे: `{props.arbitraryPhrase}`।

6. इस बात पर जोर देने के लिए कि कैसे आप कौम्पोनॅन्ट को फिर से उपयोग कर सकते है, एक अतिरिक्त `<Header />` कौम्पोनॅन्ट को about page मे ऐड करें, निम्न कोड को `src/pages/about.js` फ़ाइल में ऐड करें, और सेव करें।

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="About Gatsby" />
    <Header headerText="It's pretty cool" /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Duplicate header to show reusability](08-duplicate-header.png)

आखिर तुमने इसे हासिल कर ही लिया; एक दूसरा हेडर - किसी भी कोड को फिर से लिखे बिना - props द्वारा अलग-अलग डेटा पास करके।

### लेआउट कौम्पोनॅन्टस का उपयोग करना

लेआउट कौम्पोनॅन्टस उस साइट के अनुभागों के लिए हैं जिन्हें आप कई पेजेज में शेयर करना चाहते हैं। उदाहरण के लिए, Gatsby साइटों में आमतौर पर एक शेयर्ड हेडर और फुटर के साथ एक लेआउट कौम्पोनॅन्ट होगा। लेआउट में ऐड करने के लिए अन्य सामान्य चीजों में एक साइडबार और/या एक नेविगेशन मेनू शामिल है।

आप लेआउट कौम्पोनॅन्टस के बारे में [**भाग तीन**](/tutorial/part-three/) मे जानेंगे।

## पेजेज के बीच लिंकिंग

आप अक्सर पेजेज को आपस में बीच लिंक करना चाहते हैं - चलिए Gatsby साइट में राउटिंग देखते है।

### ✋ `<Link />` कौम्पोनॅन्ट का उपयोग करना

1. इंडेक्स पेज कौम्पोनॅन्ट (`src/pages/index.js`) को खोलें, Gatsby से `<Link />` कौम्पोनॅन्ट को इम्पोर्ट करें, हैडर के ऊपर एक `<Link />` कौम्पोनॅन्ट ऐड करें, और इसे `to` प्रॉपर्टी `"/concat/"` की वैल्यू के साथ पाथनेम के लिए पास करें::

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby" // highlight-line
import Header from "../components/header"

export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Contact</Link> {/* highlight-line */}
    <Header headerText="Hello Gatsby!" />
    <p>What a world.</p>
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

जब आप होमपेज मे "Contact" लिंक पर क्लिक करते हैं, तो आपको दिखना चाहिए ...

![Gatsby dev 404 page](09-dev-404.png)

... Gatsby डेवेलपमेंट 404 पेज क्यूं? क्योंकि आप उस पेज से लिंक करने का प्रयास कर रहे हैं जो अभी तक मौजूद नहीं है।

2. अब आपको अपने नए "Contact" पेज के लिए `src/pages/contact.js` मे एक पेज कौम्पोनॅन्ट बनाना होगा और इसे होमपेज पर वापस लिंक करना होगा:

```jsx:title=src/pages/contact.js
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Link to="/">Home</Link>
    <Header headerText="Contact" />
    <p>Send us a message!</p>
  </div>
)
```

फ़ाइल को सेव करने के बाद, आपको contact पेज दिखना चाहिए और होमपेज लिंक से होमपेज पर जा सकना चाहिए।

<video controls="controls" loop="true">
  <source type="video/mp4" src="./10-linking-between-pages.mp4"></source>
  <p>Sorry! Your browser doesn't support this video.</p>
</video>

Gatsby `<Link />` कौम्पोनॅन्ट आपकी साइट के पेजेज के बीच लिंक बनाने के लिए है। आपकी Gatsby साइट द्वारा नियंत्रित नहीं किए गए पेजेज के बाहरी लिंक के लिए, नियमित HTML `<a>` टैग का उपयोग करें।

## Gatsby साइट को डिप्लाय करना

Gatsby.js एक _मॉडर्न साइट जनरेटर_ है, जिसका अर्थ है कि कोई सर्वर सेटअप या जटिल डेटाबेस को डिप्लाय करने की आवश्यकता नहीं है। इसके बजाय, Gatsby `build` कमांड स्टॅटिक HTML और Javascript फ़ाइलों की एक फोल्डर का उत्पादन करता है जिसे आप एक स्थिर स्टॅटिक होस्टिंग सेवा में डिप्लाय कर सकते हैं।

अपनी पहली Gatsby वेबसाइट को डिप्लाय करने के लिए [Surge](http://surge.sh/) का उपयोग करने का प्रयास करें। Surge कई "स्टैटिक साइट होस्ट" में से एक है जो Gatsby साइटों को डिप्लाय करना संभव बनाता है।

यदि आपने इससे पहले Surge इंस्टॉल और सेटअप नहीं किया है, एक नई टर्मिनल विंडो खोलें और उनका कमांड-लाइन टूल इंस्टॉल करें:

```shell
npm install --global surge

# Then create a (free) account with them
surge login
```

इसके बाद, अपनी साइट के रूट में टर्मिनल में निम्नलिखित कमांड चलाकर अपनी साइट का निर्माण करें (टिप: सुनिश्चित करें कि आप इस कमांड को अपनी साइट के रूट पर चला रहे हैं, इस मामले में हैलो-वर्ल्ड फ़ोल्डर में, जिसे आप उसी विंडो में एक नया टैब खोल के कर सकते हैं जिसमे आप `gatsby develop` चलाते थे:

```shell
gatsby build
```

बिल्ड को १५-३० सेकंड लेना चाहिए। एक बार बिल्ड समाप्त हो जाने के बाद, अब उन फाइलों पर एक नज़र रखना दिलचस्प है जो `gatsby build` कमांड केवल डिप्लाय करने के लिए तैयार करता हैं।

अपनी साइट के रूट में टर्मिनल कमांड में निम्नलिखित टाइप करके उत्पन्न फ़ाइलों की सूची पर एक नज़र डालें, अब आपको `public` फोल्डर दिखेगा:

```shell
ls public
```

फिर आखिर में जनरेटेड फ़ाइलों को surge.sh पर पब्लिश करके अपनी साइट को डिप्लाय करें।

```shell
surge public/
```

> ध्यान दें कि आपके कमांड-लाइन इंटरफ़ेस पर `domain: some-name.surge.sh` जानकारी देखने के बाद आपको `enter` key दबानी होगी।

एक बार जब यह समाप्त हो जाता है, तो आपको अपने टर्मिनल में कुछ इस तरह से दिखना चाहिए:

![Screenshot of publishing Gatsby site with Surge](surge-deployment.png)

नीचे पंक्ति मे सूची वेब पते को खोलें (`lowly-pain.surge.sh`) और आप अपनी नई पब्लिश्ड साइट देखेंगे! बहुत अच्छे!

## ➡️ आगे क्या?

इस भाग में आपने:

- शुरुआत मे Gatsby स्टार्टर के बारे में, और उसे नए प्रोजेक्ट बनाने में इस्तेमाल कैसे करें सीखा
- JSX सिंटैक्स के बारे में सीखा
- कौम्पोनॅन्ट के बारे में सीखा
- Gatsby पेज कौम्पोनॅन्टस और सब-कौम्पोनॅन्टस के बारे में सीखा
- React “props” के बारे और React कौम्पोनॅन्टस का फिर से उपयोग कैसे करे सीखा

अब, [**अपनी साइट में स्टाइल्स को शामिल करने**](/tutorial/part-two/) के लिए टुटोरिअल पर चलें!
