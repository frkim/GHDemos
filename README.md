# GitHub Copilot Demo Walkthrough

In this tutorial, we are going to detail all the steps to demonstrate GitHub Copilot with several samples. This walkthrough relies on Visual Studio Code and Python programming language because these tools are very popular among developers, IT engineers, DevOps, and data scientists.

We will see how GitHub Copilot Chat can help developers as a useful assistant without leaving the editor and how GitHub Copilot can help by suggesting code snippets during the code authoring.

## Prerequisites

Before running the sample you need to install:

- [Visual Studio Code](https://code.visualstudio.com/download)
- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot&WT.mc_id=devcloud-85335-cxa) + [GitHub Copilot Chat extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)
- [Python Extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
- [Python framework](https://www.python.org/downloads/)
- [Python modules](https://docs.python.org/3/installing/index.html): requests, fastapi, uvicorn...

Type the following command in a terminal:
`
python -m pip -r requirements
`

For dev scenario(with OpenWeather)
Register a new free account on [Сurrent weather and forecast - OpenWeatherMap](https://openweathermap.org/)

For Microsoft Team Integration
Create a Webhook into a sandbox channel and get the Webhook's URL. [See this page](https://learn.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook?tabs=dotnet).

## GitHub Copilot - Inline Editing Assistant

### Q&A Editor

First, you can use your main code editor to ask your question just type the comment character followed by q:

Use the **tab** keyboard key to validate the suggestion

    # q: what REST stands for?
    # a: Representational State Transfer
    # q: can you explain what is REST?
    # a: REST is an architectural style for building distributed systems based on hypermedia.
    # q: what is the difference between a web service and a RESTful web service?
    # a: a web service is a software system designed to support interoperable machine-to-machine interaction over a network.

### Code Authoring

Create a new file named: tempconv.py and write the following comment text block:

    # Function that converts temperature from Celsius 

GitHub Copilot should complete with a code that looks like this:

    def convert_temp_C2F(temp):
        return (temp * 9/5) + 32

Then, write:

    # Function that converts temperature from Fahrenheit to Celsius

GitHub Copilot should suggest a similar code:

        def convert_temp_F2C(temp):
            return (temp - 32) * 5/9

> You can move the mouse's cursor over the grey suggestion to display a flyout menu with different solutions ([See here for shortcuts](https://docs.github.com/en/copilot/getting-started-with-github-copilot#seeing-alternative-suggestions-2)).

### Displaying multiple solutions in a Completions Panel

Type the following comment:

    # Function that converts miles to kilometers

Once you've typed **Enter** keyboard key, you can display multiple suggestions by typing the **Ctrl-Enter** shortcut.

If this shortcut doesn't work because of another keyboard mapping, just display the Visual Studio Command Palette (View\Command Palette or Ctrl-Shift-P) and type 'GitHub Copilot: Open Completions Panel'.

### SQL Code Authoring (Optionaly)

GitHub Copilot can help in writing SQL Code

Type the following code in a blank file 'sqlops.py':

    class Employee:
    def __init__(self, i, n):
        self.empid = i
        self.name = n

This code defines a class with two attributes: empid and name. If you type the following code:

    # Create Employee table

GitHub Copilot will complete with:

    cursor = dbConnection.cursor()
    cursor.execute("DROP TABLE IF EXISTS Employee")
    cursor.execute("CREATE TABLE Employee (empid INTEGER PRIMARY KEY, name TEXT)")
    dbConnection.commit()

### Unit Tests Authoring

Just below the methods type 

    # unit test methods to validate

and hit **tab** keyboard key to complete with ' the functions celcius_to_fahrenheit and fahrenheit_to_celsius', then hit **Enter** and type 'def'

GitHub Copilot should suggest the following code:

    def test_celsius_to_fahrenheit():
        assert celsius_to_fahrenheit(0) == 32
        assert celsius_to_fahrenheit(100) == 212
        assert celsius_to_fahrenheit(-40) == -40

Do the same with 'def test_fahrenheit_to_celsius()' method

    def test_fahrenheit_to_celsius():
        assert fahrenheit_to_celsius(32) == 0
        assert fahrenheit_to_celsius(212) == 100
        assert fahrenheit_to_celsius(-40) == -40

## GitHub Copilot Chat in Visual Studio Code

Now, let's explore the GitHub Copilot Chat. This new feature allows you to ask any code-related question directly within a supported IDE. Copilot Chat can help you with a variety of coding-related tasks, like offering you code suggestions, providing natural language descriptions of a piece of code's functionality and purpose, and so forth.

### First sample

Open the [GitHub Copilot Chat panel](https://docs.github.com/en/copilot/github-copilot-chat/using-github-copilot-chat#asking-your-first-question) and ask your first question:

    Hello, I'm a junior developer and I would like to learn python, what are the first steps?

### Explain code

In Copilot Chat type:

    # Function that validates an email address

GitHub Copilot should write a code something similar to:

    def is_valid_email(email):
        pattern = r'^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$'
        return re.search(pattern, email) is not None

Select and copy the regular expression and type in GitHub Copilot Chat

    Can you explain in GitHub the following regular expression: ^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$

### MSFT Stock Value in Microsoft Team

In this sample you are going to query an online API to get the Microsoft Stock Value and send it to Microsoft teams through a Webhook

Open a new file and save it to stocks.py, type

    # Function that retrieve the online MSFT stock value

Just after typing **Enter** GitHub Copilot will complete with a code like this:

    def get_stock_value():
        url = "https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol=MSFT&apikey=demo"
        response = requests.get(url)
        data = response.json()
        return data["Global Quote"]["05. price"]

Then, write the following comment:

    # Function that publish a message on Microsoft Teams Webhook

GitHub Copilot will complete with:

    def send_message(message):
        url = "https://microsoft.webhook.office.com/webhookb2/YourIncomingWebhook"
        headers = {'Content-Type': 'application/json'}
        payload = {'text': message}
        response = requests.post(url, headers=headers, data=json.dumps(payload))
        return response.status_code

Add the necessary import at the beginning of the file:

    import requests
    import json

and this one at the end:

    send_message('MSFT Stock:' + get_stock_value())

Click on [Play Button](https://code.visualstudio.com/docs/languages/python#_run-python-code) to execute the python script

Now just check in your Team a new notification "MSFT Stock:330.2200"

### Weather forecast

In this demo, we are going to query an online weather forcast web API and the create a simple web server with [FastAPI framework](https://fastapi.tiangolo.com/).

In GitHub Copilot Chat, type:

    Can you write a simple function that retrieves the weather forecast?

1) Create a new file named weatherforecast.py and copy/paste the
    function code
2) Go to OpenWeatherForecast website and retrieve your API
    Key
3) Replace YOUR_API_KEY_HERE with your own OpenWeatherMap API key

In GitHub Copilot Chat, type:

    How can I call a function in Python file from the command line?

 Open a terminal command line in Visual Studio Code and type:

    python weatherforecast.py weatherforecast.py get_weather "New York"

In GitHub Copilot Chat, type:

    Can you write a web API that returns the weather forecast with the previous function get_weather stored in weatherforecast.py file with FastAPI

To run this app, save the code to a file named app.py and run the following command in your terminal

    python -m uvicorn app:app --host 0.0.0.0 --port 3000

Open a Web browser and type in the address bar: http://localhost:3000/weather?city=Paris

## Additional References

Below, you'll find some useful links to move forward with GitHub Copilot:

- [Get Started with the Future of Coding: GitHub Copilot](https://www.youtube.com/watch?v=Fi3AJZZregI&t=469s)
- [Create a .NET Web API with Entity Framework with GitHub - Copilot](https://www.youtube.com/watch?v=A7nV0xF5vYg)
- [Create Python Django apps with GitHub Copilot](https://www.youtube.com/watch?v=HDsJQVa0R94)
- [GitHub Copilot: Getting Started with Chat](https://www.youtube.com/watch?v=3surPGP7_4o)
- [GitHub Copilot tips and tricks](https://www.youtube.com/watch?v=1qs6QKk0DVc)
