# How do I choose and create the right frontend tests for my project?

## Table of contents

1. [What is frontend testing?](#what-is-frontend-testing)
2. [Why use frontend testing?](#why-use-frontend-testing)
3. [What are the most common frontend testing frameworks/tools?](#what-are-the-most-common-frontend-testing-frameworkstools)
4. [Which parts of the application should we test?](#which-parts-of-the-application-should-we-test)
5. [Conclusion](#conclusion)

## What is frontend testing?

Frontend testing is the process of testing the user interface and functionality of a website or web application. This can include testing the layout of pages, testing for broken links, testing forms and user input, and testing the overall look and feel of the site.

## Why use frontend testing?

By thoroughly testing the frontend, you can continuously ensure that (among others);
1. The views look good across different devices/browsers.
2. Logical functions execute correctly and return the expected result.
3. The views correctly change when you (for example) press a button or add an item to a list.
4. Certain views behave differently or don't show at all depending on if authorized or not.

The big advantage of doing it with automatic tests instead of just walking through the application yourself is that you will need to test your application continuously. Every time someone changes any part of the application or any of the frameworks you use has an update, you obviously don't want to have to walk through the entire application. Instead, it would be much better to do all of this with just a single command (or better yet, run them automatically with continuous integration).

## What are the most common frontend testing frameworks/tools? Are they useful for this project?
Vue test utils allows things like mounting and emits, which are a vital part of Vue applications. I don't think any other framework does this, and Vue test utils does it quite well, it's also the 'default' implementation for tests in Vue and it has very good documentation. We still need a test runner to actually run the tests.

### Which test runner should we use for this framework?

#### Vitest
Vitest is a fast, Vite-specific test runner. It comes pre-installed with the Vue installation

#### Jest
Jest is the biggest Javascript test runner out there. It's also the test runner recommended by Vue Test Utils.

#### Mocha

#### Jasmine

#### Karma

### Bonus: Google lighthouse
Google lighthouse is a tool which can be found in the dev tools. It can generate a report to show performance, accesibility, best practises and search engine optimization issues within your webpage. It's very easy to use, as it can scan a page with just a press of a button, with no installation or research needed. Google lighthouse is compatible with this project (it should be compatible with every website anyway). While the results of these tests are not the most useful, there is no set up required so it's still worth it to run it occasionally.

## Which framework is the best choice for this project? 

## What sub-modules exist for this framework? Are they useful for this project?

## Which parts of the application should we test?

## Conclusion
