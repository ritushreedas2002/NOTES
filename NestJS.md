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
