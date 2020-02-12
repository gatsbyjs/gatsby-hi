---
title: 404 पेज ऐड करना
---

<<<<<<< HEAD
404 पेज बनाने के लिए एक पेज बनाये जिसका पाथ `^\/?404\/?$` (`/404/`, `/404`, `404/` or `404`) regex से मेल खाता हो। ज़्यादातर आप एक React कौम्पोनॅन्ट पेज बनाना चाहेंगे `src/pages/404.js`।

Gatsby यह सुनिश्चित करता है कि आपका 404 पेज `404.html` की तरह बना हो क्यूंकि ज़्यादातर स्टेटिक होस्टिंग प्लेटफॉर्म्स इसीको डिफ़ॉल्ट रूप से 404 एरर पेज की तरह इस्तेमाल करते है। यदि आप अपनी साइट को दूसरे तरीके से होस्ट कर रहे हैं, तो आपको 404 एर्ररस के लिए इस फ़ाइल को सर्व करने के लिए एक कस्टम नियम सेट-अप करने की आवश्यकता होगी।

क्योंकि Gatsby डिफ़ॉल्ट रूप से आपके लिए यह पेज बनाता है, इसलिए इसे आपकी `gatsby-node.js` फ़ाइल में कॉन्फ़िगर करने की कोई आवश्यकता नहीं है।

प्रयोग करते समय `gatsby develop`, Gatsby एक डिफ़ॉल्ट 404 पेज का उपयोग करता है जो आपके कस्टम 404 पेज को ओवरराइड करता है। हालाँकि, आप अभी भी अपने 404 पेज का पूर्वावलोकन कर सकते हैं "कस्टम 404 पेज का प्रीव्यू करें" पर क्लिक करके यह सत्यापित करें कि यह अपेक्षित है। यह उपयोगी है जब आप विकसित कर रहे हैं ताकि आप सभी उपलब्ध पेजेज को देख सकें।


नीचे दिया गया स्क्रीनशॉट Gatsby द्वारा बनाए गए डिफ़ॉल्ट 404 पेज को दिखाता है।
ये वेब्सीटेस के सारे पेजेज को लिस्ट करता है। "प्रीव्यू कस्टम 404 पेज" बटन को क्लिक करने से ये आपको 404 पेज देखने की अनुमति देगा।
![Gatsby Default 404 Page](images/gatsby-default-404.png)

नीचे दिया गया स्क्रीनशॉट कस्टम 404 पेज दिखाता है।
![Gatsby Custom 404 Page](images/gatsby-custom-404.png)
=======
To create a 404 page create a page whose path matches the regex `^\/?404\/?$` (`/404/`, `/404`, `404/` or `404`). Most often you'll want to create a React component page at `src/pages/404.js`.

Gatsby ensures that your 404 page is built as `404.html` as many static hosting platforms default to using this as your 404 error page. If you're hosting your site another way you'll need to set up a custom rule to serve this file for 404 errors.

Because Gatsby creates this page for you by default, there is no need to configure it in your `gatsby-node.js` file.

When developing using `gatsby develop`, Gatsby uses a default 404 page that overrides your custom 404 page. However, you can still preview your 404 page by clicking "Preview custom 404 page" to verify that it's working as expected. This is useful when you're developing so that you can see all the available pages.

The screenshot below shows the default 404 page that Gatsby creates. It also lists out all the pages on your website. Clicking the "Preview custom 404 page" button will allow you to view the 404 page you created.
![Gatsby Default 404 Page](./images/gatsby-default-404.png)

The screenshot below shows the custom 404 page.
![Gatsby Custom 404 Page](./images/gatsby-custom-404.png)
>>>>>>> fd3df38d5351bfbf1bf86cb9e0c8cc80dc9ba2a7
