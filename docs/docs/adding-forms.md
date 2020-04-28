---
title: फॉर्म को जोड़ना
---

Gatsby के ऊपर बनाया गया है React. तो सब कुछ जो संभव है React फॉर्म में ,वो संभव है Gatsby में भी. अतिरिक्त जानकारि की कैसे बनाएं React फॉर्म ,यहाँ पाया जा सकता है [React forms documentation](https://reactjs.org/docs/forms.html) (जो बनाया गया है Gatsby! से)

सेुरू करें निम्नलिखित पृष्ठ से.

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

ये Gatsby पृष्ठ एक React कौम्पोनॅन्ट है. जब आप एक फॉर्म चाहते हैं , आपको फॉर्म की स्टेट स्टोर करने की आवश्यकता है - उपयोगकर्ता ने क्या दर्ज किया है. अपने कृत्य(अवस्थाहीं) कौम्पोनॅन्ट कोह क्लास (स्टेटफुल) कौम्पोनॅन्ट रूपांतरित करो.

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.कौम्पोनॅन्ट {
  render() {
    return <div>Hello world!</div>
  }
}
```

अब जब आपने क्लास कौम्पोनॅन्ट बना लिया है,अब आप जोड़ सकते हो `state` कौम्पोनॅन्ट में.

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.कौम्पोनॅन्ट {
  state = {
    firstName: "",
    lastName: "",
  }

  render() {
    return <div>Hello world!</div>
  }
}
```

और अब आप कुछ इनपुट फ़ील्ड भी जोड़ सकते हैं :

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  render() {
    return (
      <form>
        <label>
          First name
          <input type="text" name="firstName" />
        </label>
        <label>
          Last name
          <input type="text" name="lastName" />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

जब कोई उपयोगकर्ता एक इनपुट बॉक्स में टाइप करता है, स्टेट को अद्यतन करना चाहिए. एक `onChange`  जोड़ें जो स्टेट अद्यतन करेगा और एक `value` प्रोप जोड़ें इनपुट को अद्यतित रखना के लीये नए स्टेट के साथ:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  handleInputChange = event => {
    const target = event.target
    const value = target.value
    const name = target.name

    this.setState({
      [name]: value,
    })
  }

  render() {
    return (
      <form>
        <label>
          First name
          <input
            type="text"
            name="firstName"
            value={this.state.firstName}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          Last name
          <input
            type="text"
            name="lastName"
            value={this.state.lastName}
            onChange={this.handleInputChange}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

अब जब कि आपके इनपुट काम कर रहे हैं, आप कुछ फॉर्म जमा करते वक़्त होने वाला बनना चाहते हैं. एक `onSubmit` प्रोप फॉर्म में जोड़ें और एक `handleSubmit` यहाँ दिखाने के लीये जब उपयोगकर्ता फ़ॉर्म सबमिट करे तो अलर्ट दिखे:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  handleInputChange = event => {
    const target = event.target
    const value = target.value
    const name = target.name

    this.setState({
      [name]: value,
    })
  }

  handleSubmit = event => {
    event.preventDefault()
    alert(`Welcome ${this.state.firstName} ${this.state.lastName}!`)
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          First name
          <input
            type="text"
            name="firstName"
            value={this.state.firstName}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          Last name
          <input
            type="text"
            name="lastName"
            value={this.state.lastName}
            onChange={this.handleInputChange}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

यह फ़ॉर्म कुछ भी नहीं कर रहा है उपयोगकर्ता द्वारा दर्ज की गई जानकारी प्रदर्शन के अलवा. इस समय, आप फ़ार्म को कौम्पोनॅन्ट चाहते हैं, फ़ार्म स्टेट को बैकएंड सर्वर पर भज सकत है, या मजबूत मान्यकरण जोर सखते है. आप ये भी उपयोग कर सकते हैं विलक्षण React फ़ार्म लाइब्रेरी जैसा [Formik](https://github.com/jaredpalmer/formik) या[Final Form](https://github.com/final-form/react-final-form) अपनी डिविलडेवेलोपमेंट गति बढ़ाने के लिए.

यह सब और इस्से अधिक भी संभव है Gatsby और React पारिस्थितिकी तंत्र की शक्ति का लाभ उठाकर!
