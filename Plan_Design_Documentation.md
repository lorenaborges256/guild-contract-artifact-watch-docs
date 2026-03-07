
# Planning & Design Documentation

## DEV1003 - Advanced Applications - Assessment 1

### Courtney - Lorena Borges Amaral - Simona

# MERN Project - Guild Availability Management System (GAMS)

## 1. Project Overview

The **Guild Availability Management System (GAMS)** is developed using an Object‑Oriented Programming (OOP) paradigm, where core entities will be modelled as objects with their own state and behaviour. The application follows a Model–View–Controller (MVC) architecture, separating data management, business logic, and user interface into clear layers that improve maintainability and scalability.  
As a MERN application, it will operates on a client/server model, with the React client handling user interactions while the Express/Mongoose server processes requests, applies business rules, and communicates with the MongoDB database.  
The project is managed using Agile principles, supporting iterative development, continuous feedback, and adaptability as requirements evolve. Task organisation is structured through a Kanban workflow, providing visibility of progress and enabling efficient team collaboration.  
Throughout development, the system adheres to ethical principles, prioritising user privacy, transparency, accessibility, and responsible handling of data to ensure a trustworthy and user‑centred application.

## 2. Software architecture

### 2.1 Programming paradigm: Object‑Oriented Programming (OOP)

The Object‑Oriented Programming (OOP) paradigm appears naturally in this project through the way Mongoose structures and manages data. In OOP, a _class_ defines what an object should look like, and each _object instance_ represents a real, individual item with its own data and behaviour. Mongoose follows this same pattern.  

When we define an `Item` schema with fields such as `name`, `description`, `stock_qty`, `created_at`, and `updated_at`, we are creating a blueprint that describes the state of every Item object in the system. Compiling this schema into a Mongoose model is similar to defining a class in traditional OOP: the model becomes the constructor used to create new Item objects. This reflects core OOP principles: encapsulation, where data and behaviour are grouped together inside the same object, and responsibility boundaries, where each Item object manages its own rules rather than relying on external code.

#### Example 1 - Simplified Object with data + behaviour (OOP encapsulation)

```javascript
const item = {
  name: "Ancient Sword",
  description: "A rare blade used by guild champions.",
  stock_qty: 3,
  isAvailable() {
    return this.stock_qty > 0;
  }
};
```
This example demonstrates the core OOP idea of encapsulation: the object stores its own data (state) and the function that operates on that data (behaviour).

#### Example 2 - Mongoose Model With a Simple Method (Real MERN OOP)

```javascript
const itemSchema = new mongoose.Schema({
  name: String,
  description: String,
  stock_qty: Number,
  created_at: Date,
  updated_at: Date
});

itemSchema.methods.isAvailable = function () {
  return this.stock_qty > 0;
};
```

Here, the model acts like a class, and each document created from it becomes an object instance with its own state and behaviour. The method `isAvailable()` belongs to the object and uses its own data, demonstrating OOP responsibility boundaries.

#### Example 3 - Controller Using Object Behaviour (Abstraction)

```javascript
if (!item.isAvailable()) {
  return res.status(400).json({ message: "Item not available" });
}
```

The controller does not calculate availability itself. Instead, it asks the object to perform the check. This is OOP abstraction, where internal logic is hidden inside the object.

#### 2.1.1 Object‑Oriented Programming Diagram - Planning and Design Version

<center><img src=".\img\OOP_Diagram.png" width="65%" alt="Object‑Oriented Programming Diagram">  </center>

_Fig 1. Example Object‑Oriented Programming Diagram for an Item entity, Image created by the team using draw.io._

### 2.2 Software architecture pattern: Model–View–Controller (MVC)

The application follows a Model–View–Controller (MVC)‑inspired architecture layered over a MERN stack.  
<center><img src=".\img\mvc-1.png" width="45%" alt="Model–View–Controller Diagram">  </center>

_Fig 2. Generic Model–View–Controller Diagram, Image from Ed Lessons website_

