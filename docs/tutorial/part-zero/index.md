---
title: अपना विकास पर्यावरण तैयार करें
typora-copy-images-to: ./
disableTableOfContents: true
---

इससे पहले कि आप अपनी पहली गैट्सबी साइट का निर्माण शुरू करें, आपको कुछ मुख्य वेब तकनीकों से खुद को परिचित करना होगा और यह सुनिश्चित करना होगा कि आपने सभी आवश्यक सॉफ़्टवेयर टूल स्थापित कर लिए हैं|

## कमांड लाइन से खुद को परिचित करें

कमांड लाइन एक टेक्स्ट-आधारित इंटरफ़ेस है जिसका उपयोग आपके कंप्यूटर पर कमांड चलाने के लिए किया जाता है। आप अक्सर इसे टर्मिनल के रूप में भी देखेंगे| इस ट्यूटोरियल में, हम दोनों का परस्पर उपयोग करते हैं। विंडोज पर मैक या एक्सप्लोरर पर फाइंडर का उपयोग करना बहुत पसंद है। खोजक और एक्सप्लोरर ग्राफिकल यूजर इंटरफेस (जीयूआई) के उदाहरण हैं। कमांड लाइन आपके कंप्यूटर के साथ बातचीत करने का एक शक्तिशाली पाठ-आधारित तरीका है।

