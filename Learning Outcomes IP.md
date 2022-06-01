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



| ![VueComponents](https://user-images.githubusercontent.com/84376526/171408014-27c3e85e-715e-4401-bda4-40a82489c785.png) |
| :--: |
| _^ These are the components that I have made for my frontend._|

{insert video showcasing frontend}


## 2. Software quality
I decided to only properly check my software quality in one of my microservices. I did this because otherwise I would be spending a lot of time doing the exact same thing multiple times, and I can still learn about and apply all the software quality principles. I chose for my BugReport microservice, as it has the most code and also because I paid more attention to software quality and error handling in this microservice.

I chose not to create unit tests for my code, as there was not enough logic to create useful tests. Instead, I opted for integration tests to test the endpoints, logic and data access in one go.

To be able to test the entire microservice, I had to mock the database and the endpoints. I mocked the database using an in-memory H2-database and I mocked the endpoints using [AutoConfigureMockMvc](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/web/servlet/AutoConfigureMockMvc.html). Before every test runs, I reset the database and add 5 records to it, this way every test will always have the exact same environment.
| ![IntegrationTestsReset](https://user-images.githubusercontent.com/84376526/171234647-ac3e3412-b2ea-4cbd-b2e7-0e87e0e9086d.png) |
| :--: |
| _^ The code that gets executed before and after each test._|

I made a total of 13 tests. These tests cover the entirety of the microservice. They test both the happy and the bad flow, and most tests have multiple asserts. Down below are 2 examples of my tests (one happy and one bad flow).

| ![IntegrationTestHappyFlow](https://user-images.githubusercontent.com/84376526/171235360-6ebdb2da-13a5-4611-ac15-e7ab8036c234.png) | ![IntegrationTestBadFlow](https://user-images.githubusercontent.com/84376526/171235379-8220f11b-ba50-4356-94a2-d3e6880099bf.png) |
| :--: | :--: |
| _^ This test performs a get request on 'BugReports/get' with an id of 1 to test whether we get a response and if this reponse returns the bugreport with id 1._ | _^ This test also performs a get request on 'BugReports/get', but instead supplies an id of a non-existing bugreport. It tests whether a response of 400 is returned and it also makes sure we don't actually receive any data._ |

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

For my continuous integration I created a workflow with Github actions which automatically builds and tests the solution. I did this for every microservice.
| ![GithubActionsBuildAndTest](https://user-images.githubusercontent.com/84376526/171378736-0997cca0-e535-47cf-b159-ebe156e9f22e.png) |
| :--: |
| _^ This is the yaml code that runs on every push to the master branch. It first checks out the code, and then sets up java 17. After this it runs `mvn -B package --file pom.xml`, which runs and tests the code._ |

| ![CiTestSuccess](https://user-images.githubusercontent.com/84376526/171381017-3e3f84b5-7cfa-4e95-9d06-dad4b1086d78.png) |
| :--: | 
| _^ This is what it looks like when **all** tests succeed._ |

| ![CiTestFail](https://user-images.githubusercontent.com/84376526/171381295-8140cd8a-bb88-49b8-ad88-cdd0eaf197a0.png) |
| :--: | 
| _^ This is what it looks like when any test fails._ |


I also added continuous integration to all of my microservices. I initially wanted to publish the application to an actual server, like on Azure or AWS. I eventually decided against this, though, as I already used a lot of my Azure credit on hosting databases. I instead went with Docker Hub. To upload to Docker Hub I have to be able to run my application within a docker image. For this I created a dockerfile.

| ![dockerfile](https://user-images.githubusercontent.com/84376526/171396851-37569cc3-fab2-416e-a7ab-72ec6360b54e.png) |
| :--: |
| _^ The dockerfile used to run my Java springboot application in a docker image._ |

| ![GithubActionsDockerPublish](https://user-images.githubusercontent.com/84376526/171398115-c4906ba5-bcd6-45b4-b884-6b99d7c0bd4f.png) |
| :--: |
| _^ The Github action to build a docker image and publish it to Docker Hub. This job depends on the test job, meaning if it fails, it will not attempt to publish it._ |

The docker repositories for each of my microservices can be found here:

https://hub.docker.com/repository/docker/maikelhendrikx/bugreport

https://hub.docker.com/repository/docker/maikelhendrikx/buggerpage

https://hub.docker.com/repository/docker/maikelhendrikx/account

## 8. Professional
