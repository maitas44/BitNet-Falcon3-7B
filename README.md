https://drive.google.com/drive/folders/1mtVun_v05ffa5i2tRiSU88e3XZa7qBcj?usp=sharing

sudo apt update
sudo apt upgrade -y
sudo apt install python3 python3-pip cmake clang git wget
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

#exit and log again to get conda base running.

sudo apt install lsb-release wget software-properties-common gnupg
sudo bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"

git clone --recursive https://github.com/microsoft/BitNet.git
cd BitNet

conda create -n bitnet-cpp python=3.9
conda activate bitnet-cpp

pip install -r requirements.txt

mkdir models
cd models
mkdir Falcon3-7B-Instruct-1.58bit
cp /mnt/chromeos/MyFiles/Downloads/Falcon3-7B-Instruct-1.58bit/* ~/BitNet/models/Falcon3-7B-Instruct-1.58bit/

cd ~/BitNet/
python setup_env.py --hf-repo tiiuae/Falcon3-7B-Instruct-1.58bit -q i2_s

cd ~/BitNet/
python run_inference.py -m models/Falcon3-7B-Instruct-1.58bit/ggml-model-i2_s.gguf -p "You are a helpful assistant" -cnv