अपने कंप्यूटर के लिए कमांड लाइन इंटरफ़ेस (CLI) का पता लगाने और खोलने के लिए कुछ समय लें। निर्भर करता है कि आप किस ऑपरेटिंग सिस्टम का उपयोग कर रहे हैं, देखें [**Mac के लिए निर्देश**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**Windows के लिए निर्देश**](https://www.quora.com/How-do-I-open-terminal-in-windows) or [**Linux के लिए निर्देश**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

## Node.js के लिए Homebrew स्थापित करें

Gatsby और Node.js को स्थापित करने के लिए, इसका उपयोग करने की अनुशंसा की जाती है [Homebrew](https://brew.sh/). शुरुआत में थोड़ा सेट अप आपको बाद में कुछ सिरदर्द से बचा सकता है! अपने कंप्यूटर पर Homebrew को कैसे स्थापित या सत्यापित करें:

1. अपना टर्मिनल खोलें।
1. देखें कि क्या Homebrew `brew -v` चलाकर स्थापित किया गया है। आपको "Homebrew" और एक संस्करण संख्या देखनी चाहिए।
1. यदि नहीं, तो निर्देशों के साथ [Homebrew](https://docs.brew.sh/Installation) डाउनलोड और इंस्टॉल करें आपके ऑपरेटिंग सिस्टम के लिए (Mac, Linux or Windows).
1. Homebrew स्थापित करने के बाद, सत्यापित करने के लिए चरण 2 को दोहराएं।

### Mac उपयोगकर्ता: Xcode कमांड लाइन उपकरण स्थापित करें

1. अपना टर्मिनल खोलें।
1. Mac पर, Xcode कमांड लाइन टूल को रन करके इंस्टॉल करें `xcode-select --install`.
   1. यदि वह विफल रहता है, तो उसे डाउनलोड करें [सीधे Apple साइट से](https://developer.apple.com/download/more/), Apple डेवलपर अकाउंट से साइन-इन करने के बाद
1. इंस्टॉलेशन शुरू करने के लिए प्रेरित होने के बाद, आपको टूल डाउनलोड करने के लिए सॉफ़्टवेयर लाइसेंस स्वीकार करने के लिए फिर से संकेत दिया जाएगा।

## ⌚ Node.js और npm स्थापित करें

Node.js एक ऐसा वातावरण है जो वेब ब्राउज़र के बाहर जावास्क्रिप्ट कोड चला सकता है। Gatsby Node.js. के साथ बनाया गया है गैट्सबी के साथ उठने और चलने के लिए, आपको अपने कंप्यूटर पर हाल ही में संस्करण स्थापित करने की आवश्यकता होगी।

_Note: Gatsby's minimum supported Node.js version is Node 8, but feel free to use a more recent version._

1. Open your Terminal.
1. Run `brew update` to make sure you have the latest version of Homebrew.
1. Run this command to install Node and npm in one go: `brew install node`

Once you have followed the installation steps, make sure everything was installed properly:

### Check your Node.js installation

1.  Open up your terminal.
2.  Run `node --version`. (If you’re new to the command line, “run `command`” means “type `node --version` in the command prompt, and hit the Enter key”. From here on, this is what we mean by “run `command`”).
3.  Run `npm --version`.

The output of each of those commands should be a version number. Your versions may not be the same as those shown below! If entering those commands doesn’t show you a version number, go back and make sure you have installed Node.js.

![Check node and npm versions in terminal](01-node-npm-versions.png)

## Install Git

Git एक स्वतंत्र और खुला स्रोत वितरित संस्करण नियंत्रण प्रणाली है जिसे गति और दक्षता के साथ छोटे से बहुत बड़े परियोजनाओं तक सब कुछ संभालने के लिए डिज़ाइन किया गया है। जब आप एक Gatsby "स्टार्टर" साइट स्थापित करते हैं, तो Gatsby अपने स्टार्टर के लिए आवश्यक फ़ाइलों को डाउनलोड और इंस्टॉल करने के लिए पर्दे के पीछे Git का उपयोग करता है। आपको अपना पहला Gatsby साइट सेट करने के लिए Git इंस्टॉल करना होगा।

Git को डाउनलोड और इंस्टॉल करने के चरण आपके ऑपरेटिंग सिस्टम पर निर्भर करते हैं। अपने सिस्टम के लिए गाइड का पालन करें:

- [Install Git on macOS](https://www.atlassian.com/git/tutorials/install-git#mac-os-x)
- [Install Git on Windows](https://www.atlassian.com/git/tutorials/install-git#windows)
- [Install Git on Linux](https://www.atlassian.com/git/tutorials/install-git#linux)

## Using the Gatsby CLI
 
Gatsby सीएलआई उपकरण आपको नए Gatsby-संचालित साइट बनाने और Gatsby साइटों को विकसित करने के लिए कमांड चलाने की सुविधा देता है। यह एक प्रकाशित npm पैकेज है।

Gatsby CLI npm के माध्यम से उपलब्ध है और इसे विश्व स्तर पर चलाकर स्थापित किया जाना चाहिए `npm install -g gatsby-cli`.

_**Note**: when you install Gatsby and run it for the first time, you'll see a short message notifying you about anonymous usage data that is being collected for Gatsby commands, you can read more about how that data is pulled out and used in the [telemetry doc](/docs/telemetry)._

To see the commands available, run `gatsby --help`.

![Check gatsby commands in terminal](05-gatsby-help.png)

> 💡 If you are unable to successfully run the Gatsby CLI due to a permissions issue, you may want to check out the [npm docs on fixing permissions](https://docs.npmjs.com/getting-started/fixing-npm-permissions), or [this guide](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Create a Gatsby site

Now you are ready to use the Gatsby CLI tool to create your first Gatsby site. Using the tool, you can download “starters” (partially built sites with some default configuration) to help you get moving faster on creating a certain type of site. The “Hello World” starter you’ll be using here is a starter with the bare essentials needed for a Gatsby site.

1.  Open up your terminal.
2.  Run `gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world`. (_Note: Depending on your download speed, the amount of time this takes will vary. For brevity's sake, the gif below was paused during part of the install_).
3.  Run `cd hello-world`.
4.  Run `gatsby develop`.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./03-create-site.mp4" />
  <p>Sorry! You browser doesn't support this video.</p>
</video>

What just happened?

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

- `new` is a gatsby command to create a new Gatsby project.
- Here, `hello-world` is an arbitrary title — you could pick anything. The CLI tool will place the code for your new site in a new folder called “hello-world”.
- Lastly, the GitHub URL specified points to a code repository that holds the starter code you want to use.

```shell
cd hello-world
```

- This says 'I want to change directories (`cd`) to the “hello-world” subfolder'. Whenever you want to run any commands for your site, you need to be in the context for that site (aka, your terminal needs to be pointed at the directory where your site code lives).

```shell
gatsby develop
```

- This command starts a development server. You will be able to see and interact with your new site in a development environment — local (on your computer, not published to the internet).

### View your site locally

Open up a new tab in your browser and navigate to [**http://localhost:8000**](http://localhost:8000/).

![Check homepage](04-home-page.png)

Congrats! This is the beginning of your very first Gatsby site! 🎉

You’ll be able to visit the site locally at [**_http://localhost:8000_**](http://localhost:8000/) for as long as your development server is running. That’s the process you started by running the `gatsby develop` command. To stop running that process (or to “stop running the development server”), go back to your terminal window, hold down the “control” key, and then hit “c” (ctrl-c). To start it again, run `gatsby develop` again!

**Note:** If you are using VM setup like `vagrant` and/or would like to listen on your local IP address, run `gatsby develop -- --host=0.0.0.0`. Now, the development server listens on both 'localhost' and your local IP.

## Set up a code editor

A code editor is a program designed specifically for editing computer code. There are many great ones out there.

### Download VS Code

Gatsby documentation sometimes includes screenshots that were taken in VS Code, so if you don't have a preferred code editor yet, using VS Code will make sure that your screen looks just like the screenshots in the tutorial and docs. If you choose to use VS Code, visit the [VS Code site](https://code.visualstudio.com/#alt-downloads) and download the version appropriate for your platform.

### Install the Prettier plugin

We also recommend using [Prettier](https://github.com/prettier/prettier), a tool that helps format your code to avoid errors.

You can use Prettier directly in your editor using the [Prettier VS Code plugin](https://github.com/prettier/prettier-vscode):

1.  Open the extensions view on VS Code (View => Extensions).
2.  Search for "Prettier - Code formatter".
3.  Click "Install". (After installation you'll be prompted to restart VS Code to enable the extension. Newer versions of VS Code will automatically enable the extension after download.)

> 💡 If you're not using VS Code, check out the Prettier docs for [install instructions](https://prettier.io/docs/en/install.html) or [other editor integrations](https://prettier.io/docs/en/editors.html).

## ➡️ What’s Next?

To summarize, in this section you:

- Learned about the command line and how to use it
- Installed and learned about Node.js and the npm CLI tool, the version control system Git, and the Gatsby CLI tool
- Generated a new Gatsby site using the Gatsby CLI tool
- Ran the Gatsby development server and visited your site locally
- Downloaded a code editor
- Installed a code formatter called Prettier

Now, move on to [**getting to know Gatsby building blocks**](/tutorial/part-one/).

## References

### Overview of core technologies

It’s not necessary to be an expert with these already — if you’re not, don’t worry! You’ll pick up a lot through the course of this tutorial series. These are some of the main web technologies you’ll use when building a Gatsby site:

- **HTML**: A markup language that every web browser is able to understand. It stands for HyperText Markup Language. HTML gives your web content a universal informational structure, defining things like headings, paragraphs, and more.
- **CSS**: A presentational language used to style the appearance of your web content (fonts, colors, layout, etc). It stands for Cascading Style Sheets.
- **JavaScript**: A programming language that helps us make the web dynamic and interactive.
- **React**: A code library (built with JavaScript) for building user interfaces. It’s the framework that Gatsby uses to build pages and structure content.
- **GraphQL**: A query language that allows you to pull data into your website. It’s the interface that Gatsby uses for managing site data.

### What is a website?

For a comprehensive introduction to what a website is--including an intro to HTML and CSS--check out “[**Building your first web page**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)”. It’s a great place to start learning about the web. For a more hands-on introduction to [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css), and [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), check out the tutorials from Codecademy. [**React**](https://reactjs.org/tutorial/tutorial.html) and [**GraphQL**](http://graphql.org/graphql-js/) also have their own introductory tutorials.

### Learn more about the command line

For a great introduction to using the command line, check out [**Codecademy’s Command Line tutorial**](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) for Mac and Linux users, and [**this tutorial**](https://www.computerhope.com/issues/chusedos.htm) for Windows users. Even if you are a Windows user, the first page of the Codecademy tutorial is a valuable read. It explains what the command line is, not just how to interface with it.

### Learn more about npm

npm is a JavaScript package manager. A package is a module of code that you can choose to include in your projects. If you just downloaded and installed Node.js, npm was installed with it!

npm has three distinct components: the npm website, the npm registry, and the npm command line interface (CLI).

- On the npm website, you can browse what JavaScript packages are available in the npm registry.
- The npm registry is a large database of information about JavaScript packages available on npm.
- Once you’ve identified a package you want, you can use the npm CLI to install it in your project or globally (like other CLI tools). The npm CLI is what talks to the registry — you generally only interact with the npm website or the npm CLI.

> 💡 Check out npm’s introduction, “[**What is npm?**](https://docs.npmjs.com/getting-started/what-is-npm)”.

### Learn more about Git

You will not need to know Git to complete this tutorial, but it is a very useful tool. If you are interested in learning more about version control, Git, and GitHub, check out GitHub's [Git Handbook](https://guides.github.com/introduction/git-handbook/).
