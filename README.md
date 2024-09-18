import os
import google.generativeai as genai
import gradio as gr

# Configure the API key
genai.configure(api_key="Enter API Key")

# Create the model configuration
generation_config = {
    "temperature": 1,
    "top_p": 0.95,
    "top_k": 64,
    "max_output_tokens": 8192,
    "response_mime_type": "text/plain",
}

# Create the GenerativeModel instance
model = genai.GenerativeModel(
    model_name="gemini-1.5-flash",
    generation_config=generation_config,
)

# Start a chat session
chat_session = model.start_chat(history=[])

# Define the chatbot function for Gradio
def chatbot(user_input):
    # Send user input to the chat session and get AI response
    response = chat_session.send_message(user_input)
    return response.text

# Create a Gradio interface
interface = gr.Interface(
    fn=chatbot,  # Function that Gradio will call
    inputs="text",  # Input type
    outputs="text",  # Output type
    title="AI-Powered Chatbot",
    description="Raj's Chatbot",
)

# Launch the interface
interface.launch()



# interface.launch(share=True)
# we use above line for Public URL
