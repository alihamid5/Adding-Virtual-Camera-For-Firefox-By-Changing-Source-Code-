# Adding-Virtual-Camera-Inside-Firefox-By-Changing-Source-Code
In this project, I have integrate a virtual camera in the source code of mozilla firefox, as it is an open source browser, in the virtual camera you can put any of your desired video in Y4M format and the whenever you have will open your camera through firefox, code will initialize the virtual camera. The physical Camera Initialization and access to Firefox have been stopped.

# Objective:
 1) A Virtual Camera which can run our desired video
 2) The Virtual Camera should be stealthy and cannot be able to detect by security system of any website, whether financial, banking, private or goverment website.
 3) That video while running through virtual camera on on any website can be adjusted through up, down, right and left keys.
 4) The flexibilty to change the video in the browser to change desired videos in virtual camera.
 5) Physical Camera should be denied or not initialized.

The source code need to be change in 6 Files. I have Provide the complete Modified files. You just need to replace the files and compile the browser to use.

NOTE: CHECK THE SOURCE CODE IF YOU CAN. YOU WILL BE RESPONSIBLE FOR ANY LEGISLATION IF YOU PERFORM ANY UNETHICAL, ILLEGAL, OR UNLAWFUL ACTIVITY BY USING THIS PROJECT. SO USE IT FOR EDUCATIONAL PURPOSES, TEACHING IN YOUR INSTITUTIONAL PROJECTS, EXPERIMENTS, OR PRIVATE ISOLATED LABS.

*********************************************************

# THE DETAIL PROCESS IS MENTIONED BELOW

THE Process is Categorize in 6 Steps.

STEP 1: DOWNLOADING SOURCE CODE
STEP 2: REPLACING THE MODIFIED FILES IN SOURCE CODE
STEP 3: DOWNLOADING FFMPEG DEPENDENCIES
STEP 4: DOWNLOADING EXTRA DEPENDENCIES FOR COMPILATION
STEP 5: COMPILATION
STEP 6: TESTING

---------------------------------------------------------

STEP 1: DOWNLOADING SOURCE CODE

1. Download the Source from Mozilla Website "https://firefox-source-docs.mozilla.org/setup/windows_build.html"

2. The above is Mozilla Firefox Official Link of "source code Downloading software", Download the "MozillaBuild" Software from the provided, and install it.
3. Then to download the source code from that software, the link i provided have compltete guides for this downloading process. but for the seek of ease for you. after 
   installing the "MozillaBuild" it will create a folder by name "mozilla-build" in your "C:/ Drive" Main Directory.
4. Go to the "C:/mozilla-build" and run "start-shell" as Administrator in Win or as Sudo in Linux. It will open the Mozilla Build Terminal. Then run these commands in that terminal.

   "cd c:/
   mkdir mozilla-source
   cd mozilla-source
   wget https://hg.mozilla.org/mozilla-central/raw-file/default/python/mozboot/bin/bootstrap.py   
   python3 bootstrap.py --vcs=git
   python3 bootstrap.py"

5. The bootstrap.py is the script that will download the complete source code of firefox (from the beginning of the Firefox till now, all source code) in "C:/mozilla-source/mozilla-unified/", In "mozilla-unified," your source code is available and all the modification is going to be there.

---------------------------------------------------------

STEP 2: REPLACING THE MODIFIED FILES IN SOURCE CODE

1. After Successfully Downloading the source code, our step 2 starts from here
2. Now we have to do modification in source code, there are 6 Targeted file which we have to replace in source code, and all the file with modified code i have attacted above. The exact location to replace each file is mentioned below.

1st Replacement:

  C:\mozilla-source\mozilla-unified\dom\media\webrtc  -  Open this Directory and Replace 4 files mention below

   1) MediaEngineWebRTC.cpp
   2) MediaEngineRemoteVideoSource.cpp
   3) MediaEngineRemoteVideoSource.h
   4) moz.build
   
2nd Replacement:

  C:\mozilla-source\mozilla-unified   -  Open this Directory and Replace 1 file mention below

   1) mozconfig (if you are on linux, then you need to first unhide the hidden files in "mozilla-unified" and then find the ".mozconfig" file"

3rd Replacement:

  C:\mozilla-source\mozilla-unified\browser\installer  -  Open this Directory and Replace 1 file mention below

   1) package-manifest.in

---------------------------------------------------------

STEP 3: DOWNLOADING FFMPEG DEPENDENCIES

1. Download This for "ffmpeg-master-latest-win64-gpl-shared.zip" From "https://github.com/btbn/ffmpeg-builds/releases" but according to your OS and Architecture.
   
2. If your creating this for windows 64x. then the name i mention for you, you have to use, other wise on the same page you will its different models as well like 
   "ffmpeg-master-latest-linux64-lgpl-shared.tar.xz and" for Linux x64 or "ffmpeg-master-latest-linuxarm64-gpl-shared.tar.xz" for Linux Arm Architecture.

