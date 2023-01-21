Okay, so I’ve uploaded here: https://github.com/ne75/p2llvm/releases/tag/v0.6

1. Download the linux one and unzip it into /opt (so that it’s /opt/p2llvm). You might need to run sudo chown $USER /opt
2. Download loadp2 (https://github.com/totalspectrum/loadp2/releases)
3. place the loadp2.linux into /opt/p2llvm/bin and rename it to loadp2

I’ve attached a basic project with a hello world to get you started. 
1. Unzip it anywhere
2. Run make to build
3. Run make load to load

Let me know what does/doesn’t work. Once you can load this, you can do it all :) 


