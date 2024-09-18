# Salon Appointment Scheduler

This project is a simple Salon Appointment Scheduler built using PostgreSQL and Bash scripting. It allows users to book appointments for various salon services by interacting with a script that manages the database operations.

## Project Overview

The Salon Appointment Scheduler project involves creating a PostgreSQL database and a Bash script to manage customer appointments. The script allows users to select a service, enter their phone number, and book an appointment. If the customer is new, their details are added to the database.

## Features

- Create and manage a PostgreSQL database for salon appointments.
- Add and manage customers, services, and appointments.
- Ensure unique phone numbers for customers.
- Display available services and prompt users for input.
- Handle new and existing customers seamlessly.

## Database Schema

The database consists of three tables: `customers`, `services`, and `appointments`.

- `customers` table:
  - `customer_id` (Primary Key, auto-increment)
  - `name` (VARCHAR, not null)
  - `phone` (VARCHAR, unique, not null)

- `services` table:
  - `service_id` (Primary Key, auto-increment)
  - `name` (VARCHAR, not null)

- `appointments` table:
  - `appointment_id` (Primary Key, auto-increment)
  - `customer_id` (Foreign Key referencing `customers(customer_id)`)
  - `service_id` (Foreign Key referencing `services(service_id)`)
  - `time` (VARCHAR, not null)

## Setup Instructions

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/salon-appointment-scheduler.git
   cd salon-appointment-scheduler
2. Create Database:
   ```sql
   psql --username=freecodecamp --dbname=postgres -c "CREATE DATABASE salon;"
3. Connect Database:
   ```sql
   psql --username=freecodecamp --dbname=salon
4. Create the Tables:
   ```sql
   CREATE TABLE customers (
   customer_id SERIAL PRIMARY KEY,
   name VARCHAR NOT NULL,
   phone VARCHAR UNIQUE NOT NULL
   );

    CREATE TABLE services (
      service_id SERIAL PRIMARY KEY,
      name VARCHAR NOT NULL
    );
    
    CREATE TABLE appointments (
      appointment_id SERIAL PRIMARY KEY,
      customer_id INT REFERENCES customers(customer_id),
      service_id INT REFERENCES services(service_id),
      time VARCHAR NOT NULL
    ); 
5. Insert Initial Data into Services Table:
   ```sql
   INSERT INTO services (name) VALUES ('cut'),('color'),('perm'),('style'),('trim');
   
6. Create the `salon.sh` File:
   ```bash
   touch salon.sh
   
7. Make the Script Executable:
   ```bash
   chmod +x salon.sh
   
8. Run the Script:
   ```bash
   ./salon.sh
   
## Usage

-  Run the salon.sh script to start the appointment scheduler.
-  Follow the prompts to select a service, enter your phone number, and book an appointment.
-  If you are a new customer, you will be prompted to enter your name.

## Saving Progress

- To save your database progress, you can create a dump of it:
  ```bash
  pg_dump -cC --inserts -U freecodecamp salon > salon.sql
  
- To rebuild the database from the dump file:
  ```bash
  psql -U postgres < salon.sql
  
## Contributing
Contributions are welcome! Please fork the repository and submit a pull request with your changes.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments
- Thanks to freeCodeCamp for providing the project framework.
- Thanks to PostgreSQL for the database management system.
