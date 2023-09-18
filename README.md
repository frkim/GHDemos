# GitHub Copilot Demo walkthrough

In this tutorial, we are going to detail all the steps to demonstrate GiHub Copilot with a few live examples. This walkthrough relies on Visual Studio Code and Python programming language. Nowadays, both VS Code and Python are popular tools in developer environments.

## Prerequisites

Before running the sample you need to install:

 - Visual Studio Code
 - GH Copilot + GH Copilot Chat extension
 - Python Extension
 - Python framework
 - Python modules: requests fastapi and uvicorn

Then, register a new free account on [Сurrent weather and forecast - OpenWeatherMap](https://openweathermap.org/)

## Copilot Chat in Visual Studio Code

### First sample

    Hello, I'm a junior developer and I would like to learn python, what are the first steps?

### Weather forecast

In Copilot Chat, type:

    Can you write a simple function that retrieves the weather forecast?

1) Create a new file named weatherforecast.py and copy/paste the
    function code
2) Go to OpenWeatherForecast website and retrieve get you API
    Key
3) Replace YOUR_API_KEY_HERE by your own OpenWeatherMap API key

In Copilot Chat, type:

    How can I call a function in Python file from the command line?

 Open a terminal command line in Visual Studio Code and type:

    python weatherforecast.py weatherforecast.py get_weather "New York"

In Copilot Chat, type:

    Can you write a web API that returns the weather forecast with the previous function get_weather stored in weatherforecast.py file with FastAPI

To run this app, save the code to a file named app.py and run the following command in your terminal
    python -m uvicorn app:app --host 0.0.0.0 --port 3000

    Open a Web browser and type in the address bar : http://localhost:3000/weather?city=Paris

# GitHub Copilot inline editing assistant

Create a new file named: tempconv.py and write the following text:

    # function that converts temperature from Celsius 

It will complete with:

    def convert_temp_C2F(temp):
        return (temp * 9/5) + 32

Then write

    # function that converts temperature from Fahrenheit to Celsius

def convert_temp_F2C(temp):
    return (temp - 32) * 5/9

Write:

    # function that convert miles to kilometers

Type ^M (Control M to display the multiple suggestions

In Copilot Chat type:

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

    Write a function that validate an email address

Select and copy the regular expression and explain

