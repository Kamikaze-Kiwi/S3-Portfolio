# Learning outcomes individual project

## Table of contents

- 1.[ Web application](#1-web-application)
- 2.[ Software quality](#2-software-quality)
- 4.[ CI/CD](#4-cicd)
- 8.[ Professional](#8-professional)


## 1. Web application

### User friendly:
Before creating the views, I created some screen designs. This allowed me to easily drag parts around until I was content with the result.

| ![Schets](https://user-images.githubusercontent.com/84376526/169283094-832a330c-2ac4-4685-853b-e7e9d48648a0.png) |
| :--: |
| ^ A first design I made for the bugger page view, along with the navbar. |


### Full-stack
As explained in more detail in [Technology choices](README.md#technology-choices), I chose JAVA with SpringBoot for my backend and Vue for my frontend.

My backend currently consists of 3 microservices. One that manages everything to do with authentication and authorization, one that manages everything to do with bugreports and another one that manages everything to do with buggerpages. All of these microservices contain an entity, a controller which handles incoming API calls, a service which manages all the logic and a repository which handles all the database stuff.


## 2. Software quality
I decided to only properly check my software quality in one of my microservices. I did this because otherwise I would be spending a lot of time doing the exact same thing multiple times, and I can still learn about and apply all the software quality principles. I chose for my BugReport microservice, as it has the most code and also because I paid more attention to software quality and error handling in this microservice.

I chose not to create unit tests for my code, as there was not enough logic to create useful tests. Instead, I opted for integration tests to test the endpoints, logic and data access in one go.

#

In addition to my own tests, I created a project on sonarcloud to automatically scan the entire codebase for one of my microservices. This report can be found [here](https://sonarcloud.io/project/overview?id=MaikelHendrikx1_bugreport). Sonarcloud automatically performs a scan everytime I push to the main branch on Github.

Sonarcloud shows me, among other things; security issues, vulnerabilites, bugs and code smells. When I press these it shows me why it's an issue and what I can do to fix it. In the example below, Sonarcloud reported a security issue with my application. This had to do with the fact that one of my API endpoints allowed every crossorigin policy. In my case, this was supposed to be happen, as this endpoint should be publicly accessable. I reviewed the security hotspot and set it's status to 'safe'. I then also added a comment explaining why it was safe in this case.
| ![SonarcloudSecurityReview](https://user-images.githubusercontent.com/84376526/171207813-c430fd71-5958-4de6-bee6-be7c0620ebab.png) |
| :--: |
| _^ Screenshot of the report by Sonarcloud. Reviewed by me. The 'activity' feed at the bottom shows the steps I took to get rid of this report. This report can be seen in more detail [here](https://sonarcloud.io/project/security_hotspots?id=MaikelHendrikx1_bugreport&hotspots=AYEAfOCwcu6je62Ut3Ix)._ |

Sonarcloud also found 2 vulnerabilities in my application. Both of these were the same issue, being the fact that I used persistent entities in my controllers instead of DTO's. This is a risk because it would be possible to send unexpected values into the database, as these persistent entities are linked to the database with Hibernate (an ORM). In this case I decided the best course of action was to fix this issue. I created a DTO and changed every reference to the persistent entity to this DTO. I made a way to convert the DTO to the entity and vice versa. In the image below you can see the result of these changes.

| ![SonarcloudMainBranchEvolution](https://user-images.githubusercontent.com/84376526/171225363-7f5a2bc1-c7a1-44e4-b510-b85bd169ea67.png) |
| :--: |
| _^ Screenshot of the Main branch status and evolution. You can see that I got rid of 2 vulnerabilities and 1 security hotspot. (we don't talk about the code smells 🤐). More details can be found [here](https://sonarcloud.io/project/overview?id=MaikelHendrikx1_bugreport)._ |

## 4. CI/CD

## 8. Professional
