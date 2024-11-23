## Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework

### AIM:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### PROBLEM STATEMENT:
Building a user-friendly application that allows seamless interaction with a large language model (LLM) is challenging without requiring specialized API keys or external resources. This project addresses the need for an accessible, open-source solution to implement such applications using pre-trained models and the Gradio Blocks framework.

### DESIGN STEPS:

#### STEP 1: Import Required Libraries
Install and import libraries like Gradio for UI design and Transformers for using open-source pre-trained models.
Ensure all dependencies are installed and configured.

#### STEP 2: Load a Pre-Trained Model
Use a model like GPT-2 or DialoGPT from the Hugging Face Model Hub.
Initialize the model using the pipeline API to simplify interaction

#### STEP 3: Define the Application Workflow
Create a function to process user input, send it to the model, and return the response.
Design the user interface using Gradio Blocks, adding input/output components and interactivity.

#### STEP 4: Launch and Deploy
Use demo.launch() to host the application locally.
Optionally deploy it to cloud platforms for public access.

### PROGRAM:
```py
import gradio as gr
from transformers import pipeline

# Load a pre-trained LLM from Hugging Face
chat_model = pipeline("text-generation", model="gpt2", max_length=200)

# Define the function to interact with the LLM
def chat_with_llm(user_input):
    try:
        # Generate a response
        response = chat_model(user_input, max_length=150, num_return_sequences=1)
        return response[0]['generated_text']
    except Exception as e:
        return f"Error: {str(e)}"

# Design the Gradio Blocks UI
with gr.Blocks() as demo:
    gr.Markdown("# 🤖 Chat with LLM")
    with gr.Row():
        with gr.Column():
            user_input = gr.Textbox(label="Enter your query:", placeholder="Type your message here...")
            submit_button = gr.Button("Submit")
        with gr.Column():
            response_output = gr.Textbox(label="LLM Response:", lines=10, interactive=False)
    
    # Add functionality
    submit_button.click(chat_with_llm, inputs=[user_input], outputs=[response_output])

# Run the application
demo.launch()

```
### OUTPUT:
![image](https://github.com/user-attachments/assets/c5ec28ce-85d0-4409-84aa-dbbc14e2047a)

### RESULT:
The "Chat with LLM" application was successfully designed and deployed using the Gradio Blocks framework, allowing seamless user interaction with a large language model.
