### Lessons from App #1
* The big challenge in microservices is data.
* Different ways to share data between services. We are going to focus on async communication.
* Async communication focuses on communicating changes using events sent to an event bus.
* Async communication encourages each services to be 100% self-sufficient, Relatively easy to handle temporary downtime or new service creation.
* Docker makes it easier to package up services. 
* Kubernetes is a pain to setup, but makes it really easy to deploy + scale services.


### Painful Things from App #1
* Lots of duplicated code!
* Really hard to picture the flow of events between services.
* Really hard to remember what properties an event should have.
* Really hard to test some event flows. 
* My machine is getting laggy running kubernetes and everything else.
* What if someone create a comment after editing 5 others after editing a post while balancing on a tight rope.....

### Solutions
* Build a central library as an NPM module to share code between our different projects.
* precisely define all of our events in this shared library.
* Write everything in Typescript
* Write tests for as much as possible/reasonable.
* Run a k8s cluster in the cloud and develop on it almost as quickly as local.
* Introduce a lot of code to handle concurrency issues. 