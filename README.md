
# 🚀 Zero-Cost @gensynai CodeAssist Setup Guide <img width="530" height="213" alt="image" src="https://github.com/user-attachments/assets/a51a1f2b-03d1-4c50-97e6-212c64ad7342" />

If you couldn’t join Gensyn due to server costs, this guide is for you!  
We’ll build a **completely free environment** and run a CodeAssist worker to collect **Participation** efficiently.


## What We’ll Do

- Set up WSL or a free cloud environment  
- Install required system tools  
- Install Docker + Python + UV  
- Run CodeAssist Worker 24/7 at zero cost  

## [1/15] Set Up WSL or Free VPS

You can run this guide on:  
✅ Your own PC  
✅ Any free cloud server  
✅ Windows WSL2 (recommended)

**WSL Setup (Windows):**  
Enable WSL2 → reboot → install Ubuntu 22.04 from Microsoft Store.  
MacOS/Linux? Just open your terminal and continue.

## [2/15] Update Packages

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git curl wget nano htop unzip jq build-essential pkg-config libleveldb-dev libssl-dev


[3/15] Remove Old Docker Packages

for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do
  sudo apt-get remove -y $pkg
done


[4/15] Install Official Docker

sudo apt-get update -y
sudo apt-get install -y ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo docker run --rm hello-world


[5/15] Install Python 3 & Essentials

sudo apt install -y python3 python3-pip python3-venv
python3 --version


[6/15] Install UV

curl -LsSf https://astral.sh/uv/install.sh | sh
export PATH="$HOME/.local/bin:$PATH"
uv --version


[7/15] Clone CodeAssist Repository

git clone https://github.com/gensyn-ai/codeassist.git
cd codeassist


[8/15] Install Dependencies

uv sync


[9/15] Start the Worker

uv run run.py

Provide Worker Name & HF Token if requested.
Look for “Job received” to confirm connection 🎉
![image](https://github.com/user-attachments/assets/02a2c677-fdbc-4646-9683-32d4c4403113)

⸻

[10/15] Keep Worker Running in Background

screen -S gensyn
cd ~/codeassist
uv run run.py

Detach: CTRL + A + D


[11/15] How to Collect Participation
	•	Keep worker online
	•	Run test queries in CodeAssist
	•	High uptime = faster Participation


[12/15] Check Performance

htop


[13/15] Add 4GB Swap (Optional)

sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo "/swapfile none swap sw 0 0" | sudo tee -a /etc/fstab


[14/15] View Worker Logs

Docker:

docker logs -f codeassist

UV:

tail -f logs/worker.log


[15/15] Update Your Worker

cd ~/codeassist
git pull
uv sync
sudo systemctl restart docker
![image](https://github.com/user-attachments/assets/3c547aef-c59f-442e-b594-897d9c8b71b4)

✅ Your CodeAssist worker is now running 24/7, collecting Participation at zero cost.
Welcome to Gensyn 🚀






Bunu yapmamı ister misin?
