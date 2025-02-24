---
layout: post
title: "PyWebIO Guide: Building Interactive Web Apps "
date: 2025-02-23
author: "Saketh, Tarun, Mrudal"
categories: [Python, Web Development]
---
## What is PyWebIO?
PyWebIO is a Python library that enables us to create interactive web applications with minimal effort just using python. For anyone wondering what web applications are, they are interactive software programs that run in a web browser, allowing users to perform tasks, submit data, and receive dynamic responses without needing to install anything on their device. PyWebIO provides a simple, high-level API for building web interfaces.

### How to install PyWebIO?
Installing PyWebIO is straightforward. Ensure that Python is already installed on your system and python version should be 3.5.2 or newer. Run the below code in 
```sh
pip install -U pywebio
```
PyWebIO is now installed on your system. Start using it with python to develop web applications!

### Features of PyWebIO
- Simple syntax
- Supports interactive UI elements
- No need to write HTML/CSS/J
- Rich Input & Output Options: It provides built-in functions for various input types like text, numbers, radio buttons, checkboxes, file uploads, and more. For output, you can display formatted text, tables, images, and even interactive elements.
- HTML and CSS Integration: While PyWebIO is Python-based, it also supports HTML and CSS through put_html(), allowing you to style your application, embed multimedia, and enhance the UI.
- Markdown & HTML Support: Render HTML and Markdown directly within your application.
- PyWebIO provides several built-in modules that allow developers to build interactive web applications easily. Below are the key modules along with their explanations:

### Built-in Modules of PyWebIO  
PyWebIO provides several built-in modules to simplify web development:  

#### 1. Input Handling (`pywebio.input`) 
This module enables user interaction by providing various input methods.  
- `input()`: Text input field.  
- `textarea()`: Multi-line text input.  
- `select()`: Dropdown selection.  
- `radio()`: Single-choice selection.  
- `checkbox()`: Multi-choice selection.  
- `file_upload()`: Allows users to upload files.  

#### 2. Output Display (`pywebio.output`)
Used for displaying text, tables, images, and formatted content.  
- `put_text()`: Displays plain text.  
- `put_html()`: Renders custom HTML and CSS.  
- `put_image()`: Displays images.  
- `put_table()`: Creates structured tables.  
- `put_markdown()`: Renders Markdown content.  
- `put_buttons()`: Adds clickable buttons for interaction.  

#### 3. Session Management (`pywebio.session`) 
Helps in managing user sessions dynamically.  
- `set_env()`: Configures UI settings.  
- `run_async()`: Executes functions asynchronously. This means that instead of waiting for a function to complete, the program can continue running other tasks simultaneously.
- `hold()`: Keeps the session open even after script execution.  

#### 4. File Handling (`pywebio.file`)
Manages file uploads and downloads.  
- `download()`: Lets users download files.  
- `file_upload()`: Allows users to upload files for processing.  

#### 5. Web Framework Integration (`pywebio.platform`)
PyWebIO can be integrated with frameworks like Flask, Django, FastAPI, and Tornado.  
- `start_server()`: Runs PyWebIO as a local web server.  
- `webio_view()`: Allows embedding PyWebIO apps inside Flask or Django routes.  

#### 6. Interactive Charts (`pywebio.output`) 
Supports visualization by integrating with Matplotlib and Plotly to display interactive graphs.  

---

These features make PyWebIO an excellent choice for developing Python-based web applications quickly and efficiently!  
### Example Codes
Here are few examples of code for demonstration:
#### 1. A simple code that creates a web page that says hello to the user
```python
from pywebio.input import input
from pywebio.output import put_text

name = input("Enter your name:")
put_text(f"Hello, {name}!")
```
Explanation:

This line imports the input function from the pywebio.input module, which allows us to take user input in a web-based interface.
```python
from pywebio.input import input
``` 
Here, we import the put_text function from pywebio.output. This function is used to display text output on the web page.

```python
from pywebio.output import put_text
```
In the next line we declare variable `name` to take input from user. Finally, the `put_text()` function is used to display a greeting message with the user's name.

Here is the input page:

![Input page1](/assests/image1.jpeg)

This is how our output looks:

![Output page2](/assests/image2.jpeg)

#### 2. A number guessing game

```python
from pywebio.input import input, NUMBER
from pywebio.output import put_text, put_html
from pywebio.session import set_env
from pywebio import start_server
import random

def number_guessing_game():
    set_env(title="Number Guessing Game")  # Sets the webpage title
    secret_number = random.randint(1, 10)  # Random number between 1 and 10
    
    put_html("<h2>Welcome to the Number Guessing Game!</h2>")
    put_text("Guess a number between 1 and 10.")
    
    # Taking user input
    guess = input("Enter your guess:", type=NUMBER)

    # Change background color using <style> tag
    if guess == secret_number:
        put_html("""
            <style>
                body { background-color: green; }
            </style>
        """)
        put_text(f"🎉 Congratulations! You guessed it right. The number was {secret_number}.")
    else:
        put_html("""
            <style>
                body { background-color: red; }
            </style>
        """)
        put_text(f"❌ Oops! Wrong guess. The number was {secret_number}. Try again!")

# Running the game
start_server(number_guessing_game, port=8080)
```
Explanation:

`set_env(title="Number Guessing Game")` This sets the title of the web page, which appears on the browser tab.

`The random.randint(1, 10)` function generates a random integer between the given range (1 to 10 in this case), which serves as the secret number for the game.

