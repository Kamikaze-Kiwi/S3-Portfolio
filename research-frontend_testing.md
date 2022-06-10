# How do I choose and create the right frontend tests for my project?

## Table of contents

- [What is frontend testing?](#what-is-frontend-testing)
- [Why use frontend testing?](#why-use-frontend-testing)
- [What are the most common frontend testing frameworks/tools? Are they useful for this project?](#what-are-the-most-common-frontend-testing-frameworkstools-are-they-useful-for-this-project)
  * [Which test runner should we use for this framework?](#which-test-runner-should-we-use-for-this-framework)
    + [Vitest](#vitest)
    + [Jest](#jest)
    + [Jasmine](#jasmine)
    + [Karma](#karma)
  * [Bonus: Google lighthouse](#bonus-google-lighthouse)
- [Which framework is the best choice for this project?](#which-framework-is-the-best-choice-for-this-project)
- [Which parts of the application should we test?](#which-parts-of-the-application-should-we-test)
  * [Reactivity](#reactivity)
  * [Logical functions](#logical-functions)
  * [Authorization](#authorization)
  * [Error handling](#error-handling)
- [Conclusion](#conclusion)

## What is frontend testing?

Frontend testing is the process of testing the user interface and functionality of a website or web application. This can include testing the layout of pages, testing for broken links, testing forms and user input, and testing the overall look and feel of the site.

## Why use frontend testing?

By thoroughly testing the frontend, you can continuously ensure that (among others);
1. The views look good across different devices/browsers.
2. Logical functions execute correctly and return the expected result.
3. The views correctly change when you (for example) press a button or add an item to a list.
4. Certain views behave differently or don't show at all depending on if authorized or not.

The big advantage of doing it with automatic tests instead of just walking through the application yourself is that you will need to test your application continuously. Every time someone changes any part of the application or any of the frameworks you use has an update, you obviously don't want to have to walk through the entire application. Instead, it would be much better to do all of this with just a single command (or better yet, run them automatically with continuous integration).

By doing it automatically on each push, you ensure that faulty code will never make it to production, meaning the users won't ever be bothered by it.

## What are the most common frontend testing frameworks/tools? Are they useful for this project?
Vue test utils allows things like mounting and emits, which are a vital part of Vue applications. I don't think any other framework does this, and Vue test utils does it quite well, it's also the 'default' implementation for tests in Vue and it has very good documentation. We still need a test runner to actually run the tests.

### Which test runner should we use for this framework?

#### Vitest
Vitest is a fast, Vite-specific test runner. It comes pre-installed with the Vue installation and has good documentation. It also supports a lot of different Javascript frameworks like Vue, Svelte and React, along with NextJs, Ruby and more. Vitest also supplies an optional UI for your test in addition to using the CLI and it also provides a lot of mocking tools, like the ability to mock the system date/time.

#### Jest
Jest is the most popular Javascript test runner out there. It's also the test runner recommended by Vue Test Utils. Jest, just like Vitest, works with a lot of Javascript frameworks like React, Angular and Vue.

#### Jasmine
Jasmine's documentation is a bit confusing and I had a hard time finding any useful info. It also does not tell you the benefits of using Jasmine instead of other runners.

#### Karma
Karma is supported by Vue Test Utils. Vue Test Utils recommends (if you choose Karma), that Mocha for writing the tests, Chai for the assertions and Sinon for creating Spies and Stubs. This is a lot of extra effort and has a much larger potential of causing conflicts. The documentation is alright, though.

### Bonus: Google lighthouse
Google lighthouse is a tool which can be found in Chrome dev tools. It can generate a report to show performance, accesibility, best practises and search engine optimization issues within your webpage. It's very easy to use, as it can scan a page with just a press of a button, with no installation or research needed. Google lighthouse is compatible with this project (it should be compatible with every website anyway). Google Lighthouse doesn't test your code, but it does look at your HTML

While the results of these tests are not the most useful, there is no set up required so it's still worth it to run it occasionally. 

## Which framework is the best choice for this project? 
Vitest and Jest are the two main contenders, but Vitest seems like it just has a few extra nifty features and has the benefit of being pre-installed. It's also possible to use Jest within Vitest, so we don't have to completely drop Jest.

## Which parts of the application should we test?
### Reactivity
This one is especially important when you're using a reactive Javascript framework (which I am). We can test whether the HTML actually properly when user inputs something (like adding something to a list).

### Logical functions
Testing the logic is important for any application. They are also the easiest tests as usually you just call a function and see if the returned value matches the expected value. 

### Authorization
Testing to ensure that only authorized users can view certain webpages and/or certain html elements is also important to test. This way you ensure that ordinary users don't get access to sensitive data or do things with your application only admins are supposed to be able to do.

### Error handling
Testing to ensure users get proper error messages is also important. You want your users to get a clear error message so that they can understand the problem themselves, but you also don't want to accidentally show sensitive information within these error messages.

## Conclusion
We found the best choice for frontend testing our Vue application (Vitest), as well as which kind of tests we should be writing. We also found that Google lighthouse can be a useful tool without any setup required.
