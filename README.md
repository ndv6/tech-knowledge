# Tech Knowledge

## Knowledge 

### Git

- Most common **Branching Strategy** used is: **Git Flow**, **GitHub Flow**, **GitLab Flow**
- Git Flow: `branch:tag(env:production)` -> `branch:master(env:staging)` -> `branch:develop(env:development)` -> `branch:feature(env:local)` 
- GitHub Flow: `branch:master(env:production)` -> `branch:feature|fix(env:development)` -> `branch:master(env:production)`
- GitLab Flow: `branch:master(env:staging)` -> `branch:pre-production(env:development)` -> `branch:production(env:production)`

### Microservice

- Is an Architectural Style/Pattern that arrange application as Loosely Coupled, Independently Deployed, and Communicating through lightweight protocol
- It falls to the category of **Domain Driven Design** (DDD) where how micro each service is defined by its domain
- Domain is usually translated as Module or Business Capability or Team
- Most common communication protocol used is HTTP with REST API style or with RPC style
- It is achievable with **Containerization** to simplify deployment, management and orchestration of services
- Containerization is a type of virtualization in which all the components of an application are bundled into a single container image and can be run in isolated user space on the same shared operating system
- Containerization Image Platform widely used is Docker, others are also available e.g. Podman, Vagrant
- Dockerfile is a text-based file with no file extension that contains a script of instructions to build a container image
- Docker Compose is for managing and orchestrating multi-container applications, facilitating complex application setups
- Docker uses specific Operating System by directly importing specific OS image of by using another image that already has an OS
- Usually, microservice consist of 2 types of categories which categorize by process initiation: request based (API Service), event based (Consumer)
- Time based process could be initiated from cloud provider tools e.g. Amazon EventBridge or GCP Cloud Scheduler or Azure Functions to publish a message to be processed by a consumer 

### REST API 

- Is an acronym for **REpresentational State Transfer**
- Is an Architectural Style or Design Principle for communication in Distributed System
- It is one of the widely used Application Programming Interface (API) style
- API that comply to the REST Principle usually referred as **RESTful API** or **RESTful Web API**
- Request is Stateless thus the Request must contain all the necessary information to understand and complete the Request
- The key abstraction of information in REST is a Resource
- Usually uses HTTP protocol as transport layer and utilizing standard HTTP Method (GET, POST, PUT, DELETE) and URI (Universal Resource Identifier) to identify Resource
- In the REST architectural style, data and functionality are considered resources and are accessed using URI
- By utilizing different HTTP Method, REST could use same URI to differentiate functionality of the Resource
- Example of RESTful API:
  - `POST /products` to create new product, sometimes it uses a singular word to describe single creation eg. `POST /product`
  - `PUT /products/{id}` to update product of selected id
  - `PATCH /products/{id}/active-state` to change active state of the product
  - `DELETE /products/{id}` to delete product of selected id
- Sometimes REST could also use rpc style to differentiate specific action
  - `PATCH /products/{id}/toggle-active-state { active: true }`
- Other commonly used API is gRPC (gRPC Remote Procedure Call), which is using rpc (Remote Procedure Call) style and uses HTTP protocol version 2
- Common Web Browser has not adopted this HTTP version 2 yet because of its complexity, thus gRPC currently only available for service-to-service communication
- By default, REST API is synchronous process since all of it is running in single process from request to response, regardless of how the service handles the request
- To make an asynchronous REST API, usually utilizing at least 2 API, first to trigger the process, second to check the progress of the process or send to result to other system eg. email/phone/push
- Synchronous is blocking process while Asynchronous is non-blocking process

### Event Driven 

- Event Driven is one of the architectures to enable asynchronous process
- There are 3 main category distinctions to initiate a process: `request based`, `time based`, and `event based`
- Request based is triggered by request from external service/client, e.g. REST API
- Time based is triggered by setting up specific counter of running time, e.g. CRON (Command Run On Notice) or Scheduler
- Event based is utilizing Message Queue and triggered by publishing/producing a message on selected event/topic which then will be push-to/pull-by consumer/subscriber
- Consumer Group is a feature to enable scaling consumer of specific event where each consumer in a group will receive one-different message at a time
- Acknowledge of consumer is required so the queue can move-on to next offset/cursor on the list
- By default, consumer will be using late-acknowledge where consumer will send ack signal to the queue after the process is done
- Retry mechanism of early-ack could be handled by the consumer whereas late-ack could be handled by the queue
- Queue could handle late-ack because when consumer has not sent ack signal, queue treat the message as not delivered yet, so usually it could run the retry mechanism 

### Distributed Tracing

- TODO

### Service Discovery

- TODO

### Circuit Breaker

