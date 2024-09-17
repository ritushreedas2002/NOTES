# NestJS Documentation for Beginners

## Introduction

NestJS is a powerful framework for building scalable and maintainable server-side applications using TypeScript. It combines the best features of modern frameworks with the flexibility and simplicity of JavaScript.

## Getting Started

To start using NestJS, follow these steps:

1. Install Node.js and npm on your machine.
2. Create a new directory for your project.
3. Open a terminal and navigate to the project directory.
4. Run the following command to create a new NestJS project:

```bash
$ npx @nestjs/cli new project-name
```

5. Once the project is created, navigate into the project directory:

```bash
$ cd project-name
```

6. Start the development server:

```bash
$ npm run start:dev
```

## Project Structure

NestJS follows a modular architecture, which helps in organizing your codebase. The default project structure looks like this:

```
project-name
├── src
│   ├── main.ts
│   ├── app.module.ts
│   ├── app.controller.ts
│   └── app.service.ts
├── test
│   └── app.e2e-spec.ts
├── nest-cli.json
├── package.json
└── tsconfig.json
```

- `src/main.ts`: The entry point of your application.
- `src/app.module.ts`: The root module of your application.
- `src/app.controller.ts`: The controller responsible for handling HTTP requests.
- `src/app.service.ts`: The service responsible for handling business logic.
- `test/app.e2e-spec.ts`: End-to-end tests for your application.

## Controllers and Routes

In NestJS, controllers are responsible for handling incoming HTTP requests and returning responses. Here's an example of a basic controller:

```typescript
import { Controller, Get } from "@nestjs/common";

@Controller("users")
export class UsersController {
  @Get()
  findAll(): string {
    return "This action returns all users";
  }
}
```

In the above example, we define a `UsersController` with a `findAll` method that handles GET requests to the `/users` route.

## Services

Services in NestJS are responsible for encapsulating business logic and can be injected into controllers or other services. Here's an example of a basic service:

```typescript
import { Injectable } from "@nestjs/common";

@Injectable()
export class UsersService {
  findAll(): string {
    return "This action returns all users";
  }
}
```

In the above example, we define a `UsersService` with a `findAll` method that returns a string.

# Now let's start in-depth NestJS

**Nestjs** is a framework for building efficient, scalable, and maintainable Node.js server-side applications.

**Nestjs** provides application architecture, configurations, and the layer of abstraction above common Node.js web frameworks with freedom of customization to create applications. The architecture is heavily inspired by **Angular**.

## Course contents

### NESTJS FUNDAMENTALS

- Controllers & Routing
- Providers
- Modules
- Guards
- Pipes
- Middlewares
- Interceptors
- Exception Filters
- Configuration

### DATABASE

- MongoDB & Mongoose
- TypeORM

### AUTH

- Cookies & Sessions
- Passport.js Integration
- RBAC
- CBA

### CACHING

- Application level caching
- Endpoints Caching
- Redis Store Integration

### FILES

- File Streaming
- File Upload - Multer
- File Upload - S3

### USEFUL PACKAGES

- HTTP Module - Axios
- CORS
- Compress
- Helmet
- CSRF & Rate Limiter

### LOGGING & DOCUMENTATION

- Application Logger
- Morgan
- Winston
- URL Versioning
- Header Versioning
- Media Type Versioning
- OpenAPI - Swagger

### TASK SCHEDULING

- Crons
- Events
- Queues

### MVC

- Template engines Integration
  - Handlebars, PUG, EJS

### SSE - SERVER SENT EVENTS

### WEB SOCKETS

### CORS

### MICROSERVICES

- NestJS Microservices Apps
- Redis Transport Integration
- Kafka Transport Integration

---

# NestJS Architecture

1. **Client**:

   - Makes requests to the NestJS application.
   - Example: Frontend application or another server.

2. **Controller**:

   - Receives requests from the client.
   - Routes requests based on specific paths (e.g., `/users`, `/profile`, `/premium`).
   - Calls the appropriate request handler.

3. **Request Handlers**:

   - Defined within the controller.
   - Handles specific routes such as:
     - `/wallet` - Handles wallet-related requests.
     - `/profile` - Handles profile-related requests.
     - `/premium` - Handles premium-related requests.

4. **Service**:

   - Contains the business logic.
   - Called by the controller to process the request and generate a response.

5. **Server**:
   - The entire NestJS application is deployed on a server.

[![](https://mermaid.ink/img/pako:eNqFkjtPwzAUhf-KdedWiGTzgITaATEwEDbMYOLbxsIv_EBCTf87TmOoEiXCg-V7zqejY8snaK1AoHD03HXkZc8MyWunJJpIttu7_hk_E4bYk5010Vul0Bfmb75wNymgDz0p_AM3Ilu3r2UmRaBkBN-WQ5y3B6lwHlMtxBR0NQi1THoeVC8GXdASNOs_pJEG_ZdscQmo_gPqKTAiIb2PD87gKaOPDbl3TsmWR2kNgxGaXuuqzRquGdWaUV-NSW804rffsMMGNHrNpcjf4zQoDGKHGhnQfBTcfwxNz5njKdrm27RAo0-4AW_TsQN64CrkKTnBI-4lz1fWRT3_ANzt08c?type=png)](https://mermaid.live/edit#pako:eNqFkjtPwzAUhf-KdedWiGTzgITaATEwEDbMYOLbxsIv_EBCTf87TmOoEiXCg-V7zqejY8snaK1AoHD03HXkZc8MyWunJJpIttu7_hk_E4bYk5010Vul0Bfmb75wNymgDz0p_AM3Ilu3r2UmRaBkBN-WQ5y3B6lwHlMtxBR0NQi1THoeVC8GXdASNOs_pJEG_ZdscQmo_gPqKTAiIb2PD87gKaOPDbl3TsmWR2kNgxGaXuuqzRquGdWaUV-NSW804rffsMMGNHrNpcjf4zQoDGKHGhnQfBTcfwxNz5njKdrm27RAo0-4AW_TsQN64CrkKTnBI-4lz1fWRT3_ANzt08c)
