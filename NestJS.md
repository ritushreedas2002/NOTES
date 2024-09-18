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

### Key Files and Directories

- **src/main.ts**: The entry point of the application. It bootstraps the main module.
- **src/app.module.ts**: The root module of the application. It imports other modules and provides the main configuration.
- **src/app.controller.ts**: The controller responsible for handling HTTP requests.
- **src/app.service.ts**: The service responsible for business logic.
- **test/app.e2e-spec.ts**: End-to-end tests for the application.
- **nest-cli.json**: Configuration file for the Nest CLI.
- **package.json**: Contains project dependencies and scripts.
- **tsconfig.json**: TypeScript configuration file.

### Modular Architecture

NestJS promotes a modular architecture, where each module encapsulates a specific feature or functionality. This approach enhances maintainability and scalability.

### Summary

- **Main Module**: Central configuration and module imports.
- **Controllers**: Handle incoming requests and route them.
- **Services**: Contain business logic and data handling.
- **Tests**: Ensure application functionality through automated tests.

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

#### Requests in NestJS are handled through 4 types of scopes:-
1. Global scope
2. Module scope
3. Controller scope
4. Request Handler / Route scope


## Superpowers of NestJS

### Middlewares

Middlewares are functions that are executed before the route handler. They can perform tasks such as logging, authentication, and request transformation.

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: Function) {
    console.log('Request...');
    next();
  }
}
```

### Guards

Guards are used to determine whether a request will be handled by the route handler. They are often used for authentication and authorization.

```typescript
import { Injectable, CanActivate, ExecutionContext } from '@nestjs/common';

@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest();
    return validateRequest(request);
  }
}
```

### Interceptors

Interceptors are used to transform the result returned by a function or to extend the behavior of a function. They can be used for logging, caching, and more.

```typescript
import { Injectable, NestInterceptor, ExecutionContext, CallHandler } from '@nestjs/common';
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';

@Injectable()
export class TransformInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(map(data => ({ data })));
  }
}
```

### Pipes

Pipes are used to transform and validate incoming data. They can be used to ensure that the data meets certain criteria before it is processed by the route handler.

```typescript
import { PipeTransform, Injectable, ArgumentMetadata, BadRequestException } from '@nestjs/common';

