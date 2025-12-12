User Flows & Interactions

User Sign Up

Actors/Elements: Customer, Frontend, API Gateway, User Service, Database.

Description: A new user registers for an account. Credentials are hashed and stored.

User Login

Actors/Elements: Customer, Frontend, API Gateway, User Service, Database.

Description: User exchanges credentials for a JWT (JSON Web Token) for session authentication.

Browse Products

Actors/Elements: Customer, Frontend, API Gateway, Product Service, Database.

Description: User views the list of available products and prices.

View Product Details

Actors/Elements: Customer, Frontend, API Gateway, Product Service, Database.

Description: User clicks a specific item to see detailed description and stock status.

Place Order (Checkout) (Unique)

Actors/Elements: Customer, Frontend, API Gateway, Order Service, Database, Message Queue.

Description: User finalizes purchase. Order is saved, inventory is checked, and an event is published for async processing.

Async Order Notification (Unique)

Actors/Elements: Message Queue, Notification Service, External Email Provider.

Description: The system picks up a "New Order" event and sends a confirmation email without blocking the user.

Admin Update Inventory (Unique)

Actors/Elements: Admin, Admin Frontend, API Gateway, Product Service, Database.

Description: Store admin updates the stock count for a specific product.

Admin View Order History (Unique)

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
