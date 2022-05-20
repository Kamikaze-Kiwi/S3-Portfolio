# Learning outcomes individual project

## Table of contents

- 1.[ Web application](#1-web-application)
- 2.[ Software quality](#2-software-quality)
- 4.[ CI/CD](#4-cicd)
- 8.[ Professional](#8-professional)


## 1. Web application

### User friendly:
| ![Schets](https://user-images.githubusercontent.com/84376526/169283094-832a330c-2ac4-4685-853b-e7e9d48648a0.png) |
| :--: |
| ^ A first design I made for the bugger page view, along with the navbar. |


### Full-stack
As explained in more detail in [Technology choices](README.md#technology-choices), I chose JAVA with SpringBoot for my backend and Vue for my frontend.

My backend currently consists of 3 microservices. One that manages everything to do with authentication and authorization, one that manages everything to do with bugreports and another one that manages everything to do with buggerpages. All of these microservices contain an entity, a controller which handles incoming API calls, a service which manages all the logic and a repository which handles all the database stuff.


## 2. Software quality
I tested everything in one of the microservices. I use endpoint tests to test wether the endpoints work and if I get back the correct status codes if I (for example) send the wrong data to the endpoint, to achieve this I use the MockMvc package included in SpringBoot. I also test the service (logic) layer. I also test the repository (data access) layer using an in-memory H2 database.

## 4. CI/CD

## 8. Professional
