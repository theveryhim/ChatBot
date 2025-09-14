# ChatBot [![Kaggle](https://kaggle.com/static/images/open-in-kaggle.svg)](https://www.kaggle.com/code/armanyazdani/chatbot)
Our goal here is to design and implement a conversational chatbot based on a Large 
Language Model (LLM) with the ability to preserve and utilize conversation history. Unlike a 
simple chatbot that only responds to the most recent input, our system maintains awareness of the 
entire dialogue context, enabling it to provide more coherent, context-aware, and human-like 
responses. This feature is crucial in creating natural and intelligent interactions where users may 
refer to earlier parts of the conversation.<br> 
*Find detailed explanations of any of the sections in notebook*
<p align="center">
    <img src="figures/1.png" alt="Descriptive Alt Text" class="fit-width-image">
    <figcaption> 7B-size chatbot </figcaption>
</p>

## Context aware chat
- Initialization → Loads model and tokenizer. 
- User Input → Reads message from console. 
- History Update → Maintains all previous exchanges in conversation_history. 
- Context Management → Before generating, the history may be trimmed using manage_context_window. 
- Input Preparation → Combines history + current user input into tokenized format. 
- Response Generation → Calls the model to produce a reply. 
- Decoding → Converts raw tokens to human-readable response. 
- Display + Save → Prints the bot reply and updates history for the next turn.
## Retrieval-Augmented Generation (RAG) 
<p align="center">
    <img src="figures/2.png" alt="Descriptive Alt Text" class="fit-width-image">
    <figcaption> Retrieved data from user's pdf </figcaption>
</p>

- RAG System Initialization
    - initialize rag if possible
    - if PDF exists at PDF PATH then
      - Extract text using 
      - Split into chunks
      - Initialize embedding model
      - Generate embeddings and normalize
      - Create FAISS index 
      - Add embeddings to index
      - Set rag enabled 

-  Information Retrieval Process
    - if rag enabled AND index exists AND chunks not empty then
      - Encode query
      - Search index
      - Format results with reference numbering
      - Return formatted system message
## WebIntegration 
<p align="center">
    <img src="figures/5.png" alt="Descriptive Alt Text" class="fit-width-image">
    <figcaption> Web search sample </figcaption>
</p>

- Preserve original user input for display
- if web search enabled AND needed then
  - search results= searchexa(user input)
  - Update data_state.webdata
## Interactive Game
<p align="center">
    <img src="figures/4.png" alt="Descriptive Alt Text" class="fit-width-image">
    <figcaption> 20Q game view </figcaption>
</p>

- Initialization 
  - Import ValidatorModel. 
  - Instantiate validator_model = ValidatorModel(). 
- Game Start 
  - Prompt the user (or system input) to confirm that the user intends to play. 
- Questioning Phase  
  - Generate a yes/no question about the secret word (e.g., "Is this an animal?"). 
  - Submit the question: validator_model.validate_question(question). 
  - Store the response. 
- Guessing Phase 
  - Use accumulated answers to form a hypothesis about the secret word. 
  - Submit the guess: validator_model.validate_guess(guess). 
  - If correct, terminate with success. 
- Termination 
  - If the model cannot guess correctly within 20 questions, terminate and mark as unsuccessful. 
## User Interface with Gradio
The interface implements a multi-tab architecture with sophisticated state management and real-time monitoring.
<p align="center">
    <img src="figures/3.png" alt="Descriptive Alt Text" class="fit-width-image">
    <figcaption> Tabs and resources </figcaption>
</p>