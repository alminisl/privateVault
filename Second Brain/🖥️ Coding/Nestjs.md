
Framework for building scalable serverside services with TS. 

Uses Fastify or Express

Supports REST / Graphql out of the box 

MVC support

Containes a ton of modules for Securit / streaming / DB 

Jest for testing 

### Parts

Controller - Routes HTTP stuff 
PRovider - shared logic 
	We can use @injectable to inject code to other modules 


### Why use it? 

- Structure
- Modularity 
- Typescript
- Graphql 
- Microservices
- Rest API 
- Documentation
- Popular / Community support

(Currently most popular backend framework besides express)

Brings Architecture and Structure to the table

## Nestjs architecture

### Modules 

- Modules is a class annotated with Module()
- MOdule cani mport other modules
- Root module app module
- every module can import controllers and providers 
- Best case scenario - Every feautre is a module 


DTOs - Data to be checked

TSS id is needed 