3. Then unzip it and you will get this folder "ffmpeg-master-latest-win64-gpl-shared" in this folder you will see "include" and "lib" then copy these two folders and then create folder by name of "bin" Inisde your main directory of "mozilla-unified".
4. And then create one more folder inside the "bin" folder by name of "ffmpeg" and then Paste here the "include" and "lib" folders.
5. now go back to the "ffmpeg-master-latest-win64-gpl-shared" folder and go to the bin folder. Inside this folder you will see lots of ".dll" files. you have to copy 
   the 4 ".dll" file from here. names are mentioned below.
   1) avcodec-61.dll
   2) avformat-61.dll
   3) avutil-59.dll
   4) swscale-8.dll"

6. Find these files one by one and copy to this folder "/mozilla-unified/bin/ffmpeg/", 

7. Also, put your desired Y4M format video inside "/mozilla-unified/bin/ffmpeg/", which you want to use as the virtual camera.

NOTE: 
 + here is tiny catch, that these files "ffmpeg-master-latest-win64-gpl-shared.zip" are constantly update with the passage of time.
 + It is possible that the name of these for ".dll" files change with the passge of time, like from "avcodec-61.dll it can change to avcodec-62.dll".
 + Only the number in the name could be change so you have to look for the name with latest no. if you dont find the with "61, 59, or 8" these files its mean that files 
   are been updated so look for the latest no.
 + and paste the latest files in "/mozilla-unified/bin/ffmpeg/"
 + and becuase no in name is change so you need to do some very tiny changes in "package-manifest.in" file as mention below
   - open the "package-manifest.in" file, go to the line no 131 and looks this.
     @BINPATH@/ffmpeg/avcodec-61.dll
     @BINPATH@/ffmpeg/avformat-61.dll
     @BINPATH@/ffmpeg/avutil-59.dll
     @BINPATH@/ffmpeg/swscale-8.dll
     in these for lines you can see your ".dll" files. if the no is different in your latest downloaded "ffmpeg-master-latest-win64-gpl-shared" folder. then change the 
     numbers in name in "package-manifest.in" as mentioned in "ffmpeg-master-latest-win64-gpl-shared/bin" folder
 + This will Update your code as latest prerequisites.


---------------------------------------------------------

STEP 4: DOWNLOADING EXTRA DEPENDENCIES FOR COMPILATION

1. Now all the modification in the code is completed, and you just need to install some dependencies according to the platform your are compiling not for the platform 2. your are building the firefox.
   1) Install "Rust"                                     # for Linux and Windows
   2) Install System wide "ffmpeg"                       # for Linux and Windows
   3) Install "Visual Studio" (for windows)              # If your are compiling on Windows
   4) Install these for Linux "sudo apt-get install \    # If you are Compiling on Linux-Debian install all these from APT repo
      autoconf \
      build-essential \
      cargo \
      clang \
      curl \
      git \
      libasound2-dev \
      libdbus-1-dev \
      libgtk-3-dev \
      libpulse-dev \
      libx11-xcb-dev \
      libxt-dev \
      mesa-common-dev \
      python3-dev \
      python3-pip \
      unzip \
      zip \
      zlib1g-dev
      
      For WebRTC (additional):
      sudo apt-get install \
      libglib2.0-dev \
      libssl-dev \
      libvpx-dev \
      yasm
      "
---------------------------------------------------------

STEP 5: COMPILATION

1. Now all the Dependencies and Modification in Source Code have been completed, so this is the time to start compiling and use your final product.
2. Go again to the "C:/mozilla-build" folder and run the "start-shell" as administrator, it will run the "Mozilla build" terminal.
3. Run these three Commands step by step in the "Mozilla Build" terminal.
   1) ./mach configure
   2) ./mach build
   3) ./mach package

4. On successful completion of these commands. your custom firefox will be ready to use. 

---------------------------------------------------------

STEP 6: TESTING

1. Now go to the "C:/mozilla-source/mozilla-unified/obj-x86_64-pc-linux-gnu/dist"
2. Here you will find a ZIP package of your Custom Ready to use Mozilla Firefox Browser.
3. Extract the zip at your Desired Location in any Win/Linux device.
4. Open the folder and Run the "Firefox.exe".
5. It will Open the firefox, now check your virtual camera, by going to any site which require camera access. or goto "https://webcamtests.com/"
6. Remember you can adjust the running video by up, down, left, right keys if you are performing your desired activity.


****************************************************************************************************

Now Enjoy it, Use it for Educational Purposes, and be careful with use and adhere to the compliance, rules, laws and ethics.

In this Process you can possibily get several issues if you are non I.T person.

so contact me at "m.alihamid763@gmail.com" if you face any type of difficulty

THANK YOU
  

