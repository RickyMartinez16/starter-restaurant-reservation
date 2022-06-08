# Reservation Table System

### Website URL: 

The Reservation Table system is a restaurant schedule management application that allows the user to manage their restaurant's reservations and tables. Users have the ability to add/delete reservations aswell as create new tables with different capacites to fit their guests. 

## Technologies Used
### Front End
- React.js
- Bootstrap
- CSS
- HTML/JSX
- React Router
- React Hooks

### Back End
- Node.js
- Express.js
- PostgreSQL 
- Knex.js
- CORS

## Installation
1. Fork and clone this repository.
2. Run `cp ./back-end/.env.sample ./back-end/.env`.
3. Update the `./back-end/.env` file with the connection URL's to your ElephantSQL database instance.
4. Run `cp ./front-end/.env.sample ./front-end/.env`.
5. You should not need to make changes to the `./front-end/.env` file unless you want to connect to a backend at a location other than `http://localhost:5001`.
6. Run `npm install` to install project dependencies.
7. Run `npm run start:dev` to start your server in development mode.

## Running Tests
Test are split up by user story. You can run the tests for a given user story by running:

`npm run test:X` where `X` is the user story number.

Have a look at the following examples:

- `npm run test:1` runs all the tests for user story 1 (both frontend and backend).
- `npm run test:3:backend` runs only the backend tests for user story 3.
- `npm run test:3:frontend` runs only the frontend tests for user story 3.

All Tests
- `npm test runs` all tests.
- `npm run test:backend` runs all backend tests.
- `npm run test:frontend` runs all frontend tests.
- `npm run test:e2e` runs only the end-to-end tests.


## Database setup

1. Set up four new ElephantSQL database instances - development, test, preview, and production - by following the instructions in the "PostgreSQL: Creating & Deleting Databases" checkpoint.
1. After setting up your database instances, connect DBeaver to your new database instances by following the instructions in the "PostgreSQL: Installing DBeaver" checkpoint.

### Knex

Run `npx knex` commands from within the `back-end` folder, which is where the `knexfile.js` file is located.

<br>

# Features

## Creating A Reservation

You can create a new reservation by selecting "New Reservation in the nav bar. This requires the customer's first name, last name, reservation date, reservation time, number of guests, and phone number.

![Create Res Form](/images/us-01-cancel-before.png)

# API

## Create Reservation

**POST** `/reservations`

- Required body:
  | Param | type |
  | ---------- | ---------- |
  | `first_name` | `str` |
  | `last_name` | `str` |
  | `party` | `int` |
  | `reservation_date` | `date` |
  | `reservation_time` | `str` |
  | `mobile_number` | `str` |

## Get Reservations by Date

**GET** `/reservations?date=<reservation_date>`

Returns reservations for a particular date

## Get Reservations by Id

`/reservations/:reservation_id`

### Available Methods

- **GET** - Returns a reservation given an existing reservation Id
- **PUT** - Modifies an existing reservation given an existing reservation Id
  - Required params:
    - `reservation_id (int)`
  - Required body:
    | Param | type |
    | ---------- | ---------- |
    | `first_name` | `str` |
    | `last_name` | `str` |
    | `party` | `int` |
    | `reservation_date` | `date` |
    | `reservation_time` | `str` |
    | `mobile_number` | `str` |

## Get Reservation Status

**GET** `/reservations/:reservation_id/status`

Returns a status of [ `booked, seated, finished, cancelled` ] for the particular reservation

## Get Tables

- **GET** `/tables`

Returns the available tables.

## Create Table

- **POST** `/tables`

Creates a table to be listed in the table list.

- Required body:
  | Param | type |
  | ---------- | ---------- |
  | `table_name` | `str` |
  | `capacity` | `int` |

## Update Table Status

- **PUT** `/tables/:table_id/seat`

Sets table status to 'occupied' and ties a `restaurant_id` to it.

- Required body:
  | Param | type |
  | ---------- | ---------- |
  | `reservation_id` | `int` |

## Finish Table

- **DELETE** `/tables/:table_id/seat`

Sets the table status to `free` and the accompanying reservation status to `finished`

- Required body:
  | Param | type |
  | ---------- | ---------- |
  | `reservation_id` | `int` |