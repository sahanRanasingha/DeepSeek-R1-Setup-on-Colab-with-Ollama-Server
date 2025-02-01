
# DeepSeek R1 Setup on Google Colab using Ollama Server

This guide will walk you through the steps to set up and run the **DeepSeek R1** model on Google Colab using the **Ollama server**. Additionally, you’ll learn how to create a **Gradio UI** to interact with the model in a user-friendly way.

---

## Prerequisites
- A Google account (to access Google Drive and Google Colab).
- Basic familiarity with Google Colab and terminal commands.

---

## Step 1: Create a New Folder in Google Drive
1. Go to [Google Drive](https://drive.google.com) and log in.
2. Click on the **+ New** button and select **Folder**.
3. Name the folder (e.g., `DeepSeek-R1-Project`).

---

## Step 2: Create a Google Colab Notebook
1. Open the folder you just created.
2. Right-click inside the folder, select **More**, and then choose **Google Colaboratory**.
3. A new Colab notebook will be created. Name it (e.g., `DeepSeek-R1-Notebook`).

---

## Important: Enable GPU/TPU for Better Performance
1. To improve the model's performance, you can enable GPU or TPU:
   - Go to **Runtime > Change runtime type**.
   - Under **Hardware accelerator**, select **GPU** or **TPU**.
   - Click **Save** and restart the notebook.

---

## Step 3: Install Required Libraries
1. In the Colab notebook, paste the following commands to install the necessary libraries:

   ```python
   !pip install langchain
   !pip install langchain-core
   !pip install langchain-community
   !pip install colab-xterm
   ```

2. Run the cells to install the libraries.

---

## Step 4: Load Colab-Xterm and Open a Terminal
1. Paste the following commands to load `colab-xterm` and open a terminal:

   ```python
   %load_ext colabxterm
   %xterm
   ```

2. A terminal will open in a new tab within Colab.

---

## Step 5: Install Ollama
1. In the terminal, run the following command to install Ollama:

   ```bash
   curl -fsSL https://ollama.com/install.sh | sh
   ```

2. Wait for the installation to complete.

---

## Step 6: Start Ollama Server and Run DeepSeek R1
1. In the terminal, start the Ollama server and load the DeepSeek R1 model by running the following commands:

   ```bash
   ollama serve &
   ```
   ```bash
   ollama run deepseek-r1:7b
   ```

2. The DeepSeek R1 model will be loaded and ready to use.

---

## Step 7: Add a Gradio UI for Interaction
To make it easier to interact with the DeepSeek R1 model, you can add a **Gradio UI**. Follow these steps:

### Step 7.1: Install Gradio
1. Install the Gradio library by running the following command in a Colab cell:

   ```python
   !pip install gradio
   ```

### Step 7.2: Create a Function to Interact with the Model
1. Define a function that sends user prompts to the DeepSeek R1 model and returns the response. Paste the following code into a Colab cell:

   ```python
   import subprocess

   def query_deepseek_r1(prompt):
       command = f'ollama run deepseek-r1:7b "{prompt}"'
       result = subprocess.run(command, shell=True, capture_output=True, text=True)
       
       return result.stdout
   ```

### Step 7.3: Build the Gradio Interface
1. Create a Gradio interface using the function above. Paste the following code into a Colab cell:

   ```python
   import gradio as gr

   def gradio_interface(prompt):
       response = query_deepseek_r1(prompt)
       return response

   iface = gr.Interface(
       fn=gradio_interface,  
       inputs="text",        
       outputs="text",       
       title="DeepSeek R1 Chatbot",  
       description="Ask anything to the DeepSeek R1 model!"
   )

   iface.launch(share=True)
   ```

2. Run the cell. Gradio will generate a public link to your UI.

### Step 7.4: Interact with the Model via Gradio
1. Open the Gradio UI link in your browser.
2. Type a prompt (e.g., "What is the capital of France?") in the input box.
3. Click **Submit**.
4. The DeepSeek R1 model will process the prompt and display the response in the output box.

---

![Gradio UI Example](https://github.com/sahanRanasingha/DeepSeek-R1-Setup-on-Colab-with-Ollama-Server/blob/main/Images/deepSeeek.png?raw=true)

---

## Step 8: Save Your Work
1. To save your Colab notebook, go to **File > Save a copy in Drive**.
2. Choose the folder you created earlier (e.g., `DeepSeek-R1-Project`).

---


## Troubleshooting
- If the Ollama server fails to start, ensure that the installation was successful and try running the commands again.
- If you encounter any issues with the model, check your internet connection and ensure that you have sufficient resources (e.g., GPU/TPU enabled).
- If the Gradio UI does not load, ensure that the `share=True` parameter is set and that your Colab runtime is active.

---

## Conclusion
You have successfully set up and run the **DeepSeek R1** model on Google Colab using the **Ollama server** and added a **Gradio UI** for easy interaction. Enjoy experimenting with the model!

---

If you have any questions or run into issues, let me know! 😊
