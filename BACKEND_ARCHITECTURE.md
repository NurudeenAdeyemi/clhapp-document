# Backend Architecture: .NET 9 Web API

This document outlines the backend architecture for our .NET 9 Web API. The architecture is designed to be robust, scalable, and maintainable, following best practices in modern software development.

## Core Principles

*   **Domain-Driven Design (DDD):** The architecture is centered around the business domain, with a rich domain model that encapsulates business logic and rules.
*   **Test-Driven Design (TDD):** Development will follow a TDD approach, where tests are written before the implementation to ensure correctness and guide the design.
*   **Vertical Slicing:** The application will be divided into vertical slices, where each slice represents a specific feature or use case. This approach promotes high cohesion and low coupling between features.

## Architecture: Onion Architecture

We will use the Onion Architecture, which places the domain model at the center and builds layers of the application around it. This ensures that the core business logic is independent of external concerns like UI, databases, or third-party services.

The layers of the Onion Architecture are:

1.  **Domain Layer:** Contains the domain entities, value objects, aggregates, and domain events. This is the heart of the application and has no dependencies on other layers.
2.  **Application Layer:** Contains the application logic, including commands, queries, and services. This layer orchestrates the domain objects to perform business operations. It depends on the Domain Layer but not on the outer layers.
3.  **Infrastructure Layer:** Contains the implementation of external concerns, such as databases, file systems, and third-party APIs. This layer depends on the Application Layer and provides implementations for the interfaces defined in the Application Layer.
4.  **Presentation Layer:** The entry point of the application, which for a Web API is the API controllers. This layer is responsible for handling HTTP requests and responses and depends on the Application Layer.

## Technology Stack

*   **ORM:** Entity Framework Core
*   **Database:** PostgreSQL

## Patterns

### Repository Pattern

The Repository Pattern will be used to abstract the data access logic. Each aggregate root will have its own repository, which will provide methods for retrieving and persisting the aggregate. We will **not** use a generic repository, as this can lead to a leaky abstraction and a violation of the Interface Segregation Principle.

### Command Query Responsibility Segregation (CQRS)

CQRS will be used to separate the read and write operations. This allows us to optimize each side independently.

*   **Commands:** Represent an intent to change the state of the system. They are handled by command handlers that contain the business logic for the operation.
*   **Queries:** Represent a request for data. They are handled by query handlers that retrieve data from the data store and return it as a DTO (Data Transfer Object).

## RESTful API Design

The API will be designed following RESTful principles.

*   **Resources:** The API will be organized around resources, which are the main entities of the system.
*   **HTTP Verbs:** We will use the standard HTTP verbs (GET, POST, PUT, DELETE) to perform operations on the resources.
*   **Status Codes:** We will use the standard HTTP status codes to indicate the outcome of an API call.
*   **Data Transfer Objects (DTOs):** We will use DTOs to transfer data between the client and the server. This ensures that the domain entities are not exposed to the presentation layer, which is a key principle of the Onion Architecture.

## Validation: FluentValidation

FluentValidation will be used for input validation. Validators will be created for each command to ensure that the input is valid before it is processed. FluentValidation provides a clean and expressive way to define validation rules.

## API Documentation: Swagger UI

Swagger UI will be configured to provide interactive documentation for the API. This will make it easy for developers to understand and test the API endpoints.

## Testing

### Unit Testing

Unit tests will be written to test individual components in isolation. This includes testing:

*   Domain entities and their business logic.
*   Command and query handlers.
*   Validators.

We will use a mocking framework like Moq to mock dependencies.

### Integration Testing

Integration tests will be written to test the interaction between different components of the application. This includes testing:

*   The entire flow of a command or query, from the controller to the database.
*   The interaction with external services.

We will use a test server to host the application in-memory and a test database to ensure that the tests are isolated and repeatable.

## Project Structure

The solution will be structured as follows:

```
/src
  /Domain
    /Entities
    /ValueObjects
    /Aggregates
    /Events
  /Application
    /Features
      /{FeatureName}
        /Commands
        /Queries
        /Validators
        /Dtos
    /Interfaces
  /Infrastructure
    /Persistence
      /Repositories
      /Migrations
    /Services
  /Api
    /Controllers
    /Extensions
    /Middleware
/tests
  /Domain.UnitTests
  /Application.UnitTests
  /Api.IntegrationTests
```

## Example: Creating a New Product

This example illustrates how the different components work together to create a new product.

### 1. Controller

