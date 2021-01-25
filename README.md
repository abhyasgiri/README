# SFIA2 Practical Project: Football Pack Player Generator 
---

## Contents
- Brief
  - Requirements
  - Additional Requirements
  - Constraints
  - My Approach
- Architecture
  - Application Architecture
  - Database Structure
  - Docker Swarm
  - CI/CD Pipeline
- Project Tracking
- Risk Assessment
- Testing
- Front-End Design
- Known Issues
- Future Improvements
- Appendix
  - Versioning
  
## Brief 
This project is designed to showcase the application of knowledge I've learnt from the first half of my DevOps training at QA. This piece of work largely focuses on the CI/CD pipeline, with a less pronounced focus on the actual coding of the applicaiton itself. 

### Requirements
To create a service-orientated architecture for an application composed of at least 4 services that work together.

- Service 1 The core service – Renders Jinja2 templates to interact with the application, it will be responsible for communicating with the other 3 services, and as wells as for persisting data in an SQL database.

- Service 2 + 3 - These will both generate a random “Object”.

- Service 4 - This service will also create an “Object” however this “Object” must be based upon the results of service #2 + #3 using some pre-defined rules.

Services 2,3 and 4 must have 2 different implementations produced. A demonstration of swapping these implementations without disrupting the user experience is expected. 

### Additional Requirements

- An Asana board (or equivalent Kanban board tech) with full expansion on tasks needed to complete the project.
- An Application fully integrated using the Feature-Branch model into a Version Control System which will subsequently be built through a CI server and deployed to a cloud-based virtual machine.
- If a change is made to a code base, then Webhooks should be used so that Jenkins recreates and redeploys the changed application
- The project must follow the Service-oriented architecture that has been asked for.
- The project must be deployed using containerisation and an orchestration tool.
- As part of the project, you need to create an Ansible Playbook that will provision the environment that your application needs to run.
- The project must make use of a reverse proxy to make your application accessible to the user.

### Constraints
- Kanban Board or equivalent: Trello Board
- Version Control: Git using a feature-branch model
- CI Server: Jenkins
- Configuration Management: Ansible
- Cloud server: GCP virtual machines
- Containerisation: Docker
- Orchestration Tool: Docker Swarm
- Reverse Proxy: NGINX
- Database: MySQL

### My Approach
To meet all of the requirements and to ensure the MVP was produced, I proposed to create my own version of a gaming function which millions of FIFA players gamble their hard-earned coins in the hope that they buy a player pack that has a supreme player card. To reproduce a much simpler version, I've decided to create:

Player Card Generator:
- Implementaton 1: 
  - Service 1 (front-end): displays the results of the other 3 services for the user to see, as well as a history of the previous few results listed in descending order.
  - Service 2 : returns a random league out of options: English, Spanish and German. 
  - Service 3: returns a random pack-type out of options: Gold, Silver and Bronze.
  - Service 4 : returns a player based on the league and pack-type chosen.
  
- Implementation 2:
  - Service 1 (front-end): displays the results of the other 3 services for the user to see, as well as a history of the previous few results listed in descending order.
  - Service 2 : returns a random league in block capitals out of options: English, Spanish and German. 
  - Service 3: returns a random pack-type out of options: Gold, Silver and Bronze. Here, the probability of a Gold pack being picked has been weighted with 80% probability. 
  - Service 4 : returns a player based on the league and pack-type chosen. Here, each pack has a multiple players to choose from. 

## Architecture 

### Application Architecture

![diagram1](https://user-images.githubusercontent.com/74771160/105645143-a9626980-5e91-11eb-8867-4aa6de9052d2.png)
As illustrated, service 1 sends GET requests to service 2 and service 3. These responses are then sent to service 4 as a POST request, which then sends a response back to the front-end. The front-end then persists the data into a MySQL managed database by inserting a new entry. A managed database was chosen as it can be a cost-effective method of running a 24-hour service with proactive monitoring at all times. Service 1 uses jinja 2 templating. 

## Database Structure (ED diagram)

![database struc](https://user-images.githubusercontent.com/74771160/105645843-34446380-5e94-11eb-9304-ea6d2fa70ab4.png)

The data stored in the database follows a simple structure. 

## Docker Swarm

![database struc (1)](https://user-images.githubusercontent.com/74771160/105646860-1da10b00-5e9a-11eb-8fe7-b5b0ee6e3297.png)
Using Docker Swarm as the container orchestration tool, a swarm of a manager and a worker (with 3 replicas) virtual machine has been created to allow for user traffic to access the application. As shown by the diagram, the user connects to the application via an NGINX machine on port 80. NGINX has been used as a reverse proxy to host the application, as well as a load-balancer; it connects the user to a node in the swarm with the least connections to prevent overload and improve performance. In this way, the user is never connected directly to the core of the application which adds a layer of security from attacks.

## CI/CD Pipeline

![CI pipeline (2) (1)](https://user-images.githubusercontent.com/74771160/105648776-2a772c00-5ea5-11eb-9805-0a77865e73e1.png)

The use of an integerated pipeline has allowed for rapid and simple development-to-deployment by automating the integration process such that one can code on a local machine and push it to GitHub, which prompts github to push the new code to Jenkins via a webhook and start build & deployment. Jenkins has been used as the CI server as it is a widely used open source platform.

### Stage 1: Testing
Testing has been made part of the CI pipeline so that tests are automated for each build. Unit tests and mock tests have written up for each service, and upon successful testing, coverage reports are published which can be viewed in the console logs. Cobertura has been used as plugin on jenkins as it calculates the percentage of code assessed by tests. JUnit is another useful plugin deployed in this project as consumes XML test reports generated during the builds and provides clear graphical visualization of previous test results, as well as functioning as a web UI for viewing test reports and tracking failures which makes debugging easier.

### Stage 2: Build & Push Images
Service containers are built from their images using Docker-compose. They are then pushed onto Dockerhub as artefacts ready for the next stage. Credentials have been used in Jenkins to save the login credentials for dockerhub as environment variables. 


image of the build logs. look at hitesh's stage view 





something about posting reports , etc. and explaining them ?
