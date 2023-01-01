Playwright Links and code

Official website
https://playwright.dev/
https://playwright.dev/docs/intro
https://playwright.dev/docs/api/class-playwright	
https://playwright.dev/docs/intro
https://playwright.dev/docs/test-assertions#list-of-assertions
https://playwright.dev/docs/actionability
https://playwright.dev/docs/locators
https://playwright.dev/docs/test-configuration
https://www.npmjs.com/package/allure-playwright
https://github.com/allure-framework/allure-js/tree/master/packages/allure-playwright

Installation and Setup
	1. Node.js installation
	2. VS Code
	3. Execute below NPM commands
	
NPM Commands in Playwright
	Setup playwright project
		npm init playwright  		
	
	Run playwright in headless mode with default configuration
		npm playwright test
	
	Run playwright in headed mode
		npm playwright test --headed
	
	To open last HTML report run
		npx playwright show-report
		
	To execute specific file
		npm playwright test tests/file1.spec.js
		
	To execute test in debug mode	
		npm playwright test tests/file1.spec.js --debug
		
	To generate playwright code
		npx playwright codegen http://www.google.com
		
	To execute custom command which saed in package.json file
		npm rum <custom Command>
	
====================================================

Playwright Code Snippets

const {test, expect} = require('@playwright/test');	

