# _ (underscore) vs. var in C#: Clean Code, Readability, and Best Practices

C# developers often use var and _ in Razor Pages, Web APIs, and other .NET apps to simplify code. While these features provide syntactic convenience, **overuse or misuse can harm code readability and maintainability,** especially in team environments.

## This article covers:

- What var and _ are
- When to use them
- When they hurt code quality
- Best practices for writing clean, readable C# code

## 1. Understanding var in C#
What it is:
`var` is a keyword that allows implicit typing. The compiler infers the type based on the assigned value.

```csharp
var name = "Gayan";                 // string
var numbers = new List<int>();      // List<int>
```
## Pros of using `var`

| Benefit | Description |
|---|---|
| Less redundancy | Avoids repeating type info: `var person = new Person();` instead of `Person person = new Person();`|
| Great for anonymous/complex types | Especially in LINQ or object initializers |
| Encourages flexibility | Simplifies variable declarations in modern APIs |

## Cons of using `var`

| Drawback | Description |
|---|---|
| Hidden types | `var x = Foo();` gives no clue what x really is |
| Readability loss | For someone scanning code, explicit types are easier to parse |
| Refactoring pain | Type change may go unnoticed in `var x = ...` if method return type changes |


## Best Practices for `var`

```csharp
// DO: When the type is obvious
var customer = new Customer();  

// DO: For LINQ or anonymous types
var result = people.Where(p => p.Age > 30).ToList();  

// DON'T: When type isn't clear from right-hand side
var data = GetSomething();  // Not clear what "data" is
```
> Tip: Use var only when it enhances clarity, not just brevity.

## 2. Understanding _ in C#
_ in modern C# is used for:
- Discards: Ignoring a value or result
- Private field naming (e.g., _logger)
- Pattern matching (e.g., case _: return;)

## Pros of _ usage

| Use Case | Benefit |
|---|---|
| Discard values | Cleaner than dummy variable names: `_ = Task.Run(...)` |
| Ignore tuple items | `(var _, var y) = GetCoordinates();` |
| Private fields | _prefix improves naming consistency |


## Cons of _ misuse

| Misuse | Problem |
|---|---|
| Too many discards | Can make control flow confusing in pattern matching |
| _ used as a variable name | Should be avoided in older C# or where it may shadow other identifiers |
| Overused discards | May hide valuable return values, especially in critical logic |


## _ vs var: Comparison Table

| Feature | var | _ |
|---|---|---|
| Purpose | Implicit typing | Discards or private field convention |
| Readability | Can be unclear without context | Clear when used as discard |
| Best use case | LINQ, obvious RHS types | Ignoring results, naming private fields |
| Worst use case | Hidden types, complex method calls | Overused pattern match discards |

---

## Best Practices for Clean and Readable Code

1. Prefer explicit types when clarity is important
   ```csharp
    Customer customer = GetCustomer(); // Better than var
   ```
2. Use var only when the type is obvious or unavoidable
    ```csharp
     var orders = new List<Order>(); // OK
     var result = dbContext.Orders.Where(...); // OK for LINQ
   ```
3. Use _ for discards, but don't overuse it
    ```csharp
     _ = DoAsync(); // Fire-and-forget
   ```
4. Stick to naming conventions for private fields
    ```csharp
     private readonly ILogger<MyPage> _logger;
   ```
   

## Conclusion

`var` and `_` are powerful tools, but with power comes the need for discipline.

When used thoughtfully, they reduce noise and increase elegance. When misused, they obscure logic and hurt readability. For team-based development, clarity should always win over cleverness.
