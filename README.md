# SimpleAndroidProject
Simpliest Possible Android App That Can Be Compiled From Command Line from Linux

The walkthrough is available on youtube here:
https://www.youtube.com/watch?v=mKvGe3ZV9g4

The goal of this project is to allow a user to build android apps entirely without the use of the Android Studio IDE. In order to do so, a couple of things must be installed. 

First, make sure that the java elements are installed.

    sudo apt-get install openjdk-8-jre-headless
    sudo apt-get install openjdk-8-jdk-headless
    java -version
    
Note: If you already have java installed (you probably do), you will need to switch the version to java 8. To do, this, run the following command:

        sudo update-alternatives --config java
        
Then, check the java version with:

        java -version
  
Someday, I hope Google makes Android-cli compatibile with Java 11.

Now, download the android command line interface tools from the android website:
[Download page] https://developer.android.com/studio/index.html#downloads

Extract the downloaded package to somewhere in your home directory, and add the programs in it to you $PATH variable

Go to your ~/.bashrc and add at the end:

    export PATH="~/path/to/download/tools/bin:$PATH"
    export PATH="~/path/to/download/tools:$PATH"
    

restart your terminal

Now, type:

    android update sdk
  
This will create a .android folder in your home directory. Navigate to the ~/.android folder, and add a new file called repositories.cfg

    nano repositories.cfg
  
I don't know why that is necessary, but for some reason the tools don't know to make that file on its' own.

Now, with the sdkmanager tools, install the latest
* platform-tools (no version)
* platform (latest version)
* system image (go with a later version if possible)
* build tools

You can list the available packages by typing:

    sdkmanager --list

For me, I installed the latest packages with this command (**these SDK versions will work with this version on github!**)

    sdkmanager "platform-tools" "platforms;android-29" "system-images;android-29;default;x86_64" "build-tools;29.0.2"
    
 Now, add platform-tools to your PATH in the .bashrc (it was just installed next to the tools directory)
 
    export PATH="~/path/to/download/platform-tools:$PATH"
  
Now, we can make an emulator with the following command:

    avdmanager create avd -n "buddy" -k "system-images;android-29;default;x86_64" --device "Nexus 6P"

Now, you have to go into your tools directory, and run the emulator program **directly** Running it from outside tools using the program name you added when you altered your $PATH variable **doesn't work!**

    ./emulator -avd "buddy"
  
If everything worked, you should see an emulator pop up. 

Now, you can install gradle with the following command:

    sudo apt-get install gradle
  
Verify that gradle downloaded correctly

    gradle -v
  
Now, download this repository, and navigate to the root of this project, and type:

    gradle assembleDebug
 
 This will build a .apk file. Install it using the following command:
 
    adb install /path/to/project_root/main-items/build/outputs/apk/debug/main-items-debug.apk
 
  
