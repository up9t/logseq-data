- Running local AI is helpful if you want to do some experiments, one of the most popular way to run local AI model in your PC is by using Ollama. If you're running on Fedora, you might have Podman installed as your container management tool. The next thing is to install Ollama inside a container and make it work. But first why do we want to install Ollama inside a container? There are several reasons including you don't want to clutter your system and you want an isolation, using container solves these problems. Let's get started!
-
- First, you need to make sure you have Podman/Docker installed.
-
- ```bash
  sudo dnf install podman
  ```
-
- Then, you need to make sure your Nvidia GPU is working correctly by installing the correct driver [[Add Nvidia Driver in Fedora Linux.]].
-
- After that, install `distrobox`. Distrobox will use Podman and Docker regarding your setup.
-
- ```bash
  sudo dnf install distrobox
  ```
-
- Then, create a container with distrobox.
-
- ```bash
  distrobox create --name ai --nvidia --no-entry --home ~/Distrobox/ai
  ```
- That command will create a container named `ai` with `nvidia` support, `--no-entry` means not to create a desktop shortcut, and finally `--home` is the home directory in the container mapped to the host, in this case `~/Distrobox/ai` is the directory in host, that is the home directory in the container.
-
- Enter the created container.
-
- ```bash
  distrobox enter ai
  ```
-
- Now, you should be inside a container. While inside it install Ollama: https://ollama.com/download/linux.
-
- ```bash
  # install zstd first
  sudo dnf install zstd
  
  curl -fsSL https://ollama.com/install.sh | sh
  
  ```
-
- Turn on ollama server:
-
- ```bash
  ollama serve
  ```
-
- Now we run Google's GEMMA 4 Model:
-
- ```bash
  ollama run hf.co/unsloth/gemma-4-E2B-it-GGUF:UD-Q4_K_XL
  ```
-
-
-
-
- ## References
-
- https://copr.fedorainfracloud.org/coprs/g/ai-ml/nvidia-container-toolkit/
-
-
-
- #linux #gpu #nvidia #ai #local #container
-
-