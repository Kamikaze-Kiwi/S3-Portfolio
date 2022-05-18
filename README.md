# S3-Portfolio
### The portfolio for my semester 3 project for software engineering.

## Table of contents

- [Repositories](#repositories)
- [The idea](#the-idea)
- [User stories](#user-stories)
- [Context diagram](#context-diagram)
- [Screen designs](#screen-designs)
- [C4 models](#c4-models)
  * [Level 1](#level-1)
  * [Level 2](#level-2)
  * [Level 3](#level-3)
- [Technology choices](#technology-choices)
  * [Frontend](#frontend)
  * [Backend](#backend)


## Repositories

### Frontend repositories

[Vue web application](https://github.com/MaikelHendrikx1/Bugger_Frontend)

### Backend repositories

[Account microservice](https://github.com/MaikelHendrikx1/account)

[Bug report microservice](https://github.com/MaikelHendrikx1/bugreport)

[Bugger page microservice](https://github.com/MaikelHendrikx1/buggerpage)

## The idea

The goal of this application is to allow video game creators and other software creators to create a place to handle all bugs, glitches and other unintended behaviours. Once a page is created, the creator can assign maintainers to maintain the page and all incoming bug reports. Everyone can now visit this page to view other bug reports and, provided they have an account and are logged in, create bug reports themselves. 


## User stories

### Roles:
•	Owner: The person in charge of a bugger page. The owner can also do everything an maintainer can do. (Probably a higher-up in a company). 

•	Maintainer: A person in charge of handling bug reports. (Probably a developer or someone tasked with tracking bugs in a company). Anything a maintainer can do, the owner can do aswell.

•	Reporter: A person that found a bug and wants to see if it is already known, or otherwise report it themselves. (A person that isn’t part of the company but consumes the product)

#

### Stories:
As an owner, I want to be able to create a page for my application, so that I can track bugs more efficiently.

As an owner, I want to be able to appoint maintainers, so that the bugs can be tracked by the entire organization.

As an owner, I want to be able to remove maintainers, so that people that don’t work at the company anymore lose access to the bug reporting page.

#

As a maintainer, I want to be able to see all reports, so that I can track and fix the bugs.

As a maintainer, I want to be able to remove or solve reports, so that solved and invalid reports don’t clog up the system.

As a maintainer, I want to be able to privatize reports, so that reports that contain sensitive data or potential security exploit aren’t visible to any reporters.

As a maintainer, I want to be able to create a list of software versions, so bugs reports can be assigned to only the version which is being affected by said bug.

#

As a reporter, I want to be able to view and search reports, so that I don’t make a report for a bug which has already been reported.

As a reporter, I want to be able to create a report, so that the developers can fix it.

As a reporter, I want to be able to attach files like images and various text documents to a report, so that I can include things like screenshots and error logs in my report. 

As a reporter, I want to be able to mark a report as private, so that I don’t share sensitive data or potential security exploits with others.


## Context diagram

![ContextDiagram drawio](https://user-images.githubusercontent.com/84376526/167130384-f34ef65e-fe6f-49a4-b9cb-2e0703af6ebc.png)

## Screen designs

### Home screen for a bug report page, the empty box on the right will show either a landing page or a bug report depending on if you have a bug report selected or not.

![Schets](https://user-images.githubusercontent.com/84376526/167130452-ed1d85aa-bd01-4deb-a228-deaf2a11db67.png)


## C4 models

### Level 1

![C4-Level 1 drawio](https://user-images.githubusercontent.com/84376526/167131036-79522e22-8230-4ac2-b826-01b5859dc255.png)
#
### Level 2

![C4-Level 2 drawio](https://user-images.githubusercontent.com/84376526/167131041-90e68349-e33a-4c8a-8921-351c987c7160.png)
#
### Level 3

![C4-Level 3 drawio](https://user-images.githubusercontent.com/84376526/167131046-1c1bdcb1-53c0-43c2-8d01-5ec52517dc12.png)
#

## Technology choices

### Frontend
There are a lot of frameworks to choose from, however. I cut this choice down to 4 frameworks. These are: React, Angular, Vue.js and Svelte. The reason I excluded other frameworks mostly boils down to the fact that most of them are very young and/or not widely used. This is a problem because it will be hard to find any information/tutorials. While Svelte is also a relatively young framework, I included it anyway because I've seen it praised a lot[<sup>[1]</sup>](https://insights.stackoverflow.com/survey/2021/?utm_source=social-share&utm_medium=social&utm_campaign=dev-survey-2021#most-loved-dreaded-and-wanted-webframe-love-dread)[<sup>[2]</sup>](https://2020.stateofjs.com/en-US/technologies/front-end-frameworks/).

|  | **Vue.js** | **React** | **Angular** | **Svelte** |
|:---:|:---:|:---:|:---:|:---:|
| **Documentation** | Good documentation with examples and live sandbox to test code. 8/10 | Decent tutorials but proper documentation is lacking. 6/10 | Quite bad documentation, hard to find what you are looking for. 3/10 | Good documentation and examples. Also a fancy interactive tutorial. 9/10 |
| **Complexity** | A bit complex at first, but it's not a big deal. 7/10 |Not too complex and very readable. 8/10 | Most complex. Code seems unnecessarily complicated for even easy tasks. 4/10 | Not complex at all, can achieve the same as the other frameworks with less work/code while still being readable. 9/10 |
| **Popularity** | Somewhat popular but slowly growing. 6/10 | Very popular and still growing. 10/10 | Quite popular but declining in use. 7/10 | Not very popular but rapidly growing 5/10 |
| **Performance** | Good performance. 8/10 | Decent performance. 7/10 | Mediocre/poor performance. 5/10 | Amazing performance due to not requiring a virtual DOM. 9/10 |
| **Learning curve** | Easy to learn. Would probably take a few days to get the basics down. 8/10 | Easy to learn, slightly easier than Vue. 8.5/10 | Hardest to learn. Could take multiple days or even a week just to get the basics down. 6/10 | Easiest to learn. Could probably get the basics within a day or two. 9/10 |

After this I was still struggling with my choice, although I have now boiled it down to just Vue.js and Svelte.
To make sure I make the right choice, I made the same demo-project in both Vue.js and Svelte.

After making a simple project that fetches some data from a public API in both frameworks, I decided to go with Vue.js. While I really like the simple syntax Svelte has, it's a lot simpler to have a multi-page application in Vue then it is in Svelte. There are also some kinks in Svelte (which I assume will be worked out in the future). One example of this is the fact that the reactiveness only works when you directly assign a variable, but not if you call a method on it like list.push().

I also made the decision to use Typescript instead of Javascript within Vue, because I find that developing with Javascript can become very cumbersome, especially when debugging something. Vue also simplifies the one problem I have with Typescript, which is the build process.

#
### Backend
For the backend, the language choice is between C# with the ASP.net (core) framework and Java with one of its many backend frameworks.

I have quite a lot of experience with C# and ASP.net core. If I were to choose this language, I'd be able to make an app with more functionality while having to do less research as I would not have to learn a new language. On the other hand, however, I would really like to learn a new language instead of just making another backend with C# that would look virtually the same as last semester's. If I were to choose Java, I'd learn a new language which is very valuable. Doing this would mean I spend more time learning instead of just doing the same stuff I've already done twice. Java is also quite similar to C#, so it should not even take that long to get the hang of the language.

I made the decision to choose Java along with the Springboot framework, and Hibernate as the ORM.
