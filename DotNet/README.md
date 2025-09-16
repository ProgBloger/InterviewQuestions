
# .NET Interview Questions and Answers

A curated list of .NET interview questions with detailed answers.  
Use this repository to prepare for interviews or refresh your knowledge.

---

## 📑 Table of Contents

1. [C# Basics](#c-basics)
2. [OOP Concepts](#oop-concepts)
3. [Advanced C#](#advanced-c)
4. [.NET Core & .NET 5+](#net-core--net-5)
5. [ASP.NET Core](#aspnet-core)
6. [Entity Framework Core](#entity-framework-core)
7. [Design Patterns](#design-patterns)
8. [Memory Management & GC](#memory-management--gc)
9. [Multithreading & Async](#multithreading--async)
10. [Miscellaneous](#miscellaneous)

---

## C# Basics

### Q: What is the heap in C#?
**Answer:**

The heap is a memory area managed by the .NET runtime where **reference types** (objects, arrays, strings, classes) are stored.
  - Unlike the **stack** (used for local variables and value types), the heap is larger and supports dynamic allocation.
  - Objects live there until no longer referenced, at which point the **Garbage Collector** reclaims the memory.

---

### Q1. What is the difference between `String` and `string` in C#?

**Answer:**  
- `string` is an alias in C# for `System.String`.  
- Both can be used interchangeably.  
- Example:  
  ```csharp
  string s1 = "Hello";
  String s2 = "World";

---

### Q2. What are value types and reference types?

**Answer:**

* **Value types** store the actual data (e.g., `int`, `float`, `struct`).
* **Reference types** store a reference (address) to the data (e.g., `class`, `string`, `object`).

---

## OOP Concepts

### Q: What are the three (four) pillars of OOP in C#?

**Answer:**
Different sources describe them slightly differently:

- **Three pillars view** →
  1. **Abstraction** - Hiding implementation details and exposing only the interface.
  2. **Inheritance** - Deriving new classes from existing ones.
  3. **Polymorphism** - Ability for methods/objects to take many forms (overloading/overriding).

In this view, *encapsulation* is treated as part of abstraction (hiding data/implementation).

- **Four pillars view** →
  1. **Encapsulation** - Placing related data and methods together inside a class.
  2. **Abstraction** - Hiding implementation details, exposing only what's necessary.
  3. **Inheritance** - Reusing code by deriving new classes.
  4. **Polymorphism** - Same interface, different behavior.

---

### Q: What are the types of polymorphism in C#?
**Answer:**
There are two common categorizations:

1. **C# / OOP view**
  - **Compile-time (static)** → method/constructor overloading, operator overloading.
  - **Run-time (dynamic)** → method overriding via `virtual`/`override`/`abstract`.

2. **Computer science view**
  - **Ad-hoc polymorphism** → a function works with different types but separately (e.g., overloading, operator overloading).
  - **Parametric polymorphism** → a function works with any type in a generic way (e.g., generics in C#).
  - **Subtype polymorphism** → using a base type reference for derived objects (e.g., inheritance + overriding).

---

## Advanced C\#

### Q: What are hash table collisions and how to prevent them in C#?
**Answer:**
A collision happens when two different keys produce the same hash code and end up in the same bucket of a hash table (e.g., `Dictionary<TKey, TValue>` or `HashSet<T>`).

  - **Handling in C#:**
    - The runtime uses **chaining** (a linked list or tree inside the bucket) to store multiple items.
    - When collisions increase, preformance degrades from O(1) average to O(n) worst-case.

  - **How to minimize collisions:**
    - Use good hash functions (`GetHashCode` implementation should spread values evenly).
    - Make keys immutable.
    - Avoid poorly designed custom `GetHashCode` overrides.

**Example:**
```csharp
class BadKey
{
  public int Value { get; set; }
  public override int GetHashCode() => 1; // Bad: all keys collide
}

var dict = new Dictionary<BadKey, string>();
dict[new BadKey { Value = 1 }] = "One";
dict[new BadKey { Value = 2 }] = "Two"; // Collision occurs here

---

### Q: Why is throwing exceptions considered a bad approach in .NET?
**Answer:**
Exceptions are slow and should only be used for unexpected errors.
Using them for normal control flow hurts performance, makes code harder to read, and hides the difference between *real errors* and *expected conditions*.

---

### Q: What are the types of delegates in .NET?

**Answer:**
A **delegate** is a type that represents references to methods with a particular parameter list and return type.

In .NET, the main types of delegates are:

1. **Single-cast delegate**
  - Points to a single method.
  - Example:
  ``` csharp
  public delegate void MyDelegate(string msg);
  ```

2. **Multi-cast delegate**
  - Can reference multople methods in its invocation list.
  - When invoked, it calls methods in order.
  - Example: event handlers use multi-cast delegates.

3. **Generic delegates** (built-in)
  - **Func\<T, TResult\>** → represents a method that returns a value.
  - **Action\<T\>** → represents a method that returns void.
  - **Predicate\<T\>** → represents a method that returns bool.

4. **Anonymous methods / lambda expressions as delegates**
  - You can assign inline code blocks or lambdas to delegate types.

---

### Q: What is the difference between `IEnumerable`, `ICollection`, `IList`, and `IQueryable` in .NET?
**Answer:**
  - **IEnumerable** - Read-only, forward-only iteration in memory.
  - **ICollection** - Extends IEnumerable, has Count and supports add/remove.
  - **IList** - Extends ICollection, allows index-based access and insertion.
  - **IQueryable** - Extends IEnumerable, builds expression trees for LINQ providers (e.g., EF Core) and runs queries on the database instead of in memory. Used for deffered, remote queries.

---

## .NET Core & .NET 5+

### Q1. What are the key differences between .NET Framework and .NET Core?

**Answer:**

* **Cross-platform** – .NET Core works on Windows, Linux, macOS.
* **Performance** – .NET Core is faster and lightweight.
* **Deployment** – .NET Core allows self-contained deployment.
* **Open Source** – .NET Core is open-source on GitHub.

---

## ASP.NET Core

### Q: What is an Action Filter in ASP.NET Core?
**Answer:**
An Action Filter is a component that runs **Before and/or after** a controller action executes.
  - Commpn use: logging, validation, caching, authorization.
  - They implement the `IActionFilter` or `IAsyncActionFilter` interface.
  - Can be applied at method, controller, or globally.

Example: log every request before and after action execution.

---

### Q: How does JWT (JSON Web Token) work?
**Answer:**

JWT is a compact token used for authentication/authorization.
 - It has 3 parts: **Header**, **Payload**, **Signature** (Base64-encoded and joined with dots).
 - The server issues a JWT after successful login and signs it with a secret key.
 - The client sends the token in the `Authorization: Bearer <token>` header.
 - The server verifies the signature to ensure the token wasn't tampered with, then reads claims from the payload (e.g., user id, roles).

 Benefit: server doesn't need to keep session state - all info is in the token, validated by the signature.

 **Example JWT:**
 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwicm9sZSI6IkFkbWluIiwiaWF0IjoxNTE2MjM5MDIyfQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

  - **Header (Base64 decoded):** `{ "alg": "HS256", "typ": "JWT" }`
  - **Payload (Base64 decoded):** `{ "sub": "1234567890", "name": "John Doe", "role": "Admin", "iat": 1516239022 }`
  - **Signature:** verifies the token's integrity.

---

### Q1. What is Middleware in ASP.NET Core?

**Answer:**

* Middleware is software that handles requests and responses.
* ASP.NET Core pipeline is a sequence of middleware components.
* Example: Authentication, Logging, Exception Handling.

---

## Entity Framework Core

### Q1. What are the advantages of EF Core over ADO.NET?

**Answer:**

* Less boilerplate code.
* Strongly typed LINQ queries.
* Built-in change tracking.
* Easier migrations and schema evolution.

---

## Design Patterns

### Q: Can circular dependencies be achieved in C# with DI? Whant happens and how to handle them?
**Answer:**

Yes, you can accidentally create circular dependencies (e.g., `A` depends on `B`, and `B` depends on `A`).

  - **What happens:** most DI containers (like Microsoft.Extensions.DependencyInjection) will throw an exception at runtime (e.g., *"A circular dependency was detected..."*).
  - **Can it actually run?** Some containers allow lazu resolution (`Lazy<T>`, `Func<T>`, or `IServiceProvider.GetService<T>`), but this usually hides a design problem.
  - **How to handle:**
    - Break the cycle by refactoring responsibilities.
    - Introduce an interface or mediator service between the two classes.
    - Apply patterns like **Observer, Mediator, or Factory** to decouple.

---

### Q: Is it possible (and okay) to have a class with 10 dependencies injected via DI in C#?
**Answer:**

Technically yes, DI will handle it. But a constructor with 10 dependencies is a design smell:
  - It usually means the class has too many responsibilities (violates SRP).
  - It becomes hard to test and maintain.

Better approaches:
  - Split into smaller services.
  - Group related dependncies into a *facade* or *parameter object*.
  - Use the **Factory pattern** to encapsulate complex object creation logic.
  - Use composition to keep classes focused.

---

### Q1. Explain the Repository Pattern.

**Answer:**

* Abstracts data access logic.
* Provides a cleaner separation of concerns.
* Example:

  ```csharp
  public interface IProductRepository {
      Task<IEnumerable<Product>> GetAllAsync();
      Task<Product> GetByIdAsync(int id);
      Task AddAsync(Product product);
  }
  ```

---

## Memory Management & GC

### Q1. How does Garbage Collection work in .NET?

**Answer:**

* Automatic memory management.
* Reclaims unused objects from the heap.
* Works in generations (Gen 0, 1, 2).
* Uses stop-the-world collection when required.

---

## Multithreading & Async

### Q: How do you stop or cancel an async method in C#?

**Answer:**
You cannot directly "stop" an async method once it has started. Instead, you use a **cancellation mechanism**.

The standart way in .NET is with `CancellationToken`:

1. Create a `CancellationTokenSource`.
2. Pass it's `Token` into the async method.
3. Inside the method, check the token (e.g., `token.ThrowIfCancellationRequested()` or `token.IsCancellationRequested`).
4. Call `Cancel()` on the source to request cancellation.

Example:
```csharp
public async Task DoWorkAsync(CancellationToken token)
{
  for(int i = 0; i < 10; i++)
  {
    token.ThrowIfCancellationRequested();
    await Task.Delay(1000, token); // Supports cancellation
  }
}

// Usage:
var cts = new CancellationTokenSource();
var task = DoWorkAsync(cts.Token);
cts.Cancel(); // Request to stop
```


### Q: Can you use `await` inside a `lock` statement in C#?

**Answer:**
No, you cannot. The `lock` statement is synchronous and does not allow `await` inside its body. If you try, the compiler will give an error.

The reason is that `await` pauses execution and may resume on another thread. If the lock were held during this pause, it could block other threads forever.

To safely combine `await` with locking, use an async-friendly alternative such as `SemaphoreSlim`:

```csharp
private readonly SemaphoreSlim _lock = new SemaphoreSlim(1, 1);

public async Task DoWorkAsync()
{
  await _lock.WaitAsync();

  try
  {
    await Task.Delay(1000); // Safe to await
  }
  finally
  {
    _lock.Release();
  }
}
```

---

### Q1. Difference between `Task`, `Thread`, and `ValueTask`?

**Answer:**

* **Thread** – OS-level lightweight process.
* **Task** – Abstraction over asynchronous operations.
* **ValueTask** – Optimized for scenarios where result may be synchronous.

---

## Miscellaneous

### Q1. Difference between REST and gRPC in .NET?

**Answer:**

* **REST** – Text-based (JSON), widely used, human-readable.
* **gRPC** – Binary protocol (Protobuf), faster, strongly typed contracts.

---
