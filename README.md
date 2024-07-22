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

Check if ollama is running:
curl http://127.0.0.1:11434/api/chat


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

**If you are on AMD hardware everything should be good to go**


**If you are on NVIDIA hardware there's more commands you need to do.**


```
sudo apt-get update
```

```
sudo apt-get install -y nvidia-container-toolkit
```

```
sudo systemctl restart docker
```

```
sudo docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

Two notes

note 1: this will make the docker run with your host network which in my experience works way better
note 2: This will require an account, if you are not into that you can use:


How to keep your Docker up-to-date:
docker run --rm --volume /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --run-once open-webui

In case you want to update your local Docker installation to the latest version, you can do it with [Watchtower](https://containrrr.dev/watchtower/).

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
```
ollama pull llama3
```
```
ollama pull mathstral
```
ollama pull codegeex4
```
ollama pull phi3:medium
```

you can find all the models here:
https://ollama.com/library
