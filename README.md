# local-llm-guide
This is a guide on how to set up LLM's locally for OpenWebUI and Brave Browser



This guide will be in two sections

**first section is for Open WebUI and the second section is for Brave BYOM**

# Table of Contents

- [Setting Up Open WebUI with Ollama](#setting-up-open-webui-with-ollama)
- [Brave BYOM via Ollama](#brave-byom-via-ollama)
- [Local LLM Setup via LMStudioAI](#local-llm-setup-via-lmstudioai)


# Open WebUI

Step 1.

Install Ollama

Linux command: 
curl -fsSL https://ollama.com/install.sh | sh

as for macOS and Windows go to:

https://ollama.com/download

Check if ollama is running:
http://localhost:11434/

![Ollama runnig](img/ollama_running.jpeg)


Note: I would also recommend downloading some models before installing Open WebUI 

```
ollama pull llama3-chatqa:8b
```

"A model from NVIDIA based on Llama 3 that excels at conversational question answering (QA) and retrieval-augmented generation (RAG)."

In my experience it's been very good for casual conversations :)

Step 3.

Install Open WebUI via docker - Linux

```
sudo apt-get update
```

```
sudo apt-get install ca-certificates curl
```

```
sudo install -m 0755 -d /etc/apt/keyrings
```

```
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```

```
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
   $(. /etc/os-release && echo "$VERSION_CODENAME") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```
sudo apt-get update
```

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

```
sudo docker run hello-world
```

```
(This is just to test if everything went correctly)
```

**Hardware Considerations**


- **AMD Hardware:** You should be good to go.
- **NVIDIA Hardware:** Additional steps are required


```
sudo apt-get update
```

```
sudo apt-get install -y nvidia-container-toolkit
```

```
sudo systemctl restart docker
```

Run Open WebUI
```
sudo docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

**Notes:**

    1. This will make the docker run with your host network, in my experience, works better.

    2. This setup requires an account. If you prefer not to create one, alternatives options are available.

    ```
    sudo docker run -d -p 8080:8080 --name open-webui --network host -e WEBUI_AUTH=False -e OLLAMA_BASE_URL=http://127.0.0.1:11434 ghcr.io/open-webui/open-webui:main
    ```

How to keep your Docker up-to-date:
```
docker run --rm --volume /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --run-once open-webui
```

In case you want to update your local Docker installation to the latest version, you can do it with [Watchtower](https://containrrr.dev/watchtower/).




# Section 2 Brave BYOM:

## Brave BYOM via Ollama

### Step 1: Install Brave Nightly

Download and install Brave Nightly from [https://brave.com/download-nightly/](https://brave.com/download-nightly/).

### Step 2: Install Ollama

For Linux, use the following command:
```
curl -fsSL https://ollama.com/install.sh | sh
```

Check if ollama is running:
http://localhost:11434/
![Ollama runnig](img/ollama_running.jpeg)


**Models examle that you can download**
```
ollama pull mathstral
```
```
ollama pull codegeex4
```
```
ollama pull phi3:medium
```

you can find all the models here:
https://ollama.com/library 

### Step 3: 

connect your model to **Brave**.

Label: Can be anything you want.
Model request name: This is important since we are calling that specific model.
Server endpoint: This is **always the same** for ollama
http://localhost:11434/v1/chat/completions

![Adding model](img/adding_to_brave.jpeg)

## Brave BYOM via LMStudio

### Step 1: Install Brave Nightly

Download and install Brave Nightly from [https://brave.com/download-nightly/](https://brave.com/download-nightly/).

### Step 2: Download LMStudio

1. Download LMStudio from [http://lmstudio.ai](http://lmstudio.ai).

   Open it, search for your preferred models in the top bar, and hit Download. Me and Brave recommend Llama3 8B and Mistral 7B since they don't use much memory but are quite capable. If you are feeling fancy, Phi3-medium is good.

   ![LMStudio Download](img/lstudio_downlaod.png)

### Step 3: Start a Local Server

2. Start a local server in the LMStudio app with your chosen model.

   Click on the ↔️ icon in the left sidebar to open the Local Server panel.

   Select a model to load on the dropdown at the top and hit Start Server (in green). Your chosen model is now running on your device!

   ![LMStudio Server](img/lmstudioserver.png)

### Step 4: Connect Brave to LMStudio

3. Connect Brave to LMStudio.

   In Brave Nightly, go to Settings > Leo and click Add new model. Enter the model request name as it appears in LMStudio’s Local Server panel.

   Set the Server endpoint to [http://localhost:1234/v1/chat/completions](http://localhost:1234/v1/chat/completions).

   Click "Add model" and you're done!

   ![Brave connections](img/bravebyom_connection_lmstudio.png)

Now you're ready to use your local AI model in Brave Nightly.

Access Leo by pressing Ctrl+B (Cmd+B on macOS).

When you click the gear icon in Leo, the new AI model you added will now be listed as one of your options.

<p align="center">
  <img src="img/selecting_model_lmstudio.png" alt="BYOM choose model">
</p>