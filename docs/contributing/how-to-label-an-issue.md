---

title: किसी समस्या को label कैसे करें
---

## label समस्या क्या हैं?

इश्यू लेबल GitHub में एक उपकरण है जो एक या अधिक श्रेणियों में समूह के मुद्दों के लिए उपयोग किया जाता है।

[Gatsby के label देखें (और उनके विवरण)](https://github.com/gatsbyjs/gatsby/issues/labels)

## label मुद्दे क्यों?

Gatsby एक बहुत ही सक्रिय परियोजना है जिसमें प्रत्येक दिन कई नए मुद्दे खोले जाते हैं। लेबलिंग मुद्दों की पहचान करने में मदद करता है:

- नए योगदानकर्ताओं के लिए अच्छे मुद्दों पर काम करना
- bug की सूचना दी और पुष्टि की
- सुविधा का अनुरोध
- डुप्लिकेट मुद्दों
- ऐसे मुद्दे जो रुके हुए या अवरुद्ध हैं

## मुद्दों को कौन label कर सकता है?

[`Gatsby मेंटेनर्स टीम`](https://github.com/orgs/gatsbyjs/teams/maintainers) का कोई भी सदस्य हो वह
 मुद्दों को लेबल कर सकते हैं।

पुल रिक्वेस्ट को Gatsby प्रोजेक्ट में मर्ज कर आप टीम को आमंत्रित कर सकते हैं। लिस्ट चेक करे
 [`हेल्प चाहिए`](https://github.com/gatsbyjs/gatsby/labels/%F0%9F%93%8D%20status%3A%20help%20wanted) इशू और [कैसे कंट्रीब्यूट करे
गाइड](/contributing/how-to-contribute/) स्टार्ट करने के लिए।

**नोट:** यदि आपके पास पहले से ही एक पुल रिक्वेस्ट मिला है और आपको _नहीं_ मैंटेनेर्स टीम को आमंत्रित किया गया है,तो कृपया जायें [डैशबोर्ड](https://store.gatsbyjs.org/) और डिस्काउंट कोड का रिक्वेस्ट करें। आपको टीम को निमंत्रण मिलना चाहिए — _और आपको मुफ्त Gatsby स्वैग मिलेगा!_ अगर वह काम नहीं करता है, तो कृपया team@gatsbyjs.com पर ईमेल करें और हम आपको आमंत्रित करेंगे।

## किसी समस्या को कैसे लेबल करें

आदर्श रूप से, हर मुद्दे सिंगल होना चाहिए `type:` उस पर लेबल लगाया होगा। वैकल्पिक रूप से ए `status:` लेबल या अन्य लेबल भी लगाए जा सकते हैं।

जारी रखने से पहले, परिचित हो जाएं [Gatsby के इशू लेबल्स और उनके डिस्क्रीप्शन्स ](https://github.com/gatsbyjs/gatsby/issues/labels).

किसी समस्या को लेबल करने के लिए व्यापक चरण हैं:

- एक मुद्दा पढ़ें
- उस समस्या पर लागू होने वाले लेबल चुनें
- वह यह है - वापस बैठो और आराम करो, शायद अच्छी तरह से किए गए काम की संतुष्टि का आनंद लेने के लिए कुछ क्षण लें

Th rest of this document will describe how to choose the right labels for an issue.

### Find an issue that you're interested in

Start with [Gatsby's issues list](https://github.com/gatsbyjs/gatsby/issues) and scroll through until you see a recent one that strikes your interest. Alternatively, you can view the [list of unlabelled issues](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aopen+is%3Aissue+no%3Alabel).

### Read the issue

Read the issue and any comments to understand what the issue is about.

### Choose one `type:` label

Choose a type label from the _labels_ dropdown to the right-hand side of the issue.

![GitHub label dropdown](./images/github-label-list.png)

You can check through the [label descriptions](https://github.com/gatsbyjs/gatsby/issues/labels) for more information on each one.

The most common type of issue is `type: question or discussion`, typically you can apply this to issues that are open-ended or have no clear next step.

It's OK to change the type of an issue as more information becomes available. What starts as `type: question or discussion`, might later need to be changed to `type: bug`.

Changing labels is quick and easily reversible, so don't worry too much about applying a "wrong" label.

Choose an appropriate `type:` label and you're ready to move on to the next step.

### Choose a `status:` label (optional)

Check through the [`status:` labels (and their descriptions)](https://github.com/gatsbyjs/gatsby/issues/labels), if any apply to this issue add them as necessary.

Examples of applying `status:` labels might be:

- An issue that depends on an external dependency being changed could be labelled with `status: blocked`

- An issue with a clear description of how it can be resolved could be labelled `status: help wanted`.

- An issue that's missing information required to help the author could be labelled with `status: needs more info`

- An issue describing a bug without clear steps to reproduce could be labelled with `status: needs reproduction`

- An issue describing a bug where there are steps to reproduce the bug _and_ you've run the code locally and seen the error yourself can be labelled `status: confirmed`

### Choose any other labels

There are a few other labels that can sometimes be applied to an issue. Here are some more examples of when to use them:

- `good first issue` can be used when an issue is a small, clearly defined piece of work that could be completed by someone without in-depth knowledge of Gatsby and how it works. These issues are particularly suitable for people making their first open source contributions.

- `stale?` can be used on an issue where the author has not replied to requests for further information in at least 20 days.

### Finish

And you're done! You can call it a day or go back to the first step to label another issue.

## Conclusion

Labelling issues is a great way to help out on the Gatsby project regardless of your experience level.