@Injectable()
export class ValidationPipe implements PipeTransform {
  transform(value: any, metadata: ArgumentMetadata) {
    if (!value) {
      throw new BadRequestException('Validation failed');
    }
    return value;
  }
}
```

## Client to Server (Request Flow):
[![](https://mermaid.ink/img/pako:eNp1UsFOAyEQ_RXCudX7HkxMq9WDiXE97mUKY5fIwsqC1rT9d4E1ATaUw2bmzWN4M29PlGmOtKEHA2NP3redIv5Mbj8DHb0fRykYWKEV2Whl8Wg7OrPC2UiBypL1-o68CM4l_oDBVE5YpOwcGJ6qMY2FZ9_YMBytNqmcgZH0KsasdcgiHFQZLSVmVxMWKOdbN6GZzuQNvxxO9gkUL-glHru2aL4Fy95LUbadndR7kKRl2kvL1lLOXuKLJSwmLQvlyKh4Tc_DMVz1Bj0KaYP8mytuVIkLOVVOVV-VWQquUmp-VYnX3KqSC7_iouYwfOmKDmgGENz_6aeAdNT2OHjLGh9yMJ_BvIvngbO6_VWMNtY4XFGj3aGnzQfIyWdu5GBxK8D7P_yjlz8BMvwv?type=png)](https://mermaid.live/edit#pako:eNp1UsFOAyEQ_RXCudX7HkxMq9WDiXE97mUKY5fIwsqC1rT9d4E1ATaUw2bmzWN4M29PlGmOtKEHA2NP3redIv5Mbj8DHb0fRykYWKEV2Whl8Wg7OrPC2UiBypL1-o68CM4l_oDBVE5YpOwcGJ6qMY2FZ9_YMBytNqmcgZH0KsasdcgiHFQZLSVmVxMWKOdbN6GZzuQNvxxO9gkUL-glHru2aL4Fy95LUbadndR7kKRl2kvL1lLOXuKLJSwmLQvlyKh4Tc_DMVz1Bj0KaYP8mytuVIkLOVVOVV-VWQquUmp-VYnX3KqSC7_iouYwfOmKDmgGENz_6aeAdNT2OHjLGh9yMJ_BvIvngbO6_VWMNtY4XFGj3aGnzQfIyWdu5GBxK8D7P_yjlz8BMvwv)

- Not only in Global scope, but in other scopes too, all 4 superpowers of NestJS can be applied.

## Server to Client (Response Flow):
[![](https://mermaid.ink/img/pako:eNqFkc9uwyAMxl8F-dzuARJp0rTuT6_rjlxc8Bo0AoyYqVPVdx8klUK3TPMBmY8f9oc5gfKaoIFDxNCJ100rncgxpP2kSLgLwRqFbLwT994xHVnCRJXYUfw0isR6fSte6CPRwM_otKXYztD1wciWUtHba24WR2abu0VFgX0NVepUyRpynIEZqew_Wb9HW1-q3f-oV3Uhp-uKD8dC5Bk8GsvF3k3ufHl7-w-2-NRF8s8BLtK_jY-mS1JWWEFPsUej8_-eiiKBO-pJQpNTjfG9jOKcOUzsd19OQcMx0QqiT4cOmje0Q96loJFpYzDPtL-o5292GrOA?type=png)](https://mermaid.live/edit#pako:eNqFkc9uwyAMxl8F-dzuARJp0rTuT6_rjlxc8Bo0AoyYqVPVdx8klUK3TPMBmY8f9oc5gfKaoIFDxNCJ100rncgxpP2kSLgLwRqFbLwT994xHVnCRJXYUfw0isR6fSte6CPRwM_otKXYztD1wciWUtHba24WR2abu0VFgX0NVepUyRpynIEZqew_Wb9HW1-q3f-oV3Uhp-uKD8dC5Bk8GsvF3k3ufHl7-w-2-NRF8s8BLtK_jY-mS1JWWEFPsUej8_-eiiKBO-pJQpNTjfG9jOKcOUzsd19OQcMx0QqiT4cOmje0Q96loJFpYzDPtL-o5292GrOA)

- Not only in Global scope, but in other scopes too, Interceptors can be applied.


## Module Structures in NestJS

In NestJS, modules are used to organize the application into cohesive blocks of functionality. There are two primary types of module structures: with controllers and without controllers.

### 1. Module with Controllers

A module with controllers typically includes one or more controllers that handle incoming HTTP requests and delegate tasks to the appropriate services. This structure is common in applications that expose RESTful APIs or handle web requests.

**Example Structure:**
- `AppModule`
  - `AppController`
  - `AppService`

**Key Components:**
- **Controller:** Defines routes and handles incoming requests.
- **Service:** Contains business logic and interacts with data sources.

### 2. Module without Controllers

A module without controllers is usually focused on providing services, utilities, or other functionalities that do not directly handle HTTP requests. These modules are often used for background tasks, data processing, or shared services across multiple modules.

**Example Structure:**
- `AuthModule`
  - `AuthService`
  - `JwtStrategy`

**Key Components:**
- **Service:** Contains business logic and interacts with data sources.
- **Provider:** Supplies additional functionalities or dependencies required by the service.

### Summary

- **Modules with Controllers:** Used for handling HTTP requests and routing.
- **Modules without Controllers:** Used for background tasks, utilities, or shared services.


## Bootstrapping a NestJS Application

The bootstrapping process in a NestJS application involves initializing the core components and starting the application. Here's a step-by-step guide:

### 1. Create the Main Module

The main module is the entry point of the application. It is typically named `AppModule` and is defined in `src/app.module.ts`.

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

### 2. Create the Main Application File

The main application file is responsible for bootstrapping the application. It is typically named `main.ts` and is located in the `src` directory.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

### 3. Run the Application

To start the application, run the following command in your terminal:

```bash
$ npm run start
```

This command will compile the TypeScript code and start the NestJS application on the specified port (default is 3000).

### Summary

- **Main Module:** Defines the root module of the application.
- **Main Application File:** Bootstraps the application and starts the server.
- **Run Command:** Compiles and starts the application.

By following these steps, you can successfully bootstrap a NestJS application and get it up and running.


## Common Scripts for a NestJS Application

NestJS applications often include a set of predefined scripts in the `package.json` file to streamline development, testing, and deployment processes. Here are some of the most common scripts:

### Development

- **Start Development Server**: Runs the application in development mode with hot-reloading.
  ```json
  "start:dev": "nest start --watch"
  ```

### Production

- **Start Production Server**: Runs the application in production mode.
  ```json
  "start:prod": "node dist/main"
  ```

### Build

- **Build Application**: Compiles the TypeScript code into JavaScript.
  ```json
  "build": "nest build"
  ```

### Testing

- **Run Unit Tests**: Executes unit tests using Jest.
  ```json
  "test": "jest"
  ```

- **Run End-to-End Tests**: Executes end-to-end tests.
  ```json
  "test:e2e": "jest --config ./test/jest-e2e.json"
  ```

- **Test Coverage**: Generates a test coverage report.
  ```json
  "test:cov": "jest --coverage"
  ```

### Linting

- **Lint Codebase**: Checks the code for linting errors using ESLint.
  ```json
  "lint": "eslint '{src,test}/**/*.ts'"
  ```

### Format

- **Format Codebase**: Formats the code using Prettier.
  ```json
  "format": "prettier --write 'src/**/*.ts' 'test/**/*.ts'"
  ```

## Understanding `module.ts` in NestJS

  The `module.ts` file in a NestJS application is crucial for organizing and managing the different parts of your application. Here's a breakdown of the key components and how they are registered inside it:

  ### Key Components

  1. **Imports**: Used to import other modules that this module depends on.
  2. **Controllers**: Define the routes and handle incoming requests.
  3. **Providers**: Include services and other providers that contain business logic.
  4. **Exports**: Make providers available to other modules.

  ### Example Structure

  ```typescript
  import { Module } from '@nestjs/common';
  import { SomeController } from './some.controller';
  import { SomeService } from './some.service';
  import { AnotherModule } from '../another/another.module';

  @Module({
    imports: [AnotherModule], // Importing other modules
    controllers: [SomeController], // Registering controllers
    providers: [SomeService], // Registering providers
    exports: [SomeService], // Exporting providers
  })
  export class SomeModule {}
  ```

  ### Detailed Breakdown

  - **Imports**: 
    - `AnotherModule`: This module depends on `AnotherModule` for additional functionality.
    
  - **Controllers**:
    - `SomeController`: Handles incoming HTTP requests and routes them to the appropriate service methods.
    
  - **Providers**:
    - `SomeService`: Contains the business logic and can be injected into controllers or other services.
    
  - **Exports**:
    - `SomeService`: Makes `SomeService` available to other modules that import `SomeModule`.

  ### Summary

  - **Imports**: Bring in other modules.
  - **Controllers**: Handle HTTP requests.
  - **Providers**: Contain business logic.
  - **Exports**: Share providers with other modules.


## Creating a Controller from Scratch

  In NestJS, controllers are responsible for handling incoming HTTP requests and returning responses. Here's a step-by-step guide to creating a controller from scratch:

  ### Step 1: Generate a Controller

  You can generate a new controller using the Nest CLI:

  ```bash
  $ nest generate controller users
  ```

  This command will create a new `UsersController` in the `src/users` directory.

  ### Step 2: Define Routes in the Controller

  Open the generated `users.controller.ts` file and define your routes:

  ```typescript
  import { Controller, Get, Post, Body } from '@nestjs/common';

  @Controller('users')
  export class UsersController {
    @Get()
    findAll(): string {
      return 'This action returns all users';
    }

    @Post()
    create(@Body() createUserDto: any): string {
      return 'This action adds a new user';
    }
  }
  ```

  ### Step 3: Register the Controller in a Module

  Ensure that the controller is registered in the corresponding module. Open `users.module.ts` and add the controller to the `controllers` array:

  ```typescript
  import { Module } from '@nestjs/common';
  import { UsersController } from './users.controller';

  @Module({
    controllers: [UsersController],
  })
  export class UsersModule {}
  ```

  ### How It Works

  - **Controller Decorator**: `@Controller('users')` defines the base route for all methods in the controller.
  - **Route Handlers**: Methods like `@Get()` and `@Post()` define specific routes and HTTP methods.
  - **Dependency Injection**: Controllers can inject services to handle business logic.


  ## Example of a Comprehensive Controller in NestJS

  In this section, we will create a more comprehensive example of a NestJS controller that includes various request handlers across different paths. This example will demonstrate how to handle different HTTP methods and routes within a single controller.

  ### Defining Routes in the Controller


  ```typescript
  import { Controller, Get, Post, Put, Delete, Param, Body, Query } from '@nestjs/common';

  @Controller('products')
  export class ProductsController {
    @Get()
    findAll(@Query('category') category: string): string {
      if (category) {
        return `This action returns all products in the ${category} category`;
      }
      return 'This action returns all products';
    }

    @Get(':id')
    findOne(@Param('id') id: string): string {
      return `This action returns the product with ID ${id}`;
    }

    @Post()
    create(@Body() createProductDto: any): string {
      return 'This action adds a new product';
    }

    @Put(':id')
    update(@Param('id') id: string, @Body() updateProductDto: any): string {
      return `This action updates the product with ID ${id}`;
    }

    @Delete(':id')
    remove(@Param('id') id: string): string {
      return `This action removes the product with ID ${id}`;
    }
  }
  ```

  
  ### Detailed Breakdown

  - **Base Route**: The base route for this controller is `/products`.
  - **GET /products**: Returns all products, optionally filtered by category.
  - **GET /products/:id**: Returns a single product by its ID.
  - **POST /products**: Creates a new product.
  - **PUT /products/:id**: Updates an existing product by its ID.
  - **DELETE /products/:id**: Deletes a product by its ID.

  ## Returning Responses from a NestJS Controller Request Handler

  In NestJS, a controller request handler can return responses in several different ways. Here are the common methods:

  1. **Return a Value Directly**:
    - Simply return a value from the handler method. NestJS will automatically serialize the response to JSON.
  ```typescript
    @Get()
    getHello(): string {
      return 'Hello World!';
    }
  ```

  2. **Return in JSON format**:
    - Simply return values in JSON format directly from the handler method.
  ```typescript
    @Get()
    getHello(): { name: string; age: string } {
      return {
        name: "Abcd",
        age: "15",
      };
    }
  ```

  3. **Return a Promise**:
    - If the handler method is asynchronous, you can return a Promise. NestJS will wait for the Promise to resolve and then serialize the response.

      #### 3.1. async/await with Promise<T>

      This is a common and clean way to handle async operations.

      ```typescript
      @Get('method1')
      async getHelloAsync1(): Promise<string> {
        return 'Hello World!';
      }
      ```

      #### 3.2. Returning a Promise directly

      You can return a Promise without using the `async` keyword. NestJS will handle the resolution.

      ```typescript
      @Get('method2')
      getHelloAsync2(): Promise {
        return Promise.resolve('Hello World!');
      }
      ```

      #### 3.3. async/await with a more complex Promise

      This shows how you might handle a more complex async operation, like one with a delay.

      ```typescript
      @Get('method3')
      async getHelloAsync3(): Promise {
        return new Promise(resolve => {
          setTimeout(() => resolve('Hello World!'), 1000);
        });
      }
      ```

      #### 3.4. Using a service method

      Often, you'll want to delegate the async operation to a service. This keeps your controllers lean and improves separation of concerns.

      ```typescript
      constructor(private readonly helloService: HelloService)  {}

      @Get('method5')
      getHelloAsync5(): Promise {
        return this.helloService.getHello();
      }
      ```

      ##### Choosing the Right Approach

      All of these methods are valid in NestJS. The choice between them depends on your specific use case:

      - Use `async/await` for most cases as it's clean and easy   to     read.
      - Return Promises directly if you're working with       Promise-based APIs.
      - Use Observables if you're dealing with streams of data  or      complex async operations.
      - Always consider moving complex logic to services, keeping controllers focused on request handling.

  4. **Return an Observable**:
    - For reactive programming, you can return an Observable. NestJS also supports RxJS Observables. NestJS will subscribe to the Observable and send the emitted value as the response.
  ```typescript
    import { Observable, of } from 'rxjs';
    import { delay } from 'rxjs/operators';

    @Get('method4')
    getHelloAsync4(): Observable {
      return of('Hello World!').pipe(delay(1000));
    }
  ```

  5. **Use Streams**:
    - For large data or file downloads, you can return a stream. NestJS will pipe the stream to the response.
  ```typescript
    @Get('file')
    getFile(@Res() res: Response): void {
      const file = createReadStream(join(__dirname, 'file.txt'));
      file.pipe(res);
    }
  ```

  6. **Use `@Res()` to Access the Response Object**:
    - By injecting the response object using `@Res()`, you can have full control over the response, including setting headers, status codes, and sending non-JSON responses.
  ```typescript
    @Get()
    getHello(@Res() res: Response): void {
      res.status(HttpStatus.OK).send('Hello World!');
    }
  ```

  These methods provide flexibility in handling different types of responses in a NestJS application.

### How to access the request object in a NestJS controller
---

   In NestJS, you can access the request object by using the `@Req()` decorator provided by the `@nestjs/common` package.
   * The `@Req()` decorator injects the request object into the handler method, allowing you to access various properties and methods of the request.
 
   * Example usage:
  ```typescript
      import { Controller, Get, Req } from '@nestjs/common';
      import { Request } from 'express';
   
      @Controller('example')
      export class ExampleController {
        @Get()
        getExample(@Req() request: Request): string {
          // Access request properties and methods here
          return `Request method: ${request.method}`;
        }
      }
   ```
   * In this example, the `getExample` method is a route handler that responds to GET requests.
   * The `@Req()` decorator injects the request object, which is then used to access the HTTP method of the request.
   * The request object is an instance of the `Request` interface from the `express` package, which provides various properties and methods to interact with the HTTP request.


  ## Setting HTTP Status Codes & Headers in NestJS

  In NestJS, you can easily set HTTP status codes and headers for your responses using decorators and the `@Res()` object. This allows you to customize the response behavior to meet your application's requirements.

  ### Setting HTTP Status Codes

  You can set HTTP status codes using the `@HttpCode()` decorator or by directly manipulating the response object with `@Res()`.

  #### Using `@HttpCode()` Decorator

  The `@HttpCode()` decorator sets the HTTP status code for the response.

  ```typescript
  import { Controller, Post, HttpCode } from '@nestjs/common';

  @Controller('example')
  export class ExampleController {
    @Post()
    @HttpCode(204)
    create(): string {
      return 'This action returns a 204 status code';
    }
  }
  ```

  #### Using `@Res()` Object

  You can also set the status code directly using the response object.

  ```typescript
  import { Controller, Get, Res } from '@nestjs/common';
  import { Response } from 'express';

  @Controller('example')
  export class ExampleController {
    @Get()
    getExample(@Res() res: Response): void {
      res.status(201).send('This action returns a 201 status code');
    }
  }
  ```

  ### Setting HTTP Headers

  You can set HTTP headers using the `@Header()` decorator or by directly manipulating the response object with `@Res()`.

  #### Using `@Header()` Decorator

  The `@Header()` decorator sets a specific header for the response.

  ```typescript
  import { Controller, Get, Header } from '@nestjs/common';

  @Controller('example')
  export class ExampleController {
    @Get()
    @Header('Cache-Control', 'none')
    getExample(): string {
      return 'This action sets a Cache-Control header';
    }
  }
  ```

  #### Using `@Res()` Object

  You can also set headers directly using the response object.

  ```typescript
  import { Controller, Get, Res } from '@nestjs/common';
  import { Response } from 'express';

  @Controller('example')
  export class ExampleController {
    @Get()
    getExample(@Res() res: Response): void {
      res.set('Cache-Control', 'none').send('This action sets a Cache-Control header');
    }
  }
  ```

  ### Combining Status Codes and Headers

  You can combine both status codes and headers in a single response using the `@Res()` object.

  ```typescript
  import { Controller, Get, Res } from '@nestjs/common';
  import { Response } from 'express';

  @Controller('example')
  export class ExampleController {
    @Get()
    getExample(@Res() res: Response): void {
      res.status(200)
         .set('Cache-Control', 'none')
         .send('This action sets both status code and header');
    }
  }
  ```

  ### Summary

  - **@HttpCode()**: Sets the HTTP status code for the response.
  - **@Header()**: Sets a specific header for the response.
  - **@Res()**: Provides full control over the response, allowing you to set status codes, headers, and send responses.

  ### Difference Between Using and Not Using `passthrough: true` in Response Object in NestJS
  ---

  In NestJS, the `@Res()` decorator can be used to inject the response object into a route handler. The `passthrough` option determines whether the response object should be passed through to the next middleware or handler.

  #### Using `passthrough: true`

  When `passthrough: true` is set, the response object is passed through to the next middleware or handler. This allows you to modify the response object without ending the response.

  **Example:**

  ```typescript
  import { Controller, Get, Res } from '@nestjs/common';
  import { Response } from 'express';

  @Controller('example')
  export class ExampleController {
    @Get('passthrough')
    getExample(@Res({ passthrough: true }) res: Response): string {
      res.set('X-Custom-Header', 'CustomValue');
      return 'Response with passthrough';
    }
  }
  ```

  In this example, the custom header is set, and the response is passed through to the next handler.

  #### Not Using `passthrough: true`

  When `passthrough: true` is not set, the response object is not passed through, and you have full control over the response. You must manually send the response using methods like `res.send()`.

  **Example:**

  ```typescript
  import { Controller, Get, Res } from '@nestjs/common';
  import { Response } from 'express';

  @Controller('example')
  export class ExampleController {
    @Get('no-passthrough')
    getExample(@Res() res: Response): void {
      res.set('X-Custom-Header', 'CustomValue');
      res.send('Response without passthrough');
    }
  }
  ```

  In this example, the custom header is set, and the response is sent immediately.

  ### Summary

  - **With `passthrough: true`**: The response object is passed through to the next middleware or handler, allowing further modifications.
  - **Without `passthrough: true`**: You have full control over the response and must manually send it.

### The order of Response and Request object does not matter while injecting in a NestJS controller, unlike ExpressJS where order is important.


## Default HTTP Status Codes in NestJS

  NestJS provides a comprehensive set of HTTP status codes through the `HttpStatus` module. These status codes are based on the standard HTTP status codes defined by the IETF. Below is a list of the default HTTP status codes available in NestJS:

  ### Informational Responses (100-199)

  - **100 CONTINUE**: The server has received the request headers and the client should proceed to send the request body.
  - **101 SWITCHING_PROTOCOLS**: The requester has asked the server to switch protocols and the server has agreed to do so.
  - **102 PROCESSING**: The server has received and is processing the request, but no response is available yet.

  ### Successful Responses (200-299)

  - **200 OK**: The request has succeeded.
  - **201 CREATED**: The request has been fulfilled and has resulted in one or more new resources being created.
  - **202 ACCEPTED**: The request has been accepted for processing, but the processing has not been completed.
  - **203 NON_AUTHORITATIVE_INFORMATION**: The server is a transforming proxy that received a 200 OK from its origin, but is returning a modified version of the origin's response.
  - **204 NO_CONTENT**: The server successfully processed the request, and is not returning any content.
  - **205 RESET_CONTENT**: The server successfully processed the request, asks that the requester reset its document view, and is not returning any content.
  - **206 PARTIAL_CONTENT**: The server is delivering only part of the resource due to a range header sent by the client.
  - **207 MULTI_STATUS**: The message body that follows is an XML message and can contain a number of separate response codes.
  - **208 ALREADY_REPORTED**: The members of a DAV binding have already been enumerated in a previous reply to this request, and are not being included again.

  ### Redirection Messages (300-399)

  - **300 MULTIPLE_CHOICES**: Indicates multiple options for the resource from which the client may choose.
  - **301 MOVED_PERMANENTLY**: This and all future requests should be directed to the given URI.
  - **302 FOUND**: Tells the client to look at (browse to) another URL.
  - **303 SEE_OTHER**: The response to the request can be found under another URI using a GET method.
  - **304 NOT_MODIFIED**: Indicates that the resource has not been modified since the version specified by the request headers.
  - **305 USE_PROXY**: The requested resource is available only through a proxy, the address for which is provided in the response.
  - **307 TEMPORARY_REDIRECT**: In this case, the request should be repeated with another URI; however, future requests should still use the original URI.
  - **308 PERMANENT_REDIRECT**: The request and all future requests should be repeated using another URI.

  ### Client Error Responses (400-499)

  - **400 BAD_REQUEST**: The server cannot or will not process the request due to an apparent client error.
  - **401 UNAUTHORIZED**: Authentication is required and has failed or has not yet been provided.
  - **402 PAYMENT_REQUIRED**: Reserved for future use.
  - **403 FORBIDDEN**: The request was valid, but the server is refusing action.
  - **404 NOT_FOUND**: The requested resource could not be found but may be available in the future.
  - **405 METHOD_NOT_ALLOWED**: A request method is not supported for the requested resource.
  - **406 NOT_ACCEPTABLE**: The requested resource is capable of generating only content not acceptable according to the Accept headers sent in the request.
  - **407 PROXY_AUTHENTICATION_REQUIRED**: The client must first authenticate itself with the proxy.
  - **408 REQUEST_TIMEOUT**: The server timed out waiting for the request.
  - **409 CONFLICT**: Indicates that the request could not be processed because of conflict in the request, such as an edit conflict between multiple simultaneous updates.
  - **410 GONE**: Indicates that the resource requested is no longer available and will not be available again.
  - **411 LENGTH_REQUIRED**: The request did not specify the length of its content, which is required by the requested resource.
  - **412 PRECONDITION_FAILED**: The server does not meet one of the preconditions that the requester put on the request.
  - **413 PAYLOAD_TOO_LARGE**: The request is larger than the server is willing or able to process.
  - **414 URI_TOO_LONG**: The URI provided was too long for the server to process.
  - **415 UNSUPPORTED_MEDIA_TYPE**: The request entity has a media type which the server or resource does not support.
  - **416 RANGE_NOT_SATISFIABLE**: The client has asked for a portion of the file (byte serving), but the server cannot supply that portion.
  - **417 EXPECTATION_FAILED**: The server cannot meet the requirements of the Expect request-header field.
  - **418 I_AM_A_TEAPOT**: This code was defined in 1998 as one of the traditional IETF April Fools' jokes.
  - **421 MISDIRECTED_REQUEST**: The request was directed at a server that is not able to produce a response.
  - **422 UNPROCESSABLE_ENTITY**: The request was well-formed but was unable to be followed due to semantic errors.
  - **423 LOCKED**: The resource that is being accessed is locked.
  - **424 FAILED_DEPENDENCY**: The request failed due to failure of a previous request.
  - **425 TOO_EARLY**: Indicates that the server is unwilling to risk processing a request that might be replayed.
  - **426 UPGRADE_REQUIRED**: The client should switch to a different protocol.
  - **428 PRECONDITION_REQUIRED**: The origin server requires the request to be conditional.
  - **429 TOO_MANY_REQUESTS**: The user has sent too many requests in a given amount of time ("rate limiting").
  - **431 REQUEST_HEADER_FIELDS_TOO_LARGE**: The server is unwilling to process the request because its header fields are too large.
  - **451 UNAVAILABLE_FOR_LEGAL_REASONS**: The user-agent requested a resource that cannot legally be provided, such as a web page censored by a government.

  ### Server Error Responses (500-599)

  - **500 INTERNAL_SERVER_ERROR**: A generic error message, given when an unexpected condition was encountered and no more specific message is suitable.
  - **501 NOT_IMPLEMENTED**: The server either does not recognize the request method, or it lacks the ability to fulfill the request.
  - **502 BAD_GATEWAY**: The server was acting as a gateway or proxy and received an invalid response from the upstream server.
  - **503 SERVICE_UNAVAILABLE**: The server cannot handle the request (because it is overloaded or down for maintenance).
  - **504 GATEWAY_TIMEOUT**: The server was acting as a gateway or proxy and did not receive a timely response from the upstream server.
  - **505 HTTP_VERSION_NOT_SUPPORTED**: The server does not support the HTTP protocol version used in the request.
  - **506 VARIANT_ALSO_NEGOTIATES**: Transparent content negotiation for the request results in a circular reference.
  - **507 INSUFFICIENT_STORAGE**: The server is unable to store the representation needed to complete the request.
  - **508 LOOP_DETECTED**: The server detected an infinite loop while processing a request.
  - **510 NOT_EXTENDED**: Further extensions to the request are required for the server to fulfill it.
  - **511 NETWORK_AUTHENTICATION_REQUIRED**: The client needs to authenticate to gain network access.

  ### Usage Example

  To use these status codes in your NestJS application, you can import the `HttpStatus` module and use the constants provided:

  ```typescript
  import { HttpStatus, Controller, Get, Res } from '@nestjs/common';
  import { Response } from 'express';

  @Controller('example')
  export class ExampleController {
    @Get()
    getExample(@Res() res: Response): void {
      res.status(HttpStatus.OK).send('This action returns a 200 status code');
    }
  }
  ```

  This example demonstrates how to set the HTTP status code to `200 OK` using the `HttpStatus` module.

  ## Redirection of Paths in a NestJS Controller

  In NestJS, you can perform redirection of paths using the `@Res()` decorator to access the response object and then use the `redirect()` method. This allows you to redirect incoming requests to different URLs.

  ### Example of Redirection

  Here's an example of how to perform a redirection in a NestJS controller:

  ```typescript
  import { Controller, Get, Res } from '@nestjs/common';
  import { Response } from 'express';

  @Controller('redirect')
  export class RedirectController {
    @Get()
    redirectTo(@Res() res: Response): void {
      res.redirect('https://example.com');
    }
  }
  ```

  In this example, when a GET request is made to the `/redirect` route, the server will respond with a redirection to `https://example.com`.

  ### Conditional Redirection

  You can also perform conditional redirection based on certain conditions:

  ```typescript
  import { Controller, Get, Query, Res } from '@nestjs/common';
  import { Response } from 'express';

  @Controller('conditional-redirect')
  export class ConditionalRedirectController {
    @Get()
    conditionalRedirect(@Query('to') to: string, @Res() res: Response): void {
      if (to === 'google') {
        res.redirect('https://google.com');
      } else {
        res.redirect('https://example.com');
      }
    }
  }
  ```

  In this example, the redirection URL is determined based on the query parameter `to`. If `to` is `google`, the request is redirected to `https://google.com`; otherwise, it is redirected to `https://example.com`.

  ### Using the Redirect Module

  NestJS also provides a `Redirect` module that can be used for redirection. This module simplifies the redirection process by using the `@Redirect()` decorator.

  #### Example of Using the Redirect Module

  Here's an example of how to use the `Redirect` module in a NestJS controller:

  ```typescript
  import { Controller, Get, Redirect } from '@nestjs/common';

  @Controller('redirect')
  export class RedirectController {
    @Get()
    @Redirect('https://example.com')
    redirectTo(): void {
      // This method can be empty as the redirection is handled by the @Redirect decorator
    }
  }
  ```

  In this example, the `@Redirect()` decorator is used to specify the redirection URL. When a GET request is made to the `/redirect` route, the server will respond with a redirection to `https://example.com`.

  ### Conditional Redirection with the Redirect Module

  You can also perform conditional redirection using the `@Redirect()` decorator:

  ```typescript
  import { Controller, Get, Query, Redirect } from '@nestjs/common';

  @Controller('conditional-redirect')
  export class ConditionalRedirectController {
    @Get()
    @Redirect()
    conditionalRedirect(@Query('to') to: string): { url: string } {
      if (to === 'google') {
        return { 
          url: 'https://google.com',
          statusCode: 302, 
        };
      } else {
        return { 
          url: 'https://example.com',
          statusCode: 302,
        };
      }
    }
  }
  ```

  In this example, the redirection URL is determined based on the query parameter `to`. The `@Redirect()` decorator is used without a URL, and the method returns an object with the `url` property to specify the redirection URL.

  ### Summary

  - **Basic Redirection**: Use `res.redirect()` to redirect to a specific URL.
  - **Conditional Redirection**: Use logic to determine the redirection URL based on request parameters or other conditions.
  - **Using the Redirect Module**: Use the `@Redirect()` decorator for simpler redirection.

  By using these techniques, you can effectively manage redirections in your NestJS application.

