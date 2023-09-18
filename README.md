# GitHub Copilot Demo walkthrough

In this tutorial, we are going to detail all the steps to demonstrate GiHub Copilot with several samples. This walkthrough relies on Visual Studio Code and Python programming language because these tools are very popular.

We will see how GitHub Copilot Chat can help developers as a usefull assistant wihtout leaving the editor and how GitHub Copilot can help by suggesting code snippet during the code authoring.

## Prerequisites

Before running the sample you need to install:

- [Visual Studio Code](https://code.visualstudio.com/download)
- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot&WT.mc_id=devcloud-85335-cxa) + [GitHub Copilot Chat extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)
- [Python Extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
- [Python framework](https://www.python.org/downloads/)
- [Python modules](https://docs.python.org/3/installing/index.html): requests fastapi and uvicorn
  - python -m pip install requests
  - python -m pip install fastapi
  - python -m pip install uvicorn

For dev scenario(with OpenWeather)
Register a new free account on [Сurrent weather and forecast - OpenWeatherMap](https://openweathermap.org/)

For Microsoft Team Integration
Create a Webhook into a sandbox channel and get the Webhook's URL. [See this page](https://learn.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook?tabs=dotnet).


## GitHub Copilot Chat in Visual Studio Code

### First sample

    Hello, I'm a junior developer and I would like to learn python, what are the first steps?

### MSFT Stock Value in Microsoft Team

In this sample you are going to query an online API to get the Microsoft Stock Value and send it to Microsoft teams through a Webhook

Open a new file and save it to stocks.py, then type

    # Function that get the online MSFT stock value

Github Copilot will complete with a code like:

    def get_stock_value():
        url = "https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol=MSFT&apikey=demo"
        response = requests.get(url)
        data = response.json()
        return data["Global Quote"]["05. price"]

Then, write the following comment:
    
    # Function that a message on Microsoft Teams Webhook

GitHub Copilot will suggests:

    def send_message(message):
        url = "https://microsoft.webhook.office.com/webhookb2/YourIncomingWebhook"
        headers = {'Content-Type': 'application/json'}
        payload = {'text': message}
        response = requests.post(url, headers=headers, data=json.dumps(payload))
        return response.status_code

Add this code at the begging of the file:

    import requests
    import json

and this one at the end:

    send_message('MSFT Stock:' + get_stock_value())

And click on [Play Button](https://code.visualstudio.com/docs/languages/python#_run-python-code) to execute the python script

Now just check in your Team a new notification "MSFT Stock:330.2200"

### Weather forecast

In GitHub Copilot Chat, type:

    Can you write a simple function that retrieves the weather forecast?

1) Create a new file named weatherforecast.py and copy/paste the
    function code
2) Go to OpenWeatherForecast website and retrieve get you API
    Key
3) Replace YOUR_API_KEY_HERE by your own OpenWeatherMap API key

In GitHub Copilot Chat, type:

    How can I call a function in Python file from the command line?

 Open a terminal command line in Visual Studio Code and type:

    python weatherforecast.py weatherforecast.py get_weather "New York"

In GitHub Copilot Chat, type:

    Can you write a web API that returns the weather forecast with the previous function get_weather stored in weatherforecast.py file with FastAPI

To run this app, save the code to a file named app.py and run the following command in your terminal

    python -m uvicorn app:app --host 0.0.0.0 --port 3000

Open a Web browser and type in the address bar : http://localhost:3000/weather?city=Paris

## GitHub Copilot inline editing assistant

### Q&A Editor

First you can use the editor pane to ask your question just type the comment character followed by q:

Use tab keyboard to validate the suggestion

    # q: what REST stands for?
    # a: Representational State Transfer
    # q: can you explain what is REST?
    # a: REST is an architectural style for building distributed systems based on hypermedia.
    # q: what is the difference between a web service and a RESTful web service?
    # a: a web service is a software system designed to support interoperable machine-to-machine interaction over a network.

### Code Authoring

Create a new file named: tempconv.py and write the following text:

    # Function that converts temperature from Celsius 

GitHub Copilot should complete with a code that looks like:

    def convert_temp_C2F(temp):
        return (temp * 9/5) + 32

Then write:

    # Function that converts temperature from Fahrenheit to Celsius

GitHub Copilot should suggest a similar code:

        def convert_temp_F2C(temp):
            return (temp - 32) * 5/9

### Displaying multiple solutions

Type the following comment:

    # Function that converts miles to kilometers

Once you've typed **Enter** keyboard you can display multiple suggestions by typing the **Ctrl-Enter** shorthcut. 

If this shortcut doesn't work because another keyboard mapping, just display the Visual Studio Command Palette (View\Command Palette or Ctrl-Shift-P) and type 'GitHub Copilot: Open Completions Panel'.

### SQL Code Authoring (Optionnaly)

GitHub Copilot can help in writing SQL Code

Type the following code in a blank file:

    class Employee:
    def __init__(self, i, n):
        self.empid = i
        self.name = n

This code defines a class with two attributes: empid and name. If you type the following code

    # Create Employee table

GitHub Copilot will complete with:

    cursor = dbConnection.cursor()
    cursor.execute("DROP TABLE IF EXISTS Employee")
    cursor.execute("CREATE TABLE Employee (empid INTEGER PRIMARY KEY, name TEXT)")
    dbConnection.commit()

### Unit Test Authoring

In GitHub Copilot Chat type:

    How to write a unit test to validate celsius_to_fahrenheit and fahrenheit_to_celsius ?

Create a new file test_tempconv.py and paste  the suggested code:

    import unittest
    from tempconv import celsius_to_fahrenheit, fahrenheit_to_celsius

    class TestTempConv(unittest.TestCase):
        def test_celsius_to_fahrenheit(self):
            self.assertEqual(celsius_to_fahrenheit(0), 32)
            self.assertEqual(celsius_to_fahrenheit(100), 212)
            self.assertEqual(celsius_to_fahrenheit(-40), -40)
        
        def test_fahrenheit_to_celsius(self):
            self.assertEqual(fahrenheit_to_celsius(32), 0)
            self.assertEqual(fahrenheit_to_celsius(212), 100)
            self.assertEqual(fahrenheit_to_celsius(-40), -40)

    if __name__ == '__main__':
        unittest.main()

Click on Testing Icon [See Testing Python in Visual Studio Code](https://code.visualstudio.com/docs/python/testing) and launch the test

![Testing Python in VS Code](https://code.visualstudio.com/assets/docs/python/testing/test-explorer-no-tests.png)


### Explain code

In Copilot Chat type:

    # Function that validates an email address

GitHub Copilot should write a code something similar to:

    def is_valid_email(email):
        pattern = r'^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$'
        return re.search(pattern, email) is not None

Select and copy the regular expression and type in GitHub Copilot Chat

    Can you explain in GitHub the following regular expression: ^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$

### Additionnal References

- [Get Started with the Future of Coding: GitHub Copilot](https://www.youtube.com/watch?v=Fi3AJZZregI&t=469s)
- [Create a .NET Web API with Entity Framework with GitHub - Copilot](https://www.youtube.com/watch?v=A7nV0xF5vYg)
- [Create Python Django apps with GitHub Copilot](https://www.youtube.com/watch?v=HDsJQVa0R94)
- [GitHub Copilot: Getting Started with Chat](https://www.youtube.com/watch?v=3surPGP7_4o)
- [GitHub Copilot tips and tricks](https://www.youtube.com/watch?v=1qs6QKk0DVc)
