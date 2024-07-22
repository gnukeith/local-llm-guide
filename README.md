# local-llm-guide
This is a guide on how to set up LLM's locally for OpenWebUI and Brave Browser

This guide will be in two sections

first section is for Open WebUI and the second section is for Brave BYOM



Step 1.

Install Ollama

Linux command: 
curl -fsSL https://ollama.com/install.sh | sh

as for macOS and Windows go to:

https://ollama.com/download

Note: I would also recommend downloading some models before installing Open WebUI 

ollama pull llama3-chatqa:8b

"A model from NVIDIA based on Llama 3 that excels at conversational question answering (QA) and retrieval-augmented generation (RAG)."

In my experience it's been very good for casual conversations :)

Step 3.

Install Open WebUI via docker - Linux

sudo apt-get update




Section 2 Brave BYOM:



Step 1.

Install brave nightly:
https://brave.com/download-nightly/

step 2.

Install Ollama

Linux command: 
curl -fsSL https://ollama.com/install.sh | sh

as for macOS and Windows go to:

https://ollama.com/download

step 3.

Install a model:

using this command: ollama pull modelname

Example:
ollama pull llama3
ollama pull mathstral
ollama pull codegeex4
ollama pull phi3:medium

you can find all the models here:
https://ollama.com/library