## Route Parameters in NestJS

  Route parameters are dynamic segments of a URL that can be used to capture values at specific positions in the URL path. In NestJS, route parameters are defined using the colon (`:`) syntax in the route path and can be accessed within the controller methods using the `@Param()` decorator.

  ### Defining Route Parameters

  To define a route parameter, include a colon followed by the parameter name in the route path. For example, to define a route parameter named `id`:

  ```typescript
  import { Controller, Get, Param } from '@nestjs/common';

  @Controller('users')
  export class UsersController {
    @Get(':id')
    findOne(@Param('id') id: string): string {
      return `This action returns a user with ID ${id}`;
    }
  }
  ```

  In this example, the `findOne` method handles GET requests to the `/users/:id` route. The `@Param('id')` decorator extracts the `id` parameter from the URL and makes it available as a method argument.

  ### Multiple Route Parameters

  You can define multiple route parameters in a single route. For example, to define `userId` and `postId` parameters:

  ```typescript
  import { Controller, Get, Param } from '@nestjs/common';

  @Controller('users')
  export class UsersController {
    @Get(':userId/posts/:postId')
    findPost(@Param('userId') userId: string, @Param('postId') postId: string): string {
      return `This action returns post ${postId} for user ${userId}`;
    }
  }
  ```

  In this example, the `findPost` method handles GET requests to the `/users/:userId/posts/:postId` route. The `@Param()` decorator is used to extract both `userId` and `postId` parameters from the URL.

  ### Accessing All Route Parameters

  If you need to access all route parameters as an object, you can use the `@Param()` decorator without specifying a parameter name:

  ```typescript
  import { Controller, Get, Param } from '@nestjs/common';

  @Controller('users')
  export class UsersController {
    @Get(':userId/posts/:postId')
    findPost(@Param() params: { userId: string; postId: string }): string {
      return `This action returns post ${params.postId} for user ${params.userId}`;
    }
  }
  ```

  In this example, the `params` object contains all route parameters, allowing you to access `userId` and `postId` as properties of the object.

  ### Summary

  - **Defining Route Parameters**: Use the colon (`:`) syntax in the route path to define route parameters.
  - **Accessing Route Parameters**: Use the `@Param()` decorator to access route parameters within controller methods.
  - **Multiple Route Parameters**: Define and access multiple route parameters in a single route.
  - **Accessing All Parameters**: Use the `@Param()` decorator without a parameter name to access all route parameters as an object.


  ## Query Parameters in NestJS

  Query parameters are key-value pairs that appear after the question mark (`?`) in a URL. They are used to pass additional information to the server. In NestJS, you can easily access query parameters in your controller methods using the `@Query()` decorator.

  ### Defining Query Parameters

  To define query parameters, you simply append them to the URL after a question mark. For example, to define a query parameter named `page`:

  ```typescript
  import { Controller, Get, Query } from '@nestjs/common';

  @Controller('items')
  export class ItemsController {
    @Get()
    findAll(@Query('page') page: number): string {
      return `This action returns items on page ${page}`;
    }
  }
  ```

  In this example, the `findAll` method handles GET requests to the `/items` route. The `@Query('page')` decorator extracts the `page` query parameter from the URL and makes it available as a method argument.

  ### Multiple Query Parameters

  You can define multiple query parameters in a single route. For example, to define `page` and `limit` parameters:

  ```typescript
  import { Controller, Get, Query } from '@nestjs/common';

  @Controller('items')
  export class ItemsController {
    @Get()
    findAll(@Query('page') page: number, @Query('limit') limit: number): string {
      return `This action returns ${limit} items on page ${page}`;
    }
  }
  ```

  In this example, the `findAll` method handles GET requests to the `/items` route. The `@Query()` decorator is used to extract both `page` and `limit` query parameters from the URL.

  ### Accessing All Query Parameters

  If you need to access all query parameters as an object, you can use the `@Query()` decorator without specifying a parameter name:

  ```typescript
  import { Controller, Get, Query } from '@nestjs/common';

  @Controller('items')
  export class ItemsController {
    @Get()
    findAll(@Query() query: { page: number; limit: number }): string {
      return `This action returns ${query.limit} items on page ${query.page}`;
    }
  }
  ```

  In this example, the `query` object contains all query parameters, allowing you to access `page` and `limit` as properties of the object.

  ### Summary

  - **Defining Query Parameters**: Append key-value pairs to the URL after a question mark (`?`).
  - **Accessing Query Parameters**: Use the `@Query()` decorator to access query parameters within controller methods.
  - **Multiple Query Parameters**: Define and access multiple query parameters in a single route.
  - **Accessing All Parameters**: Use the `@Query()` decorator without a parameter name to access all query parameters as an object.

  ## Request Headers in NestJS

  Request headers are key-value pairs sent by the client to the server as part of an HTTP request. They provide additional information about the request, such as the content type, authorization tokens, user agent, and more. In NestJS, you can access and utilize request headers in your controllers using the `@Headers()` decorator.

  ### Accessing Request Headers

  To access request headers in a NestJS controller, use the `@Headers()` decorator. This decorator can be used to inject all headers as an object or to extract a specific header by name.

  #### Accessing All Headers

  You can access all request headers as an object using the `@Headers()` decorator without specifying a header name:

  ```typescript
  import { Controller, Get, Headers } from '@nestjs/common';

  @Controller('headers')
  export class HeadersController {
    @Get()
    getAllHeaders(@Headers() headers: Record<string, string>): string {
      return `Request headers: ${JSON.stringify(headers)}`;
    }
  }
  ```

  In this example, the `getAllHeaders` method handles GET requests to the `/headers` route. The `@Headers()` decorator injects all request headers as an object, which can then be used within the method.

  #### Accessing a Specific Header

  You can also access a specific header by name using the `@Headers()` decorator with the header name as an argument:

  ```typescript
  import { Controller, Get, Headers } from '@nestjs/common';

  @Controller('headers')
  export class HeadersController {
    @Get()
    getUserAgent(@Headers('user-agent') userAgent: string): string {
      return `User-Agent: ${userAgent}`;
    }
  }
  ```

  In this example, the `getUserAgent` method handles GET requests to the `/headers` route. The `@Headers('user-agent')` decorator extracts the `user-agent` header from the request and makes it available as a method argument.

  ### Summary

  - **Accessing All Headers**: Use the `@Headers()` decorator without arguments to access all request headers as an object.
  - **Accessing a Specific Header**: Use the `@Headers()` decorator with the header name as an argument to access a specific header.

  By utilizing request headers in your NestJS controllers, you can handle additional request information and customize responses based on header values.

 ## Accessing Request Body in NestJS Controllers

  In NestJS, you can access the body of a request sent from the client side using the `@Body()` decorator. This is particularly useful for handling data submissions in JSON and URL-encoded formats.

  ### Accessing JSON Data

  When a client sends data in JSON format, you can access it directly in your controller method using the `@Body()` decorator.

  #### Example

  ```typescript
  import { Controller, Post, Body } from '@nestjs/common';

  @Controller('data')
  export class DataController {
    @Post('json')
    handleJson(@Body() body: any): string {
      return `Received JSON data: ${JSON.stringify(body)}`;
    }
  }
  ```

  In this example, the `handleJson` method handles POST requests to the `/data/json` route. The `@Body()` decorator injects the entire request body, which is expected to be in JSON format.

  ### Accessing URL-encoded Data

  When a client sends data in URL-encoded format, you can also access it using the `@Body()` decorator.

  #### Example

  ```typescript
  import { Controller, Post, Body } from '@nestjs/common';

  @Controller('data')
  export class DataController {
    @Post('urlencoded')
    handleUrlencoded(@Body() body: any): string {
      return `Received URL-encoded data: ${JSON.stringify(body)}`;
    }
  }
  ```

  In this example, the `handleUrlencoded` method handles POST requests to the `/data/urlencoded` route. The `@Body()` decorator injects the entire request body, which is expected to be in URL-encoded format.

  ### Summary

  - **Accessing JSON Data**: Use the `@Body()` decorator to access JSON data sent in the request body.
  - **Accessing URL-encoded Data**: Use the `@Body()` decorator to access URL-encoded data sent in the request body.

  By using the `@Body()` decorator, you can easily handle data submissions in both JSON and URL-encoded formats in your NestJS controllers.

