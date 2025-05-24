# 🛒 E-commerce Backend API

A comprehensive e-commerce backend system built with Spring Boot, providing robust REST APIs for managing products, categories, users, orders, and authentication. This application serves as the backend for a full-featured e-commerce platform with JWT-based authentication and role-based access control.

## 🚀 Features

### 🔐 Authentication & Authorization

- **JWT Token Authentication** with cookie-based sessions
- **Role-based Access Control** (USER, ADMIN)
- **User Registration & Login** with password encryption
- **Secure Endpoints** with Spring Security

### 📦 Product Management

- Create, read, update, and delete products
- **Category-based Product Organization**
- **Product Search** by keyword and category
- **Pagination Support** for product listings
- **Image Upload** functionality for products

### 🛍️ Shopping Cart

- Add/remove items from cart
- **Persistent Cart** per user
- Cart item quantity management
- Cart total calculations

### 📋 Order Management

- **Complete Order Processing** workflow
- Order history tracking
- **Order Status Management**
- Integration with payment processing

### 👤 User Management

- User profile management
- **Address Management** for shipping
- User authentication and authorization

### 🏷️ Category Management

- Product categorization
- Category CRUD operations
- Category-based product filtering

## 🛠️ Technology Stack

- **Framework:** Spring Boot 3.2.5
- **Language:** Java 17
- **Database:** PostgreSQL (Production), H2 (Development/Testing)
- **Security:** Spring Security with JWT
- **ORM:** Spring Data JPA with Hibernate
- **Build Tool:** Maven
- **Additional Libraries:**
  - Lombok for reducing boilerplate code
  - ModelMapper for object mapping
  - Bean Validation for input validation

## 📋 Prerequisites

Before running this application, ensure you have:

- **Java 17** or higher installed
- **Maven 3.6+** for dependency management
- **PostgreSQL** database server (for production)
- **Git** for cloning the repository

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/NassimKhaldi/Ecommerce-Backend.git
cd Ecommerce-Backend
```

### 2. Database Configuration

#### PostgreSQL Setup (Production)

1. Create a PostgreSQL database named `ecommerce`
2. Update the database configuration in `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/ecommerce
spring.datasource.username=your_username
spring.datasource.password=your_password
```

#### H2 Database (Development/Testing)

To use H2 in-memory database for development, uncomment these lines in `application.properties`:

```properties
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:test
```

### 3. JWT Configuration

Update JWT settings in `application.properties`:

```properties
spring.app.jwtSecret=your_secret_key_here
spring.app.jwtExpirationMs=3000000
```

### 4. Build and Run

#### Using Maven Wrapper (Recommended)

```bash
# On Windows
./mvnw spring-boot:run

# On Unix/Linux/Mac
./mvnw spring-boot:run
```

#### Using Maven

```bash
mvn clean install
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

## 📚 API Documentation

### Base URL

```
http://localhost:8080/api
```

### 🔐 Authentication Endpoints

| Method | Endpoint        | Description              | Access        |
| ------ | --------------- | ------------------------ | ------------- |
| POST   | `/auth/signup`  | Register new user        | Public        |
| POST   | `/auth/signin`  | User login               | Public        |
| POST   | `/auth/signout` | User logout              | Authenticated |
| GET    | `/auth/user`    | Get current user details | Authenticated |

### 👤 User Management

| Method | Endpoint                | Description    | Access |
| ------ | ----------------------- | -------------- | ------ |
| GET    | `/admin/users`          | Get all users  | Admin  |
| GET    | `/admin/users/{userId}` | Get user by ID | Admin  |
| PUT    | `/admin/users/{userId}` | Update user    | Admin  |
| DELETE | `/admin/users/{userId}` | Delete user    | Admin  |

### 🏷️ Category Management

| Method | Endpoint                         | Description        | Access |
| ------ | -------------------------------- | ------------------ | ------ |
| GET    | `/public/categories`             | Get all categories | Public |
| POST   | `/admin/categories`              | Create category    | Admin  |
| PUT    | `/admin/categories/{categoryId}` | Update category    | Admin  |
| DELETE | `/admin/categories/{categoryId}` | Delete category    | Admin  |

### 📦 Product Management

| Method | Endpoint                                   | Description                  | Access |
| ------ | ------------------------------------------ | ---------------------------- | ------ |
| GET    | `/public/products`                         | Get all products (paginated) | Public |
| GET    | `/public/categories/{categoryId}/products` | Get products by category     | Public |
| GET    | `/public/products/keyword/{keyword}`       | Search products              | Public |
| POST   | `/admin/categories/{categoryId}/product`   | Create product               | Admin  |
| PUT    | `/admin/products/{productId}`              | Update product               | Admin  |
| DELETE | `/admin/products/{productId}`              | Delete product               | Admin  |

