# transcrobialGAN
GAN art project for Danino lab 

## Setting up Torch for OSX 

Run all commands in Terminal

1. Install Homebrew
2. Install Torch 

First, install Torch in home folder by running the commands below separately
```
git clone https://github.com/torch/distro.git ~/torch --recursive
cd ~/torch; bash install-deps;
./install.sh
```
Next, return to home directory and create a .profile file

```
cd ..
touch .profile
```

Open the .profile file using a text editor and paste the following line (replace username)
```
. /Users/myusername/torch/install/bin/torch-activate
```
3. Install dependencies 
Install torch packages display and nngraph required for CDGAN script
```
luarocks install nngraph
luarocks install https://raw.githubusercontent.com/szym/display/master/display-scm-0.rockspec
```

With homebrew installed, install dependencies for the image preprocessing with linux tools
```
brew install coreutils # for gwc
brew install findutils # for gfind
```
3. Clone art-DCGAN repo

Clone github repo
```
https://github.com/robbiebarrat/art-DCGAN/
cd art-DCGAN
```
May need to run following command in case of unauthenticated git protocol error

```
git config --global url."https://".insteadOf git://
```
4. Scrape, train & generate

If not using GPU, should put 0 for all GPU options in commands.
Also, always run .profile command at the beginning (before first training attempt) to set up env! 
Example below:

```
source ~/.profile
python3 genre-scraper.py --genre flower-painting --output_dir flowers
DATA_ROOT=graffiti dataset=folder ndf=50 ngf=150 niter=200 gpu=0 saveIter=200 th main.lua
net=checkpoints/experiment1_200_net_G.t7 th generate.lua
```
To see display, run following and go to local server in browser
```
th -ldisplay.start
```
