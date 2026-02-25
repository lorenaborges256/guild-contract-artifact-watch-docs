
# Planning & Design Documentation

## DEV1003 - Advanced Applications

### Courtney & Lorena Borges Amaral

# MERN Project Title - Guild Contract & Artifact Watch System

## 1. Introduction

## 2. Project overview

## 3. Software architecture

### 3.1 Programming paradigm: Object‑Oriented Programming (OOP)

This project uses an Object‑Oriented Programming (OOP) paradigm to organise the system around meaningful entities such as ``User``, ``Artifact``, and ``Quest``. In OOP, each entity has its own data (state) and the functions that operate on that data (behaviour). Even though JavaScript uses prototypes rather than classical classes, the MERN stack still applies OOP principles through ``Mongoose models``, ``methods``, and ``structured objects``. OOP helps keep logic predictable by grouping related data and behaviour together, which is essential for managing reservations, quest availability, and user watchlists.

#### 3.1.1 Example 1
#### 3.1.2 Example 2
#### 3.1.3 Example 3
#### 3.1.4 Object‑Oriented Programming Diagram

### 3.2 Software architecture pattern: Model–View–Controller (MVC)

The application follows a Model–View–Controller (MVC)‑inspired architecture layered over a MERN stack.  
<center><img src=".\img\mvc-1.png" width="60%" alt="Model–View–Controller Diagram">  </center>
*Generic Model–View–Controller Diagram* [1. Image from Ed Lessons website]

The **Model** layer (Mongoose schemas and domain logic) represents entities such as `User`, `Artifact`, and `Quest`. The **Controller** layer (Express controllers) coordinates requests, applies business rules, and interacts with models. The **View** layer will be implemented in React, consuming the backend’s REST API and rendering the user interface for dashboards, lists, and detail views.

## 4. Development methodologies

## 5. Client/server explanation

## 6. ERD explanation

The Entity Relationship Diagram (ERD) models the core data structures and interactions within the Guild Contract & Artifact Watch System, capturing how users engage with artifacts, quests, reservations, and notifications. It separates the two availability, behaviours—inventory‑based items and time‑window‑based quests—into distinct entities, each with their own attributes and relational rules. Supporting entities such as Reservation, QuestAcceptance, Watchlist, and Notification represent user actions and system‑generated events, ensuring that every interaction is stored in a structured and traceable way.

![ERD Guild Contract & Artifact Watch System - Planing and Design Version]( .\ERD\guild-erd.png "Logo Title Text 1")

 The ERD follows a fully normalised design, reducing redundancy and clarifying the relationships between users, items, and quests, while also supporting polymorphic associations for watch and notification functionality. This schema provides a stable foundation for the application’s API, business logic, and future scalability.

## 7. User stories

## 8. Ethical considerations

## 9. Wireframe overview

## 10. Conclusion

## 11. References

1. MVC Image from [https://edstem.org/au/courses/25180/lessons/84072/slides/573930]