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

**First sample**

    Hello, I'm a junior developer and I would like to learn python, what are the first steps?

**Weather forecast**

In Copilot Chat, type:

    Can you write a simple function that retrieves the weather forecast?

 - [ ] Create a new file named weatherforecast.py and copy/paste the
    function code
 - [ ] Go to OpenWeatherForecast website and retrieve get you API
    Key
 - [ ] Replace YOUR_API_KEY_HERE by your own OpenWeatherMap API key

In Copilot Chat, type:

    How can I call a function in Python file from the command line?

 Open a terminal command line in Visual Studio Code and type:

    python weatherforecast.py weatherforecast.py get_weather "New York"

In Copilot Chat, type:
    Can you write a web API that returns the weather forecast with the previous function get_weather stored in weatherforecast.py file with FastAPI

To run this app, save the code to a file named app.py and run the following command in your terminal
    python -m uvicorn app:app --host 0.0.0.0 --port 3000

Open a Web browser and type in the address bar : http://localhost:3000/weather?city=Paris





















