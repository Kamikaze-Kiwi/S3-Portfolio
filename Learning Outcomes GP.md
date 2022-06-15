# Learning outcomes group project

## Table of contents

- 1.[ Web application](#1-web-application)
- 3.[ Agile method](#3-agile-method) 
- 5.[ Cultural differences and ethics](#5-cultural-differences-and-ethics)
- 6.[ Requirements and design](#6-requirements-and-design)
- 7.[ Business processes](#7-business-processes)
- 8.[ Professional](#8-professional)


## 1. Web application
### - User-friendly
In the group project I made a distribution for which temperature should be displayed in which colour on the heatmap. To achieve this I initially used my own preferences, and then I consulted the other group members for some minor adjustments.

| ![oldDistributionMap](https://user-images.githubusercontent.com/84376526/170819348-5b5a2c66-a47c-492b-9966-7a509bcdd414.png) | ![newDistributionMap](https://user-images.githubusercontent.com/84376526/170819353-17ceb54e-9689-41ac-8da8-8f2767b577c1.png) |
|:--:|:--:|
| ![Temperature distribution](https://user-images.githubusercontent.com/84376526/164173973-db06c558-5d59-44df-9334-74948ea69a36.png) | ![temperature distribution new](https://user-images.githubusercontent.com/84376526/170005293-0eab2076-a945-45a1-bf73-2fc67f1d3f77.png) |
| _^ Initial heatmap temperature distribution. The entire heatmap is mostly green, even though the temperatures vary wildly (from 20.8 to 24.6)._ | _^ The heatmap temperature distribution after some changes. The heatmap now properly shows the hotter areas._ |

<br>

### - Full-stack
In the group project I worked on a frontend to display temperature/humidity data using Vue.js. We ended up scrapping this idea, however, after a meeting with the project-leader.

| ![Scrapped temperature graph](https://user-images.githubusercontent.com/84376526/164178056-6cdd4ee0-010f-4573-8060-79f1133a649e.png) |
| :--: |
| _^ One of the (dynamic) graphs I made using HighCharts + Vue.js (with random mock data)._ |
<br>

I also worked on the heatmap together with Rick, which we made using HighCharts.

| ![heatmap sample](https://user-images.githubusercontent.com/84376526/164218604-12e747b5-59e9-40fd-8d77-144b33c58337.png) |
| :--: |
| _^ A screenshot of the heatmap (with random mock data)_ |
<br>

Furthermore, I worked with Rens to receive the data from the MQTT broker and to send this data over to a database. We achieved this using a C# API which listens to the MQTT broker. Using this API it's also possible to view the current status of the API and the broker.

<br>

In the last few weeks I spent most of my time making the heatmap reactive: 

| ![Heatmap Tools](https://user-images.githubusercontent.com/84376526/170819986-ebe25d4a-117b-43f5-9266-9fabd2414830.png) |
| :-- |
| <ul><li>Top left: the ability to select a date and update the heatmap. Also a button that goes to the current date/time.</li><li>Right beside the datepicker: a label that shows the currently selected time.</li><li>Beside the time label: a button that opens a popup that allows you to copy a url, so anyone who visits this link automatically goes to the datetime you had selected when you pressed share. </li><li>Top right: a dropdown with 2 buttons to pick a floor or go to the next/previous floor. This automatically updates the background image aswell.</li><li>Bottom: a slider to select a time. You can't surpass the current time (if you are on today). </li><li>Changing the date, time or floor will update the URL (without refreshing the page), so you can also share the URL by copying it from the address bar.</li></ul>|

<br>

## 3. Agile method
There are a lot of different agile methodologies, the most popular being Kanban and Scrum. These two are quite similar in that they both use a board with multiple columns (To Do, Doing and Done). The main difference between these is that Scrum splits the project into multiple sprints. There are also some less common methodologies, like Extreme Programming, Feature Driven Development, Dynamic Systems Development Method and Crystal. We decided to go with Scrum, because we were familiar with it and because we didn't want to dwell on this choice too long. Because our product owner uses Kanban in their company, he pushed us a little towards using it as well. Because of this we ended up with a kind of hybrid between the two systems.

In the group project we use a [Notion](https://right-metacarpal-459.notion.site/Dashboard-S3-Groep-3-a0a557bce28b4c35ba0b1655da06f22f), which is an alternative to Trello. In here we have our roadmap, user stories, documents and more.

Together with the product owner, we created a list of user stories and ordered them by importance. At the start of every sprint we pick a few of these and create cards from them, with each of them getting a definition of done.


| ![User stories sample](https://user-images.githubusercontent.com/84376526/164202907-e209347f-5025-4966-9314-caedc814cf5c.png)   | ![notion roadmap sample](https://user-images.githubusercontent.com/84376526/164204103-0b2dc7c2-1c76-458f-ba72-f82149340b52.png)   |
|------|------|
| _^ A small sample of our user stories._ | _^ A small sample of our roadmap, with each entry containing more details and a definition of done when pressed._ |
<br>

We also have (atleast) a stand-up and a stand-down every day so we always know what the other team members are currently working on and to review eachothers work. At the start of each sprint we select all the user stories that we want to work on for that sprint and divide them among us. At the end of each sprint we do a sprint review with the product owner and a sprint retrospective.

<br>

## 5. Cultural differences and ethics

### Ethics

#### What is ethics in software engineering?

Ethics, as described by Oxford Languages, is a set of moral principles that govern the behaviour of a person or the conduction of an activity. Ethics are used to measure the righteousness of an action, acting as criteria for judging whether something is right or not. In the scope of software engineering, ethics dictate the values a software engineer should adhere to in a professional environment. This includes ethics related to cultural differences, software, source code and communication.

####  Why is ethics important in software engineering?

Within the software engineering space, a number of widely used ethical guidelines can be found on the internet. One such guideline is the ACM Software Engineering Code of Ethics, which states that software engineers should strife to analyze, design, develop, test and maintain software in a truthful, upfront and professional manner for the better of public health, safety and welfare of humanity, according to the following eight principles:

PUBLIC – Software engineers shall act consistently with the public interest.
CLIENT AND EMPLOYER – Software engineers shall act in a manner that is in the best interests of their client and employer consistent with the public interest.
PRODUCT – Software engineers shall ensure that their products and related modifications meet the highest professional standards possible.
JUDGMENT – Software engineers shall maintain integrity and independence in their professional judgment.
MANAGEMENT – Software engineering managers and leaders shall subscribe to and promote an ethical approach to the management of software development and maintenance.
PROFESSION – Software engineers shall advance the integrity and reputation of the profession consistent with the public interest.
COLLEAGUES – Software engineers shall be fair to and supportive of their colleagues.
SELF – Software engineers shall participate in lifelong learning regarding the practice of their profession and shall promote an ethical approach to the practice of the profession.

####  What do you have to do as a software engineer to address ethical aspects in your work?

In order to verify all software engineers ethical values match up, it is important for all parties involved to converse about the topic. Allowing everyone to share their ethical values and boundaries with one another makes it possible to create a working environment in which all parties involved can work comfortably.

####  How do you know that your ethical considerations match with those of other software engineers?
In order to verify all software engineers ethical values match up, it is important for all parties involved to converse about the topic. Allowing everyone to share their ethical values and boundaries with one another makes it possible to create a working environment in which all parties involved can work comfortably.

#### Which ethical aspects play a role in your project?
One of the ethical aspects in our group project that we faced was the licensing of third party libraries(Highcharts). As our project lives in a gray area between commercial and non-profit (the organization is a business, while the application is strictly for internal use without any direct link to generating profit), we considered whether purchasing a license for these libraries would be necessary.

#### Do you foresee ethical conflicts caused by your software? What kind of?
I personally don't expect any ethical conflicts to be caused by our software, considering it's for internal use only and we don't even store any data about our users. Users also can't change anything within our application (like adding comments). The only thing our application does is show the user a temperature heatmap of the office.

<br>

### Culture

#### What is culture?
Culture is everything from our language, food and clothing to our behaviour. Things that are considered normal in one culture might be considered rude or offensive in another one.

#### Which are well-known dimensions on cultural differences?
The 6 well-known culture dimensions of Hofstede are:

- Power distance Power distance is the degree a society accepts or rejects the unequal distribution of power in organisations and society. In high power distance cultures such as Japan, we expect to find great respect for age, status and titles. This could create problems for an American visitor used to the informality of a more moderate power distance culture, and accustomed to using first names and casual dress in the office.

- Uncertainty Avoidance Uncertainty avoidance is the degree a society tolerates or is uncomfortable with risk, change, and situational uncertainty. In high uncertainty avoidance cultures, such as France or Japan, one would expect to find a preference for structure, order and predictability.

- Individualism-Collectivism Individualism-collectivism is the degree to which a society emphasises an individual’s accomplishments and self-interest, versus the accomplishments and interests of groups. In Hofstede’s data, the United States had the highest individualism score of any country.

- Masculinity-Femininity Masculinity-femininity is the degree a society values assertiveness and materialism versus feelings, relationships, and quality of life. You might think of it as a tendency to emphasise stereotypical masculine or feminine traits and attitudes towards gender roles. Visitors to Japan, with the highest masculinity score in Hofstede’s research, will probably notice how restricted career opportunities can be for women.

- Time Orientation This is the degree to which a society emphasises short-term or long-term goals. Americans are notorious for being impatient and wanting quick, even instant gratification. Accordingly, American companies are expected to achieve short-term results. Many Asian cultures are the opposite, valuing persistence, being patient, and are willing to work for long-term success.

- Indulgence-Restraint The Indulgence dimension is a relatively new dimension to the model. This dimension is defined as the extent to which people try to control their desires and impulses, based on the way they were raised. Relatively weak control is called Indulgence and relatively strong control is called Restraint. Cultures can, therefore, be described as Indulgent or Restrained. Indulgence stands for a society that allows relatively free gratification of basic and natural human drives related to enjoying life and having fun. Restraint stands for a society that suppresses gratification of needs and regulates it by means of strict social norms.

Source : Hofstede's cultural dimensions

#### Can you give examples for cultural differences that you have experienced in your study or life? How do you explain these differences?
One big cultural difference I experienced over the years by visiting countries during holidays is the time at which you eat dinner. Here in the Netherlands it's normal to eat between 17:00 to 18:00, while in countries like France and Spain that's mostly unheard of. In these countries they tend to eat much later, like after 19:00.

#### What is your culture?
My main culture is Dutch, but there is also some culture specific to the province and to the city which I live in. 
<br>

### Game
We (Liang, Rens, Rick and me) played the game offered in the Canvas course. These are the scores we achieved at the end of the game:

|    Name    |Score|
|------------|-----|
| **Maikel** | 121 |
| **Rick**   | 114 |
| **Liang**  | 113 |
| **Rens**   | 112 |

Down below I will answer the questions at the end of the game, to reflect on it.

- **What insights and learnings did you have while playing the game?** 

    I learned a lot about other cultures, specifically how different cultures can act differently in the same situation. This has made me more understanding of certain other cultures, and I believe it will be less likely for me to accidentally cause a disagreement if I were to work together with people from other cultures.
- **Which of these could you immediately apply to your job or your relationships with others?** 

    Before I did this quiz, if a vietnamese person were on the phone with me, and they suddenly hang up without saying goodbye, I would assume they were either angry with me or the connection was lost. Now I know that ending a call like that is perfectly normal in Vietnam, so there is no risk of a disagreement happening between us because of a suddenly ended phone call anymore.
- **How did playing the game bring out the cultural values of the players, e.g., did you compete or collaborate? What kind of culture did your team become?** 

    We mostly agreed on most questions, but we did have a discussion on the question about your Polish coworkers calling you Dr. Kim instead of Dr. Park. I assumed that First names and surnames were the same in Asia as they were in the Western world, however Liang taught me that names in large parts of Asia are actually flipped, so their family name often comes before their own name.
- **What are some consequences you see as a result of playing this game? What next steps will you take?**
 
    I got more accepting and knowledgeable about other cultures. I will continue being curious and careful when it comes to other cultures, to ensure I don't accidentally offend someone.
- **What would you like to know more about? Are there cards you would like to discuss further?**
 
    I would like to know more things that are considered normal in the Netherlands but could be seen as offensive in other cultures (and vice versa.).

<br>

## 6. Requirements and design
We asked for feedback on our products to ensure we created something which is as close as possible to whatever the stakeholder envisioned. We applied this feedback to better our products. We try to have a meeting with the stakeholder once a week, this means that we get constant feedback on our products which ensures we never spend a lot of time on something that the stakeholder doesn't like.

In the group we discussed almost every design choice we made. For example, we had a big discussion about how to allow the user to switch floors. We considered another (vertical) slider on the left of the heatmap, but we decided not to do this as the page would become too crowded and unclear. 

We also considered putting an arrow button on both sides of the heatmap to change floor, but we threw away this idea as well, for the same reason as before but also because floors are ontop of eachother, and not side to side. 

Another idea we had was to have a bunch of radio buttons (in a layout similar to the one found in elevators) for switching floors (we even considered having elevator doors closing over the heatmap, and open again once the data for this floor gets loaded). We scrapped this idea too, however, as it was unnecessarily complex, and if you have a lot of floors it would become very disorganised very quickly. 

{add bullet list instead of these ideas, and add pictures of designs we threw away}

We eventually agreed on a simple dropdown containing all the floors, with 2 buttons on the side with one arrow pointing up and one arrow pointing down, as seen in the image below. 

| ![verdieping](https://user-images.githubusercontent.com/84376526/169983528-b1295fe0-1e64-4979-97e1-2f0fd5b17ad3.png) |
| :--: |
| _^ The input for changing floors in the heatmap. This input is found under the bottom-right of the heatmap._ |

<br>

## 7. Business processes
| ![Business process](https://user-images.githubusercontent.com/84376526/169815643-b14fc448-b26b-4365-bfe7-6d9445a06598.png) |
| :--: |
| _^ The business process for a hypothetical order picking process. We chose this hypothetical process because we found it difficult to visualize a process for our group project. After discussing this with Marc we came to the conclusion that we should use another business or a hypothetical business to visualize a process instead. We chose an order picking business because Rens does orderpicking for his job, while Rick is creating an orderpicking system for his individual project. <hr> We created this using Engage Process Modeler, as we already had experience with this tool from the first semester._ |

Analyzing the business process is important because it allows you to see how the workflow in a company looks. This allows you to optimize said workflow by (for example) automating certain steps. It also allows you to link software to the workflow in other ways, for example, if there is a step where the employee checks in on a screen every morning and check out at the end of the day, you could get the amount of employees currently in the building. In our project this could be used to see if the amount of people that are in the building has any correlation to the temperature.

<br>

## 8. Professional
As described in [3. Agile method](#3-agile-method), we commit ourselves to the scrum methodology as we hold daily stand-ups and stand-downs, as well as sprint reviews etc.

I always try to communicate professionally and in a timely manner with my group members, as well as with the product owners. For example if I'm unable to make it or if I'm a bit later. I also communicate well about the project itself, by asking for help whenever I require it and also by offering my help to whoever needs it.

Whenever a group member is unable to join in with the daily stand-up/stand-down, we make sure it is possible to join the meeting virtually, so they will still be able to track our progress as well as share their own.

In the earlier meetings I did not talk a lot during meetings with the stakeholder, and also meetings with the rest of the group. During the semester I worked on this and now I feel like I am able to sufficiently contribute in the meetings.
