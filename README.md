# Synopsis  
**Azywave Technology**

## Installation & Prerequisites

### System Requirements
- **Operating System**: Windows 10 / Windows 11  
- **SDK**: .NET SDK 8.0 (**Mandatory**)  
- **IDE**: Visual Studio 2022 (v17.8 or later)  
- **API Testing Tool**: Postman  

--

## Project Overview

### Fixed Window Rate Limiting API
		
- **Solution Name**: :Zywave.RateLimit.Svc
- **Startup Project** : Zywave.RateLimit.Web.Api		 
		
- **Zywave.RateLimit.Svc** is a MicroService Its design and implemented a Fixed Window Rate Limiting API using .NET 8.0, 
		Its capable of controlling incoming requests per user with APIkey to prevent abuse,and protect backend services.		
		The solution is thread-safe, scalable, and production-ready, with support for in-memory or Redis-backed storage.


## Setup & Execution

- **Step 1**: 
				please follow the Installation and Prerequsite that mentioned in the Above
- **Step 2**:
				Configure  RATELIMIT_ENVIRONMENT ENVIRONMENT Variable on your system or server. 

- **Notes** : Steps to Configure Environment Variables Search for Edit the system environment variables Click Environment Variables
			    Add a new System Variable Set the variable based on the environment 
			    e.q RATELIMIT_ENVIRONMENT = local
			    RATELIMIT_ENVIRONMENT = Production
				RATELIMIT_ENVIRONMENT = Testing
		
- **Step 3**: 
				Download folder Zywave.RateLimit.Web source code from the provided GitHub/GitLab public repository.		

- **Step 4**: 
				Open the solution in Visual Studio (Run as Administrator)
				Build and run the project
				The Swagger UI will automatically open in the browser

## Testing the Project (Local)

- **Steps for tests api Project on local your system**
				Open postman put the below values in the Header and Body section        			
- **Mandatory Step** 
	For all API calls, the following header must be provided:

    **Key : apiKey**

	**Value : Test1**

- **Sample Request Body**

  **Body - {
					  "userId": "1234",
					  "apiKey": "Test1"
		   }**
			
	   
  **Post - EndPoint** : https://localhost:7198/api/RateLimit/userCheck

  **Note** -  **RateLimit/userCheck** work as per the AddRateLimiter configuration in the program.cs file

--

  **Post - Endpoint** : https://localhost:7198/api/RateLimit/check

  **Note** : This endpoint handled by business layer in memory using ConcurrentDictionary
			
--
			      
  **GET – Endpoint**  : https://localhost:7198/api/RateLimit/totalRequestCount			 

  **Note** :Get endpoint will call after the POST End point api/RateLimit/check to get the User Request Count

## Design Decisions & Trade-offs

○ The rate-limiting algorithm you chose and why. 
		 Rate-limiting algorithm : Fixed Window 
		 Why :Simple,Predictable High performance - Fixed Window Rate Limiting suitable for internal microservices
 
○ The structure of your code and the reasoning behind it.
	Separation of Concerns - The system is deliberately split into clear layers, each with one responsibility
	

**The solution follows Separation of Concerns, with each layer having a single responsibility:**

 **Web API Layer**
	Handles HTTP requests and responses

 **Service Layer**
	Executes business logic and rate-limiting rules

 **Data Layer**
	Handles data persistence and cache/database interaction

 **DTO Layer**
	Manages data transfer objects

 **Validator Layer**
	Validates user input and request rules for all the endpoints in single place 

 **Test Layer**
	Contains positive and negative test cases with code coverage