The Model layer (Mongoose schemas and domain logic) represents entities such as `User`, `Item`, and `Contract`. The Controller layer (Express controllers) coordinates requests, applies business rules, and interacts with models. The View layer will be implemented in React, consuming the backend’s REST API and rendering the user interface for dashboards, lists, and detail views.

#### 2.2.1 How MVC Maps to the MERN Stack

<center><img src="img\mvc_HightLevel_structure.png" width="65%" alt="Model–View–Controller High Level Structure">  </center>

_Fig 3. High Level Structure Model–View–Controller Diagram, Image created by the team using draw.io._

- **View (React Frontend)**: Displays data to the user and sends requests to the backend. Example: Item list page, Contract details page.
- **Controller (Express.js)**: Receives HTTP requests, calls the appropriate model methods, and returns responses. Example: `itemController.js`, `contractController.js`.
- **Model (MongoDB + Mongoose)**: Defines the structure of data and encapsulates business logic. Example: `Item`, `User`, `Contract` models.

#### 2.2.2 Example of How MVC Will Be Applied in This Project

##### Scenario: A user wants to reserve an item

1. View (React): The user clicks “Reserve” on the Item Details page. React sends a request: `POST /items/123/reserve`
2. Controller (Express): The `reserveItem` controller receives the request. It loads the Item object and calls its OOP method: `item.isAvailable()`
3. Model (Mongoose): The Item object checks its own state (`stock_qty`). If available, it updates itself and saves to MongoDB.
4. Response: The controller sends a success or error message back to React. React updates the UI accordingly.

<center><img src="img\mvc_example_Reserve.png" width="80%" height="80%" alt="Example of How MVC Will Be Applied in GAMS Project">  </center>

_Fig 4. MVC Applied in GAMS project Diagram, Image created by the team using draw.io._

## 3. Development methodologies

## 4. Client/server explanation

The Guild Availability Management System (GAMS) follows a client–server architecture implemented using the MERN stack (MongoDB, Express, React, Node.js). This architecture separates responsibilities between the frontend and backend to improve maintainability, scalability, and security.
In this model, the React application acts as the client. It runs in the user’s browser and is responsible for rendering the user interface, handling user interactions, and sending HTTP requests to the backend API.
The Express application acts as the server. It receives incoming requests, applies business logic, validates data, enforces authorisation rules, and communicates with MongoDB through Mongoose models.
MongoDB serves as the persistent data layer. It stores core entities such as Users, Items, Contracts, Reservations, Watchlists, and Notifications. All permanent system data is managed centrally through the backend, ensuring data integrity and preventing direct client access to the database.
This separation ensures that the frontend focuses on presentation and usability, while the backend controls system rules and data management.

## 4.1 Client/Server Communication

![Client Server Communication](img/client-server-communication.png)

_Fig 5. Client–server communication flow between the user's browser, the internet network and the application server._

Communication between the client and server follows a RESTful request–response model over HTTP.
The React frontend sends HTTP requests (GET, POST, PUT, DELETE) to API endpoints defined in the Express backend.
Each request follows this process:

1. The client sends an HTTP request to a specific endpoint.
2. The Express router maps the request to the appropriate controller.
3. The controller applies business logic.
4. The controller interacts with the relevant Mongoose model.
5. The model performs database operations in MongoDB.
6. The server returns a structured JSON response.
7. The client updates the interface based on the response.
   
Because this architecture is stateless, each request contains all the information required to process it. It reduces the server's reliance on session state and supports scalability.

## 4.2 Data Distribution

![Data Distribution](img/data-distribution.png)

_Fig 6. Data distribution between multiple clients, the central server and the database._

GAMS centralises all persistent data within MongoDB, which acts as the single source of truth.
The client does not store authoritative system data. Instead, it retrieves data from the backend when needed and updates information only through API requests.
The server manages all database interactions and determines what data can be accessed or modified. Core entities such as Users, Items, Contracts, Reservations, Watchlists, and Notifications are stored in MongoDB and accessed exclusively through the backend.
This approach ensures consistency, prevents client-side manipulation of sensitive information, and maintains overall system integrity.

