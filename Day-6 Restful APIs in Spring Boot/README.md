Q1. Designing a Product Service without exposing JPA entities
Q1.A Why use DTOs instead of entities?

Also, how do you map between them?

I use DTOs instead of exposing JPA entities because entities are directly linked to the database. Exposing them can leak internal fields and tightly couple the API with the database structure. Any database change may impact the API if entities are exposed.

DTOs help define a clean API contract and control what data is sent to the client.

Mapping between entity and DTO can be done manually or using tools like ModelMapper or MapStruct. I usually prefer manual mapping because it is simple, readable, and easy to debug.

Q1.B Where should validation occur — controller or service?

Validation should occur at both levels but for different purposes.

In the controller layer, I validate incoming requests using annotations like @Valid to ensure input data is correct.

In the service layer, I handle business validations such as checking if a product already exists or if an operation is allowed.

Q1.C How do you keep controllers thin and services fat?

Controllers should only handle request and response logic. They should not contain business logic.

All business rules, calculations, and database interactions should be written inside the service layer. This makes the application easier to maintain and test.

Q1.D Which annotations are essential for clean API design?

Some important annotations are:

@RestController

@RequestMapping

@GetMapping, @PostMapping, @PutMapping, @DeleteMapping

@PathVariable

@RequestParam

@RequestBody

Q2. Consistent error responses and backward-compatible APIs
Q2.A How do you implement global error handling?

I use @ControllerAdvice to handle exceptions globally instead of handling them in every controller. Inside it, I define methods using @ExceptionHandler for different exception types.

This keeps controllers clean and ensures all APIs return consistent error responses.

Q2.B What should a standard error response contain?

A standard error response usually contains:

Timestamp

HTTP status code

Error type

Error message

Request path

This information helps both frontend developers and backend debugging.

Q2.C How do you plan API versioning and deprecation?

I use URL-based versioning such as /api/v1/products. This approach is simple and easy to manage.

For deprecation, older versions are supported for a certain period while new versions are introduced. Clients are informed in advance before removing old APIs.

Q2.D How do you return custom HTTP status codes?

I use ResponseEntity when I need control over the HTTP response, such as returning custom status codes, headers, or error responses.

Q3. Idempotent and resilient Create Order API
Q3.A How do you implement idempotency keys and deduplication?

The client sends an idempotency key with the request. This key is stored along with the processed response.

If the same request is received again with the same key, I return the stored response instead of creating a new order. This prevents duplicate order creation.

Q3.B How do you handle timeouts, retries, and circuit breakers?

Using Resilience4j, I configure timeouts to avoid long waits, retries for temporary failures, and circuit breakers to stop repeated failing calls.

This protects the system from cascading failures and improves reliability.

Q3.C How do you return 202 Accepted for async processing?

For long-running operations, I return 202 Accepted and provide a status endpoint that the client can poll.

In more advanced systems, webhooks can be used to notify the client when processing is completed.

Q3.D How do you handle partial failures?

Partial failures are handled using compensating actions. If one step fails after a previous step succeeds, the earlier step is rolled back logically.

Patterns like Saga help manage such distributed transactions.

Q4. Backend validations for POST APIs
Q4.A Why are validations critical?

Validations prevent invalid or malicious data from entering the system. They help maintain data integrity and improve API security.

Q4.B How do you use @Valid and constraint annotations?

Validation annotations such as @NotBlank, @Email, and @Size are added to DTO fields. The controller uses @Valid to trigger validation automatically.

Q4.C How do you send validation errors in a structured way?

When validation fails, Spring throws a validation exception. I handle this globally and return a structured response with field-level error messages.

Q4.D What happens when validation fails?

If validation fails, the API returns a 400 Bad Request status with detailed error messages instead of a generic response.
