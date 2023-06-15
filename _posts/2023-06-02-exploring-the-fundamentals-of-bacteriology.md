---
layout: post
title:  Exploring the Fundamentals of Bacteriology
date:   2023-06-02 18:00:00
description: Creating a Customizable Glossary Application with Python and Tkinter 
---
As an educator tasked with introducing a comprehensive bacteriology course, I have come to appreciate the importance of mastering the foundational concepts. While the process of learning definitions may seem tedious, it is crucial for aspiring biologists to develop the precision and fluency necessary for effective communication in their field.

Embarking on the journey of deepening one's knowledge in bacteriology is akin to traversing a path riddled with obstacles, yet brimming with intellectual rewards.

In order to facilitate the learning process, I decided to employ the power of technology. Leveraging the versatility of the Python programming language, I developed a sophisticated glossary application with the aid of Tkinter. This innovative tool not only enables students to access a comprehensive list of terms but also offers the convenience of customization in various languages. By employing the model-view-controller (MVC) design pattern, I aimed to optimize the functionality of the application, although there is room for further improvement in this aspect.

## The Model-View-Controller (MVC) Design

To delve deeper into the concept of the MVC design pattern, let us turn to the renowned online encyclopedia, Wikipedia. According to their definition, the MVC design pattern is a software architectural pattern that separates the application logic into three interconnected components: the model, the view, and the controller [1](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller). This separation allows for a clear division of responsibilities, enhancing the overall organization and maintainability of the application.

<br>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mvc.png" title="Diagram of model-view-controller software design pattern" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Diagram of MVC pattern.
</div>

<br>

## Utilizing the deep-translator Package

