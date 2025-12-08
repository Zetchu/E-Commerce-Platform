Project: E-Commerce Platform

A scalable microservices-based e-commerce platform that centralizes product inventory, user identity, and order fulfillment across distributed services, and exposes secure, event-driven APIs for seamless web storefront experiences and administrative operations.

1. What are the elements of your project?

My project is an E-Commerce backend system designed to handle browsing, cart management, and order processing. The core elements are:

Client/Frontend: A web application (React) where users browse and purchase items.

API Gateway: The single entry point that routes requests to the appropriate backend services.

Product Service: Manages inventory, product descriptions, and categories.

Order Service: Handles shopping cart logic, order placement, and history.

User Service: Manages user profiles and authentication credentials.

Notification Service: Sends email updates for order confirmations.

Database: A relational database for ACID compliance on orders and inventory.

2. Which architectural patterns will apply?

Microservices Architecture: The system is decomposed into distinct domains (Products, Orders, Users) to allow for independent development and scaling.

API Gateway Pattern: Acts as a reverse proxy to handle routing, rate limiting, and request aggregation, shielding internal services from the public internet.

Layered Architecture: Within each service, code is organized into Controller, Service, and Data Access layers to maintain separation of concerns.

3. How will the pieces communicate with each other?

Frontend to Backend: The client communicates with the API Gateway using REST (JSON over HTTP).

Service to Service (Synchronous): Services use REST for real-time data retrieval (e.g., The Order Service querying the Product Service for current prices).

Service to Service (Asynchronous): Critical but non-blocking tasks use a Message Queue (e.g., RabbitMQ). When an order is placed, the Order Service publishes an OrderCreated event, which the Notification Service consumes to send an email.

4. What kind of authN and authZ will be needed where?

Authentication (AuthN): Implemented using JWT .

The User Service issues a token upon login.

The API Gateway validates this token on every incoming request to ensure the user is known.

Authorization (AuthZ): Implemented using RBAC (Role-Based Access Control).

Customer Role: Can GET products and POST orders.

Admin Role: Can POST/PUT products (update inventory) and view all system orders.