test("First Playwright Test", async ({ browser }) => {
	const context = await browser.newContext();
	const page = await context.newPage();
	await page.goto("https://rahulshettyacademy.com/loginpagePractise/");
}

const {test, expect} = require('@playwright/test');	
test("Second Playwright Test", async ({ page }) => {
	await page.goto("https://www.google.com");
	await expect(page).toHaveTitle("Google");
}

//configure browser
Update below details playwright.config.js
use:{
	browserName: 'chromium'
}


// execute specific test in file
	use .only keyword in test as below

test.only("Second Playwright Test", async ({ page }) => {
	await page.goto("https://rahulshettyacademy.com/loginpagePractise/");
}

	
//configure headless property
Update below details playwright.config.js

use:{
	headless: true
}	

// Configure timeout for expect assertions
Update below details playwright.config.js

expect:{
	timeout: 5000
}

// Configure timeout at script level
Update below details playwright.config.js
const config = {
  testDir: './tests',
  retries :1,
  
  /* Maximum time one test can run for. */
  timeout: 30 * 1000,
}


test("Third Playwright Test", async ({ browser }) => {
	const context = await browser.newContext();
	const page = await context.newPage();
	await page.goto("https://rahulshettyacademy.com/loginpagePractise/");
	console.log(await page.title());
	//css
	await page.locator('#userName').type("rahulshetty");
	await page.locator('[type='password']').type("learning");
	await page.locator('#signIn').click();
	console.log(await page.locator("[style*='block']").textContent());
	await expect(page.locator("[style*='block']")).toContainText("Incorrect");
}


test("Fourth Playwright Test", async ({ browser }) => {
	const context = await browser.newContext();
	const page = await context.newPage();  
	const userName = page.locator("#username");
	const signIn = page.locator("#signInBtn");
	await page.goto("https://rahulshettyacademy.com/loginpagePractise/");
	console.log(await page.title());
	//css
	await userName.type("rahulshetty");
	await page.locator("[type='password']").type("learning");
	await signIn.click();
	console.log(await page.locator("[style*='block']").textContent());
	await expect(page.locator("[style*='block']")).toContainText("Incorrect");
	//type - fill
	await userName.fill("");
	await userName.fill("rahulshettyacademy");
	//race condition
	await Promise.all([page.waitForNavigation(), signIn.click()]);
	console.log(await cardTitles.first().textContent());
	console.log(await cardTitles.nth(1).textContent());
	const allTitles = await cardTitles.allTextContents();

	console.log(allTitles);
	await page.pause();
}


test("@Web UI Controls", async ({ page }) => {
	await page.goto("https://rahulshettyacademy.com/loginpagePractise/");
	const userName = page.locator("#username");
	const signIn = page.locator("#signInBtn");
	const documentLink = page.locator("[href*='documents-request']");
	const dropdown = page.locator("select.form-control");
	await dropdown.selectOption("consult");
	await page.locator(".radiotextsty").last().click();  // select last instance with given xpath
	await page.locator("#okayBtn").click();
	console.log(await page.locator(".radiotextsty").last().isChecked());
	await expect(page.locator(".radiotextsty").last()).toBeChecked();
	await page.locator("#terms").click();   // check checkbox
	await expect(page.locator("#terms")).toBeChecked();
	await page.locator("#terms").uncheck();  // Uncheck checkbox
	expect(await page.locator("#terms").isChecked()).toBeFalsy(); // verify is checkbox checked
	await expect(documentLink).toHaveAttribute("class", "blinkingText");
});


// Handle child window
test("Child windows hadl", async ({ browser }) => {
	const context = await browser.newContext();
	const page = await context.newPage();
	const userName = page.locator("#username");
	await page.goto("https://rahulshettyacademy.com/loginpagePractise/");
	const documentLink = page.locator("[href*='documents-request']");

	const [newPage] = await Promise.all([
	context.waitForEvent("page"),
	documentLink.click(),
	]);

	const text = await newPage.locator(".red").textContent();
	const arrayText = text.split("@");
	const domain = arrayText[1].split(" ")[0];
	console.log(domain);
	await page.locator("#username").type(domain);
	console.log(await page.locator("#username").textContent());
});

configure screenshot
Update below details playwright.config.js

use:{
	screenshot: 'on'
}	

Configure trace for each step in script
Update below details playwright.config.js

use:{
	trace: 'on'
}


// TO make delay in typing
await page.locator("[placeholder*='Country']").type("ind",{delay:100});


// Locator chaining in playwright
const count = await products.count();
for(let i =0; i < count; ++i){
	if(await products.nth(i).locator("b").textContent() === productName){
		//add to cart
		await products.nth(i).locator("text= Add To Cart").click();
		break;
	 }
}


// Naviagte back and forward
await page.goto("https://rahulshettyacademy.com/AutomationPractice/");
await page.goto("http://google.com");
await page.goBack();
await page.goForward();


// visibility and invisibility of element
await expect(page.locator("#displayed-text")).toBeVisible();
await page.locator("#hide-textbox").click();
await expect(page.locator("#displayed-text")).toBeHidden();



// Handle javaScript Alert
page.on('dialog',dialog => dialog.accept());
page.on('dialog',dialog => dialog.dismiss());


// Hover over an element
await page.locator("#mousehover").hover();


// Switch to frame
const framesPage = page.frameLocator("#courses-iframe");
await framesPage.locator("li a[href*='lifetime-access']:visible").click();  // Switch to only visible locator
 const textCheck =await framesPage.locator(".text h2").textContent();
console.log(textCheck.split(" ")[1]);


// Wait stratergies
await dropdown.waitFor();
await page.waitForLoadState('networkidle');
context.waitForEvent("page");
page.waitForNavigation()

// List of Assertions
https://playwright.dev/docs/test-assertions#list-of-assertions


// Test Login api/class-playwright
const {test, expect, request} = require('@playwright/test');
const loginPayLoad = {userEmail:"anshika@gmail.com",userPassword:"Iamking@000"};

const apiContext = await request.newContext();

const loginResponse =  await this.apiContext.post("https://rahulshettyacademy.com/api/ecom/auth/login",{data:this.loginPayLoad})//200,201,
const loginResponseJson = await loginResponse.json();
const token =loginResponseJson.token;
console.log(token);	

// End to End API & Web Mix Test
APIUtils Path : C:\Users\DELL\Downloads\PlayWrightAutomation\PlayWrightAutomation\utils\APiUtils.js

Script code : C:\Users\DELL\Downloads\PlayWrightAutomation\PlayWrightAutomation\tests\WebAPIPart1.spec.js


// Copy All data from Local Storage to Json file using API code
test.beforeAll(async({browser})=>{  
    const context = await browser.newContext();
    const page = await context.newPage();
    await page.goto("https://rahulshettyacademy.com/client");
    await page.locator("#userEmail").fill("anshika@gmail.com");
    await page.locator("#userPassword").type("Iamking@000");
    await page.locator("[value='Login']").click();
    await page.waitForLoadState('networkidle');
    await context.storageState({path: 'state.json'});
    webContext=  await browser.newContext({storageState:'state.json'});
})

//Injecting Local Storage into test using webContext
test('@API Test case 2', async ()=>{
    const email = "";
    const productName = 'Zara Coat 4';
    const page =  await webContext.newPage();
    await page.goto("https://rahulshettyacademy.com/client");
    await page.waitForLoadState('networkidle');
    const products = page.locator(".card-body");
    const titles= await page.locator(".card-body b").allTextContents();
   console.log(titles);

})


// Mock Response & Inject dummy data in response
test.skip('Place the order', async ({page})=>{
    page.addInitScript(value => {
        window.localStorage.setItem('token',value);
    }, response.token );
	await page.goto("https://rahulshettyacademy.com/client/");

	await page.route("https://rahulshettyacademy.com/api/ecom/order/get-orders-for-customer/62026f4edfa52b09e0a20b18",
	async route=>{
	  const response =  await page.request.fetch(route.request());
	  let body =fakePayLoadOrders;
	   route.fulfill(
		  {
			response,
			body,
		  });
		//intercepting response - APi response->{ playwright fakeresponse}->browser->render data on front end
	});

	await page.locator("button[routerlink*='myorders']").click();
	//await page.pause();
	console.log(await page.locator(".mt-4").textContent());
});

// Debug Web and API Script in Playwright
https://www.udemy.com/course/playwright-tutorials-automation-testing/learn/lecture/31110862#overview


// Open trace file
 drop file into trace.playwright.dev
 
 
// Mock request & Inject dummy data in request
const {test, expect, request} = require('@playwright/test');
const {APiUtils} = require('../utils/APiUtils');
const loginPayLoad = {userEmail:"rahulshetty@gmail.com",userPassword:"Iamking@00"};
const orderPayLoad = {orders:[{country:"Cuba",productOrderedId:"62023a7616fcf72fe9dfc619"}]};
const fakePayLoadOrders = {data:[],message:"No Orders"};

let response;
test.beforeAll( async()=>{
   const apiContext = await request.newContext();
   const apiUtils = new APiUtils(apiContext,loginPayLoad);
   response =  await apiUtils.createOrder(orderPayLoad);
})

test('Place the order', async ({page})=>{
    page.addInitScript(value => {
        window.localStorage.setItem('token',value);
    }, response.token );
	await page.goto("https://rahulshettyacademy.com/client/");
	await page.locator("button[routerlink*='myorders']").click();
	await page.route("https://rahulshettyacademy.com/api/ecom/order/get-orders-details?id=6218dad22c81249b296508b9",
	route=> route.continue({url: 'https://rahulshettyacademy.com/api/ecom/order/get-orders-details?id=621661f884b053f6765465b6'})
	)
	await page.locator("button:has-text('View')").first().click();
});


// Abort Network calls for request and response
https://www.udemy.com/course/playwright-tutorials-automation-testing/learn/lecture/31110920#overview


// Capture Screenshot
test("Screenshot & Visual comparision",async({page})=>{
    await page.goto("https://rahulshettyacademy.com/AutomationPractice/");
    await expect(page.locator("#displayed-text")).toBeVisible();
    await page.locator('#displayed-text').screenshot({path:'partialScreenshot.png'}); // Object level screenshot
    await page.locator("#hide-textbox").click();
    await page.screenshot({path: 'screenshot.png'});  // Page level screenshot
    await expect(page.locator("#displayed-text")).toBeHidden();
});


// Visual Testing with playwright
//screenshot -store -> screenshot -> 
test('visual',async({page})=>{    
    await page.goto("https://rahulshettyacademy.com/loginpagePractise/");
    expect(await page.screenshot()).toMatchSnapshot('landing.png');

})

// Page Object Model

POManager.js
const { LoginPage } = require("./LoginPage");
const { DashboardPage } = require("./DashboardPage");
const { OrdersHistoryPage } = require("./OrdersHistoryPage");
const { OrdersReviewPage } = require("./OrdersReviewPage");
const { CartPage } = require("./CartPage");

class POManager {
  constructor(page) {
    this.page = page;
    this.loginPage = new LoginPage(this.page);
    this.dashboardPage = new DashboardPage(this.page);
    this.ordersHistoryPage = new OrdersHistoryPage(this.page);
    this.ordersReviewPage = new OrdersReviewPage(this.page);
    this.cartPage = new CartPage(this.page);
  }

  getLoginPage() {
    return this.loginPage;
  }

  getCartPage() {
    return this.cartPage;
  }

  getDashboardPage() {
    return this.dashboardPage;
  }
  getOrdersHistoryPage() {
    return this.ordersHistoryPage;
  }

  getOrdersReviewPage() {
    return this.ordersReviewPage;
  }
}
module.exports = { POManager };


LoginPage.js
class LoginPage {
  constructor(page) {
    this.page = page;
    this.signInbutton = page.locator("[value='Login']");
    this.userName = page.locator("#userEmail");
    this.password = page.locator("#userPassword");
  }

  async goTo() {
    await this.page.goto("https://rahulshettyacademy.com/client");
  }

  async validLogin(username, password) {
    await this.userName.type(username);
    await this.password.type(password);
    await this.signInbutton.click();
    await this.page.waitForLoadState("networkidle");
  }
}
module.exports = { LoginPage };

Test1.js

test(`Client App login`, async ({ page, testDataForOrder }) => {
	const poManager = new POManager(page);
	//js file- Login js, DashboardPage
	const products = page.locator(".card-body");
	const loginPage = poManager.getLoginPage();
	await loginPage.goTo();
	await loginPage.validLogin(testDataForOrder.username, testDataForOrder.password);
	
	const dashboardPage = poManager.getDashboardPage();	
	await dashboardPage.navigateToCart();

	const cartPage = poManager.getCartPage();	
	await cartPage.Checkout();
});


// Data Driven Testing
TestData.json

[
  {
    "username": "anshika@gmail.com",
    "password": "Iamking@000",
    "productName": "Zara Coat 4"
  },
  {
    "username": "rahulshetty@gmail.com",
    "password": "Iamking@00",
    "productName": "Adidas Orignals"
  }
]

Test1.js

const { test, expect } = require("@playwright/test");
const { POManager } = require("../pageobjects/POManager");
const dataset = JSON.parse(
  JSON.stringify(require("../utils/placeorderTestData.json"))
);

test('Client App Login', async ({ page }) => {
    const poManager = new POManager(page);
    //js file- Login js, DashboardPage
    const products = page.locator(".card-body");
    const loginPage = poManager.getLoginPage();
    await loginPage.goTo();
    await loginPage.validLogin(data.username, data.password);
    const dashboardPage = poManager.getDashboardPage();
    await dashboardPage.searchProductAddCart(data.productName);
    await dashboardPage.navigateToCart();

    const cartPage = poManager.getCartPage();
    await cartPage.VerifyProductIsDisplayed(data.productName);
    await cartPage.Checkout();
}
 
// Parameterise Test with mutiple data set
Test1.js

const { test, expect } = require("@playwright/test");

const { POManager } = require("../pageobjects/POManager");
const dataset = JSON.parse(
  JSON.stringify(require("../utils/placeorderTestData.json"))
);

for (const data of dataset) {
  test(`@Web Client App login for ${data.productName}`, async ({ page }) => {
    const poManager = new POManager(page);
    //js file- Login js, DashboardPage
    const products = page.locator(".card-body");
    const loginPage = poManager.getLoginPage();
    await loginPage.goTo();
    await loginPage.validLogin(data.username, data.password);
    const dashboardPage = poManager.getDashboardPage();
    await dashboardPage.searchProductAddCart(data.productName);
    await dashboardPage.navigateToCart();

    const cartPage = poManager.getCartPage();
    await cartPage.VerifyProductIsDisplayed(data.productName);
    await cartPage.Checkout();

    const ordersReviewPage = poManager.getOrdersReviewPage();
    await ordersReviewPage.searchCountryAndSelect("ind", "India");
    const orderId = await ordersReviewPage.SubmitAndGetOrderId();
    console.log(orderId);
    await dashboardPage.navigateToOrders();
    const ordersHistoryPage = poManager.getOrdersHistoryPage();
    await ordersHistoryPage.searchOrderAndSelect(orderId);
    expect(orderId.includes(await ordersHistoryPage.getOrderId())).toBeTruthy();
  });
}

// Data Driven Test using Fixture

TestData.js

const base = require("@playwright/test");

exports.customtest = base.test.extend({
  testDataForOrder: {
    username: "anshika@gmail.com",
    password: "Iamking@000",
    productName: "Zara Coat 4",
  },
});


const { test, expect } = require("@playwright/test");
const { customtest } = require("../utils/test-base");

const { POManager } = require("../pageobjects/POManager");
const dataset = JSON.parse(
  JSON.stringify(require("../utils/placeorderTestData.json"))
);

Test1.js

customtest(`Client App login`, async ({ page, testDataForOrder }) => {
  const poManager = new POManager(page);
  //js file- Login js, DashboardPage
  const products = page.locator(".card-body");
  const loginPage = poManager.getLoginPage();
  await loginPage.goTo();
  await loginPage.validLogin(
    testDataForOrder.username,
    testDataForOrder.password
  );
  const dashboardPage = poManager.getDashboardPage();
  await dashboardPage.searchProductAddCart(testDataForOrder.productName);
  await dashboardPage.navigateToCart();

  const cartPage = poManager.getCartPage();
  await cartPage.VerifyProductIsDisplayed(testDataForOrder.productName);
  await cartPage.Checkout();
});


// Execute with Custom Config file
npm playwright test tests/file1.spec.js --config <CustomConfig.File.js>

// Multiple Configuration for project in same config file
Update playwright.config.js file as below

  projects : [
    {
      name : 'safari',
      use: {

        browserName : 'webkit',
        headless : true,
        screenshot : 'off',
        trace : 'on',//off,on 
        ...devices['iPhone 11'],    
      }

    },
    {
      name : 'chrome',
      use: {

        browserName : 'chromium',
        headless : false,
        screenshot : 'on',
        video: 'retain-on-failure',
        ignoreHttpsErrors:true,
        permissions:['geolocation'],
        
        trace : 'on',//off,on
       // ...devices['']
     //   viewport : {width:720,height:720}
         }

    }
    ]
	
	Hit below command in command line
	npm playwright test tests/file1.spec.js --config <CustomConfig.File.js> --project=<Project Name>
	
Configure Browser size
	Update playwright.config.js file as below
	
	use: {
       viewport : {width:720,height:720}
    }
	 
	 
Configure Browser size as per mobile device screen size	 
	Update playwright.config.js file as below
	
	use: {
       ...devices['iPhone 11'],  
    }
	 
Ignore SSL Certificate for website	 
	Update playwright.config.js file as below
	
	use: {
       ignoreHttpsErrors:true, 
	   permissions:['geolocation'],	   
    }
	 
	 
Configure video recording for test
	Update playwright.config.js file as below
	
	use: {
       video: 'retain-on-failure',  
    }
	 
Configure Retry failed test cases	 
	Update playwright.config.js file as below
	
	const config = {	  
	  retries :1,	
	};
	
	
Configure to execute test in parallel	
	Update playwright.config.js file as below
	
	const config = {	  
		  workers: 3,	
	};
	
Configure to execute test in parallel & serial	
	test.describe.configure({mode:'serial'});	
	test.describe.configure({mode:'parallel'});
	
Tag test cases for execution

customtest(`@Web Client App login`, async ({ page, testDataForOrder }) => {
  const poManager = new POManager(page);
  //js file- Login js, DashboardPage
  const products = page.locator(".card-body");
  const loginPage = poManager.getLoginPage();
  await loginPage.goTo();
  await loginPage.validLogin(
    testDataForOrder.username,
    testDataForOrder.password
  );
  
  Hit below command in command line
	npm playwright test tests/file1.spec.js --grep @Web
	
	
Generate HTML Report
	Update playwright.config.js file as below
	
	const config = {
		reporter: 'html'
	}
	
	
Generate Allure Report	
	Enter command in command prompt
		npm i -D @playwright/test allure-playwright
	Execute script by providing allure configuration in command
		npm playwright test tests/file1.spec.js --reporter=line,allure-playwright
	Generate allure report
		allure generate ./allure-results --clean
	Open Allure Report
		allure open ./allure-report