In order to enhance the language localization capabilities of the glossary application, the deep-translator package proves to be an invaluable tool. By leveraging this package, developers gain access to a variety of translation features. With the ability to install the version 1.11.1 of [deep-translator](https://pypi.org/project/deep-translator/), users can take advantage of its latest functionalities and ensure optimal performance.

## Building a Bacteriology Glossary Application in Python

In the world of bacteriology, understanding and effectively communicating key concepts is paramount. To aid in this pursuit, I have developed a Python glossary application that empowers users to explore and comprehend fundamental terminologies.

### 1. Create Application Structure

```txt
.
└── mydirectory
    ├── GlossaryApp
    │   ├── __init__.py
    │   ├── controller.py
    │   ├── model.py
    │   ├── views.py
    ├── glossary.json
    ├── run.py
```

To ensure a well-organized project, we have established a structured directory for the application. The layout consists of the GlossaryApp package, housing essential files such as `__init__.py`, `controller.py`, `model.py`, and `views.py`. Additionally, a `glossary.json` file has been created to store the relevant terminologies and their definitions.

### 2. Create the JSON file

The `glossary.json` file acts as a data repository for the glossary application. It follows a common data format, providing a comprehensive list of terms along with their corresponding definitions.

```json
{
    "term1":{
        "fr-term": "Anticodon",
        "fr-def":"Séquence de trois nucléotides d'un ARNt (ARN de transfert) complémentaire du codon présent sur l'ARNm"
    },
    "term2":{
        "fr-term": "ARN messager (ARNm)",
        "fr-def": "Synthétisé au contact de l'ADN, transférant l'information génétique aux ribosomes"
    },
    "term3":{
        "fr-term": "ARN de transfert (ARNt)",
        "fr-def": "Lie spécifiquement un acide aminé (aminoacyl-ARNt) et le transfère au ribosome"
    }
}
```

<br>

### 3. Create Init File

The `__init__.py` file serves a crucial role in making the GlossaryApp package recognizable as a Python package. By including the `__all__` variable, we ensure that the package components, such as the controller, models, and views, are accessible to other modules.

```python
__all__ = ['controller', 'models', 'views']

```

<br>

### 4. Create Controller File

The `controller.py` file encompasses the logic that manipulates user input and interacts with the model. It utilizes the Tkinter library to create the main application window. The controller establishes various widgets, including a dropdown menu for term selection, a quit button, and labels for term selection and definition display. The functionality of showing definitions and translating them to English is implemented using the deep-translator package.

```python
import tkinter as tk
from tkinter import ttk
from deep_translator import GoogleTranslator

class MainApp(tk.Tk):

    def __init__(self, data):
        super().__init__()
        self.geometry("500x500")
        self.title("Glossary-App")
        self.configure(bg="#C2FCEE")
        self.resizable(False, False)
        self.data = data
        # Extract fr-term values from the data data
        self.terms = [values['fr-term'] for values in self.data.values()]
        self.setup()

    def setup(self):
        self.widgets()
        self.layouts()

    def widgets(self):
        # Create a dropdown menu for term selection
        self.term_combobox = ttk.Combobox(values=self.terms)
        # Create a quit button to exit the application
        self.quit_btn = tk.Button(text="Quit", command=self.quit)
        # Create a label for term selection
        self.term_label = tk.Label(text="Select a term")
        # Create a button to show the definition
        self.show_button = tk.Button(text="Show Definition", command=self.show_definition)
        # Create a button to translate the definition to English
        self.translate_button = tk.Button(text="Translate to English", command=self.translate_definition)
        # Create a label for the definition
        self.definition_label = tk.Label(text="", wraplength=400)

    def layouts(self):
        '''organize the widgets in block
        '''
        self.term_combobox.pack()
        self.term_label.pack()
        self.show_button.pack()
        self.translate_button.pack()
        self.definition_label.pack()
        self.quit_btn.pack()

    def show_definition(self):
        ''' select the term from a list
        return a error message in case of missing definition
        '''
        selected_fr_term = self.term_combobox.get()
        selected_term = next((term for term, values in self.data.items() if values['fr-term'] == selected_fr_term), None)
        if selected_term:
            definition = self.data[selected_term]['fr-def']
            self.definition_label.configure(text=definition)
        else:
            self.definition_label.configure(text="Definition not found for selected term.")

    def translate_definition(self):
        selected_fr_term = self.term_combobox.get()
        selected_term = next((term for term, values in self.data.items() if values['fr-term'] == selected_fr_term), None)
        if selected_term:
            definition = self.data[selected_term]['fr-def']
            translation = GoogleTranslator(source='fr', target='en').translate(definition)
            self.definition_label.configure(text=translation)
        else:
            self.definition_label.configure(text="Definition not found for selected term.")

```

<br>

### 5. Create Model File

The `model.py` file focuses on loading and parsing the `glossary.json` file. It utilizes the JSON module to read the data and store it in the `data` variable, which is then imported into the views file.

```python
import json

# Load JSON from a file with the correct encoding of your computer
with open('glossary.json', 'r', encoding='utf-8') as file:
    json_doc = file.read()

# Parse JSON
# the data variable is going to be import in the views file
data = json.loads(json_doc)

```

<br>

### 6. Create Views File

The `views.py` file imports the MainApp class from the controller and the data from the model. It instantiates the MainApp class, passing the data as a parameter. Finally, the main event loop, `mainloop()`, is utilized to run the application.

```python
from .controller import MainApp
from .models import data


def app():
    app = MainApp(data)
    app.mainloop()

```

<br>

### 7. Create Run File

The `run.py` file serves as the entry point for executing the application. It imports the `app()` function from the views file and runs it if the file is being executed as the main script. Additionally, the `if __name__ == "__main__"` idiom enables code execution specific to running the file as a script.

```python
from GlossaryApp.views import app

if __name__ == "__main__":
    app()

```

<br>

## Conclusion

With the completion of the code structure, we have laid the foundation for a powerful and user-friendly Bacteriology Glossary Application. By implementing the MVC design pattern, leveraging the Tkinter library, and utilizing the deep-translator package, we have created a versatile tool that facilitates term selection, definition display, and translation. Through continued refinement and expansion, this application holds immense potential for enhancing the learning experience in the field of bacteriology.

Please note: To run the application successfully, ensure that the deep-translator package version 1.11.1 is installed.

### Images Attribution

* Image [gradient-ui-ux-bg](https://www.freepik.com/free-vector/gradient-ui-ux-background_17349978.htm#query=application&position=45&from_view=search&track=sph) by Freepik.
* Image [by upklyak](https://www.freepik.com/free-vector/button-press-isometric-set-vector-isolated-illustration_12089298.htm#query=data%20base&position=39&from_view=search&track=ais) on Freepik.
* Image [by upklyak](https://www.freepik.com/free-vector/man-looking-window-rain-city-street-vector-cartoon-illustration-thunderstorm-with-lightning-town-with-houses-road-person-standing-inside-home-rainy-night_23639559.htm#query=views&position=25&from_view=search&track=sph) on Freepik.