## 4.3 Feature Distribution

The system distributes features according to responsibility.
The React frontend handles presentation and user interaction. It renders pages such as the item list, item details, contract views, watchlists, notifications, and administrative dashboards. It captures user actions, including reserving an item, accepting a contract, updating stock (admin), or managing watch preferences.
The Express backend enforces business rules and system logic. It processes requests, checks item availability, updates stock quantities, validates contract conditions, generates notifications, and controls access based on user roles.
By keeping decision-making logic on the server, the system prevents users from bypassing rules through client-side manipulation.

## 4.4 Authorisation

![Authentication and Authorisation](img/authentication-authorisation.png)

_Fig 7. Authentication and role-based authorisation process within the GAMS system._

GAMS uses role-based authorisation to control access to sensitive features.
After authentication, the backend identifies the user and assigns permissions based on their role (for example, regular user or admin).
Regular users can:

1. Browse items and contracts.
2. Reserve available items.
3. Accept contracts within defined conditions.
4. Manage their own watchlist and notifications.

Admin users have additional permissions. They can:

1. Create and edit items and contracts.
2. Update stock quantities.
3. Manage availability settings.
4. Perform administrative management actions.
The backend enforces these permissions on protected routes. Even if the frontend hides certain interface elements, the server performs the final authorisation check before executing any restricted operation.

## 4.5 Validation

Validation ensures that incoming data meets system requirements before being processed or stored.

### Client-side validation (React)

The React frontend performs basic validation to improve usability. It includes checking required fields, validating simple formats (such as email addresses), and preventing clearly invalid input (such as negative numbers in stock fields).
However, client-side validation is not sufficient for security because users can bypass the interface.

### Server-side validation (Express + Mongoose)

The backend performs final validation before updating the database. The server verifies that:
1. Required fields are present
2. Data types are correct
3. Values comply with business rules (for example, stock_qty cannot be negative)
4. The target record exists.
Mongoose schema definitions provide additional validation at the model level to maintain data consistency.
If validation fails, the server returns an appropriate error response and does not modify the database. If validation succeeds, the server completes the request and returns a success response to the client.

## 5. ERD explanation

The Entity Relationship Diagram (ERD) models the core data structures and interactions within the Guild Contract & Item Watch System, capturing how users engage with items, contracts, reservations, and notifications. It separates the two availability, behaviours—inventory‑based items and time‑window‑based contracts—into distinct entities, each with their own attributes and relational rules. Supporting entities such as Reservation, ContractAcceptance, Watchlist, and Notification represent user actions and system‑generated events, ensuring that every interaction is stored in a structured and traceable way.

<center><img src=".\ERD\guild-erd.png" alt="ERD Guild Availability Management System - Planing and Design Version">  </center>

_Fig 5. Entity Relationship Diagram (ERD) for the Guild Availability Management System, created by the student team using draw.io._

The ERD follows a fully normalised design, reducing redundancy and  clarifying the relationships between users, items, and contracts, while also supporting polymorphic associations for watch and notification functionality. This schema provides a stable foundation for the application’s API, business logic, and future scalability.

## 6. User stories

## 7. Ethical considerations

## 8. Wireframe overview

## 9. Conclusion

While this documentation outlines the conceptual and architectural direction of the system, several important steps remain before the application can be fully implemented. The next phase will involve building the initial data models, setting up the Express routes and controllers, and creating the first React components to establish the core user interface.  
Testing strategies, validation rules, and security considerations will also need to be expanded as development progresses. As the project moves into implementation, the team will continue to iterate on features, refine requirements, and ensure alignment with both technical goals and ethical standards.

## 10. References

1. MVC Image from [https://edstem.org/au/courses/25180/lessons/84072/slides/573930]
