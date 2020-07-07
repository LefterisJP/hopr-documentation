---
description: >-
  Get familiar with HOPR by using HOPR Chat in your system using the Developer
  Setup
---

# Developer Setup

This detailed setup will show you how to use **HOPR** by installing **HOPR Chat** on your system using Docker or Nodejs on your computer. In this step-by-step guide, we will download the adequate software, run **HOPR Chat,** and send a message to another user in the **HOPR network,** in the same way the developers of **HOPR Chat** do.

Depending on your device capabilities, pick the method that works best for you. Using Docker is faster than using Nodejs, but has higher hardware and disk space requirements. In the other hand, Nodejs requires a bit more setup, but can be completed by even limited devices.

## Setting up your machine for HOPR Chat

### Using Docker

The Docker setup allows you quickly get started with **HOPR Chat** without having to download any other software requirements in your machine. This allows you to quickly get started using the system, but has some hardware requirements to be aware of.

To use Docker, you will need a device that supports hardware-level virtualisation: VT-x for Intel-based PCs and AMD-V for AMD processors. Most of the Mac and Linux machines support it out of the box,  but for PC you will need to make sure it's turned on and perhaps enable it in the BIOS settings. It will be different for different BIOS, just look for VT-x / AMD-V switch.

Additionally, ensure you have enough memory \(e.g. 2 GB\) and disk space \(e.g. 1 GB\) before starting.

#### How to Install Docker

Before doing anything else, you need to install [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac/) on your machine. Docker is natively supported in MacOS/Linux, and will prompt you with any additional requirements, depending on your operating system. Windows 10 will require different configurations depending on your version \(Home or Pro/Enterprise\). Depending on your setup, you might need to follow additional steps to ensure your computer works properly with Docker.

{% tabs %}
{% tab title="Linux" %}
Depending of your distribution, please follow the official guidelines for how to install and run Docker on your workstation.

