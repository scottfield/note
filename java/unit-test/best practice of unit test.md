##Common Warning Signs of Hard to Test Code
- Static Properties and Fields

Static properties and fields or, simply put, global state, can complicate code comprehension and testability, by hiding the information required for a method to get its job done, by introducing non-determinism, or by promoting extensive usage of side effects. Functions that read or modify mutable global state are inherently impure.

For example, it is hard to reason about the following code, which depends on a globally accessible property:
```
if (!SmartHomeSettings.CostSavingEnabled) { _swimmingPoolController.HeatWater(); }
```
What if the HeatWater() method doesn’t get called when we are sure it should have been? Since any part of the application might have changed the CostSavingEnabled value, we must find and analyze all the places modifying that value in order to find out what’s wrong. Also, as we’ve already seen, it is not possible to set some static properties for testing purposes (e.g., DateTime.Now, or Environment.MachineName; they are read-only, but still non-deterministic).

On the other hand, immutable and deterministic global state is totally OK. In fact, there’s a more familiar name for this — a constant. Constant values like Math.PI do not introduce any non-determinism, and, since their values cannot be changed, do not allow any side effects:
```
double Circumference(double radius) { return 2 * Math.PI * radius; } // Still a pure function!
```
- Singletons

Essentially, the Singleton pattern is just another form of the global state. Singletons promote obscure APIs that lie about real dependencies and introduce unnecessarily tight coupling between components. They also violate the Single Responsibility Principle because, in addition to their primary duties, they control their own initialization and lifecycle.

Singletons can easily make unit tests order-dependent because they carry state around for the lifetime of the whole application or unit test suite. Have a look at the following example:
```
User GetUser(int userId)
{
    User user;
    if (UserCache.Instance.ContainsKey(userId))
    {
        user = UserCache.Instance[userId];
    }
    else
    {
        user = _userService.LoadUser(userId);
        UserCache.Instance[userId] = user;
    }
    return user;
}
```
In the example above, if a test for the cache-hit scenario runs first, it will add a new user to the cache, so a subsequent test of the cache-miss scenario may fail because it assumes that the cache is empty. To overcome this, we’ll have to write additional teardown code to clean the UserCache after each unit test run.

Using Singletons is a bad practice that can (and should) be avoided in most cases; however, it is important to distinguish between Singleton as a design pattern, and a single instance of an object. In the latter case, the responsibility of creating and maintaining a single instance lies with the application itself. Typically, this is handed with a factory or Dependency Injection container, which creates a single instance somewhere near the “top” of the application (i.e., closer to an application entry point) and then passes it to every object that needs it. This approach is absolutely correct, from both testability and API quality perspectives.

- The new Operator

Newing up an instance of an object in order to get some job done introduces the same problem as the Singleton anti-pattern: unclear APIs with hidden dependencies, tight coupling, and poor testability.

For example, in order to test whether the following loop stops when a 404 status code is returned, the developer should set up a test web server:
```
using (var client = new HttpClient())
{
    HttpResponseMessage response;
    do
    {
        response = await client.GetAsync(uri);
        // Process the response and update the uri...
    } while (response.StatusCode != HttpStatusCode.NotFound);
}
```
However, sometimes new is absolutely harmless: for example, it is OK to create simple entity objects:
```
var person = new Person("John", "Doe", new DateTime(1970, 12, 31));
```
It is also OK to create a small, temporary object that does not produce any side effects, except to modify their own state, and then return the result based on that state. In the following example, we don’t care whether Stack methods were called or not — we just check if the end result is correct:
```
string ReverseString(string input)
{
    // No need to do interaction-based testing and check that Stack methods were called or not;
    // The unit test just needs to ensure that the return value is correct (state-based testing).
    var stack = new Stack<char>();
    foreach(var s in input)
    {
        stack.Push(s);
    }
    string result = string.Empty;
    while(stack.Count != 0)
    {
        result += stack.Pop();
    }
    return result;
}
```
- Static Methods

Static methods are another potential source of non-deterministic or side-effecting behavior. They can easily introduce tight coupling and make our code untestable.

For example, to verify the behavior of the following method, unit tests must manipulate environment variables and read the console output stream to ensure that the appropriate data was printed:
```
void CheckPathEnvironmentVariable()
{

    if (Environment.GetEnvironmentVariable("PATH") != null)
    {
        Console.WriteLine("PATH environment variable exists.");
    }

    else
    {
       Console.WriteLine("PATH environment variable is not defined.");
    }

}
```
However, pure static functions are OK: any combination of them will still be a pure function. For example:
```
double Hypotenuse(double side1, double side2) { return Math.Sqrt(Math.Pow(side1, 2) + Math.Pow(side2, 2)); }
```