`put_html("<h2>Welcome to the Number Guessing Game!</h2>")` This uses put_html() to insert an HTML <h2> heading, making the introduction more visually appealing.

`input("Enter your guess:", type=NUMBER)` Unlike the previous example, this input() function specifies type=NUMBER, ensuring that the user can only enter numeric values.

`<style>` is used to change background colour. The `put_html()` function is used to inject CSS styles dynamically.
If the user guesses correctly, it changes the background to green.
If the guess is incorrect, it changes the background to red.

`start_server(number_guessing_game, port=8080)`This runs the function number_guessing_game() as a PyWebIO web application on port 8080, making it accessible in a web browser.

This is the input page:

![Input page3](/assests/image3.jpeg)

This is the output when guessed number is correct:

![Output page4](/assests/image5.jpeg)

This is the output when guessed number is wrong:

![Output page5](/assests/image4.jpeg)

#### 3. Multiplication table generator

```python
from pywebio.input import input as web_input, NUMBER
from pywebio.output import put_text, put_table, clear
from pywebio import start_server

def generate_table():
    num = web_input("Enter a number to generate its multiplication table:", type=NUMBER)
    
    # Clear previous output
    clear()
    
    put_text(f"Multiplication Table for {num}")
    
    # Generate table data
    table_data = [["Multiplier", "Result"]]
    for i in range(1, 11):
        table_data.append([f"{num} × {i}", num * i])
    
    put_table(table_data)

if __name__ == "__main__":
    start_server(generate_table, port=8080)
```
Explanation: 

Input is imported as `web_input` from `pywebio.input` import input as web_input renames input to web_input to avoid conflicts with Python's built-in input() function.

`clear()` is used to remove any previous output before displaying the new multiplication table.

`put_table()` This function is used to display tabular data in a structured format. The first row `(table_data = [["Multiplier", "Result"]])` serves as the header.

`if __name__ == "__main__":` This ensures the script only runs the web server when executed directly, preventing unintended execution when imported into another script.

Input:

![Input page6](/assests/image7.png)

Output:

![Output page7](/assests/image6.png)

#### 4. Guessing whether the given number is Happy number or not

```python
from pywebio.input import input
from pywebio.output import put_text, put_buttons, clear
from pywebio import start_server
import random

def is_happy_number(n):
    seen = set()
    while n != 1 and n not in seen:
        seen.add(n)
        n = sum(int(digit) ** 2 for digit in str(n))
    return n == 1

def play_game():
    clear()  
    put_markdown(
        "A **Happy Number** is a number that will eventually reache **1** when you keep "
        "replacing it with the sum of the squares of its digits. If it falls into "
        "a repeating cycle that does **not reach 1**, then it is **not a Happy Number**."
    )
    put_markdown(
        "**Example:**\n"
        "- **19** → 1² + 9² = 82\n"
    )
    num = random.randint(1, 1000)  
    put_text(f"The generated number is: {num}")

    def check_answer(choice):
        correct = is_happy_number(num)
        if (choice == "Happy Number" and correct) or (choice == "Not a Happy Number" and not correct):
            put_text("Correct Answer!")
        else:
            put_text(f"Wrong! It is {'Happy Number' if correct else 'Not a Happy Number'}.")

    put_text("Do you think this is a Happy Number?")
    put_buttons(["Happy Number", "Not a Happy Number"], onclick=check_answer)

if __name__ == "__main__":
    start_server(play_game, port=8080)
```
Explanation:

`put_buttons(["Label"], onclick=function_name)` for creating a button. Clicking it runs the function.

`span(result, 'color:blue; font-weight:bold;')` styles output text (making it bold and blue).

`put_markdown()` to display the Happy Number definition.

Input page:

![Input page8](/assests/image8.jpeg)

After choosing answer:

![Output page9](/assests/image9.jpeg)

### Use Cases: Practical Applications

PyWebIO makes web app development much simplier, making it useful in numerous real-life situations. Some of it's practical applications are:

-Interactive Learning Platforms: PyWebIO can be used to develop educational tools and quizzes.

-Data Collection & Surveys: Easily build online forms for collecting user feedback, conducting surveys, and processing responses.

-Prototyping & Rapid Development: Quickly create web interfaces for testing algorithms, machine learning models, or automation scripts without dealing with front-end complexities.

-Games & Fun Applications: Creating interactive games or other engaging applications.

### Conclusion
PyWebIO is a simple yet powerful library that allows developers to build interactive web applications using only Python, without the need of HTML, CSS, or JavaScript. With its simple and straightforward input and output functions, support for interactive UI elements, and integration with other Python modules, PyWebIO makes web development accessible to both beginners and experienced programmers.

Whether you are building educational tools, data collection forms, real-time calculators, or fun applications, PyWebIO provides an efficient and lightweight way to create engaging web experiences. By eliminating the complexities of front-end development, it allows developers to focus entirely on the logic of their applications.

If you're looking for a quick and hassle-free way to build interactive web apps, PyWebIO is definitely worth exploring! 

For further details and advanced usage, refer to the [official PyWebIO documentation](https://pywebio.readthedocs.io/en/latest/).

### References and Further Reading
- [Official PyWebIO documentation](https://pywebio.readthedocs.io/en/latest/)
- [PyWebIO GitHub Repository](https://github.com/pywebio/PyWebIO)
- [Geeksforgeeks](https://www.geeksforgeeks.org/daily-latest-news-webapp-using-pywebio-in-python/)
- [Why PyWebIO Github Repository](https://github.com/pywebio/PyWebIO/wiki/Why-PyWebIO%3F)