### 🛒 Cart Management

| Method | Endpoint                                          | Description           | Access |
| ------ | ------------------------------------------------- | --------------------- | ------ |
| GET    | `/carts`                                          | Get user's cart       | User   |
| POST   | `/carts/products/{productId}/quantity/{quantity}` | Add item to cart      | User   |
| PUT    | `/carts/products/{productId}/quantity/{quantity}` | Update cart item      | User   |
| DELETE | `/carts/{cartId}/product/{productId}`             | Remove item from cart | User   |

### 📋 Order Management

| Method | Endpoint                  | Description         | Access |
| ------ | ------------------------- | ------------------- | ------ |
| GET    | `/orders`                 | Get user's orders   | User   |
| POST   | `/orders`                 | Place new order     | User   |
| GET    | `/admin/orders`           | Get all orders      | Admin  |
| PUT    | `/admin/orders/{orderId}` | Update order status | Admin  |

### 🏠 Address Management

| Method | Endpoint                 | Description          | Access |
| ------ | ------------------------ | -------------------- | ------ |
| GET    | `/addresses`             | Get user's addresses | User   |
| POST   | `/addresses`             | Add new address      | User   |
| PUT    | `/addresses/{addressId}` | Update address       | User   |
| DELETE | `/addresses/{addressId}` | Delete address       | User   |

## 📝 Request/Response Examples

### User Registration

```json
POST /api/auth/signup
{
    "username": "johndoe",
    "email": "john@example.com",
    "password": "password123",
    "role": ["user"]
}
```

### User Login

```json
POST /api/auth/signin
{
    "username": "johndoe",
    "password": "password123"
}
```

### Create Product

```json
POST /api/admin/categories/1/product
{
    "productName": "Laptop",
    "description": "High-performance laptop",
    "price": 999.99,
    "quantity": 50,
    "discount": 10.0
}
```

### Add to Cart

```json
POST /api/carts/products/1/quantity/2
```

## 📂 Project Structure

```
src/
├── main/
│   ├── java/com/ecommerce/project/
│   │   ├── config/          # Application configuration
│   │   ├── controller/      # REST controllers
│   │   ├── model/          # Entity models
│   │   ├── payload/        # DTOs and response objects
│   │   ├── repositories/   # Data access layer
│   │   ├── security/       # Security configuration & JWT
│   │   ├── service/        # Business logic layer
│   │   └── util/           # Utility classes
│   └── resources/
│       └── application.properties
└── test/                   # Test classes
```

## 🔒 Security Features

- **JWT Authentication** with secure token generation
- **Password Encryption** using BCrypt
- **Role-based Authorization** (USER, ADMIN)
- **CORS Configuration** for cross-origin requests
- **Input Validation** with Bean Validation
- **SQL Injection Protection** through JPA

## 🚀 Deployment

### Development

```bash
mvn spring-boot:run
```

### Production

```bash
mvn clean package
java -jar target/sb-ecom-0.0.1-SNAPSHOT.jar
```

### Docker (Optional)

```dockerfile
FROM openjdk:17-jdk-slim
COPY target/sb-ecom-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

## 🔧 Configuration

### Environment Variables

Set these environment variables for production:

```bash
export DB_URL=jdbc:postgresql://localhost:5432/ecommerce
export DB_USERNAME=your_db_username
export DB_PASSWORD=your_db_password
export JWT_SECRET=your_jwt_secret_key
export JWT_EXPIRATION=86400000
```

### Application Properties

Key configuration options in `application.properties`:

```properties
# Server Configuration
server.port=8080

# Database Configuration
spring.datasource.url=${DB_URL:jdbc:postgresql://localhost:5432/ecommerce}
spring.datasource.username=${DB_USERNAME:postgres}
spring.datasource.password=${DB_PASSWORD:admin@123}

# JPA Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect

# JWT Configuration
spring.app.jwtSecret=${JWT_SECRET:mySecretKey123}
spring.app.jwtExpirationMs=${JWT_EXPIRATION:3000000}

# File Upload
project.image=images/
```

## 🧪 Testing

Run tests using Maven:

```bash
mvn test
```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **Nassim Khaldi** - _Initial work_ - [NassimKhaldi](https://github.com/NassimKhaldi)

## 🙏 Acknowledgments

- Spring Boot team for the excellent framework
- Spring Security for robust authentication mechanisms
- PostgreSQL for reliable database management
- All contributors who helped with this project

## 📞 Support

If you have any questions or issues, please open an issue on GitHub or contact the maintainers.

---

**Happy Coding! 🚀**
