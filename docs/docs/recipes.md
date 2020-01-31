---
शीर्षक: व्यंजनों
सामग्री की तालिका गहराई
: 2
---

<!-- Basic template for a Gatsby recipe:

## कार्य पूरा करने के लिए.
इसके बारे में 1-2 वाक्य। अधिक संक्षिप्त और ध्यान केंद्रित, बेहतर!

### आवश्यक शर्तें
- सिस्टम / संस्करण आवश्यकताएँ
- कार्य को सेट करने के लिए आवश्यक सब कुछ
- जिसमें नेटलिफ़ जैसी अन्य साइटों पर खाते स्थापित करना शामिल है
- देख [docs templates](/docs/docs-templates/) युक्तियाँ स्वरूपण के लिए

### दिशा-निर्देश
चरण-दर-चरण निर्देश। प्रत्येक चरण दोहराए जाने योग्य और बिंदु पर होना चाहिए। कार्य के लिए महत्वपूर्ण कुछ भी नहीं छोड़ा जाना चाहिए.

#### जीवंत उदाहरण (optional)
नुस्खा की प्रकृति के आधार पर एक जीवित उदाहरण संभव नहीं हो सकता है, जिस स्थिति में यह छोड़ना ठीक है.

### अतिरिक्त संसाधन
- ट्यूटोरियल
- डॉक्स पेज
- प्लगइन READMEs
- आदि।

See [docs templates](/docs/docs-templates/) in the contributing docs for more help.
-->

के बीच एक खुशहाल माध्यम क्रैडिंग [full-length tutorials](/tutorial/) और रेंगते हुए [docs](/docs/)? यहाँ चीजों का निर्माण करने के लिए मार्गदर्शक व्यंजनों की एक रसोई की किताब है, गैट्सबी शैली।
## 1.पेज और लेआउट

### परियोजना की संरचना

एक गैट्सबी परियोजना के अंदर, आप निम्नलिखित फ़ोल्डर या फ़ाइलों में से कुछ या सभी देख सकते हैं:

```
|-- /.cache
|-- /plugins
|-- /public
|-- /src
    |-- /pages
    |-- /templates
    |-- html.js
|-- /static
|-- gatsby-config.js
|-- gatsby-node.js
|-- gatsby-ssr.js
|-- gatsby-browser.js
```

कुछ उल्लेखनीय फाइलें और उनकी परिभाषाएँ:

- `gatsby-config.js` — प्रोजेक्ट शीर्षक, विवरण, प्लगइन्स, आदि के लिए मेटाडेटा के साथ एक गैट्सबी साइट के लिए विकल्प कॉन्फ़िगर करें।
- `gatsby-node.js` — गैट्सबी लागू करें Node.js APIs निर्माण प्रक्रिया को प्रभावित करने वाली डिफ़ॉल्ट सेटिंग्स को अनुकूलित और विस्तारित करने के लिए
- `gatsby-browser.js` — Gatsby के ब्राउज़र का उपयोग करके, ब्राउज़र को प्रभावित करने वाली डिफ़ॉल्ट सेटिंग्स को अनुकूलित और विस्तारित करें APIs
- `gatsby-ssr.js` —सर्वर-साइड रेंडरिंग को प्रभावित करने वाली डिफ़ॉल्ट सेटिंग्स को कस्टमाइज़ करने के लिए गैट्सबी के सर्वर-साइड रेंडरिंग एपीआई का उपयोग करें

#### अतिरिक्त संसाधन