```csharp
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    private readonly IMediator _mediator;

    public ProductsController(IMediator mediator)
    {
        _mediator = mediator;
    }

    [HttpPost]
    public async Task<IActionResult> CreateProduct([FromBody] CreateProductCommand command)
    {
        var productId = await _mediator.Send(command);
        return CreatedAtAction(nameof(GetProduct), new { id = productId }, null);
    }

    [HttpGet("{id}")]
    public async Task<IActionResult> GetProduct(Guid id)
    {
        var product = await _mediator.Send(new GetProductQuery { Id = id });
        return Ok(product);
    }
}
```

### 2. Command

```csharp
public class CreateProductCommand : IRequest<Guid>
{
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

### 3. Query

```csharp
public class GetProductQuery : IRequest<ProductDto>
{
    public Guid Id { get; set; }
}
```

### 4. DTO

```csharp
public class ProductDto
{
    public Guid Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

### 5. Validator

```csharp
public class CreateProductCommandValidator : AbstractValidator<CreateProductCommand>
{
    public CreateProductCommandValidator()
    {
        RuleFor(x => x.Name).NotEmpty().MaximumLength(100);
        RuleFor(x => x.Price).GreaterThan(0);
    }
}
```

### 6. Command Handler

```csharp
public class CreateProductCommandHandler : IRequestHandler<CreateProductCommand, Guid>
{
    private readonly IProductRepository _productRepository;

    public CreateProductCommandHandler(IProductRepository productRepository)
    {
        _productRepository = productRepository;
    }

    public async Task<Guid> Handle(CreateProductCommand request, CancellationToken cancellationToken)
    {
        var product = new Product(request.Name, request.Price);
        await _productRepository.AddAsync(product);
        return product.Id;
    }
}
```

### 7. Query Handler

```csharp
public class GetProductQueryHandler : IRequestHandler<GetProductQuery, ProductDto>
{
    private readonly IProductRepository _productRepository;

    public GetProductQueryHandler(IProductRepository productRepository)
    {
        _productRepository = productRepository;
    }

    public async Task<ProductDto> Handle(GetProductQuery request, CancellationToken cancellationToken)
    {
        var product = await _productRepository.GetByIdAsync(request.Id);
        return new ProductDto
        {
            Id = product.Id,
            Name = product.Name,
            Price = product.Price
        };
    }
}
```

### 8. Repository

```csharp
public interface IProductRepository
{
    Task<Product> GetByIdAsync(Guid id);
    Task AddAsync(Product product);
}

public class ProductRepository : IProductRepository
{
    private readonly ApplicationDbContext _context;

    public ProductRepository(ApplicationDbContext context)
    {
        _context = context;
    }

    public async Task<Product> GetByIdAsync(Guid id)
    {
        return await _context.Products.FindAsync(id);
    }

    public async Task AddAsync(Product product)
    {
        await _context.Products.AddAsync(product);
        await _context.SaveChangesAsync();
    }
}
```

### 9. Unit Test

```csharp
public class CreateProductCommandHandlerTests
{
    [Fact]
    public async Task Handle_Should_Create_Product_And_Return_Id()
    {
        // Arrange
        var productRepositoryMock = new Mock<IProductRepository>();
        var handler = new CreateProductCommandHandler(productRepositoryMock.Object);
        var command = new CreateProductCommand { Name = "Test Product", Price = 10.0m };

        // Act
        var productId = await handler.Handle(command, CancellationToken.None);

        // Assert
        productRepositoryMock.Verify(x => x.AddAsync(It.Is<Product>(p => p.Name == command.Name && p.Price == command.Price)), Times.Once);
        Assert.NotEqual(Guid.Empty, productId);
    }
}
```

### 10. Integration Test

```csharp
public class ProductsControllerTests : IClassFixture<CustomWebApplicationFactory<Startup>>
{
    private readonly HttpClient _client;

    public ProductsControllerTests(CustomWebApplicationFactory<Startup> factory)
    {
        _client = factory.CreateClient();
    }

    [Fact]
    public async Task CreateProduct_Should_Return_Created()
    {
        // Arrange
        var command = new CreateProductCommand { Name = "Test Product", Price = 10.0m };
        var content = new StringContent(JsonSerializer.Serialize(command), Encoding.UTF8, "application/json");

        // Act
        var response = await _client.PostAsync("/api/products", content);

        // Assert
        response.EnsureSuccessStatusCode();
        Assert.Equal(HttpStatusCode.Created, response.StatusCode);
    }
}
```