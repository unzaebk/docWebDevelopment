# Как использовать прокси в NodeJS Selenium?

```javascript
const { Builder } =  require('selenium-webdriver');
const chrome = require('selenium-webdriver/chrome');

let proxyAddress = '212.56.139.253:80'
// Setting the proxy-server option is needed to info chrome to use proxy
let option = new chrome.Options().addArguments(`--proxy-server=http://${proxyAddress}`)

const driver = new Builder()
  .forBrowser('chrome')
  .setChromeOptions(option)
  .build()

driver.get('http://whatismyip.host/')
  .then(() => console.log('DONE'))
```


**********
[node.js](/tags/node.js.md)
[Selenium](/tags/Selenium.md)
[proxy](/tags/proxy.md)
