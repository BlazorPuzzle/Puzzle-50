# Blazor Puzzle #50

## Clicky No Worky!

YouTube Video: https://youtu.be/Tq_RAUuxphY

Blazor Puzzle Home Page: https://blazorpuzzle.com

### The Challenge:

This is a simple Blazor Web App with Global Server Interactivity.

Clicking the button should calculate the time difference between the server and your local time.

However, it doesn't seem to work. Can you fix it?

### The Solution:

The problem is that the JavaScript method is not being called asynchronously. If you don't use the await keyword, your code control may return before the JavaScript finishes executing.

The solution is to make the `CalculateTimeDifference()` method async, and then use await to call the JavaScript method:

```c#
private async Task CalculateTimeDifference()
{
    // Step 1: Get the server's current time
    ServerTime = DateTime.UtcNow;

    // Step 2: Get the client's local time zone offset via JavaScript
    var result = await JS.InvokeAsync<int>("getClientTimezoneOffset");

    // Step 3: Use the result to calculate the user's local time
    LocalTime = ServerTime.AddMinutes(-result);
}
```

