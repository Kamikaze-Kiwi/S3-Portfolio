# Portfolio

## Table of contents

1. [Languages and frameworks choice](#language-and-framework-choice) \
  1.1 [Frontend](#frontend) \
  1.2 [Backend](#backend)
2. [...](#portfolio)



## Language and framework choice

### Frontend
For the frontend, the programming language does not have to be considered as the only programming language natively supported by all browsers is Javascript.

There are a lot of frameworks to choose from, however. I cut this choice down to 4 frameworks. These are: React, Angular, Vue.js and Svelte. The reason I excluded other frameworks mostly boils down to the fact that most of them are very young and/or not widely used. This is a problem because it will be hard to find any information/tutorials. While Svelte is also a relatively young framework, I included it anyway because I've seen it praised a lot[<sup>[1]</sup>](https://insights.stackoverflow.com/survey/2021/?utm_source=social-share&utm_medium=social&utm_campaign=dev-survey-2021#most-loved-dreaded-and-wanted-webframe-love-dread)[<sup>[2]</sup>](https://2020.stateofjs.com/en-US/technologies/front-end-frameworks/).

|  | **Vue.js** | **React** | **Angular** | **Svelte** |
|:---:|:---:|:---:|:---:|:---:|
| **Documentation** | Good documentation with examples and live sandbox to test code. 8/10 | Decent tutorials but proper documentation is lacking. 6/10 | Quite bad documentation, hard to find what you are looking for. 3/10 | Good documentation and examples. Also a fancy interactive tutorial. 9/10 |
| **Complexity** | A bit complex at first, but it's not a big deal. 7/10 |Not too complex and very readable. 8/10 | Most complex. Code seems unnecessarily complicated for even easy tasks. 4/10 | Not complex at all, can achieve the same as the other frameworks with less work/code while still being readable. 9/10 |
| **Popularity** | Somewhat popular but slowly growing. 6/10 | Very popular and still growing. 10/10 | Quite popular but declining in use. 7/10 | Not very popular but rapidly growing 5/10 |
| **Performance** | Good performance. 8/10 | Decent performance. 7/10 | Mediocre/poor performance. 5/10 | Amazing performance due to not requiring a virtual DOM. 9/10 |
| **Learning curve** | Easy to learn. Would probably take a few days. 8/10 | Easy to learn, slightly easier than Vue. 8.5/10 | Hardest to learn. Could take multiple days or even a week to learn. 6/10 | Easiest to learn. Could probably learn in a day or two. 9/10 |

After this I was still struggling with my choice, although I have now boiled it down to just Vue.js and Svelte.
To make sure I make the right choice, I made the same demo-project in both Vue.js and Svelte.

After making a simple project that fetches some data from a public API in both frameworks, I decided to go with Vue.js. While I really like the simple syntax Svelte has, it's a lot simpler to have a multi-page application in Vue then it is in Svelte. There are also some kinks in Svelte (which I assume will be worked out in the future). One example of this is the fact that the reactiveness only works when you directly assign a variable, but not if you call a method on it like list.push().

I also made the decision to use Typescript instead of Javascript within Vue, because I find that developing with Javascript can become very cumbersome, especially when debugging something. Vue also simplifies the one problem I have with Typescript, which is the build process.

### Backend
For the backend, the language choice is between C# with the ASP.net (core) framework and Java with one of its many backend frameworks.

I have quite a lot of experience with C# and ASP.net core. If I were to choose this language, I'd be able to make an app with more functionality while having to do less research as I would not have to learn a new language. On the other hand, however, I would really like to learn a new language instead of just making another backend with C# that would look virtually the same as last semester's. If I were to choose Java, I'd learn a new language which is very valuable. Doing this would mean I spend more time learning instead of just doing the same stuff I've already done twice. Java is also quite similar to C#, so it should not even take that long to get the hang of the language.

I made the decision to choose Java along with the Springboot framework, and Hibernate as the ORM.