- सभी सामान्य फ़ोल्डर और फ़ाइलों के दौरे के लिए, डॉक्स को पढ़ें[Gatsby's Project Structure](/docs/gatsby-project-structure/)
- सामान्य आदेशों के लिए, बाहर की जाँच करें [Gatsby CLI docs](/docs/gatsby-cli)
- इसकी जाँच पड़ताल करो [Gatsby Cheat Sheet](/docs/cheat-sheet/) एक नज़र में डाउनलोड करने योग्य जानकारी के लिए
### स्वचालित रूप से पृष्ठ बनाना

गैट्सबी कोर स्वचालित रूप से रिएक्ट घटकों को चालू करता है `src/pages`URL वाले पृष्ठों में।
उदाहरण के लिए, घटक `src/pages/index.js` तथा `src/pages/about.js` साइट के इंडेक्स पेज के लिए स्वचालित रूप से उन फ़ाइलनामों से पेज बनाए जाएंगे (`/`) तथा `/about`.

#### आवश्यक शर्तें

-ए[Gatsby site](/docs/quick-start)
- यह [Gatsby CLI](/docs/gatsby-cli) स्थापित किया गया

#### दिशा-निर्देश

1. यदि आपकी साइट में पहले से कोई नहीं है, तो `src / pages` के लिए एक निर्देशिका बनाएँ.
2. पेज डायरेक्टरी में एक कंपोनेंट फाइल जोड़ें:

```jsx:title=src/pages/about.js
import React from "react"

const AboutPage = () => (
  <main>
    <h1>लेखक के बारे में</h1>
    <p>मेरी गैट्सबी साइट पर आपका स्वागत है.</p>
  </main>
)

export default AboutPage
```

3. विकास सर्वर शुरू करने के लिए `gatsby develop` चलाएँ।
4.ब्राउज़र में अपने नए पृष्ठ पर जाएँ: <http: // localhost: 8000 / about>

#### अतिरिक्त संसाधन

- [Creating and modifying pages](/docs/creating-and-modifying-pages/)

### पृष्ठों के बीच लिंकिंग

गैट्सबी में रूटिंग `<लिंक />` घटक पर निर्भर करता है।

#### आवश्यक शर्तें

- दो पेज घटकों के साथ एक गैट्सबी साइट:`index.js` तथा`contact.js`
- द गैट्सबी `<Link />` अंग
- चलाने के लिए [Gatsby CLI] (/ डॉक्स / gatsby-cli /) `gatsby develop`

#### दिशा-निर्देश

1. अनुक्रमणिका पृष्ठ घटक (`src / Pages / index.js`) खोलें, Gatsby से` <Link /> `घटक आयात करें, शीर्ष लेख के ऊपर एक` <Link /> घटक जोड़ें, और इसे एक `to` गुण दें pathname के लिए `" / contact / "` के मान के साथ:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby"

export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Contact</Link>
    <p>क्या दुनिया है.</p>
  </div>
)
```

2.`Gatsby develop` को रन करें और इंडेक्स पेज पर जाएँ। आपके पास एक लिंक होना चाहिए जो क्लिक किए जाने पर आपको संपर्क पृष्ठ पर ले जाए!

> **Note**: Gatsby's `<Link />`घटक एक आवरण है [`@reach/router`'s Link component](https://reach.tech/router/api/Link).गैट्सबी के बारे में अधिक जानकारी के लिए `<Link />` component, consult the [API reference for `<Link />`](/docs/gatsby-link/).

### एक लेआउट घटक बनाना

रिएक्ट लेआउट घटक के साथ पृष्ठों को लपेटना आम है, जो कई पृष्ठों में मार्कअप, शैलियों और कार्यक्षमता को साझा करना संभव बनाता है।
#### आवश्यक शर्तें
- एक गैट्सबी साइट

#### दिशा-निर्देश

1.में एक लेआउट घटक बनाएँ `src/components`,जहां बाल घटकों को सहारा के रूप में पारित किया जाएगा:
```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

2. किसी पृष्ठ में लेआउट घटक को आयात और उपयोग करें:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <Link to="/contact/">Contact</Link>
    <p>क्या दुनिया है।</p>
  </Layout>
)
```

#### अतिरिक्त संसाधन
- में एक लेआउट घटक बनाएँ [tutorial part three](/tutorial/part-three/#your-first-layout-component)
- के साथ स्टाइल [Layout Components](/docs/layout-components/)

### प्रोग्राम बनाना पेजपज के साथ

आप प्रोग्राम को गणितीय रूप से 'gatsby-node.js' फ़ाइल में सहायक तरीके से बना सकते हैं, जिसे Gatsby प्रदान करता है।
#### आवश्यक शर्तें
- A [Gatsby site](/docs/quick-start)
- A `gatsby-node.js` file

#### दिशा-निर्देश

1.`Gatsby-node.js` में,` createPages` के लिए एक निर्यात जोड़ें
```javascript:title=gatsby-node.js
// highlight-start
exports.createPages = ({ actions }) => {
  // ...
}
// highlight-end
```

2. उपलब्ध कार्यों से `createPage` एक्शन को नष्ट करें ताकि इसे स्वयं कहा जा सके, और डेटा जोड़ें या प्राप्त करें

```javascript:title=gatsby-node.js
exports.createPages = ({ actions }) => {
  // highlight-start
  const { createPage } = actions
  // pull in or use whatever data
  const dogData = [
    {
      name: "Fido",
      breed: "Sheltie",
    },
    {
      name: "Sparky",
      breed: "Corgi",
    },
  ]
  // highlight-end
}
```

3. `Gatsby-node.js` में डेटा के माध्यम से लूप करें और प्रत्येक मंगलाचरण के लिए` createPage` को पथ, टेम्प्लेट, और संदर्भ (जो डेटा प्रॉपर 'पेज कॉन्टेक्स्ट में पास किया जाएगा) प्रदान करें।

```javascript:title=gatsby-node.js
exports.createPages = ({ actions }) => {
  const { createPage } = actions

  const dogData = [
    {
      name: "Fido",
      breed: "Sheltie",
    },
    {
      name: "Sparky",
      breed: "Corgi",
    },
  ]
  // highlight-start
  dogData.forEach(dog => {
    createPage({
      path: `/${dog.name}`,
      component: require.resolve(`./src/templates/dog-template.js`),
      context: { dog },
    })
  })
  // highlight-end
}
```

4.अपने पृष्ठ के लिए टेम्पलेट के रूप में सेवा करने के लिए एक प्रतिक्रिया घटक बनाएँ जो `createPage` में उपयोग किया गया था

```jsx:title=src/templates/dog-template.js
import React from "react"

export default ({ pageContext: { dog } }) => (
  <section>
    {dog.name} - {dog.breed}
  </section>
)
```

5. अपने द्वारा बनाए गए पृष्ठों को प्रदर्शित करने के लिए `gatsby develop` को चलाएं और आपके द्वारा बनाए गए पृष्ठों में से एक के पथ पर नेविगेट करें (जैसे <http: // localhost: 8000 / Fido>)।

#### अतिरिक्त संसाधन

- पर ट्यूटोरियल अनुभाग [programmatically creating pages from data](/tutorial/part-seven/)
- संदर्भ गाइड पर [using Gatsby without GraphQL](/docs/using-gatsby-without-graphql/)
- [Example repo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-createPage) इस नुस्खे के लिए
## 2. सीएसएस के साथ स्टाइल

आपकी वेबसाइट पर शैलियों को जोड़ने के कई तरीके हैं; Gatsby आधिकारिक और सामुदायिक प्लगइन्स के माध्यम से लगभग हर संभव विकल्प का समर्थन करता है।

### लेआउट घटक के बिना वैश्विक सीएसएस फ़ाइलों का उपयोग करना
#### आवश्यक शर्तें

- एक मौजूदा [Gatsby site](/docs/quick-start/) एक सूचकांक पृष्ठ घटक के साथ
- A `gatsby-browser.js` file

#### दिशा-निर्देश

1. के रूप में एक वैश्विक सीएसएस फ़ाइल बनाएँ `src/styles/global.css` और फ़ाइल में निम्नलिखित पेस्ट करें:

```css:title=src/styles/styles/global.css
html {
  background-color: lavenderblush;
}

p {
  color: maroon;
}
```

2. निम्नलिखित के रूप में `gatsby-browser.js` फ़ाइल में वैश्विक सीएसएस फ़ाइल आयात करें:

```javascript:gatsby-browser.js
import "./src/styles/global.css"
```

> **Note:**आप इसका उपयोग भी कर सकते हैं`require('./src/styles/global.css')`अपने में वैश्विक सीएसएस फ़ाइल आयात करने के लिए `gatsby-config.js` फ़ाइल।

3.अपनी साइट पर लागू की जा रही वैश्विक स्टाइल का निरीक्षण करने के लिए `gatsby-develop` चलाएँ।

> **Note:** यह दृष्टिकोण सबसे अच्छा फिट नहीं है यदि आप अपनी साइट को स्टाइल करने के लिए CSS-in-JS का उपयोग कर रहे हैं, तो उस स्थिति में सभी साझा घटकों के साथ एक लेआउट पृष्ठ का उपयोग किया जाना चाहिए। यह अगली रेसिपी में शामिल है।
#### अतिरिक्त संसाधन
- अधिक [adding global styles without a layout component](/docs/global-css/#adding-global-styles-without-a-layout-component)

### एक लेआउट घटक में वैश्विक शैलियों का उपयोग करना

#### आवश्यक शर्तें

- A [Gatsby site](/docs/quick-start/) एक सूचकांक पृष्ठ घटक के साथ

#### Directions

आप वैश्विक शैलियों को जोड़ सकते हैं [shared layout component](/tutorial/part-three/#your-first-layout-component). इस घटक का उपयोग उन चीज़ों के लिए किया जाता है, जो पूरे देश में आम हैं, जैसे हेडर या फुटर।
1.यदि आपके पास पहले से एक नहीं है, तो अपनी साइट पर `/ src / Components` में एक नई निर्देशिका बनाएं।
2.घटक निर्देशिका के अंदर, दो फाइलें बनाएं: `लेआउट.एससीएस` और` लेआउट.जेएस`।
3. निम्नलिखित को `layout.css` में जोड़ें:

```css:title=/src/components/layout.css
body {
  background: red;
}
```

4. CSS फ़ाइल और आउटपुट लेआउट मार्कअप आयात करने के लिए `layout.js` संपादित करें:

```jsx:title=/src/components/layout.js
import React from "react"
import "./layout.css"

export default ({ children }) => <div>{children}</div>
```

5. अब अपनी साइट के होमपेज को `/ src / पेज / index.js` पर संपादित करें और नए लेआउट घटक का उपयोग करें:

```jsx:title=/src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Hello world!</Layout>
```

#### अतिरिक्त संसाधन

- [Standard Styling with Global CSS Files](/docs/global-css/)
- [More about layout components](/tutorial/part-three)

### स्टाइल घटकों का उपयोग करना

#### आवश्यक शर्तें

- A [Gatsby site](/docs/quick-start/) एक सूचकांक पृष्ठ घटक के साथ
- [gatsby-plugin-styled-components, styled-components, and babel-plugin-styled-components](/packages/gatsby-plugin-styled-components/) में स्थापित `package.json`

#### दिशा-निर्देश

1. अपने `gatsby-config.js` फ़ाइल ऐड के अंदर `gatsby-plugin-styled-components`

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

2.सूचकांक पृष्ठ घटक खोलें(`src/pages/index.js`)  और `styled-components` पैकेज का आयात करें 

3. प्रत्येक तत्व प्रकार के लिए शैली ब्लॉक बनाकर शैली घटक

4. JSX में स्टाइल घटकों को शामिल करके पृष्ठ पर लागू करें

```jsx:title=src/pages/index.js
import React from "react"
import styled from "styled-components" //highlight-line

const Container = styled.div`
  margin: 3rem auto;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`

const Avatar = styled.img`
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
`

const Username = styled.h2`
  margin: 0 0 12px 0;
  padding: 0;
`

const User = props => (
  <>
    <Avatar src={props.avatar} alt={props.username} />
    <Username>{props.username}</Username>
  </>
)

export default () => (
  <Container>
    <h1>About Styled Components</h1>
    <p>Styled Components is cool</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
    />
  </Container>
)
```

4. परिवर्तनों को देखने के लिए `gatsby develop` को चलाएं

#### अतिरिक्त संसाधन

- [More on Using Styled Components](/docs/styled-components/)
- [Egghead lesson](https://egghead.io/lessons/gatsby-style-gatsby-sites-with-styled-components)

### सीएसएस मॉड्यूल का उपयोग करना

#### आवश्यक शर्तें
- एक मौजूदा[Gatsby site](/docs/quick-start/)एक सूचकांक पृष्ठ घटक के साथ

#### दिशा-निर्देश

1. के रूप में एक सीएसएस मॉड्यूल बनाएँ `src/pages/index.module.css` और मॉड्यूल में निम्नलिखित पेस्ट करें:

```css:title=src/components/index.module.css
.feature {
  margin: 2rem auto;
  max-width: 500px;
}
```

2.CSS मॉड्यूल को JSX ऑब्जेक्ट `style` के रूप में पेज को संशोधित करके` index.js` फ़ाइल में आयात करें ताकि यह निम्न प्रकार दिखाई दे:

```jsx:title=src/pages/index.js
import React from "react"

// highlight-start
import style from "./index.module.css"

export default () => (
  <section className={style.feature}>
    <h1>Using CSS Modules</h1>
  </section>
)
// highlight-end
```

3.परिवर्तनों को देखने के लिए `gatsby develop` को चलाएं।

**Note:**
ध्यान दें कि फ़ाइल एक्सटेंशन `.module.css` की जगह` .css` है, जो कि Gatsby को बताता है कि यह एक CSS मॉड्यूल है.

#### अतिरिक्त संसाधन

- More on [Using CSS Modules](/tutorial/part-two/#css-modules)
- [Live example on Using CSS modules](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-css-modules)

### Sass / SCSS का उपयोग करना

Sass CSS का एक विस्तार है जो आपको नेस्टेड नियम, चर, मिश्रण, और अधिक जैसी उन्नत सुविधाएँ प्रदान करता है।

Sass में 2 सिंटैक्स हैं। सबसे अधिक इस्तेमाल किया जाने वाला वाक्यविन्यास "SCSS" है, और CSS का एक सुपरसेट है। इसका मतलब है कि सभी वैध CSS सिंटैक्स, मान्य SCSS सिंटैक्स है। SCSS फाइलें एक्सटेंशन .scss का उपयोग करती हैं

सैस आपके लिए .scs और .sass फ़ाइलों को .css फ़ाइलों को संकलित करेगा, इसलिए आप अपनी स्टाइलशीट को और अधिक उन्नत सुविधाओं के साथ लिख सकते हैं।

#### Prerequisites

- A [Gatsby site](/docs/quick-start/).

#### दिशा-निर्देश

1. Gatsby प्लगइन स्थापित करें [gatsby-plugin-sass](https://www.gatsbyjs.org/packages/gatsby-plugin-sass/) and `node-sass`.

`npm install --save node-sass gatsby-plugin-sass`

2. अपने में प्लगइन को शामिल करें `gatsby-config.js` फ़ाइल।

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```
3. अपने स्टाइलशीट को `.sass` या` .scss` फ़ाइलों के रूप में लिखें और उन्हें आयात करें। यदि आप शैलियों को आयात करना नहीं जानते हैं, तो देख लें [Styling with CSS](/docs/recipes/#2-styling-with-css)

```css:title=styles.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```css:title=styles.sass
$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

```javascript
import "./styles.scss"
import "./styles.sass"
```

_Note: आप Sass / SCSS फ़ाइलों को मॉड्यूल के रूप में भी उपयोग कर सकते हैं, जैसे कि CSS मॉड्यूल के बारे में पिछली रेसिपी में उल्लेख किया गया है, इस अंतर के साथ कि .css के बजाय एक्सटेंशन को .scs या .sass होना चाहिए।

#### अतिरिक्त संसाधन

- [Difference between .sass and .scss](https://responsivedesign.is/articles/difference-between-sass-and-scss/)
- [Sass guide from the official Sass website](https://sass-lang.com/guide)
- [A more complete installation tutorial on Sass with some more explanations and more resources](https://www.gatsbyjs.org/docs/sass/)

### एक स्थानीय फ़ॉन्ट जोड़ना

#### आवश्यक शर्तें

- A [Gatsby site](/docs/quick-start/)
- A font file: `.woff2`, `.ttf`, etc.

#### दिशा-निर्देश

1. अपने गैट्सबी प्रोजेक्ट में एक फ़ॉन्ट फ़ाइल की प्रतिलिपि बनाएँ, जैसे कि `src/fonts/fontname.woff2`.

```
src/fonts/fontname.woff2
```

2. इसे अपनी Gatsby साइट में बंडल करने के लिए एक CSS फ़ाइल में फ़ॉन्ट संपत्ति आयात करें:

```css:title=src/css/typography.css
@font-face {
  font-family: "Font Name";
  src: url("../fonts/fontname.woff2");
}
```

**Note:** सुनिश्चित करें कि फ़ॉन्ट का नाम प्रासंगिक CSS से संदर्भित है, उदा .:

```css:title=src/components/layout.css
body {
  font-family: "Font Name", sans-serif;
}
```

HTML `body` तत्व को लक्षित करके, आपका फ़ॉन्ट पृष्ठ के अधिकांश पाठ पर लागू होगा। अतिरिक्त सीएसएस अन्य तत्वों को लक्षित कर सकता है, जैसे `button` या` textarea`।

यदि फोंट ऊपर दिए गए चरणों का अद्यतन नहीं कर रहे हैं, तो प्रासंगिक फॉन्ट-परिवार को प्रासंगिक सीएसएस में बदलना सुनिश्चित करें।

#### अतिरिक्त संसाधन

- More on [importing assets into files](/docs/importing-assets-into-files/)

### Emotion का उपयोग करना

[Emotion](https://emotion.sh) एक शक्तिशाली CSS-IN_JSS लाइब्रेरी है जो इनलाइन CSS styles और स्टाइल घटकों दोनों का समर्थन करता है। आप प्रत्येक स्टाइलिंग सुविधा को व्यक्तिगत रूप से या एक साथ एक ही फ़ाइल में उपयोग कर सकते हैं।

#### आवश्यक शर्तें

- A [Gatsby site](/docs/quick-start)

#### दिशा-निर्देश

1.स्थापित करें[Gatsby Emotion plugin](/packages/gatsby-plugin-emotion/) and Emotion packages.

```shell
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

2. `Gatsby-plugin-emotion` प्लगइन को अपने` gatsby-config.js` फ़ाइल में जोड़ें:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

3. यदि आपके पास पहले से कोई नहीं है, तो अपनी Gatsby साइट पर एक पेज बनाएँ `src/pages/emotion-sample.js`.


आयात Emotion's `css` core package.आप तब उपयोग कर सकते हैं`css` prop to add [Emotion object styles](https://emotion.sh/docs/object-styles)एक घटक के अंदर किसी भी तत्व के लिए:

```jsx:title=src/pages/emotion-sample.js
import React from "react"
import { css } from "@emotion/core"

export default () => (
  <div>
    <p
      css={{
        background: "pink",
        color: "blue",
      }}
    >
      This page is using Emotion.
    </p>
  </div>
)
```

4. Emotions's का उपयोग करने के लिए [styled components](https://emotion.sh/docs/styled), पैकेज आयात करें और उन्हें `style` फ़ंक्शन का उपयोग करके परिभाषित करें।

```jsx:title=src/pages/emotion-sample.js
import React from "react"
import styled from "@emotion/styled"

const Content = styled.div`
  text-align: center;
  margin-top: 10px;
  p {
    font-weight: bold;
  }
`

export default () => (
  <Content>
    <p>This page is using Emotion.</p>
  </Content>
)
```

#### अतिरिक्त संसाधन

- [Using Emotion in Gatsby](/docs/emotion/)
- [Emotion website](https://emotion.sh)
- [Getting started with Emotion and Gatsby](https://egghead.io/lessons/gatsby-getting-started-with-emotion-and-gatsby)

### Google फ़ॉन्ट्स का उपयोग करना

स्थानीय रूप से एक परियोजना के भीतर अपने [Google फ़ॉन्ट्स] (https://fonts.google.com/) को होस्ट करने का अर्थ है कि जब आपकी साइट लोड होती है, तो आपकी साइट के गति सूचकांक को ~ 300 तक बढ़ाकर उन्हें नेटवर्क पर लाना नहीं पड़ेगा। डेस्कटॉप पर मिलीसेकंड और 3 जी पर 1 सेकंड। यह कस्टम फ़ॉन्ट उपयोग को केवल प्रदर्शन के लिए आवश्यक करने के लिए सीमित करने की भी सिफारिश की गई है।

#### आवश्यक शर्तें

- A [Gatsby site](/docs/quick-start)
-[Gatsby CLI] (/docs/ gatsby-cli /) स्थापित
- से एक फॉन्ट पैकेज चुनना [the typefaces project](https://github.com/KyleAMathews/typefaces)

#### दिशा-निर्देश

1. इसे चलाओ `npm install --save typeface-your-chosen-font`, जगह `your-chosen-font` wउस फ़ॉन्ट के नाम के साथ जिसे आप इंस्टॉल करना चाहते हैं [the typefaces project](https://github.com/KyleAMathews/typefaces).

लोकप्रिय 'सोर्स सेन्स प्रो' फ़ॉन्ट को लोड करने के लिए एक उदाहरण होगा: `npm install --save typeface-source-sans-pro`.

2. जोड़ना `import "typeface-your-chosen-font"`एक लेआउट टेम्पलेट, पेज घटक, या`gatsby-browser.js`.

```jsx:title=src/components/layout.js
import "typeface-your-chosen-font"
```

3. एक बार जब यह आयात हो जाता है, तो आप CSS स्टाइलशीट, CSS Module या CSS-in-JS. में फ़ॉन्ट नाम का संदर्भ दे सकते हैं।

```css:title=src/components/layout.css
body {
  font-family: "Your Chosen Font";
}
```

_NOTE: तो उपरोक्त उदाहरण के लिए, प्रासंगिक सीएसएस घोषणा होगी `font-family: 'Source Sans Pro';`_

#### अतिरिक्त संसाधन

- [Typography.js](/docs/typography-js/) - एक Gatsby साइट पर Google फोंट का उपयोग करने का दूसरा विकल्प
- [The Typefaces Project Docs](https://github.com/KyleAMathews/typefaces/blob/master/README.md)
- [Live example on Kyle Mathews' blog](https://www.bricolage.io/typefaces-easiest-way-to-self-host-fonts/)

## 3.शुरुआत के साथ काम करना

[Starters](/docs/starters/) are boilerplate Gatsby sites maintained officially, or by the community.

### स्टार्टर का उपयोग करना

#### पूर्वापेक्षाएँ

- The [Gatsby CLI](/docs/gatsby-cli) स्थापित किया गया

#### दिशा-निर्देश

1. वह स्टार्टर ढूंढें जिसका आप उपयोग करना चाहते हैं। (_The [Starter Library](/starters/?v=2) देखने के लिए एक अच्छी जगह है! _) 

2. स्टार्टर के आधार पर एक नई साइट बनाएं। टर्मिनल में, चलाएं: 

```shell
gatsby new {अपने-परियोजना के नाम} {लिंक करने के लिए स्टार्टर}
```

> _Don't run the above command as-is -- remember to replace {your-project-name} and {link-to-starter}!_

3. अपनी नई साइट चलाएं:

```shell
cd {अपने-परियोजना के नाम}
gatsby develop
```

#### अतिरिक्त संसाधन

- Gatsby शुरुआत का उपयोग करने पर एक [more detailed guide](/docs/starters/)का पालन करें।

-जानें कि कैसे उपयोग करें [Gatsby CLI](/docs/gatsby-cli) में शुरुआत का उपयोग करने के लिए उपकरण [tutorial part one](/tutorial/part-one/#using-gatsby-starters)
- ब्राउज़ करें [Starter Library](/starters/?v=2)
- Gatsby की जाँच करें [official default starter](https://github.com/gatsbyjs/gatsby-starter-default)

## 4. थीम के साथ काम करना

एक Gatsby विषय अमूर्त Gatsby विन्यास (साझा कार्यक्षमता, डेटा सोर्सिंग, डिज़ाइन) को एक संस्थापित पैकेज में देता है। इसका मतलब यह है कि कॉन्फ़िगरेशन और कार्यक्षमता सीधे आपकी परियोजना में नहीं लिखी गई है, बल्कि संस्करण, केंद्रीय रूप से प्रबंधित, और एक निर्भरता के रूप में स्थापित है। आप मूल रूप से एक विषय को अपडेट कर सकते हैं, एक साथ विषयों की रचना कर सकते हैं, और यहां तक कि दूसरे के लिए एक संगत विषय को स्वैप कर सकते हैं।

- आगे पढ़ें [What is a Gatsby Theme?](/docs/themes/what-are-gatsby-themes)

### थीम स्टार्टर का उपयोग करके एक नई साइट बनाना

किसी विषय को कॉन्फ़िगर करने वाले स्टार्टर के आधार पर साइट बनाना उसी प्रक्रिया का अनुसरण करता है जैसे स्टार्टर के आधार पर साइट बनाना जो ** थीम को कॉन्फ़िगर नहीं करता है। इस उदाहरण में आप उपयोग कर सकते हैं 
[starter for creating a new site that uses the official Gatsby blog theme](https://github.com/gatsbyjs/gatsby-starter-blog-theme).

#### आवश्यक शर्तें

- [Gatsby CLI](/docs/gatsby-cli) स्थापित

#### दिशा-निर्देश

1. ब्लॉग थीम स्टार्टर के आधार पर एक नई साइट बनाएं:

```shell
gatsby new {your-project-name} https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

2. अपनी नई साइट चलाएं:

```shell
cd {your-project-name}
gatsby develop
```

#### अतिरिक्त संसाधन

- में मौजूदा गैट्सबी थीम का उपयोग करना सीखें [shorter conceptual guide](/docs/themes/using-a-gatsby-theme) या अधिक विस्तृत [step-by-step tutorial](/tutorial/using-a-theme).

### एक नए विषय का निर्माण

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-the-gatsby-theme-workspace-starter-to-begin-building-a-new-theme"
  lessonTitle="एक नए थीम का निर्माण शुरू करने के लिए गैट्सबी थीम वर्कस्पेस स्टार्टर का उपयोग करें"
/>

####आवश्यक शर्तें

- The [Gatsby CLI](/docs/gatsby-cli)स्थापित

* [Yarn](https://yarnpkg.com/lang/en/docs/install/#mac-stable) स्थापित

#### दिशा-निर्देश

1.का उपयोग कर एक नया विषय कार्यक्षेत्र उत्पन्न करें [Gatsby theme workspace starter](https://github.com/gatsbyjs/gatsby-starter-theme-workspace):

```shell
gatsby new {your-project-name} https://github.com/gatsbyjs/gatsby-starter-theme-workspace
```

2. कार्यस्थान में उदाहरण साइट चलाएँ:

```shell
yarn workspace example develop
```

#### अतिरिक्त संसाधन

-एक का पालन करें [more detailed guide](/docs/themes/building-themes/) Gatsby विषय कार्यक्षेत्र स्टार्टर का उपयोग करने पर।
- में अपनी खुद की थीम बनाने का तरीका जानें [Gatsby Theme Authoring video course on Egghead](https://egghead.io/courses/gatsby-theme-authoring), or in the [video course's complementary written tutorial companion](/tutorial/building-a-theme).

## 5. सोर्सिंग डेटा

Gatsby में डेटा सोर्सिंग प्लगइन-चालित है; स्रोत प्लगइन्स अपने स्रोत से डेटा प्राप्त करते हैं (उदा। `Gatsby-source-filesystem` प्लगइन फ़ाइल सिस्टम से डेटा प्राप्त करता है,` gatsby-source-wordpress` प्लगइन WordPress API, आदि से डेटा प्राप्त करता है)। आप डेटा को खुद भी सोर्स कर सकते हैं।

### GraphQL में डेटा जोड़ना

Gatsby की [GraphQL data layer](/docs/querying-with-graphql/) नोड्स का उपयोग डेटा के मॉडल विखंडन के लिए करती है। गैट्सबी स्रोत प्लगइन्स स्रोत नोड जोड़ते हैं जिन्हें आप क्वेरी कर सकते हैं, लेकिन आप स्वयं स्रोत नोड भी बना सकते हैं। अपने आप को GraphQl डेटा लेयर में कस्टम डेटा जोड़ने के लिए, गैट्सबी उन तरीकों को प्रदान करता है जिनका आप लाभ उठा सकते हैं।
यह नुस्खा आपको दिखाता है कि कस्टम डेटा का उपयोग कैसे किया जाए `createNode()`.

#### दिशा-निर्देश

1.`Gatsby-node.js` में डेटा को क्वेरी करने में सक्षम होने के लिए नोड्स बनाने और निर्यात करने के लिए` sourceNodes () `और` क्रियाएँ.createNode () `का उपयोग करें।

```javascript:title=gatsby-node.js
exports.sourceNodes = ({ actions, createNodeId, createContentDigest }) => {
  const pokemons = [
    { name: "Pikachu", type: "electric" },
    { name: "Squirtle", type: "water" },
  ]

  pokemons.forEach(pokemon => {
    const node = {
      name: pokemon.name,
      type: pokemon.type,
      id: createNodeId(`Pokemon-${pokemon.name}`),
      internal: {
        type: "Pokemon",
        contentDigest: createContentDigest(pokemon),
      },
    }
    actions.createNode(node)
  })
}
```

2. इसे चलाओ `gatsby develop`.

   > _Note: `Gatsby-node.js` में परिवर्तन करने के बाद, आपको प्रभावी होने के लिए बदलावों के लिए` gatsby develop` को फिर से चलाना होगा ।_

3. Query the data (in GraphiQL or in your components).

```graphql
query MyPokemonQuery {
  allPokemon {
    nodes {
      name
      type
      id
    }
  }
}
```

#### अतिरिक्त संसाधन

- Walk through an example using the `gatsby-source-filesystem` plugin in [tutorial part five](/tutorial/part-five/#source-plugins)
- Search available source plugins in the [Gatsby library](/plugins/?=source)
- Understand source plugins by building one in the [Pixabay source plugin tutorial](/docs/pixabay-source-plugin-tutorial/)
- The createNode function [documentation](/docs/actions/#createNode)

### Sourcing Markdown data for blog posts and pages with GraphQL

You can source Markdown data and use Gatsby's [`createPages` API](/docs/actions/#createPage) to create pages dynamically.

This recipe shows how to create pages from Markdown files on your local filesystem using Gatsby's GraphQL data layer.

#### Prerequisites

- A [Gatsby site](/docs/quick-start) with a `gatsby-config.js` file
- The [Gatsby CLI](/docs/gatsby-cli) installed
- The [gatsby-source-filesystem plugin](/packages/gatsby-source-filesystem) installed
- The [gatsby-transformer-remark plugin](/packages/gatsby-transformer-remark) installed
- A `gatsby-node.js` file

#### Directions

1. In `gatsby-config.js`, configure `gatsby-transformer-remark` along with `gatsby-source-filesystem` to pull in Markdown files from a source folder. This would be in addition to any previous `gatsby-source-filesystem` entries, such as for images:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `content`,
        path: `${__dirname}/src/content`,
      },
    },
  ]
```

2. Add a Markdown post to `src/content`, including frontmatter for the title, date, and path, with some initial content for the body of the post:

```markdown:title=src/content/my-first-post.md
---
title: My First Post
date: 2019-07-10
path: /my-first-post
---

This is my first Gatsby post written in Markdown!
```

3. Start up the development server with `gatsby develop`, navigate to the GraphiQL explorer at <http://localhost:8000/___graphql>, and write a query to get all markdown data:

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        frontmatter {
          path
        }
      }
    }
  }
}
```

<iframe
  title="Query for all markdown"
  src="https://q4xpb.sse.codesandbox.io/___graphql?explorerIsOpen=false&query=%7B%0A%20%20allMarkdownRemark%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D"
  width="600"
  height="300"
/>

4. Add the JavaScript code to generate pages from Markdown posts at build time by copying the GraphQL query into `gatsby-node.js` and looping through the results:

```js:title=gatsby-node.js
const path = require(`path`)

exports.createPages = async ({ actions, graphql }) => {
  const { createPage } = actions

  const result = await graphql(`
    {
      allMarkdownRemark {
        edges {
          node {
            frontmatter {
              path
            }
          }
        }
      }
    }
  `)
  if (result.errors) {
    console.error(result.errors)
  }

  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.frontmatter.path,
      component: path.resolve(`src/templates/post.js`),
    })
  })
}
```

5. Add a post template in `src/templates`, including a GraphQL query for generating pages dynamically from Markdown content at build time:

```jsx:title=src/templates/post.js
import React from "react"
import { graphql } from "gatsby"

export default function Template({ data }) {
  const { markdownRemark } = data // data.markdownRemark holds your post data
  const { frontmatter, html } = markdownRemark
  return (
    <div className="blog-post">
      <h1>{frontmatter.title}</h1>
      <h2>{frontmatter.date}</h2>
      <div
        className="blog-post-content"
        dangerouslySetInnerHTML={{ __html: html }}
      />
    </div>
  )
}

export const pageQuery = graphql`
  query($path: String!) {
    markdownRemark(frontmatter: { path: { eq: $path } }) {
      html
      frontmatter {
        date(formatString: "MMMM DD, YYYY")
        path
        title
      }
    }
  }
`
```

6. Run `gatsby develop` to restart the development server. View your post in the browser: <http://localhost:8000/my-first-post>

#### अतिरिक्त संसाधन

- [Tutorial: Programmatically create pages from data](/tutorial/part-seven/)
- [Creating and modifying pages](/docs/creating-and-modifying-pages/)
- [Adding Markdown pages](/docs/adding-markdown-pages/)
- [Guide to creating pages from data programmatically](/docs/programmatically-create-pages-from-data/)
- [Example repo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-sourcing-markdown) for this recipe

### Sourcing from WordPress

#### Prerequisites

- An existing [Gatsby site](/docs/quick-start/) with a `gatsby-config.js` and `gatsby-node.js` file
- A WordPress instance, either self-hosted or on Wordpress.com

#### Directions

1. Install the `gatsby-source-wordpress` plugin by running the following command:

```shell
npm install gatsby-source-wordpress --save
```

2. Configure the plugin by modifying the `gatsby-config.js` file such that it includes the following:

```javascript:title=gatsby-config.js
module.exports = {
  ...
  plugins: [
    {
      resolve: `gatsby-source-wordpress`,
      options: {
        // baseUrl will need to be updated with your WordPress source
        baseUrl: `wpexample.com`,
        protocol: `https`,
        // is it hosted on wordpress.com, or self-hosted?
        hostingWPCOM: false,
        // does your site use the Advanced Custom Fields Plugin?
        useACF: false
      }
    },
  ]
}
```

> **Note:** Refer to the [`gatsby-source-wordpress` plugin docs](/packages/gatsby-source-wordpress/?=wordpre#how-to-use) to know more about configuring your plugins.

3. Create a template component such as `src/templates/post.js` with the following code in it:

```javascript:title=post.js
import React, { Component } from "react"
import { graphql } from "gatsby"
import PropTypes from "prop-types"

class Post extends Component {
  render() {
    const post = this.props.data.wordpressPost

    return (
      <>
        <h1>{post.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.content }} />
      </>
    )
  }
}

Post.propTypes = {
  data: PropTypes.object.isRequired,
  edges: PropTypes.array,
}

export default Post

export const pageQuery = graphql`
  query($id: String!) {
    wordpressPost(id: { eq: $id }) {
      title
      content
    }
  }
`
```

4. Create dynamic pages for your WordPress posts by pasting the following sample code in `gatsby-node.js`:

```javascript:title=gatsby-node.js
const path = require(`path`)
const slash = require(`slash`)

exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions

  // query content for WordPress posts
  const result = await graphql(`
    query {
      allWordpressPost {
        edges {
          node {
            id
            slug
          }
        }
      }
    }
  `)

  const postTemplate = path.resolve(`./src/templates/post.js`)
  result.data.allWordpressPost.edges.forEach(edge => {
    createPage({
      // `path` will be the url for the page
      path: edge.node.slug,
      // specify the component template of your choice
      component: slash(postTemplate),
      // In the ^template's GraphQL query, 'id' will be available
      // as a GraphQL variable to query for this posts's data.
      context: {
        id: edge.node.id,
      },
    })
  })
}
```

5. Run `gatsby-develop` to see the newly generated pages and navigate through them.

6. Open the `GraphiQL IDE` at `localhost:8000/__graphql` and open the Docs or Explorer to observe the queryable fields for `allWordpressPosts`.

The dynamic pages created above in `gatsby-node.js` have unique paths for navigating to particular posts, using a template component for the posts and a sample GraphQL query to source WordPress post content.

#### अतिरिक्त संसाधन

- [Getting Started with WordPress and Gatsby](/blog/2019-04-26-how-to-build-a-blog-with-wordpress-and-gatsby-part-1/)
- More on [Sourcing from WordPress](/docs/sourcing-from-wordpress/)
- [Live example on Sourcing from WordPress](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-wordpress)

### Sourcing data from Contentful

#### Prerequisites

- A [Gatsby site](/docs/quick-start/)
- A [Contentful account](https://www.contentful.com/)
- The [Contentful CLI](https://www.npmjs.com/package/contentful-cli) installed

#### Directions

1. Log in to Contentful with the CLI and follow the steps. It will help you create an account if you don't have one.

```shell
contentful login
```

2. Create a new space if you don't already have one. Make sure to save the space ID given to you at the end of the command. If you already have a Contentful space and space ID, you can skip steps 2 and 3.

Note: for new accounts, you can overwrite the default onboarding space. Check to see the [spaces included with your account](https://app.contentful.com/account/profile/space_memberships).

```shell
contentful space create --name 'Gatsby example'
```

3. Seed the new space with example blog content using the new space ID returned from the previous command, in place of `<space ID>`.

```shell
contentful space seed -s '<space ID>' -t blog
```

For example, with a space ID in place: `contentful space seed -s '22fzx88spbp7' -t blog`

4. Create a new access token for your space. Remember this token, as you will need it in step 6.

```shell
contentful space accesstoken create -s '<space ID>' --name 'Example token'
```

5. Install the `gatsby-source-contentful` plugin in your Gatsby site:

```shell
npm install --save gatsby-source-contentful
```

6. Edit the file `gatsby-config.js` and add the `gatsby-source-contentful` to the `plugins` array to enable the plugin. You should strongly consider using [environment variables](/docs/environment-variables/) to store your space ID and token for security purposes.

```javascript:title=gatsby-config.js
plugins: [
   // add to array along with any other installed plugins
   // highlight-start
   {


    resolve: `gatsby-source-contentful`,
    options: {
      spaceId: `<space ID>`, // or process.env.CONTENTFUL_SPACE_ID
      accessToken: `<access token>`, // or process.env.CONTENTFUL_TOKEN
    },
  },
  // highlight-end
],
```

7. Run `gatsby develop` and make sure the site compiled successfully.

8. Query data with the [GraphiQL editor](/docs/introducing-graphiql/) at <https://localhost:8000/___graphql>. The Contentful plugin adds several new node types to your site, including every content type in your Contentful website. Your example space with a "Blog Post" content type produces a `allContentfulBlogPost` node type in GraphQL.

![the graphql interface, with a sample query outlined below](./images/recipe-sourcing-contentful-graphql.png)

To query for Blog Post titles from Contentful, use the following GraphQL query:

```graphql
{
  allContentfulBlogPost {
    edges {
      node {
        title
      }
    }
  }
}
```

Contentful nodes also include several metadata fields like `createdAt` or `node_locale`.

9. To show a list of links to the blog posts, create a new file in `/src/pages/blog.js`. This page will display all posts, sorted by updated date.

```jsx:title=src/pages/blog.js
import React from "react"
import { graphql, Link } from "gatsby"

const BlogPage = ({ data }) => (
  <div>
    <h1>Blog</h1>
    <ul>
      {data.allContentfulBlogPost.edges.map(({ node, index }) => (
        <li key={index}>
          <Link to={`/blog/${node.slug}`}>{node.title}</Link>
        </li>
      ))}
    </ul>
  </div>
)

export default BlogPage

export const query = graphql`
  {
    allContentfulBlogPost(sort: { fields: [updatedAt] }) {
      edges {
        node {
          title
          slug
        }
      }
    }
  }
`
```

To continue building out your Contentful site including post detail pages, check out the rest of the [Gatsby docs](/docs/sourcing-from-contentful/) and additional resources below.

#### अतिरिक्त संसाधन

- [Building a Site with React and Contentful](/blog/2018-1-25-building-a-site-with-react-and-contentful/)
- [More on Sourcing from Contentful](/docs/sourcing-from-contentful/)
- [Contentful source plugin](/packages/gatsby-source-contentful/)
- [Long-text field types returned as objects](/packages/gatsby-source-contentful/#a-note-about-longtext-fields)
- [Example repository for this recipe](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-sourcing-contentful)

### Pulling data from an external source and creating pages without GraphQL

You don't have to use the GraphQL data layer to include data in pages, [though there are reasons why you should consider GraphQL](/docs/why-gatsby-uses-graphql/). You can use the node `createPages` API to pull unstructured data directly into Gatsby sites rather than through GraphQL and source plugins.

In this recipe, you'll create dynamic pages from data fetched from the [PokéAPI’s REST endpoints](https://www.pokeapi.co/). The [full example](https://github.com/jlengstorf/gatsby-with-unstructured-data/) can be found on GitHub.

#### Prerequisites

- A Gatsby Site with a `gatsby-node.js` file
- The [Gatsby CLI](/docs/gatsby-cli) installed
- The [axios](https://www.npmjs.com/package/axios) package installed through npm

#### Directions

1. In `gatsby-node.js`, add the JavaScript code to fetch data from the PokéAPI and programmatically create an index page:

```js:title=gatsby-node.js
const axios = require("axios")

const get = endpoint => axios.get(`https://pokeapi.co/api/v2${endpoint}`)

const getPokemonData = names =>
  Promise.all(
    names.map(async name => {
      const { data: pokemon } = await get(`/pokemon/${name}`)
      return { ...pokemon }
    })
  )
exports.createPages = async ({ actions: { createPage } }) => {
  const allPokemon = await getPokemonData(["pikachu", "charizard", "squirtle"])

  // Create a page that lists Pokémon.
  createPage({
    path: `/`,
    component: require.resolve("./src/templates/all-pokemon.js"),
    context: { allPokemon },
  })
}
```

2. Create a template to display Pokémon on the homepage:

```js:title=src/templates/all-pokemon.js
import React from "react"

export default ({ pageContext: { allPokemon } }) => (
  <div>
    <h1>Behold, the Pokémon!</h1>
    <ul>
      {allPokemon.map(pokemon => (
        <li key={pokemon.id}>
          <img src={pokemon.sprites.front_default} alt={pokemon.name} />
          <p>{pokemon.name}</p>
        </li>
      ))}
    </ul>
  </div>
)
```

3. Run `gatsby develop` to fetch the data, build pages, and start the development server.
4. View your homepage in a browser: <http://localhost:8000>

#### अतिरिक्त संसाधन

- [Full Pokemon data repo](https://github.com/jlengstorf/gatsby-with-unstructured-data/)
- More on using unstructured data in [Using Gatsby without GraphQL](/docs/using-gatsby-without-graphql/)
- When and how to [query data with GraphQL](/docs/querying-with-graphql/) for more complex Gatsby sites

### Sourcing content from Drupal

#### Prerequisites

- A [Gatsby site](/docs/quick-start)
- A [Drupal](http://drupal.org) site
- The [JSON:API module](https://www.drupal.org/project/jsonapi) installed and enabled on the Drupal site

#### Directions

1. Install the `gatsby-source-drupal` plugin.

```
npm install --save gatsby-source-drupal
```

2. Edit your `gatsby-config.js` file to enable the plugin and configure it.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-drupal`,
      options: {
        baseUrl: `https://your-website/`,
        apiBase: `api`, // optional, defaults to `jsonapi`
      },
    },
  ],
}
```

3. Start the development server with `gatsby develop`, and open the GraphiQL explorer at <http://localhost:8000/___graphql>. Under the Explorer tab, you should see new node types, such as `allBlockBlock` for Drupal blocks, and one for every content type in your Drupal site. For example, if you have a "Page" content type, it will be available as `allNodePage`. To query all "Page" nodes for their title and body, use a query like:

```graphql
{
  allNodePage {
    edges {
      node {
        title
        body {
          value
        }
      }
    }
  }
}
```

4. To use your Drupal data, create a new page in your Gatsby site at `src/pages/drupal.js`. This page will list all Drupal "Page" nodes.

_**Note:** the exact GraphQL schema will depend on your how Drupal instance is structured._

```jsx:title=src/pages/drupal.js
import React from "react"
import { graphql } from "gatsby"

const DrupalPage = ({ data }) => (
  <div>
    <h1>Drupal pages</h1>
    <ul>
    {data.allNodePage.edges.map(({ node, index }) => (
      <li key={index}>
        <h2>{node.title}</h2>
        <div>
          {node.body.value}
        </div>
      </li>
    ))}
   </ul>
  </div>
)

export default DrupalPage

export const query = graphql`
  {
  allNodePage {
    edges {
      node {
        title
        body {
          value
        }
      }
    }
  }
}
```

5. With the development server running, you can view the new page by visiting <http://localhost:8000/drupal>.

#### अतिरिक्त संसाधन

- [Using Decoupled Drupal with Gatsby](/blog/2018-08-13-using-decoupled-drupal-with-gatsby/)
- [More on sourcing from Drupal](/docs/sourcing-from-drupal)
- [Tutorial: Programmatically create pages from data](/tutorial/part-seven/)

## 6. Querying data

### Querying data with a Page Query

You can use the `graphql` tag to query data in the pages of your Gatsby site. This gives you access to anything included in Gatsby's data layer, such as site metadata, source plugins, images, and more.

#### Directions

1. Import `graphql` from `gatsby`.

2. Export a constant named `query` and set its value to be a `graphql` template with the query between two backticks.

3. Pass in `data` as a prop to the component.

4. The `data` variable holds the queried data and can be referenced in JSX to output HTML.

```jsx:title=src/pages/index.js
import React from "react"
// highlight-next-line
import { graphql } from "gatsby"

import Layout from "../components/layout"

// highlight-start
export const query = graphql`
  query HomePageQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end

// highlight-next-line
const IndexPage = ({ data }) => (
  <Layout>
    // highlight-next-line
    <h1>{data.site.siteMetadata.title}</h1>
  </Layout>
)

export default IndexPage
```

#### अतिरिक्त संसाधन

- [GraphQL and Gatsby](/docs/graphql/): understanding the expected shape of your data
- [More on querying data in pages with GraphQL](/docs/page-query/)
- [MDN on Tagged Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) like the ones used in GraphQL

### Querying data with the StaticQuery Component

`StaticQuery` is a component for retrieving data from Gatsby's data layer in [non-page components](/docs/static-query/), such as a header, navigation, or any other child component.

#### Directions

1. The `StaticQuery` Component requires two render props: `query` and `render`.

```jsx:title=src/components/NonPageComponent.js
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const NonPageComponent = () => (
  <StaticQuery
    query={graphql` // highlight-line
      query NonPageQuery {
        site {
          siteMetadata {
            title
          }
        }
      }
    `}
    render={(
      data // highlight-line
    ) => (
      <h1>
        Querying title from NonPageComponent with StaticQuery:
        {data.site.siteMetadata.title}
      </h1>
    )}
  />
)

export default NonPageComponent
```

2. You can now use this component as you would [any other component](/docs/building-with-components#non-page-components) by importing it into a larger page of JSX components and HTML markup.

### Querying data with the useStaticQuery hook

Since Gatsby v2.1.0, you can use the `useStaticQuery` hook to query data with a JavaScript function instead of a component. The syntax removes the need for a `<StaticQuery>` component to wrap everything, which some people find simpler to write.

The `useStaticQuery` hook takes a GraphQL query and returns the requested data. It can be stored in a variable and used later in your JSX templates.

#### Prerequisites

- You'll need React and ReactDOM 16.8.0 or later (keeping Gatsby updated handles this)
- Recommended reading: the [Rules of React Hooks](https://reactjs.org/docs/hooks-rules.html)

#### Directions

1. Import `useStaticQuery` and `graphql` from `gatsby` in order to use the hook query the data.

2. In the start of a stateless functional component, assign a variable to the value of `useStaticQuery` with your `graphql` query passed as an argument.

3. In the JSX code returned from your component, you can reference that variable to handle the returned data.

```jsx:title=src/components/NonPageComponent.js
import React from "react"
import { useStaticQuery, graphql } from "gatsby" //highlight-line

const NonPageComponent = () => {
  // highlight-start
  const data = useStaticQuery(graphql`
    query NonPageQuery {
      site {
        siteMetadata {
          title
        }
      }
    }
  `)
  // highlight-end
  return (
    <h1>
      Querying title from NonPageComponent: {data.site.siteMetadata.title}{" "}
      //highlight-line
    </h1>
  )
}

export default NonPageComponent
```

#### अतिरिक्त संसाधन

- [More on Static Query for querying data in components](/docs/static-query/)
- [The difference between a static query and a page query](/docs/static-query/#how-staticquery-differs-from-page-query)
- [More on the useStaticQuery hook](/docs/use-static-query/)
- [Visualize your data with GraphiQL](/docs/introducing-graphiql/)

### Limiting with GraphQL

When querying for data with GraphQL, you can limit the number of results returned with a specific number. This is helpful if you only need a few pieces of data or need to [paginate data](/docs/adding-pagination/).

To limit data, you'll need a Gatsby site with some nodes in the GraphQL data layer. All sites have some nodes like `allSitePage` and `sitePage` created automatically: more can be added by installing source plugins like `gatsby-source-filesystem` in `gatsby-config.js`.

#### Prerequisites

- A [Gatsby site](/docs/quick-start/)

#### Directions

1. Run `gatsby develop` to start the development server.
2. Open a tab in your browser at: <http://localhost:8000/___graphql>.
3. Add a query in the editor with the following fields on `allSitePage` to start off:

```graphql
{
  allSitePage {
    edges {
      node {
        id
        path
      }
    }
  }
}
```

4. Add a `limit` argument to the `allSitePage` field and give it an integer value `3`.

```graphql
{
  allSitePage(limit: 3) { // highlight-line
    edges {
      node {
        id
        path
      }
    }
  }
}
```

5. Click the play button in the GraphiQL page and the data in the `edges` field will be limited to the number specified.

#### अतिरिक्त संसाधन

- Learn about [nodes in Gatsby's GraphQL data API](/docs/node-interface/)
- [Gatsby GraphQL reference for limiting](/docs/graphql-reference/#limit)
- Live example:

<iframe
  title="Limiting returned data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(limit%3A%203)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Sorting with GraphQL

The ordering of your results can be specified with the GraphQL `sort` argument. You can specify which fields to sort by and the order to sort in.

For this recipe, you'll need a Gatsby site with a collection of nodes to sort in the GraphQL data layer. All sites have some nodes like `allSitePage` created automatically: more can be added by installing source plugins.

#### Prerequisites

- A [Gatsby site](/docs/quick-start)
- Queryable fields prefixed with `all`, e.g. `allSitePage`

#### Directions

1. Run `gatsby develop` to start the development server.
2. Open the GraphiQL explorer in a browser tab at: <http://localhost:8000/___graphql>
3. Add a query in the editor with the following fields on `allSitePage` to start off:

```graphql
{
  allSitePage {
    edges {
      node {
        id
        path
      }
    }
  }
}
```

4. Add a `sort` argument to the `allSitePage` field and give it an object with the `fields` and `order` attributes. The value for `fields` can be a field or an array of fields to sort by (this example uses the `path` field), the `order` can be either `ASC` or `DESC` for ascending and descending respectively.

```graphql
{
  allSitePage(sort: {fields: path, order: ASC}) { // highlight-line
    edges {
      node {
        id
        path
      }
    }
  }
}

```

5. Click the play button in the GraphiQL page and the data returned will be sorted ascending by the `path` field.

#### अतिरिक्त संसाधन

- [Gatsby GraphQL reference for sorting](/docs/graphql-reference/#sort)
- Learn about [nodes in Gatsby's GraphQL data API](/docs/node-interface/)
- Live example:

<iframe
  title="Sorting data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(sort%3A%20%7Bfields%3A%20path%2C%20order%3A%20ASC%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Filtering with GraphQL

Queried results can be filtered down with operators like `eq` (equals), `ne` (not equals), `in`, and `regex` on specified fields.

For this recipe, you'll need a Gatsby site with a collection of nodes to filter in the GraphQL data layer. All sites have some nodes like `allSitePage` created automatically: more can be added by installing source and transformer plugins like `gatsby-source-filesystem` and `gatsby-transformer-remark` in `gatsby-config.js` to produce `allMarkdownRemark`.

#### Prerequisites

- A [Gatsby site](/docs/quick-start)
- Queryable fields prefixed with `all`, e.g. `allSitePage` or `allMarkdownRemark`

#### Directions

1. Run `gatsby develop` to start the development server.
2. Open the GraphiQL explorer in a browser tab at: <http://localhost:8000/___graphql>
3. Add a query in the editor using a field prefixed by 'all', like `allMarkdownRemark` (meaning that it will return a list of nodes)

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        frontmatter {
          title
          categories
        }
      }
    }
  }
}
```

4. Add a `filter` argument to the `allMarkdownRemark` field and give it an object with the fields you'd like to filter by. In this example, Markdown content is filtered by the `categories` attribute in frontmatter metadata. The next value is the operator: in this case `eq`, or equals, with a value of 'magical creatures'.

```graphql
{
  allMarkdownRemark(filter: {frontmatter: {categories: {eq: "magical creatures"}}}) { // highlight-line
    edges {
      node {
        frontmatter {
          title
          categories
        }
      }
    }
  }
}
```

5. Click the play button in the GraphiQL page. The data that matches the filter parameters should be returned, in this case only sourced Markdown files tagged with a category of 'magical creatures'.

#### अतिरिक्त संसाधन

- [Gatsby GraphQL reference for filtering](/docs/graphql-reference/#filter)
- [Complete list of possible operators](/docs/graphql-reference/#complete-list-of-possible-operators)
- Learn about [nodes in Gatsby's GraphQL data API](/docs/node-interface/)
- Live example:

<iframe
  title="Filtering data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allMarkdownRemark(filter%3A%20%7Bfrontmatter%3A%20%7Bcategories%3A%20%7Beq%3A%20%22magical%20creatures%22%7D%7D%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20title%0A%20%20%20%20%20%20%20%20%20%20categories%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### GraphQL Query Aliases

You can rename any field in a GraphQL query with an alias.

If you would like to run two queries on the same datasource, you can use an alias to avoid a naming collision with two queries of the same name.

#### Directions

1. Run `gatsby develop` to start the development server.
2. Open the GraphiQL explorer in a browser tab at: <http://localhost:8000/___graphql>
3. Add a query in the editor using two fields of the same name like `allFile`

```graphql
{
  allFile {
    totalCount
  }
  allFile {
    pageInfo {
      currentPage
    }
  }
}
```

4. Add the name you would like to use for any field before the name of the field in your GraphQL schema, separated by a colon. (E.g. `[alias-name]: [original-name]`)

```graphql
{
  fileCount: allFile { // highlight-line
    totalCount
  }
  filePageInfo: allFile { // highlight-line
    pageInfo {
      currentPage
    }
  }
}
```

5. Click the play button in the GraphiQL page and 2 objects with alias names you provided should be output.

#### अतिरिक्त संसाधन

- [Gatsby GraphQL reference for aliasing](/docs/graphql-reference/#aliasing)
- Live example:

<iframe
  title="Using aliases"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20fileCount%3A%20allFile%20%7B%20%0A%20%20%20%20totalCount%0A%20%20%7D%0A%20%20filePageInfo%3A%20allFile%20%7B%0A%20%20%20%20pageInfo%20%7B%0A%20%20%20%20%20%20currentPage%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### GraphQL Query Fragments

GraphQL fragments are shareable chunks of a query that can be reused.

You might want to use them to share multiple fields between queries or to colocate a component with the data it uses.

#### Directions

1. Declare a `graphql` template string with a Fragment in it. The fragment should be made up of the keyword `fragment`, a name, the GraphQL type it is associated with (in this case of type `Site`, as demonstrated by `on Site`), and the fields that make up the fragment:

```jsx
export const query = graphql`
  // highlight-start
  fragment SiteInformation on Site {
    title
    description
  }
  // highlight-end
`
```

2. Now, include the fragment in a query for a field of the type specified by the fragment. This includes those fields without having to declare them all independently:

```diff
export const pageQuery = graphql`
  query SiteQuery {
    site {
-     title
-     description
+   ...SiteInformation
    }
  }
`
```

**Note**: Fragments don't need to be imported in Gatsby. Exporting a query with a Fragment makes that Fragment available in _all_ queries in your project.

Fragments can be nested inside other fragments, and multiple fragments can be used in the same query.

#### अतिरिक्त संसाधन

- [Simple example repo using fragments](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-fragments)
- [Gatsby GraphQL reference for fragments](/docs/graphql-reference/#fragments)
- [Gatsby image fragments](/docs/gatsby-image/#image-query-fragments)
- [Example repo with co-located data](https://github.com/gatsbyjs/gatsby/tree/master/examples/gatsbygram)

## 7. Working with images

### Import an image into a component with webpack

Images can be imported right into a JavaScript module with webpack. This process automatically minifies and copies the image to your site's `public` folder, providing a dynamic image URL for you to pass to an HTML `<img>` element like a regular file path.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-import-a-local-image-into-a-gatsby-component-with-webpack"
  lessonTitle="Import a Local Image into a Gatsby Component with webpack"
/>

#### Prerequisites

- A [Gatsby Site](/docs/quick-start) with a `.js` file exporting a React component
- an image (`.jpg`, `.png`, `.gif`, `.svg`, etc.) in the `src` folder

#### Directions

1. Import your file from its path in the `src` folder:

```jsx:title=src/pages/index.js
import React from "react"
// Tell webpack this JS file uses this image
import FiestaImg from "../assets/fiesta.jpg" // highlight-line
```

2. In `index.js`, add an `<img>` tag with the `src` as the name of the import you used from webpack (in this case `FiestaImg`), and add an `alt` attribute [describing the image](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"
import FiestaImg from "../assets/fiesta.jpg"

export default () => (
  // The import result is the URL of your image
  <img src={FiestaImg} alt="A dog smiling in a party hat" /> // highlight-line
)
```

3. Run `gatsby develop` to start the development server.
4. View your image in the browser: <http://localhost:8000/>

#### अतिरिक्त संसाधन

- [Example repo importing an image with webpack](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-webpack-image)
- [More on all image techniques in Gatsby](/docs/images-and-files/)

### Reference an image from the `static` folder

As an alternative to importing assets with webpack, the `static` folder allows access to content that gets automatically copied into the `public` folder when built.

This is an **escape route** for [specific use cases](/docs/static-folder/#when-to-use-the-static-folder), and other methods like [importing with webpack](#import-an-image-into-a-component-with-webpack) are recommended to leverage optimizations made by Gatsby.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-a-local-image-from-the-static-folder-in-a-gatsby-component"
  lessonTitle="Use a local image from the static folder in a Gatsby component"
/>

#### Prerequisites

- A [Gatsby Site](/docs/quick-start) with a `.js` file exporting a React component
- An image (`.jpg`, `.png`, `.gif`, `.svg`, etc.) in the `static` folder

#### Directions

1. Ensure that the image is in your `static` folder at the root of the project. Your project structure might look something like this:

```
├── gatsby-config.js
├── src
│   └── pages
│       └── index.js
├── static
│       └── fiesta.jpg
```

2. In `index.js`, add an `<img>` tag with the `src` as the relative path of the file from the `static` folder, and add an `alt` attribute [describing the image](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <img src={`fiesta.jpg`} alt="A dog smiling in a party hat" /> // highlight-line
)
```

3. Run `gatsby develop` to start the development server.
4. View your image in the browser: <http://localhost:8000/>

#### अतिरिक्त संसाधन

- [Example repo referencing an image from the static folder](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-static-image)
- [Using the Static Folder](/docs/static-folder/)
- [More on all image techniques in Gatsby](/docs/images-and-files/)

### Optimizing and querying local images with gatsby-image

The `gatsby-image` plugin can relieve much of the pain associated with optimizing images in your site.

Gatsby will generate optimized resources which can be queried with GraphQL and passed into Gatsby's image component. This takes care of the heavy lifting including creating several image sizes and loading them at the right time.

#### Prerequisites

- The `gatsby-image`, `gatsby-transformer-sharp`, and `gatsby-plugin-sharp` packages installed and added to the plugins array in `gatsby-config`
- [Images sourced](/packages/gatsby-image/#install) in your `gatsby-config` using a plugin like `gatsby-source-filesystem`

#### Directions

1. First, import `Img` from `gatsby-image`, as well as `graphql` and `useStaticQuery` from `gatsby`

```jsx
import { useStaticQuery, graphql } from "gatsby" // to query for image data
import Img from "gatsby-image" // to take image data and render it
```

2. Write a query to get image data, and pass the data into the `<Img />` component:

Choose any of the following options or a combination of them.

a. a single image queried by its file [path](/docs/content-and-data/) (Example: `images/corgi.jpg`)

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) { // highlight-line
      childImageSharp {
        fluid {
          base64
          aspectRatio
          src
          srcSet
          sizes
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="A corgi smiling happily" />
)
```

b. using a [GraphQL fragment](/docs/using-graphql-fragments/), to query for the necessary fields more tersely

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fluid {
          ...GatsbyImageSharpFluid // highlight-line
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="A corgi smiling happily" />
)
```

c. several images from a directory (Example: `images/dogs`) [filtered](/docs/graphql-reference/#filter) by the `extension` and `relativeDirectory` fields, and then mapped into `Img` components

```jsx
const data = useStaticQuery(graphql`
  query {
    allFile(
      // highlight-start
      filter: {
        extension: { regex: "/(jpg)|(png)|(jpeg)/" }
        relativeDirectory: { eq: "dogs" }
      }
      // highlight-end
    ) {
      edges {
        node {
          base
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
`)

return (
  <div>
    // highlight-start
    {data.allFile.edges.map(image => (
      <Img
        fluid={image.node.childImageSharp.fluid}
        alt={image.node.base.split(".")[0]} // only use section of the file extension with the filename
      />
    ))}
    // highlight-end
  </div>
)
```

**Note**: This method can make it difficult to match images with `alt` text for accessibility. This example uses images with `alt` text included in the filename, like `dog in a party hat.jpg`.

d. an image of a fixed size using the `fixed` field instead of `fluid`

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fixed(width: 250, height: 250) { // highlight-line
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`)
return (
  <Img fixed={data.file.childImageSharp.fixed} alt="A corgi smiling happily" />
)
```

e. an image of a fixed size with a `maxWidth`

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fixed(maxWidth: 250) { // highlight-line
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`)
return (
  <Img fixed={data.file.childImageSharp.fixed} alt="A corgi smiling happily" /> // highlight-line
)
```

f. an image filling a fluid container with a max width (in pixels) and a higher quality (the default value is 50 i.e. 50%)

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fluid(maxWidth: 800, quality: 75) { // highlight-line
          ...GatsbyImageSharpFluid
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="A corgi smiling happily" />
)
```

3. (Optional) Add inline styles to the `<Img />` like you would to other components

```jsx
<Img
  fluid={data.file.childImageSharp.fluid}
  alt="A corgi smiling happily"
  style={{ border: "2px solid rebeccapurple", borderRadius: 5, height: 250 }} // highlight-line
/>
```

4. (Optional) Force an image into a desired aspect ratio by overriding the `aspectRatio` field returned by the GraphQL query before it is passed into the `<Img />` component

```jsx
<Img
  fluid={{
    ...data.file.childImageSharp.fluid,
    aspectRatio: 1.6, // 1280 / 800 = 1.6
  }}
  alt="A corgi smiling happily"
/>
```

5. Run `gatsby develop`, to generate images from files in the filesystem (if not done already) and cache them

#### अतिरिक्त संसाधन

- [Example repository illustrating these examples](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipes-gatsby-image)
- [Gatsby Image API](/docs/gatsby-image/)
- [Using Gatsby Image](/docs/using-gatsby-image)
- [More on working with images in Gatsby](/docs/working-with-images/)
- [Free egghead.io videos explaining these steps](https://egghead.io/playlists/using-gatsby-image-with-gatsby-ea85129e)

### Optimizing and querying images in post frontmatter with gatsby-image

For use cases like a featured image in a blog post, you can _still_ use `gatsby-image`. The `Img` component needs processed image data, which can come from a local (or remote) file, including from a URL in the frontmatter of a `.md` or `.mdx` file.

To inline images in markdown (using the `![]()` syntax), consider using a plugin like [`gatsby-remark-images`](/packages/gatsby-remark-images/)

#### Prerequisites

- The `gatsby-image`, `gatsby-transformer-sharp`, and `gatsby-plugin-sharp` packages installed and added to the plugins array in `gatsby-config`
- [Images sourced](/packages/gatsby-image/#install) in your `gatsby-config` using a plugin like `gatsby-source-filesystem`
- Markdown files sourced in your `gatsby-config` with image URLs in frontmatter
- [Pages created](/docs/creating-and-modifying-pages/) from Markdown using [`createPages`](https://www.gatsbyjs.org/docs/node-apis/#createPages)

#### Directions

1. Verify that the Markdown file has an image URL with a valid path to an image file in your project

```mdx:title=post.mdx
---
title: My First Post
featuredImage: ./corgi.png // highlight-line
---

Post content...
```

2. Verify that a unique identifier (a slug in this example) is passed in context when `createPages` is called in `gatsby-node.js`, which will later be passed into a GraphQL query in the Layout component

```js:title=gatsby-node.js
exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions

  // query for all markdown

  result.data.allMdx.edges.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: path.resolve(`./src/components/markdown-layout.js`),
      // highlight-start
      context: {
        slug: node.fields.slug,
      },
      // highlight-end
    })
  })
}
```

3. Now, import `Img` from `gatsby-image`, and `graphql` from `gatsby` into the template component, write a [pageQuery](/docs/page-query/) to get image data based on the passed in `slug` and pass that data to the `<Img />` component:

```jsx:title=markdown-layout.jsx
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Img from "gatsby-image" // highlight-line

export default ({ children, data }) => (
  <main>
    // highlight-start
    <Img
      fluid={data.markdown.frontmatter.image.childImageSharp.fluid}
      alt="A corgi smiling happily"
    />
    // highlight-end
    {children}
  </main>
)

// highlight-start
export const pageQuery = graphql`
  query PostQuery($slug: String) {
    markdown: mdx(fields: { slug: { eq: $slug } }) {
      id
      frontmatter {
        image {
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
`
// highlight-end
```

4. Run `gatsby develop`, which will generate images for files sourced in the filesystem

#### अतिरिक्त संसाधन

- [Example repository using this recipe](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipes-gatsby-image)
- [Featured images with frontmatter](/docs/working-with-images-in-markdown/#featured-images-with-frontmatter-metadata)
- [Gatsby Image API](/docs/gatsby-image/)
- [Using Gatsby Image](/docs/using-gatsby-image)
- [More on working with images in Gatsby](/docs/working-with-images/)

## 8. Transforming data

Transforming data in Gatsby is plugin-driven. Transformer plugins take data fetched using source plugins, and process it into something more usable (e.g. JSON into JavaScript objects, and more).

### Transforming Markdown into HTML

The `gatsby-transformer-remark` plugin can transform Markdown files to HTML.

#### Prerequisites

- A Gatsby site with `gatsby-config.js` and an `index.js` page
- A Markdown file saved in your Gatsby site `src` directory
- A source plugin installed, such as `gatsby-source-filesystem`
- The `gatsby-transformer-remark` plugin installed

#### Directions

1. Add the transformer plugin in your `gatsby-config.js`:

```js:title=gatsby-config.js
plugins: [
  // not shown: gatsby-source-filesystem for creating nodes to transform
  `gatsby-transformer-remark`
],
```

2. Add a GraphQL query to the `index.js` file of your Gatsby site to fetch `MarkdownRemark` nodes:

```jsx:title=src/pages/index.js
export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

3. Restart the development server and open GraphiQL at <http://localhost:8000/___graphql>. Explore the fields available on the `MarkdownRemark` node.

#### अतिरिक्त संसाधन

- [Tutorial on transforming Markdown to HTML](/tutorial/part-six/#transformer-plugins) using `gatsby-transformer-remark`
- Browse available transformer plugins in the [Gatsby plugin library](/plugins/?=transformer)

## 9. Deploying your site

Showtime. Once you are happy with your site, you are ready to go live with it!

### Preparing for deployment

#### Prerequisites

- A [Gatsby site](/docs/quick-start)
- The [Gatsby CLI](/docs/gatsby-cli) installed

#### Directions

1. Stop your development server if it is running (`Ctrl + C` on your command line in most cases)

2. For the standard site path at the root directory (`/`), run `gatsby build` using the Gatsby CLI on the command line. The built files will now be in the `public` folder.

```shell
gatsby build
```

3. To include a site path other than `/` (such as `/site-name/`), set a path prefix by adding the following to your `gatsby-config.js` and replacing `yourpathprefix` with your desired path prefix:

```js:title=gatsby-config.js
module.exports = {
  pathPrefix: `/yourpathprefix`,
}
```

There are a few reasons to do this -- for instance, hosting a blog built with Gatsby on a domain with another site not built on Gatsby. The main site would direct to `example.com`, and the Gatsby site with a path prefix could live at `example.com/blog`.

4. With a path prefix set in `gatsby-config.js`, run `gatsby build` with the `--prefix-paths` flag to automatically add the prefix to the beginning of all Gatsby site URLs and `<Link>` tags.

```shell
gatsby build --prefix-paths
```

5.सुनिश्चित करें कि जब आपकी साइट `gatsby build` के साथ` gatsby develop` के रूप में चल रही हो तो वही दिखता है। जब आप अपनी साइट का निर्माण कर रहे हैं, तो `gatsby serve` चलाकर, आप तैयार उत्पाद का परीक्षण कर सकते हैं (और यदि आवश्यक हो तो) इसे लाइव करने से पहले तैयार उत्पाद पर रख सकते हैं।

```shell
gatsby build && gatsby serve
```

#### अतिरिक्त संसाधन

- में एक उदाहरण साइट के निर्माण और तैनाती के माध्यम से चलो [tutorial part one](/tutorial/part-one/#deploying-a-gatsby-site)
- के बारे में जानना [performance optimization](/docs/performance/)
- के बारे में [other deployment related topics](/docs/preparing-for-deployment/)
- इसकी जाँच पड़ताल करो [deployment docs](/docs/deploying-and-hosting/) विशिष्ट होस्टिंग प्लेटफार्मों के लिए और उन्हें कैसे तैनात किया जाए
### Netlify को नियुक्त करना

कमांड लाइन इंटरफ़ेस को छोड़ने के बिना अपने Gatsby एप्लिकेशन को तैनात करने के लिए [`netlify-cli`] (https://www.netlify.com/docs/cli/) का उपयोग करें।

#### आवश्यक शर्तें

-  [Gatsby site](/docs/quick-start) एक एकल घटक के साथ `index.js`
- [netlify-cli](https://www.npmjs.com/package/netlify-cli) स्थापित
-  [Gatsby CLI](/docs/gatsby-cli) स्थापित

#### दिशा-निर्देश

1. `gatsby build` का उपयोग करके अपने गैट्सबी एप्लिकेशन का निर्माण करें

2. netlify में `netlify login` का उपयोग करके लॉगिन करें

3. कमांड चलाएँ `netlify init`। "एक नई साइट बनाएं और कॉन्फ़िगर करें" विकल्प चुनें।

4. यदि आप चाहें तो एक कस्टम वेबसाइट का नाम चुनें या एक यादृच्छिक प्राप्त करने के लिए एंटर दबाएं।

5. अपनी [Team](https://www.netlify.com/docs/teams/) चुनें।

6. तैनाती पथ को `public/` में बदलें

7. सुनिश्चित करें कि `netlify deploy --prod` का उपयोग करके उत्पादन के लिए तैनात करने से पहले सब कुछ ठीक लगता है

#### अतिरिक्त संसाधन

- [Hosting on Netlify](/docs/hosting-on-netlify)
- [gatsby-plugin-netlify](/packages/gatsby-plugin-netlify)

### अब ZEIT में तैनाती

कमांड-लाइन इंटरफ़ेस को छोड़े बिना अपने गैट्सबी एप्लिकेशन को तैनात करने के लिए [अब CLI] (https://zeit.co/download) का उपयोग करें।
#### आवश्यक शर्तें

- [[ZEIT Now] (https://zeit.co/signup) खाता
- एक एकल घटक `index.js` के साथ एक [Gatsby site] (/docs/quick-start)
- [अब CLI] (https://zeit.co/download) पैकेज इंस्टॉल किया गया
- [Gatsby CLI](/docs/gatsby-cli) स्थापित

#### दिशा-निर्देश

1. अब 'अब लॉगिन' का उपयोग करके अब CLI में लॉगिन करें

2. यदि आप पहले से ही वहां नहीं हैं तो टर्मिनल में अपने Gatsby.js एप्लिकेशन की निर्देशिका में बदलें

3. इसे तैनात करने के लिए `now` चलाएं

#### अतिरिक्त संसाधन

- [Deploying to ZEIT Now](/docs/deploying-to-zeit-now/)
