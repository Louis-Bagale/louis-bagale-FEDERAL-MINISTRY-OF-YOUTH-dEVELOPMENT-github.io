// C# Backend Example (Controller)
// Code for handling requests and interacting with the database

[Route("api/youth")]
public class YouthController : ControllerBase
{
    private readonly YouthService _youthService;

    public YouthController(YouthService youthService)
    {
        _youthService = youthService;
    }

    [HttpGet]
    public async Task<IActionResult> GetAllYouth()
    {
        var youth = await _youthService.GetAllYouth();
        return Ok(youth);
    }

    // Other CRUD operations and business logic
}

// Blazor Component (Frontend)
// Sample component to display youth information

@page "/youth"
@inject HttpClient HttpClient

<h3>Youth Information</h3>

@if (youthList != null)
{
    foreach (var youth in youthList)
    {
        <div>@youth.Name - @youth.Age</div>
    }
}

@code {
    List<Youth> youthList;

    protected override async Task OnInitializedAsync()
    {
        youthList = await HttpClient.GetFromJsonAsync<List<Youth>>("api/youth");
    }
}
