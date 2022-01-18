# Creating Game Servers on AWS EC2 Instances
How I set up and run my own game servers on AWS EC2 Instances.

- [Creating Game Servers on AWS EC2 Instances](#creating-game-servers-on-aws-ec2-instances)
  - [Setting Up Minecraft Server On Linux EC2](#setting-up-minecraft-server-on-linux-ec2)
  - [Setting Up Terraria Server On Linux EC2](#setting-up-terraria-server-on-linux-ec2)

## Setting Up Minecraft Server On Linux EC2
Let's start with an overview. the AWS Linux image doesn't have the newest version of Java, so we need to uninstall the old version and install the newest one ourselves.

List all packages, to determine our Java version  
`sudo yum list installed`

Remove old java version  
`sudo yum remove java-1.7`

Find the most recent stable version of openjdk and download the .rpm file (x86).  
https://openjdk.java.net/projects/jdk/  
https://www.oracle.com/java/technologies/downloads/

copy the link, then run `wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.rpm` to download the .rpm file.

Then run  
`sudo yum localinstall jdk-17_linux-x64_bin.rpm` to install the new version of java

Create folder for minecraft  
`mkdir minecraft_server`  
`cd minecraft_server`

Go to the minecraft server download page [here](https://www.minecraft.net/en-us/download/server) and copy the link for the latest .jar file At the time of writing this, current version is 1.13  
`wget https://launcher.mojang.com/mc/game/1.13/server/d0caafb8438ebd206f99930cfaecfa6c9a13dca0/server.jar`

If you cannot use wget, you'll need to download it locally to your machine and then use pscp (PuTTY scp command) to copy the file to the remote machine.

Run minecraft server without user interface  
`java -jar server.jar nogui`

When you run the command for the first time, it will create the files and folders and then fail to start. type in `nano eula.txt` and change `false` to `true`, then rerun the java command.

## Setting Up Terraria Server On Linux EC2
First step, we want to download a library that allows us to use mono.
Mono is an open implementation of Microsoft's .NET framework. This means that if an application is built on that framework, it can be run through mono. This allows us to run specific `.exe` files in linux environments.

This was the only website I could find that had the `libpng15-1.5.28-2.fc26.x86_64.rpm` file ([link](http://archives.fedoraproject.org/pub/archive/fedora/linux/releases/26/Everything/x86_64/os/Packages/l/libpng15-1.5.28-2.fc26.x86_64.rpm)). If the link doesn't work anymore google for a new one.  
`wget archives.fedoraproject.org/pub/archive/fedora/linux/releases/26/Everything/x86_64/os/Packages/l/libpng15-1.5.28-2.fc26.x86_64.rpm`

Install the library from the download  
`sudo yum install -y libpng15-1.5.28-2.fc26.x86_64.rpm`

Remove the download  
`sudo rm libpng15-1.5.28-2.fc26.x86_64.rpm`

Now that we have the library,  we can install mono  
`sudo yum install mono`

After mono is correctly installed, we need to download the tshock release of terraria. [TShock](https://github.com/Pryaxis/TShock) is server software offering great customization and versatility for terraria servers.
https://github.com/Pryaxis/TShock/releases

At the current time of writing, the most recent release is tshock_4.3.25.  
`wget https://github.com/Pryaxis/TShock/releases/download/v4.3.25/tshock_4.3.25.zip`  

Unzip and create folder called tshock  
`unzip tshock_4.3.25.zip -d tshock/`

Remove tshock zip  
`sudo rm tshock_4.3.25.zip`

Now run your server!  
`cd tshock`  
`mono TerrariaServer.exe`

It will prompt you to choose settings for the world size, max players, etc. Once you choose your options it will start up!
