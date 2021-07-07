---
title: Adding a Manifest File
---

अगर आपने [audit with Lighthouse](/docs/audit-with-lighthouse/) चलाया है, तो आपने "प्रोग्रेसिव वेब ऐप" श्रेणी में एक शानदार स्कोर देखा होगा। आइए पता करें कि आप उस स्कोर को कैसे सुधार सकते हैं।

लेकिन पहले, वास्तव में PWA क्या है?

वे नियमित वेबसाइटें हैं जो ऐप की तरह सुविधाओं और लाभों के साथ वेब अनुभव को बढ़ाने के लिए आधुनिक ब्राउज़र कार्यक्षमता का लाभ उठाती हैं। इसे देखें [Google's overview](https://developers.google.com/web/progressive-web-apps/) क्या एक PWA अनुभव और [Progressive web apps (PWAs) doc](/docs/progressive-web-app/) को परिभाषित करता है कि कैसे एक Gatsby साइट एक प्रगतिशील वेब ऐप है।

एक वेब ऐप मैनिफेस्ट में शामिल होना आम तौर पर स्वीकृत तीन में से एक है [baseline requirements for a PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1).

का हवाला देते हुए [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> वेब ऐप मैनिफ़ेस्ट एक साधारण JSON फ़ाइल है जो ब्राउज़र को आपके वेब एप्लिकेशन के बारे में बताती है और उपयोगकर्ता के मोबाइल डिवाइस या डेस्कटॉप पर 'इंस्टॉल' होने पर इसे कैसे व्यवहार करना चाहिए।

[Gatsby's manifest plugin](/packages/gatsby-plugin-manifest/) हर साइट के निर्माण पर एक `manifest.webmanifest`फ़ाइल बनाने के लिए Gatsby को कॉन्फ़िगर करता है।

## `gatsby-plugin-manifest` का उपयोग करते हुए

1.  प्लग-इन इंस्टॉल करें :

```shell
npm install --save gatsby-plugin-manifest
```

2. `Src / images / icon.png` के तहत अपने ऐप के लिए एक फ़ेविकॉन जोड़ें। आइकन प्रकट करने के लिए सभी छवियों का निर्माण करने के लिए आवश्यक है। अधिक जानकारी के लिए डॉक्स को देखें [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).

3. अपने `gatsby-config.js` फ़ाइल में` प्लगइन्स `सरणी में प्लगइन जोड़ें।

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: "GatsbyJS",
        short_name: "GatsbyJS",
        start_url: "/",
        background_color: "#6b37bf",
        theme_color: "#6b37bf",
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: "standalone",
        icon: "src/images/icon.png", // This path is relative to the root of the site.
        // An optional attribute which provides support for CORS check.
        // If you do not provide a crossOrigin option, it will skip CORS for manifest.
        // Any invalid keyword or empty string defaults to `anonymous`
        crossOrigin: `use-credentials`,
      },
    },
  ]
}
```

एक गैट्सबी साइट पर एक वेब मेनिफ़ेस्ट जोड़ने के साथ आपको शुरुआत करने के लिएी यह सब काफी है। दिया गया उदाहरण आधार विन्यास को दर्शाता है - देखें [plugin reference](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) अधिक विकल्पों के लिए।
