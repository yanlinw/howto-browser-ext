---
title: Browser Extension Howto
description: How to develop browser extension
marp: true
paginate: true
theme: default
---
![bg right](https://i0.wp.com/techrafiki.com/wp-content/uploads/2021/03/browser-extensies-1216x856-1.jpg?resize=696%2C490&ssl=1)



browser extesion howtos 
====

# ![]()


[yanlinw@yahoo.com](yanlinw@yahoo.com)

---
![bg right 95%](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Anatomy_of_a_WebExtension/webextension-anatomy.png)

# anatomy of an extension
# ![]()

---
![bg left 95%](https://wd.imgix.net/image/BrQidfK9jaQyIHwdw91aVpkPiib2/466ftDp0EXB4E1XeaGh0.png?auto=format&w=439)
# Architecture
# ![]()

---

# message passing

```js
//Sending a request from a content script
chrome.runtime.sendMessage({greeting: "hello"}, function(response) {
  console.log(response.farewell);
});

//Sending a request from the extension to a content script
chrome.tabs.query({active: true, currentWindow: true}, function(tabs) {
  chrome.tabs.sendMessage(tabs[0].id, {greeting: "hello"}, function(response) {
    console.log(response.farewell);
  });
});

//the listener 
chrome.runtime.onMessage.addListener(
  function(request, sender, sendResponse) {
    console.log(sender.tab ?
                "from a content script:" + sender.tab.url :
                "from the extension");
    if (request.greeting === "hello")
      sendResponse({farewell: "goodbye"});
  }
);
```
---

# chrome extension debug

- chrome upacked
- webpack server + hot file save https://github.com/lxieyang/chrome-extension-boilerplate-react
- 'inspect view' for background.js debug 
- 'devtool' for content scripts

----

# firefox extension debug

- firefox load temporary add-on
- archive into zip (no unpack)
- inspect for for background.js debug
- 'devtool' for content scripts
- cmd + shift + J to bring up the browser console (content loading)

---




