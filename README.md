# RoomX Server

## Overview

RoomX is a platform that connects hosts and guests, enabling seamless room bookings and management. This server-side application, built with Node.js, Express, and MongoDB, provides the necessary APIs for user authentication, room management, booking services, and statistical analysis.

## Features

-   **User Authentication:** Secure authentication using JWT (JSON Web Tokens) and cookie-based sessions.
-   **Role-Based Access Control:** Implements admin and host roles with specific privileges.
-   **Room Management:** APIs for hosts to list, update, and delete rooms.
-   **Booking Services:** Allows guests to book rooms and manages booking information.
-   **Payment Integration:** Integration with Stripe for handling payments.
-   **Email Notifications:** Sends email notifications for booking confirmations and other events using Nodemailer.
-   **Statistics:** Provides statistical data for admins, hosts, and guests.

## Technologies Used

-   [Node.js](https://nodejs.org/): JavaScript runtime environment
-   [Express](https://expressjs.com/): Web application framework
-   [MongoDB](https://www.mongodb.com/): NoSQL database
-   [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken): For creating JSON Web Tokens
-   [cookie-parser](https://www.npmjs.com/package/cookie-parser): For parsing cookies
-   [cors](https://www.npmjs.com/package/cors): For enabling Cross-Origin Resource Sharing
-   [dotenv](https://www.npmjs.com/package/dotenv): For loading environment variables
-   [nodemailer](https://nodemailer.com/): For sending emails
-   [stripe](https://stripe.com/): For payment processing

## Setup

### Prerequisites

-   Node.js and npm installed
-   MongoDB account and cluster set up
-   Stripe account and API keys
-   Gmail account for Nodemailer

### Installation

1.  Clone the repository:

    ```sh
    git clone https://github.com/isha-web1/RoomX-server.git
    cd roomx-server
    ```

2.  Install dependencies:

    ```sh
    npm install
    ```

3.  Set up environment variables:

    -   Create a `.env` file in the root directory.
    -   Add the following environment variables:

        ```
        PORT=8000
        DB_USER=<your-mongodb-user>
        DB_PASS=<your-mongodb-password>
        ACCESS_TOKEN_SECRET=<your-jwt-access-token-secret>
        STRIPE_SECRET_KEY=<your-stripe-secret-key>
        TRANSPORTER_EMAIL=<your-gmail-email>
        TRANSPORTER_PASS=<your-gmail-app-password>
        NODE_ENV=development # or production
        ```

4.  Run the server:

    ```sh
    npm start
    ```

    or for development:

    ```sh
    npm run dev
    ```

## API Endpoints

### Authentication

-   `POST /jwt`: Generate a JWT token for user authentication.
-   `GET /logout`: Clear the token cookie to log out the user.

### User Management

-   `PUT /user`: Save or update user data in the database.
-   `GET /users`: Get all users (admin only). Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) and [`verifyAdmin`](c:\Level1-project\roomx-server\index.js) middleware.
-   `PATCH /users/update/:email`: Update a user's role.
-   `GET /user/:email`: Get a user's information by email.

### Room Management

-   `GET /rooms`: Get all rooms, optionally filtered by category.
-   `POST /room`: Save a room (host only). Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) and [`verifyHost`](c:\Level1-project\roomx-server\index.js) middleware.
-   `GET /my-listings/:email`: Get all rooms for a specific host. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) and [`verifyHost`](c:\Level1-project\roomx-server\index.js) middleware.
-   `DELETE /room/:id`: Delete a room (host only). Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) and [`verifyHost`](c:\Level1-project\roomx-server\index.js) middleware.
-   `GET /room/:id`: Get a single room by ID.
-   `PATCH /room/status/:id`: Update room status.
-   `PUT /room/update/:id`: Update room data (host only). Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) and [`verifyHost`](c:\Level1-project\roomx-server\index.js) middleware.

### Booking Management

-   `POST /booking`: Save booking data. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) middleware.
-   `GET /my-bookings/:email`: Get all bookings for a guest. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) middleware.
-   `GET /manage-bookings/:email`: Get all bookings for a host. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) and [`verifyHost`](c:\Level1-project\roomx-server\index.js) middleware.
-   `DELETE /booking/:id`: Delete a booking. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) middleware.

### Payment

-   `POST /create-payment-intent`: Create a payment intent. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) middleware.

### Statistics

-   `GET /admin-stat`: Get admin statistics. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) and [`verifyAdmin`](c:\Level1-project\roomx-server\index.js) middleware.
-   `GET /host-stat`: Get host statistics. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) and [`verifyHost`](c:\Level1-project\roomx-server\index.js) middleware.
-   `GET /guest-stat`: Get guest statistics. Requires [`verifyToken`](c:\Level1-project\roomx-server\index.js) middleware.

## Middleware

-   [`verifyToken`](c:\Level1-project\roomx-server\index.js): Verifies the JWT token.
-   [`verifyAdmin`](c:\Level1-project\roomx-server\index.js): Checks if the user has the admin role.
-   [`verifyHost`](c:\Level1-project\roomx-server\index.js): Checks if the user has the host role.

## Email Configuration

The server uses Nodemailer to send emails. Ensure that the `TRANSPORTER_EMAIL` and `TRANSPORTER_PASS` environment variables are correctly set up with a valid Gmail account and an app-specific password.

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your changes.

## License

[ISC](LICENSE)