- TODO

### Push Technology

- Is a communication method, where the communication is initiated by a server rather than a client
- Commonly used tools to enable this is using Socket or Firebase

### Auth

- Usually there are 2 main purposes of Auth: `Authentication` and `Authorization`
- Authentication: is used to verify if the user is the real user (original)
- Authentication could be verified by using Single Factor Authentication eg. password/pin
- Authentication could also be verified using Multi Factor Authentication (could be 2 Factor or even more)
- Additional Factor used to verify MFA usually consist of biometric (fingerprint, face) or specific token (One Time Password, Device Token)
- Usually it is using JSON (JavaScript Object Notation) Web Token (JWT) format to verify claims
- JWT is a compact URL-safe means of representing claims to be transferred between two parties
- JWT structure consist of 3 parts:
  - header: to identifies which algorithm is used to generate the signature
  - payload: contains a set of claims. has several standard fields:
    - iss: issuer of the token
    - sub: subject of the token (usually the user or owner of the resource)
    - aud: audience of the token (usually the party that will use the token)
    - exp: expiration time
  - signature: to securely validates the token
- JWT is capable to be used for decentralized auth where the audience could verify claim legitimacy by only using the token without needing to connect to the issuer
- Custom field of payload could be added to transfer information:
  - `{ payload: { scp: "repo package:delete" } }`
- OAuth (Open Authorization) is a standard designed to allow a website or application to access resources hosted by other web apps on behalf of a user
- Widely used OAuth is version 2.0
- OAuth main roles are:
  - Resource Owner: The user or system that owns the protected resources and can grant access to them
  - Client: The client is the system that requires access to the protected resources. To access resources, the Client must hold the appropriate Access Token
  - Authorization Server: This server receives requests from the Client for Access Tokens and issues them upon successful authentication and consent by the Resource Owner
  - Resource Server: A server that protects the user’s resources and receives access requests from the Client
- OAuth provides several Grant Types, most used are:
  - Authorization Code Grant: The Authorization server returns a single-use Authorization Code to the Client, which is then exchanged for an Access Token
  - Client Credentials Grant: Used for non-interactive applications where the application is authenticated by using its client id and secret
  - Refresh Token Grant: The flow that involves the exchange of a Refresh Token for a new Access Token
  - Resource Owner Credentials Grant: This grant requires the Client first to acquire the resource owner’s credentials, which are passed to the Authorization server
- OAuth Scope is used to specify exactly the reason for which access to resources may be granted
- OAuth Scope usually consists of multiple claims e.g. `scope: package` is a group of several claims e.g. `package:create`, `package:delete`
- OAuth uses JWT as token format

### Unit Test

- It Is commonly used to verify function behavior consistency by giving it several different inputs then evaluate expectation of its output
- External dependencies usually mocked/stubbed for consistency, because the purpose of Unit Test is to verify the internal function behavior not external parties
- External Party contract (request-response) should be agreed before integration and usually tested in System Integration Test (SIT) process

## Test Cases

**Q:** Could you explain what is your most technically challenging in your working experience?

**A:** The answer may describe candidate's knowledge:

- When the challenge is about learning curve/process, usually the candidate is still having issue on learning something new, thus could hinder Technical Growth
- When the challenge is about implementing feature or fix, usually the candidate has no issue on learning something new and eager to explore new challenges

**Q:** What is the difference between `Git Merge` and `Git Rebase`?

**A:** There are some distinct differences:

- Git Merge will apply remote changes on top of local changes
- Git Rebase will apply local changes on top of remote changes

**Q:** How would you implement REST API to handle active state update of certain product?

**A:** There are usually 2 approaches to answer this:

- Resource style:
  - `PATCH /products/{id}/active-state { active_state: true }`
  - it could also toggle `active_state` without sending any payload
- RPC Style:
  - `PATCH /update-products-active-state { id: 1, active_state: true }`
- Usually, it uses PATCH since its only changing some parts/fields of the resource

**Q:** How would you implement REST API to handle import list of products from csv?

**A:** There are several approaches to answer this:

- FTP (File Transfer Protocol) based:
  - User will upload csv to some File Storage
  - File will be picked-up and processed by some Scheduler later-on
- API based:
  - User will use REST API `POST /products/import`
  - Ways for the Service to process the File:
    - synchronously reading the File content and insert it to the database while User wait for the response which could possibly reach timeout when the File is too Large
    - Asynchronously by publishing Message/Event to Queue to be processed by Consumer/Worker while User will get `Status Code 201 Accepted` which means the request is Accepted and will be processed Asynchronously
    - Service could response with `process_id` so User could check the progress using another REST API `GET /products/import/{process_id}`
