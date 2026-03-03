
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
