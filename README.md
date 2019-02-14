# Project Trello Board

https://trello.com/b/IeOy1pGI/back-end-project-week

**_A blockchain enabled note taking platform_**

Lambda Notes utilizes [Blockstacks's](https://blockstack.org/) 
innovative technology which allows developers to build dApps
(decentralized apps) and users to access them throught the Blockstack browser. With Blockstack, the data generated in an app is owned by the user and privacy, security, and freedom are maintained. Blockstack provides key tools and infrastructure for enabling decentralized storage and decentralized authentication and identity. After logging in using Blockstack's identity verificatiion, the user's notes are stored in decentralized multi-player Gaia storage.

## Team

### Developers
[James Hutton](https://github.com/FreeKeyBoy)

## Tech Stack

Lambda Notes utilizes [Heroku](https://www.heroku.com/) and [Netlify](https://www.netlify.com/) for deployment, and is built in full stack JavaScript with a [React.js](https://reactjs.org/) frontend, a [Node.js](https://nodejs.org/en/) and [Express.js](https://expressjs.com/) backend, Blockstack's [Gaia](https://github.com/blockstack/gaia/blob/master/README.md) high-performance decentralized storage system is used to store notes in production, and a [SQLite3](https://www.sqlite.org/index.html) database in development.

### Rationale

#### Frontend
- netlify

- React

  - Blazing fast rendering with the virtual DOM
  - Robust developer tools for debugging
  - Component based structure maximizes reusablity and makes codebase more maintainable
  - Unidirectional data flow increases app performance and makes debugging easier
  - API friendly library works seamlessly with and is extendable across numerous frameworks to leverage advanced UI development

- Styled Components

  - Scopes styles to a component to avoid style leaks
  - Linters will show unused components so they can be removed
  - Source order independence eliminates the need to import files in a certain order
  - Compose new styles from existing components
  - Passing properties to the component allows for more flexibility

#### Backend

- heroku

- Node.js

  - Utilizes Google's V8 JS engine which is lightening fast, highly performant, and more scalable
  - Event loop allows non-blocking I/O operations which enhances speed of code execution
  - Integrates seamlessly with microservices architecture
  - Fullstack JS allows JS developers to work on both client and server sides potentially increasing productivity and saving money for startups

- Express

  - Includes numerous routing features and separate handlers for HTTP methods
  - Serves static files such as images and CSS / JS files
  - Integrates seamlessly with many popular template engine and NPM module plugins

## API

### Third Party API

[Gaia](https://github.com/blockstack/gaia)

  - Blockstack applications use the Gaia storage system to store data on behalf of a user. When the user logs in to an application, the authentication process gives the application the URL of a Gaia hub, which performs writes on behalf of that user. The Gaia hub authenticates writes to a location by requiring a valid authentication token, generated by a private key authorized to write at that location.

- [Stripe](https://stripe.com/docs/api)

- Users can pay for the premium version of the serbvice. Stripe verifies and charges their credit card.

- [Blockstack](https://github.com/blockstack/blockstack.js/blob/master/src/auth/README.md)
 - Users can sign up/log in using Blockstack's bearer token-based authentication system.

### API Endpoints

| Method | Endpoint            | Request               | Response                      |
| ------ | ------------------- | --------------------- | ----------------------------- |
| GET    | /users/profile      |                       | Object of logged in user      |
| GET    | /users/subscription | email\                | Object with subscription type |
| GET    | /payment            |                       | Array of invoice objects      |
| POST   | /payment            | userId, stripeCharges | Invoice                       |
| GET    | /notes              |                       | Array of notes                |
| GET    | /notes/:id          |                       | Single note                   |
| POST   | /create             |                       | Create note object            |
| PUT    | /edit/:id           |                       | Edit existing note object     |
| DELETE | /delete/:id/        |                       | Delete an existing note       |
| GET    | /auth/logout        |                       | 200 on successful logout      |

## Security

### Authentication & Authorization

#### Blockstack

Blockstack Authentication provides single sign on and authentication without third parties or remote servers. Blockstack Authentication is a bearer token-based authentication system. From an app user's perspective, it functions similar to legacy third-party authentication techniques that they're familiar with. For an app developer, the flow is a bit different from the typical client-server flow of centralized sign in services (e.g., OAuth). Rather, with Blockstack, the authentication flow happens entirely client-side.

### Payments

#### Stripe & Credits

Stripe is used to securely verify user credit cards and payments. After a user submits a payment, if it is successful, Stripe will send back a response the the payment is valid as well as an invoice that is saved to the database. Once this is complete, the user can access the premium features.