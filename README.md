# learnllama2

I tried multiple openai API implementation(eg: [gpt4all](https://github.com/nomic-ai/gpt4all)) for llama2, [llama-cpp-python] provides the best compatiblity with openai API.

llama-cpp-python offers a web server which aims to act as a drop-in replacement for the OpenAI API. This allows you to use llama.cpp compatible models with any OpenAI compatible client (language libraries, services, etc).

## Setup LLaMa2 + openai API endpoint on Ubuntu 22.04 without GPU
You are experience slow response with 8G memory. You can get good performance with 16G memory

### Create VM on Azure (optional)
Create VM with Ubuntu Minimal 22.04 LTS, Standard D4s v3 (4 vcpus, 16 GiB memory) prefered.

### Install llama-cpp-python[server]

```sh
sudo apt-get install pip
pip install llama-cpp-python[server]
```

### Download the model
You may choose the model from https://huggingface.co/TheBloke/Llama-2-7b-Chat-GGUF.

```sh
wget https://huggingface.co/TheBloke/Llama-2-7b-Chat-GGUF/resolve/main/llama-2-7b-chat.Q4_K_M.gguf
```

### Launch llama-cpp-python server

```
export HOST=0.0.0.0
export PORT=8080
python3 -m llama_cpp.server --model `pwd`/llama-2-7b-chat/llama-2-7b-chat.Q4_K_M.gguf &
```

### Verify the endpoint.

llama-cpp-python provides implementation of [openai](https://platform.openai.com/docs/guides/gpt) interface. Just replace `https://api.openai.com` with `http://{yourip}:8080`, then you are good to go.

For example, the completions API:

```
https://api.openai.com/v1/completions
```

```
http://{yourip}:8080/v1/completions
```
