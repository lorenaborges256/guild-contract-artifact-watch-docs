# Guild Contract & Artifact Watch System

## Scope (v2 – Draft for Alignment)

### Project Overview

A dashboard-style availability and reservation system where users can create an account, browse items (inventory-based items) and guild contracts (time-based quests), and interact with them based on their availability.

Items can be reserved while in stock, generating a reservation number for in-person payment and collection at the guild. Guild contracts can be accepted during their active window, providing users with instructions to present to the guild upon completion to collect their reward.

Users can watch unavailable items or contracts and receive notifications when they become available.

The system models two different availability behaviours:

- Items are inventory-based.
- Contracts are time-window based.

---

### Core User Roles

- User
- Admin

---

### Core Features

#### Authentication

- User account creation
- Login/logout functionality
- Role-based access (User vs Admin)

---

#### Items – Inventory-Based

- Admin sets `stock_quantity`
- Users can reserve `while stock_quantity > 0`
- Users can reserve an item while it’s in stock
- Reserving decrements stock by 1 and generates a reservation number
- When stock reaches 0, item becomes unavailable
- Users can watch unavailable items and get notified when restocked (0 → >0)

##### Reservation scope:

- No cart, payments, or order history
- Reservation number is used for payment/collection in person at the guild

---

#### Guild Contracts – Time-Based

- Admin sets `start_at`, `end_at`, and `max_acceptances`
- A contract is available only within the time window and while acceptances remain
- Users can accept a contract while it’s available
- Accepting generates directions/instructions to present to the guild on completion to collect the reward
- Users can watch unavailable contracts and get notified when the contract opens

##### Reward scope

- Rewards are collected in person (no redemption tracking in the app)

---

#### Watch & Notification Behaviour

- Users can watch unavailable items and contracts
- Notifications are triggered when:
  - Item becomes available (stock changes from 0 → >0)
  - Contract becomes available (time window starts and max_acceptances are not reached)
- Users can view and manage their watched items/contracts and notifications

---

#### Admin Capabilities

- Create and edit items and contracts
- Set stock quantities (items)
- Set start/end time windows (contracts)
- Manage users
- Trigger availability changes that generate notifications

---

#### Core Data Entities (Initial)

- User
- Item
- Contract
- Reservation
- ContractAcceptance
- Watchlist
- Notification

---

#### Optional Extensions (Time Permitting)

- Email notifications (in addition to in-app)
- Enhanced notification history with read/unread status
- Audit/log view for admin actions

---
