# Angular Assignment

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 12.0.5.

This code base was created to demonstrate an application built with Angular that interacts with a mock backend server wtih CRUD operations. The main purpose of this project is to practice developing an e2e automation test suite.

## Get started

### Clone the repo

```shell
git clone https://github.com/Mr-YaRou/angular-assignment-2.git
cd angular-assignment-2
```

### Install the npm dependancies and start application

Install the `npm` packages described in the `package.json` and verify that it works:

```bash
npm install
npm run start:proxy
```

[JSON Server](https://github.com/typicode/json-server) was used as a full fake REST API. Start the `JSON Server` with the following command:

```bash
json-server -w .\\database-sample.json
```

Go to `http://localhost:3000/` to verify `JSON Server` works.

The `npm run start:proxy` command builds (compiles Typescript and copies assets) and watches for changes to the source files and runs the application on  `http://localhost:4200/`. A basic server-side proxy was created for Angular to connect to Json-server.


Shut it down application manually with `Ctrl-C`.

## Functionality Overview

The application created is a Health Appointment Management System. It uses both angular in-memory-web-api and json-server to simulate CRUD operations overy a RESTy API.

**General Functionality:**

- Authenticate users via JWT (Login/Register pages + Logout Button)
- CRUD Usrs (Able to create, read, update and delete users registered as Admin)
- CRUD Appointments (Able to create, read, update Appointments scheduled)
- GET and display paginated list of Appointments

![Demo](https://github.com/Mr-YaRou/angular-assignment-2/blob/main/src/assets/search-demo.gif)

## Testing Overview

These are the test-related scripts:

```bash
npm run tests
```


The end-to-end test framework used is [Protractor](https://www.protractortest.org/#/). Protractor runs tests against the application in a real browser, interacting with it as a user would. Protractor is built on top of WebDriver JS (Selenuim).

Test case flow were designed to be self-cleaning. Below is the list of test cases created:


### Test Script Samples

Form Validation test case on Login page. 

```ts
  it('should display error message if provided incorrect credentails',function()
  {
    browser.get('http://localhost:4200/');
    element(by.xpath('.//input[@formcontrolName="username"]')).sendKeys('incorrect');
    element(by.xpath('.//input[@formcontrolName="password"]')).sendKeys('incorrect');
    element(by.xpath(".//button[contains(text(),'Login')]")).click()
    browser.sleep(1000);
    expect(element(by.xpath(".//span[text()='Username or password is incorrect']")).getText()).toEqual('Username or password is incorrect');
  });
```

Page Redirection test case

```ts
    it('should redirect to Users page and have correct titles ',function()
    {
      element(by.xpath("//a[@routerlink='/users'][text()='Users']")).click();

      expect(element(by.xpath(".//h1[contains(text(),'Manage Users')]")).getText()).toEqual('Manage Users');
      
    });
```

Sample run of Test Automation

![Demo](https://github.com/Mr-YaRou/angular-assignment-2/blob/main/src/assets/test-demo.gif)

At the end of Test execution, a html report will be generated in `/Reports/screenshots/report.html` with browser screenshots of each step.

A Sample report below:

![Demo](https://github.com/Mr-YaRou/angular-assignment-2/blob/main/src/assets/report-demo.png)



