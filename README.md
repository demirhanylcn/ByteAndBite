# ByteAndBite(SQL)
Summer Semester 2023, RBD Project

ByteAndBite is a relational database project crafted to manage and enhance data operations in a restaurant environment. The database handles customer information, orders, chefs, recipes, ingredients, and payment details, bridging the gap between digital data and culinary operations.

## Project Overview

ByteAndBite is built to streamline restaurant management through a structured SQL schema. It allows for efficient storage, retrieval, and analysis of essential restaurant data, helping businesses optimize their processes, improve customer service, and gain insights into their operations.

## Features

- **Customer and Chef Management**: Store detailed information about customers and chefs, including relationships and hierarchical structures (e.g., mentor-chef assignments).
- **Order Processing and Payment Tracking**: Track orders from creation to completion, with seamless payment integration.
- **Recipe and Ingredient Organization**: Maintain a repository of recipes and their required ingredients, supporting menu planning and inventory management.
- **Data Relationships**: Leverage foreign keys to link various entities, ensuring referential integrity across tables.
- **Query Capabilities**: Predefined SQL queries provide insights, such as total orders in a time frame or categorization of payment amounts.

## Database Schema

The ByteAndBite schema includes the following tables:

- **Person**: Stores basic information for all individuals, including chefs and customers.
- **Chef**: Contains chef-specific data, such as hire dates and master-chef relationships.
- **Customer**: Includes customer-related information and links to `Person`.
- **Order**: Tracks customer orders, order details, and related data.
- **Payment**: Manages payment details, including amount, type, and payment date.
- **Payment_Type**: Defines categories of payments (e.g., Normal, Expensive).
- **Recipe and Ingredients**: Stores recipes and the ingredients required, linking dishes to their components.

## Installation

1. Clone this repository:
   `git clone https://github.com/demirhanylcn/ByteAndBite.git`
2. Import the SQL scripts into your SQL server or database environment to create the schema.

## Usage

1. Run the `oracle_create_and_insert.sql` script to set up the database schema.
2. Use the `oracle_queries.sql` file for sample queries, such as retrieving all payments within a specific date range or listing all chefs and their specialties.