* [Installing Docker in Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
* [Installing Docker in Fedora](https://docs.docker.com/engine/install/fedora/)
* [Installing Docker in Debian](https://docs.docker.com/engine/install/debian/)
* [Installing Docker in CentOS](https://docs.docker.com/engine/install/centos/)
{% endtab %}

{% tab title="macOS" %}
1. Visit [Docker Hub ](https://hub.docker.com/editions/community/docker-ce-desktop-mac/)and download **Docker Desktop** to your computer.
2. Follow the wizard steps to ensure Docker is installed.
3. Ensure the installation was successful by running `docker ps` in your terminal.
{% endtab %}

{% tab title="Windows 10 Home" %}
1. Go to [Docker Hub](https://docs.docker.com/toolbox/overview/) to download **Docker Toolbox** in your computer.
2. Follow-up the wizard steps to ensure Docker is installed.
3. Ensure the installation was successful by running `docker ps`
{% endtab %}

{% tab title="Windows 10 Pro" %}
1. Go to [Docker ](https://www.docker.com/products/docker-desktop)and download **Docker Desktop** in your computer.
2. Follow-up the wizard steps to ensure Docker is installed.
3. Ensure the installation was successful by running `docker ps`
{% endtab %}
{% endtabs %}

#### Downloading HOPR Chat image from Docker Hub

Once Docker is up and running, you need to download a valid **HOPR Chat** Docker Image. To do so, run `docker pull hopr/chat` from your terminal. This process may take some time depending on your internet connection, as it will download around `0.5 GB` from our [Docker Hub Registry](https://hub.docker.com/r/hopr/chat).

![Currently HOPR Chat is about ~0.5 GB, please be patient.](../../.gitbook/assets/docker_install_macos.gif)

To ensure your machine has successfully downloaded **HOPR Chat,** run `docker images`.You will be shown the **HOPR Chat** image being installed locally, ready to be run.

![HOPR Chat distributed as a Docker image](../../.gitbook/assets/docker_images.gif)

### Using Nodejs

The Nodejs setup allows you to run **HOPR Chat** as a Nodejs application, ensuring your experience is a close as to the developer’s have when developing **HOPR Chat** and the **HOPR Core** protocol. Nodejs might require further software installation, but is able to be run in less hardware demanding machines, while taking considerable less space in comparison to Docker \(i.e. 50mb\).

#### How to Install Nodejs using NVM

To use Nodejs, we recommend installing [nvm](https://github.com/nvm-sh/nvm), a Nodejs version manager. This ensures we can install and uninstall as many versions of Nodejs as needed. Furthermore, it will help you installing any additional requirements \(if any\) for running Nodejs. In case of Windows, you will need [nvm-windows](https://github.com/coreybutler/nvm-windows), which is its PC equivalent.

To install nvm in Linux or macos, please follow the instructions in their [GitHub website](https://github.com/nvm-sh/nvm), or run any of the following commands in your terminal instead \(will use nvm `v0.35.3`\) depending on whether you have `curl` or `wget` in your system. 

{% tabs %}
{% tab title="cURL" %}
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
{% endtab %}

{% tab title="Wget" %}
```text
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
{% endtab %}
{% endtabs %}

For Windows, download nvm-windows latest binary available in their [releases](https://github.com/coreybutler/nvm-windows/releases) page.

**Installing Nodejs**

After you have downloaded and setup nvm in your machine \(run `nvm ls` to ensure everything is in place\), now you need to install a specific version of Nodejs before running **HOPR Chat**.

At the time of writing, **HOPR Chat** runs on Nodejs `>v12`. Specifically, **HOPR Chat** has been developed and tested in `v12.9.1`, so in case you run on any issues with **HOPR Chat,**  try switch to `v12.9.1` to see if those issues disappear.

To install Nodejs with nvm, run the following in your Terminal, Bash or Powershell.

```text
$ nvm install v12.9.1
$ nvm use v12.9.1
```

If everything was done properly, you can run `node --version` to see your current `node` version, alongside running basic commands as shown when running simply `node` in your terminal.

![](../../.gitbook/assets/node.gif)

## **Running HOPR Chat** 

### **Using Docker**

To run **HOPR Chat** via Docker**,** you need to copy and paste the following command. You can replace `switzerland` for anything else, but ensure to always use the same password as this will be used by **HOPR Chat**. Furthermore, you can also use your own [Infura](https://infura.io/) credentials instead of the ones provided here, but ensure you use the Kovan provider, as currently **HOPR Core** Ethereum contracts are only deployed there.

#### macOS/Linux commands

{% tabs %}
{% tab title="ch-t-01" %}
```text
docker run -v $(pwd)/db:/app/db \
-e HOST_IPV4=0.0.0.0:9091 \
-e BOOTSTRAP_SERVERS=/dns4/ch-test-01.hoprnet.io/tcp/9091/p2p/16Uiu2HAm5WUS1kv8p3uiSgZmz2uh427qr8jJZ8jrFCePHATaVgz2 \
-e ETHEREUM_PROVIDER=wss://kovan.infura.io/ws/v3/f7240372c1b442a6885ce9bb825ebc36 \
-p 9091:9091 -it hopr/chat -p switzerland
```
{% endtab %}

{% tab title="ch-t-02" %}
```text
docker run -v $(pwd)/db:/app/db \
-e HOST_IPV4=0.0.0.0:9091 \
-e BOOTSTRAP_SERVERS=/dns4/ch-test-02.hoprnet.io/tcp/9091/p2p/16Uiu2HAmRD7iEEopoiHWz7NpsM4wwSc5yWpdSX3esb3kYkJNY1yn \
-e ETHEREUM_PROVIDER=wss://kovan.infura.io/ws/v3/f7240372c1b442a6885ce9bb825ebc36 \
-p 9091:9091 -it hopr/chat -p switzerland
```
{% endtab %}
{% endtabs %}

#### Windows commands

{% tabs %}
{% tab title="ch-t-01" %}
```text
docker run -v %cd%/db:/app/db ^ 
-e HOST_IPV4=0.0.0.0:9091 ^ 
-e BOOTSTRAP_SERVERS=/dns4/ch-test-01.hoprnet.io/tcp/9091/p2p/16Uiu2HAm5WUS1kv8p3uiSgZmz2uh427qr8jJZ8jrFCePHATaVgz2 ^ 
-e ETHEREUM_PROVIDER=wss://kovan.infura.io/ws/v3/f7240372c1b442a6885ce9bb825ebc36 ^ 
-p 9091:9091 -it hopr/chat -p switzerland
```
{% endtab %}

{% tab title="ch-t-02" %}
```
docker run -v %cd%/db:/app/db ^ 
-e HOST_IPV4=0.0.0.0:9091 ^ 
-e BOOTSTRAP_SERVERS=/dns4/ch-test-02.hoprnet.io/tcp/9091/p2p/16Uiu2HAmRD7iEEopoiHWz7NpsM4wwSc5yWpdSX3esb3kYkJNY1yn ^ 
-e ETHEREUM_PROVIDER=wss://kovan.infura.io/ws/v3/f7240372c1b442a6885ce9bb825ebc36 ^ 
-p 9091:9091 -it hopr/chat -p switzerland
```
{% endtab %}
{% endtabs %}

You will be welcomed by the following message.

In case you see an `Unable to connect to Bootstrap node` message, use other bootstrap nodes \(marked as `ch-t-01` and `ch-t-02`\). You can learn more about Bootstrap Nodes in our page.

{% page-ref page="bootstrap-nodes.md" %}

After running any of these commands, you will be welcomed by **HOPR Chat**’s introductory screen which provides you with further instructions.

![](../../.gitbook/assets/hopr.gif)

{% hint style="info" %}
Depending on your configuration and version of **HOPR Chat**, you might need to fund your **HOPR Chat** account with some tokens. Please follow our “**Funding your account**” Page for those cases.
{% endhint %}

{% page-ref page="funding-account.md" %}

### Using Nodejs

To run **HOPR Chat** via Nodejs**,** you need to download our pre-compiled binary for each version. You can find these binaries in our [Releases](https://github.com/hoprnet/hopr-core/releases) page inside a zip file. Version `1.1.4-dev` used for generating this documentation is available [here](https://github.com/hoprnet/hopr-core/releases/tag/1.1.4-dev.64c3c2b).

![Please select the correct distribution for your operating system.](../../.gitbook/assets/image%20%288%29.png)

These files have **HOPR Chat** pre-configured and compiled to work in your system. Click on the executable file inside that folder to see **HOPR Chat** up and running. Depending on your distribution, this file might be different.

{% tabs %}
{% tab title="Linux" %}
On Linux, double-click or execute the file named `hopr-chat.sh`. Behind the scenes, it will run `node index.js` from the directory you are currently working, ensuring it has the configuration settings distributed with the binary.
{% endtab %}

{% tab title="macOS" %}
On macOS, double-click or execute the file named `hopr-chat.command`. Behind the scenes, it will run `node index.js` from the directory you are currently working, ensuring it has the configuration settings distributed with the binary.
{% endtab %}

{% tab title="Windows 10" %}
On Windows, double-click the file named `hopr-chat.bat` or right-click and select the option “Run with Powershell”. A prompt from Windows Defender might request your permission to run it. Behind the scenes, it will run `node index.js` from the directory you are currently working, ensuring it has the configuration settings distributed with the binary.
{% endtab %}
{% endtabs %}

As soon as you double-click in the executable file, you will be welcomed by the **HOPR Chat** initial message, which might look different depending on your OS. A password will be required, and every time you run **HOPR Chat** it will prompt it again.

{% hint style="info" %}
Since **HOPR Chat** is being distributed as a Nodejs binary, the included pre-compiled binary [might trigger some prompts in macos](https://docs.hoprnet.io/home/getting-started/hopr-chat/troubleshooting) which you will need to accept and provided access through. To work around these issues, please see our Troubleshooting guide under the **HOPR Chat** page in the tutorial.
{% endhint %}

{% page-ref page="troubleshooting.md" %}

## Sending a HOPR message

With **HOPR Chat** up and running, you can now send messages to any connected nodes in the network. You can either have a friend send you their address, or you can also start another **HOPR Chat** instance. You can also find **HOPR Chat** users in our [Telegram](https://t.me/hoprnet).

{% hint style="info" %}
In case you are using a version of **HOPR Chat** with **HOPR Core** `<v0.6.10`, please ensure you have enough **HOPR Tokens** to send and receive messages.
{% endhint %}

Now, let's find some nodes to talk to. To do this, run `crawl`, which will show you other users that are connected to the **HOPR Network** and are available to chat.

![The crawl command will show you other connected nodes.](../../.gitbook/assets/running_hopr_chat_and_crawling.gif)

To talk to other users, copy another connected user address and send a message to them with the `send` command. This will look something like: `send 16Uiu2HAmCtWxx3Ky3ZjtWj1whkezdRvMAYKU9f57CRPj2FkPtWsD`

**HOPR Chat** will then prompt you for a message to send.

![Your message will be sent privately through the HOPR network](../../.gitbook/assets/running_hopr_chat_and_sending.gif)

Congratulations! You have communicated with another node using a privacy-preserving decentralised protocol. **HOPR Chat** is just a proof of concept right now, but you can already see the capabilities of the protocol. Click next to learn about **Bootstrap Nodes,** or go back to see the general introduction about **HOPR Chat.**
