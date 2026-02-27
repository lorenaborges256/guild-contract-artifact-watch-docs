
# Planning & Design Documentation

## DEV1003 - Advanced Applications

### Courtney & Lorena Borges Amaral

# MERN Project Title - Guild Contract & Artifact Watch System

## 1. Introduction

## 2. Project overview

## 3. Software architecture

### 3.1 Programming paradigm: Object‑Oriented Programming (OOP)

The Object‑Oriented Programming (OOP) paradigm appears naturally in this project through the way Mongoose structures and manages data. In OOP, a _class_ defines what an object should look like, and each _object instance_ represents a real, individual item with its own data and behaviour. Mongoose follows this same pattern.  

When we define an `Artifact` schema with fields such as `name`, `description`, `stock_qty`, `created_at`, and `updated_at`, we are creating a blueprint that describes the state of every Artifact object in the system. Compiling this schema into a Mongoose model is similar to defining a class in traditional OOP: the model becomes the constructor used to create new Artifact objects. This reflects core OOP principles: **encapsulation**, where data and behaviour are grouped together inside the same object, and **responsibility boundaries**, where each Artifact object manages its own rules rather than relying on external code.

#### 3.1.1 Example 1 - Simplified Object with data + behaviour (OOP encapsulation)

```javascript
const artifact = {
  name: "Ancient Sword",
  description: "A rare blade used by guild champions.",
  stock_qty: 3,
  isAvailable() {
    return this.stock_qty > 0;
  }
};

```
This example demonstrates the core OOP idea of encapsulation: the object stores its own data (state) and the function that operates on that data (behaviour).

#### 3.1.2 Example 2 - Mongoose Model With a Simple Method (Real MERN OOP)

```javascript
const artifactSchema = new mongoose.Schema({
  name: String,
  description: String,
  stock_qty: Number,
  created_at: Date,
  updated_at: Date
});

artifactSchema.methods.isAvailable = function () {
  return this.stock_qty > 0;
};

```

Here, the model acts like a **class**, and each document created from it becomes an **object instance** with its own state and behaviour. The method `isAvailable()` belongs to the object and uses its own data, demonstrating OOP responsibility boundaries.


#### 3.1.3 Example 3 - Controller Using Object Behaviour (Abstraction)

```javascript
if (!artifact.isAvailable()) {
  return res.status(400).json({ message: "Artifact not available" });
}
```

The controller does not calculate availability itself. Instead, it **asks the object** to perform the check. This is OOP **abstraction**, where internal logic is hidden inside the object.

#### 3.1.4 Object‑Oriented Programming Diagram - Planning and Design Version

<center><img src=".\img\OOP_Diagram.png" width="50%" height="50%" alt="Object‑Oriented Programming Diagram">  </center>

_Fig 1. Example Object‑Oriented Programming Diagram for an Artifact entity, Image created by the team using draw.io._

### 3.2 Software architecture pattern: Model–View–Controller (MVC)

The application follows a Model–View–Controller (MVC)‑inspired architecture layered over a MERN stack.  
<center><img src=".\img\mvc-1.png" width="35%" height="35%" alt="Model–View–Controller Diagram">  </center>

_Fig 2. Generic Model–View–Controller Diagram, Image from Ed Lessons website_

The **Model** layer (Mongoose schemas and domain logic) represents entities such as `User`, `Artifact`, and `Quest`. The **Controller** layer (Express controllers) coordinates requests, applies business rules, and interacts with models. The **View** layer will be implemented in React, consuming the backend’s REST API and rendering the user interface for dashboards, lists, and detail views.

#### 3.2.1 How MVC Maps to the MERN Stack

<center><img src="img\mvc_HightLevel_structure.png" width="60%" height="60%" alt="Model–View–Controller High Level Structure">  </center>

_Fig 3. High Level Structure Model–View–Controller Diagram, Image created by the team using draw.io._

- **View (React Frontend)**: Displays data to the user and sends requests to the backend. Example: Artifact list page, Quest details page.
- **Controller (Express.js)**: Receives HTTP requests, calls the appropriate model methods, and returns responses. Example: `artifactController.js`, `questController.js`.
- **Model (MongoDB + Mongoose)**: Defines the structure of data and encapsulates business logic. Example: `Artifact`, `User`, `Quest` models.

#### 3.2.2 Example of How MVC Will Be Applied in This Project

**Scenario: A user wants to reserve an artifact**
1. View (React): The user clicks “Reserve” on the Artifact Details page. React sends a request: `POST /artifacts/123/reserve`
2. Controller (Express): The `reserveArtifact` controller receives the request. It loads the Artifact object and calls its OOP method: `artifact.isAvailable()`
3. Model (Mongoose): The Artifact object checks its own state (`stock_qty`). If available, it updates itself and saves to MongoDB.
4. Response: The controller sends a success or error message back to React. React updates the UI accordingly.

<center><img src="img\mvc_example_Reserve.png" width="80%" height="80%" alt="Example of How MVC Will Be Applied in GAMS Project">  </center>

_Fig 3. MVC Applied in GAMS project Diagram, Image created by the team using draw.io._


## 4. Development methodologies

## 5. Client/server explanation

## 6. ERD explanation

The Entity Relationship Diagram (ERD) models the core data structures and interactions within the Guild Contract & Artifact Watch System, capturing how users engage with artifacts, quests, reservations, and notifications. It separates the two availability, behaviours—inventory‑based items and time‑window‑based quests—into distinct entities, each with their own attributes and relational rules. Supporting entities such as Reservation, QuestAcceptance, Watchlist, and Notification represent user actions and system‑generated events, ensuring that every interaction is stored in a structured and traceable way.

<center><img src=".\ERD\guild-erd.png" alt="ERD Guild Contract & Artifact Watch System - Planing and Design Version">  </center>

_Fig 3. Entity Relationship Diagram (ERD) for the Guild Contract & Artifact Watch System, created by the student team using draw.io._

 The ERD follows a fully normalised design, reducing redundancy and  clarifying the relationships between users, items, and quests, while also supporting polymorphic associations for watch and notification functionality. This schema provides a stable foundation for the application’s API, business logic, and future scalability.

## 7. User stories

## 8. Ethical considerations

## 9. Wireframe overview

## 10. Conclusion

## 11. References

1. MVC Image from [https://edstem.org/au/courses/25180/lessons/84072/slides/573930]