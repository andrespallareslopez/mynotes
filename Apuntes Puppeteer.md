# Apuntes Puppeteer
Utilizar la version 14.4.1 de puppeteer

### Puppeteer Quick Tip: How to do Basic Authentication ###

https://dev.to/sonyarianto/puppeteer-quick-tip-how-to-do-basic-authentication-2pe7

___

### Automatically Login to Google Using Puppeteer ###

https://www.youtube.com/watch?v=CRi6PJOauSQ

para autenticarse para la cuenta de google, en este ejemplo, necesitamos dos librerias mas:

~~~
npm install puppeteer-extra
npm install puppeteer-extra-plugin-stealth
~~~



~~~
const { Keyboard } = require('puppeteer');
const puppeteer = require('puppeteer-extra');
const StealthPlugin = require('puppeteer-extra-plugin-stealth');

puppeteer.use(StealthPlugin());

const googleUsername = "YOUR_USERNAME";
const googlePassword = "YOUR_PASSWORD";

(async () => {
   const browser = await puppeteer.launch({
      headless: false,
      args:[
         '--no-sandbox',
         '--disable-gpu',
         '--enable-webgl',
         '--window-size=800,800'
      ]
   }); 

   const loginUrl = "https://accounts.google.com/AccountChooser?service=mail&continue=https://google.com&hl=en";
   const ua = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.91 Mobile Safari/537.36'; 
   const page = await browser.newPage();

   await page.setUserAgent(ua);
   await page.goto(loginUrl, { waitUntil: 'networkidle2' });
   await page.type('input[type="email"]', googleUsername);
   await page.keyboard.press('Enter');
   await page.waitForTimeout(2000);
   await page.type('input[type="password"]', googlePassword);
   await page.keyboard.press('Enter');
})();
~~~



___

### Web scraper using Puppeteer - How to login to a website? ###

https://browsee.io/blog/web-scraper-using-puppeteer-how-to-login-to-a-website/



Fichero constas.js
~~~
module.exports = {
                   username: 'abcd@abc.com',
                   password: 'abc123'
                 }


~~~

Fichero scraper.js
~~~
const puppeteer = require('puppeteer');
const C = require('./constants');
const USERNAME_SELECTOR = '#login-email';
const PASSWORD_SELECTOR = '#login-password';
const CTA_SELECTOR = '#login-submit';

async function startBrowser() {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  return {browser, page};
}

async function closeBrowser(browser) {
  return browser.close();
}

async function playTest(url) {
  const {browser, page} = await startBrowser();
  page.setViewport({width: 1366, height: 768});
  await page.goto(url);
  await page.click(USERNAME_SELECTOR);
  await page.keyboard.type(C.username);
  await page.click(PASSWORD_SELECTOR);
  await page.keyboard.type(C.password);
  await page.click(CTA_SELECTOR);
  await page.waitForNavigation();
  await page.screenshot({path: 'linkedin.png'});
}

(async () => {
  await playTest("https://www.linkedin.com/");
  process.exit(1);
})();
~~~


___

How To Submit A Form With Puppeteer?

https://www.scrapingbee.com/blog/submit-form-puppeteer/

~~~
const puppeteer = require('puppeteer');
    async function main() {
        const browser = await puppeteer.launch({
            headless: false
        });
        const page = await browser.newPage();
        await page.goto('https://www.scrapingbee.com/');
        await page.waitForTimeout(5000); // wait for 5 seconds
        await browser.close();
    }
    main();
~~~


Ejemplo de autenticacion
~~~
const puppeteer = require('puppeteer');
    async function main() {
        const browser = await puppeteer.launch({
            headless: false
        });
        const page = await browser.newPage();
        await page.goto('https://www.yelp.com/');
        await page.type('#find_desc', 'Pizza Delivery');
        await page.type('#dropperText_Mast', 'Toronto, ON');
        await page.click('#header-search-submit');
        await page.waitForTimeout(5000); // wait for 5 seconds
        await browser.close();
    }
    main();
~~~

Ejemplo de autenticacion con page.evaluate
~~~
async function withInputName() {
        const browser = await puppeteer.launch({
            headless: false
        });
        const page = await browser.newPage();
        await page.goto('https://github.com/login');
        
        await page.type('input[id=login_field]', 'John');
        await page.type('input[name=password]', 'Password');
        await page.evaluate(() => {
            document.querySelector('input[type=submit]').click();
        });
    }
    withInputName();
~~~

Ejemplo de subir un archivo
~~~
async function uploadFile() {
        const browser = await puppeteer.launch({
            headless: false
        });
        const page = await browser.newPage();
        await page.goto('https://www.w3schools.com/howto/howto_html_file_upload_button.asp');
        const element = await page.$("input[type=file]");
        await element.uploadFile('./myfile.pdf');
    }
    uploadFile();

~~~

___




___