## Simple CRUD Operations on User Entity

  In this section, we will create a simple CRUD (Create, Read, Update, Delete) operation on a `User` entity using NestJS. We will use `UserDto` for type definitions and utilize `@Body()` and `@Param()` decorators in our controllers.

  #### UserDto

  First, let's define the `UserDto` class which will be used for type definitions.

  ```typescript
  export class UserDto {
    id: number;
    name: string;
    email: string;
  }
  ```

  #### UserController

  Next, we will create the `UserController` with CRUD operations.

  ```typescript
  import { Controller, Get, Post, Put, Delete, Body, Param } from '@nestjs/common';
  import { UserDto } from './user.dto';

  @Controller('users')
  export class UserController {
    private users: UserDto[] = [];

    @Post()
    createUser(@Body() userDto: UserDto): string {
      this.users.push(userDto);
      return `User ${userDto.name} created successfully`;
    }

    @Get(':id')
    getUser(@Param('id') id: number): UserDto {
      return this.users.find(user => user.id === id);
    }

    @Get()
    getAllUsers(): UserDto[] {
      return this.users;
    }

    @Put(':id')
    updateUser(@Param('id') id: number, @Body() userDto: UserDto): string {
      const userIndex = this.users.findIndex(user => user.id === id);
      if (userIndex >= 0) {
        this.users[userIndex] = userDto;
        return `User ${userDto.name} updated successfully`;
      }
      return `User with id ${id} not found`;
    }

    @Delete(':id')
    deleteUser(@Param('id') id: number): string {
      const userIndex = this.users.findIndex(user => user.id === id);
      if (userIndex >= 0) {
        this.users.splice(userIndex, 1);
        return `User with id ${id} deleted successfully`;
      }
      return `User with id ${id} not found`;
    }
  }
  ```

  ### Summary

  - **Create User**: Uses `@Post()` and `@Body()` to create a new user.
  - **Get User by ID**: Uses `@Get(':id')` and `@Param('id')` to retrieve a user by ID.
  - **Get All Users**: Uses `@Get()` to retrieve all users.
  - **Update User**: Uses `@Put(':id')`, `@Param('id')`, and `@Body()` to update a user by ID.
  - **Delete User**: Uses `@Delete(':id')` and `@Param('id')` to delete a user by ID.

  This example demonstrates how to perform basic CRUD operations on a `User` entity in a NestJS application.
