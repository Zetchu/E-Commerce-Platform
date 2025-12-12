User Flows & Interactions

Core User Flows

Here are the primary interactions within the system, detailing the services and data stores involved in each.

1. User Sign Up

Actors/Elements: Customer, Frontend, API Gateway, User Service, Database.

Description: A new user registers for an account. Credentials are hashed and stored.

2. User Login

Actors/Elements: Customer, Frontend, API Gateway, User Service, Database.

Description: User exchanges credentials for a JWT (JSON Web Token) for session authentication.

3. Browse Products

Actors/Elements: Customer, Frontend, API Gateway, Product Service, Database.

Description: User views the list of available products and prices.

4. View Product Details

Actors/Elements: Customer, Frontend, API Gateway, Product Service, Database.

Description: User clicks a specific item to see detailed description and stock status.

5. Place Order (Checkout) (Unique)

Actors/Elements: Customer, Frontend, API Gateway, Order Service, Database, Message Queue.

Description: User finalizes purchase. Order is saved, inventory is checked, and an event is published for async processing.

6. Async Order Notification (Unique)

Actors/Elements: Message Queue, Notification Service, External Email Provider.

Description: The system picks up a "New Order" event and sends a confirmation email without blocking the user.

7. Admin Update Inventory (Unique)

Actors/Elements: Admin, Admin Frontend, API Gateway, Product Service, Database.

Description: Store admin updates the stock count for a specific product.

8. Admin View Order History (Unique)

Actors/Elements: Admin, Admin Frontend, API Gateway, Order Service, Database.

Description: Admin retrieves a paginated list of all orders across the system for analytics.

Sequence Diagrams (Unique Flows)

1. Place Order (Checkout)

This flow is unique because it handles the critical transition from a browsing state to a transactional state and triggers asynchronous events.

2. Async Order Notification

This flow is unique because it happens completely in the background (server-to-server) decoupled from the user's browser session.

3. Admin Update Inventory

This flow represents a privileged write operation that directly impacts the Product domain's state.

4. Admin View Order History

A complex read operation that aggregates data typically restricted from standard users.
