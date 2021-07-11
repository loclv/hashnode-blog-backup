## 🐱 NestJS - Node.js TypeScript Backend Framework lấy cảm hứng từ Angular 🅰️ - Có chắc đây là yêu 💜 từ cái nhìn đầu tiên về các nét cơ bản

## Vài điều cơ bản về [NestJS](https://nestjs.com/)

- Source code của `NestJS` được viết toàn bộ bằng `TypeScript`. Các tín đồ của `TypeScript` đã thấy phấn khích chưa ạ?? 😘

Theo như [github source repository](https://github.com/nestjs/nest) thì số lượng `star` là >= 38.5k (tại thời điểm 2021/07). Số lượng người follow trên [twitter - @nestframework](https://twitter.com/nestframework) là >= 17.8K. Framework được tạo ra từ năm 2017 bởi [@kammysliwiec](https://twitter.com/kammysliwiec).

- Sử dụng Dependency injection (DI), được truyền cảm hứng từ [Dependency injection in Angular](https://angular.io/guide/dependency-injection). Thông thường được sử dụng để trả về 1 thực thể (instance) đã được truyền vào (inject) đâu đó trong app rồi, từ đó tái sử dụng và dùng chung 1 service.

- support:
  - [GraphQL](https://graphql.org/)
  - WebSockets
  - Microservices
  - `Lazy-loading modules` cho phía backend, giảm thời gian load modules (khác hoàn toàn so với `Lazy-loading modules` của Angular đấy nhé 😄)
  - [OpenAPI - swagger](https://swagger.io/specification/)
  - [TypeORM](https://docs.nestjs.com/recipes/sql-typeorm)
  - [Prisma ORM](https://www.prisma.io/)

### 👷🏽 Controllers

`cats.controller.ts`:

```ts
import { Controller, Get } from '@nestjs/common';

@Controller('cats')
export class CatsController {
  @Get()
  findAll(): string {
    return 'This action returns all cats';
  }
}
```

Support:

- Route wildcards
- Status code
- Headers
- Redirection
- Route parameters
- Sub-Domain Routing
- Không đồng Bộ
- Request payloads
- ...

Routing: sử dung `@Controller()` decorator để định nghĩa. Với ví dụ trên là `@Controller('cats')`.

### Providers

Ý tưởng về phần `provider` là nó sẽ được `injected` dưới dạng 1 dependency áp dụng nguyên lý DI (Dependency injection) đã nói bên trên.

Các loại provider như: services, repositories, factories, helpers, ...

Ví dụ như `cats.service.ts`, dùng để lưu trữ và lấy ra data:

```ts
import { Injectable } from '@nestjs/common';
import { Cat } from './interfaces/cat.interface';

@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  create(cat: Cat) {
    this.cats.push(cat);
  }

  findAll(): Cat[] {
    return this.cats;
  }
}
```

`interfaces/cat.interface.ts`:

```ts
export interface Cat {
  name: string;
  age: number;
  breed: string;
}
```

Giờ là lúc inject vào `CatsController`:

```ts
import { Controller, Get, Post, Body } from '@nestjs/common';
import { CreateCatDto } from './dto/create-cat.dto';
import { CatsService } from './cats.service';
import { Cat } from './interfaces/cat.interface';

@Controller('cats')
export class CatsController {
  constructor(private catsService: CatsService) {}

  @Post()
  async create(@Body() createCatDto: CreateCatDto) {
    this.catsService.create(createCatDto);
  }

  @Get()
  async findAll(): Promise<Cat[]> {
    return this.catsService.findAll();
  }
}
```

### 🎬 Interceptors

Là chốt chặn giữa `clients` và `Route Handler`, mục đích là thêm thắt, quản lý response và request.

> An interceptor is a class annotated with the `@Injectable()` decorator.

Class `annotated` (hay chú thích) `@Injectable()` là khái niệm khá quen trong `Angular`.

### 💼 Database

Support SQL hoặc NoSQL database. Thông thường NestJS hỗ trợ kết nối với database đơn giản giống như [Express](https://expressjs.com/en/guide/database-integration.html) hay `Fastify`. Ngoài ra nó còn có các package hỗ trợ làm việc với các ORM ([Object–relational mapping](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping)]:

- [Sequelize](https://sequelize.org/)
- [Knex.js](https://knexjs.org/)
- [TypeORM](https://github.com/typeorm/typeorm)
- [Prisma](https://github.com/prisma/prisma)

## Tổng kết

Ngoài ra còn rất nhiều thứ vân vân và mây mây nữa trong [NestJS](https://nestjs.com/).

Để làm quen với framework này bạn nhất thiết phải nắm được khái niệm DI.

Điểm mạnh của `NestJS` so với các framework khác là:

- Sử dụng `TypeScript` có thể tái sử dụng để check kiểu cho API ở `TypeScript` phía Frontend, đặc biệt khi sử dụng thiết kế API - [OpenAPI - swagger](https://swagger.io/specification/). Điều này giúp an tâm đồng bộ kiểu trong việc call API, giảm thiểu lỗi về call không đúng cấu trúc API.
- Có thể tích hợp nhiều `ORM` khác nhau.

---

Photo by <a href="https://unsplash.com/@browaterboy?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Trison Thomas</a> on <a href="https://unsplash.com/@browaterboy?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
