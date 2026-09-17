# Restaurant Operations Management System

A multi-restaurant operations management system developed in **Java**, designed to coordinate customer orders, kitchen workflows, inventory, stock replenishment, payments and administrative monitoring through a centralized business architecture.

The application uses a **layered architecture** with dedicated business subsystems, Facades and Data Access Objects (DAOs), backed by a **MariaDB relational database**.

---

## Overview

The system models the day-to-day operations of a restaurant chain and integrates several areas of the business into a single application.

It provides dedicated interfaces for:

* Customers placing and customizing orders
* Kitchen/workstation employees processing orders
* Warehouse employees managing stock and replenishment
* Managers monitoring restaurant performance and communicating with operational displays

Multiple restaurant locations are supported through the same system and database.

---

## Key Features

### Customer Ordering

Customers can:

* Browse currently available products
* Create new orders
* Add and remove products
* Select product quantities
* Customize products by removing ingredients
* Add notes to an order
* Choose between dine-in and takeaway
* Confirm or cancel an order
* Pay using different payment methods
* Receive an invoice after payment

Product availability is dynamically determined according to the ingredient stock of the selected restaurant.

---

### Order Processing

Restaurant workstations can:

* View pending orders
* Track order state
* Update order status
* Register preparation delays
* Access order information
* Request missing ingredients from stock

This creates a workflow between customer ordering, preparation and inventory management.

---

### Inventory Management

The inventory subsystem provides functionality for:

* Monitoring current ingredient quantities
* Managing stock per restaurant
* Defining minimum and recommended quantities
* Requesting ingredient replenishment
* Monitoring pending replenishment requests
* Setting estimated replenishment times
* Completing replenishment operations
* Restoring restaurant stock

Each restaurant maintains its own independent stock.

---

### Administration

Authenticated users have access to administrative features according to the restaurants assigned to their account.

The administration subsystem supports:

* User authentication
* Restaurant access management
* Viewing restaurant performance indicators
* Monitoring total revenue
* Monitoring average service time
* Sending messages to restaurant displays
* Managing sessions across the application

The database supports both centralized management roles and restaurant-specific users.

---

# Architecture

The application follows a layered architecture that separates user interaction, business logic and persistence.

```text
┌─────────────────────────────────────┐
│           Presentation Layer        │
│                                     │
│  Customer │ Counter │ Warehouse     │
│             Administration          │
└───────────────────┬─────────────────┘
                    │
                    ▼
┌─────────────────────────────────────┐
│             Controllers             │
└───────────────────┬─────────────────┘
                    │
                    ▼
┌─────────────────────────────────────┐
│             LN Facade               │
│                                     │
│             ILNFacade               │
│             LNFacade                │
└───────────────────┬─────────────────┘
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
┌─────────────┐ ┌─────────┐ ┌─────────┐
│Administration│ │ Orders  │ │  Stock  │
│  Subsystem   │ │Subsystem│ │Subsystem│
└──────┬──────┘ └────┬────┘ └────┬────┘
       │              │           │
       └──────────────┼───────────┘
                      │
                      ▼
┌─────────────────────────────────────┐
│          Persistence Layer          │
│                                     │
│                DAOs                 │
└───────────────────┬─────────────────┘
                    │
                    ▼
             ┌─────────────┐
             │   MariaDB   │
             └─────────────┘
```

---

## Business Subsystems

The business layer is divided into three main subsystems.

### Administration Subsystem

Responsible for:

* Authentication
* User sessions
* Restaurant access
* Operational indicators
* Internal messages

---

### Order Subsystem

Responsible for:

* Order creation
* Products and menus
* Product customization
* Order status
* Payments
* Invoices
* Preparation delays

---

### Stock Subsystem

Responsible for:

* Ingredient inventory
* Restaurant stock
* Workstations
* Replenishment requests
* Replenishment times
* Stock updates

---

# Getting Started

## Requirements

To run the application you need:

* Java 17 or newer
* MariaDB
* Gradle is not required separately because the Gradle Wrapper is included

---

## 1. Start MariaDB

Make sure the MariaDB server is running.

On Linux:

```bash
sudo systemctl start mariadb
```

---

## 2. Initialize the Database

The repository includes a complete SQL script containing the database schema and sample data.

From the `final` directory:

```bash
mariadb < database.sql
```

This creates and populates the `dssrestaurantes` database.

---

## 3. Database Configuration

Database connection settings are defined in:

```text
src/main/java/projeto/data/Config.java
```

The application expects a MariaDB server running at:

```text
localhost:3306
```

Update the configuration if your local database uses different credentials or connection settings.

> The credentials and example accounts included in the SQL file are intended only for local development and academic demonstration. They should not be used in a production environment.

---

## 4. Build the Application

```bash
./gradlew build
```

Alternatively:

```bash
./gradlew compileJava
```

---

## 5. Run the Application

```bash
./gradlew run
```

For cleaner terminal output:

```bash
./gradlew run --console=plain
```

---

# Authors

Developed by:

* **Heitor Araújo Fernandes**
* **José Pedro Joaquim Perera**
* **Juliana Sofia Vaz da Silva**
* **Sofia Margarida Rodrigues Freitas**
* **Soraia Filipa Ribeiro Pereira**

---

# Academic Context

Developed during the **2025/2026 academic year** as a **Software Systems Development** project.
