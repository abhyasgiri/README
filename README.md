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
- Service 1 (front-end): displays the results of the other 3 services for the user to see, as well as a history of the previous few results listed in descending order.
- Service 2 : returns a random league out of options: English, Spanish and German. 
- Service 3: returns a random pack-type out of options: Gold, Silver and Bronze.
- Service 4 : returns a player based on the league and pack-type chosen.

## Architecture 

### Application Architecture

![diagram1](https://user-images.githubusercontent.com/74771160/105645143-a9626980-5e91-11eb-8867-4aa6de9052d2.png)


simple object generator application which produced a football player card 


