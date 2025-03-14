# Adding-Virtual-Camera-Inside-Firefox-By-Changing-Source-Code
In this project, I have integrate a virtual camera in the source code of mozilla firefox, as it is an open source browser, in the virtual camera you can put any of your desired video in Y4M format and the whenever you have will open your camera through firefox, code will initialize the virtual camera. The physical Camera Initialization and access to Firefox have been stopped. 

The source code need to be change in 6 Files. I have Provide the complete Modified files. You just need to replace the files and compile the browser to use.

NOTE: CHECK THE SOURCE CODE IF YOU CAN. YOU WILL BE RESPONSIBLE FOR ANY LEGISLATION IF YOU PERFORM ANY UNETHICAL, ILLEGAL, OR UNLAWFUL ACTIVITY BY USING THIS PROJECT. SO USE IT FOR EDUCATIONAL PURPOSES, TEACHING IN YOUR INSTITUTIONAL PROJECTS, EXPERIMENTS, OR PRIVATE ISOLATED LABS.

*********************************************************

THE DETAIL PROCESS IS MENTIONED BELOW

---------------------------------------------------------

STEP 1:

Download the Source from Mozilla Website:

https://firefox-source-docs.mozilla.org/setup/windows_build.html

The above is Mozilla Firefox Official source code Downloading software link, Download the "MozillaBuild" Software from thier and install it, Then to download the soruce from that software, the link i provided have compltete guides for. but for the seek of ease for you. after installing the "MozillaBuild" it will create a folder by name "mozilla-build" in your "C:/ Drive" Main Directory. go to "C:/mozilla-build" and run "start-shell" as Administrator in Win or as Sudo in Linux. Then run these commands 

# Using the C:\mozilla-build\start-shell.bat shell from step 1:
cd c:/
mkdir mozilla-source
cd mozilla-source
wget https://hg.mozilla.org/mozilla-central/raw-file/default/python/mozboot/bin/bootstrap.py

# To use Git as your VCS
python3 bootstrap.py --vcs=git

# To use Mercurial as your VCS
python3 bootstrap.py

The bootstrap.py is the script that will download the complete source code of firefox (from the beginning of the Firefox till now, all source code) in "C:/mozilla-source/mozilla-unified/", In "mozilla-unified," your source code is available and all the modification is going to be there.

---------------------------------------------------------

STEP 2:

After Successfully Downloading the source code, our step 2 starts from here, now we have to do modification in source code, there are 6 Targeted file which we have to replace in source code, and all the file with modified code i have attact above. The exact location to replace each file is Mention Below.

1st Replacement:

C:\mozilla-source\mozilla-unified\dom\media\webrtc  -  Open this Directory and Replace 4 files mention below

 1) MediaEngineWebRTC.cpp
 2) MediaEngineRemoteVideoSource.cpp
 3) MediaEngineRemoteVideoSource.h

2nd Replacement:

C:\mozilla-source\mozilla-unified   -  Open this Directory and Replace 1 file mention below

 1) mozconfig (if you are on linux, then you need to first unhide the hidden files in "mozilla-unified" and then find the ".mozconfig" file"

3rd Replacement:

C:\mozilla-source\mozilla-unified\browser\installer  -  Open this Directory and Replace 1 file mention below

 1) package-manifest.in

---------------------------------------------------------

STEP 3: 

Download This for "ffmpeg-master-latest-win64-gpl-shared.zip" From "https://github.com/btbn/ffmpeg-builds/releases" but according to your OS and Architecture.
If your creating this for windows 64x. then the i mention i for you other wise on the same page you will its different models as well like "ffmpeg-master-latest-linux64-lgpl-shared.tar.xz and" for Linux x64 or "ffmpeg-master-latest-linuxarm64-gpl-shared.tar.xz" for Linux Arm Architecture.

Then unzip it and you will get this folder "ffmpeg-master-latest-win64-gpl-shared" in this folder you will see "include" and "lib" then copy these two folders and then create folder by name of "bin" Inisde your main directory of "mozilla-unified" and then create one more folder inside the "bin" folder by name of "ffmpeg" and then Paste here the "include" and "lib" folders. now go back to the "ffmpeg-master-latest-win64-gpl-shared" folder and go to the bin folder inside it. form here you will see lots of ".dll" files. you have to copy the 4 ".dll" file from here. names are mentioned below.


 1) avcodec-61.dll
 2) avformat-61.dll
 3) avutil-59.dll
 4) swscale-8.dll"

Find these files one by one and copy to this folder "/mozilla-unified/bin/ffmpeg/", 

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

STEP 4:

Now all the modification in the code is completed, and you just need to install some dependencies according to the platform your are compiling not for the platform your are building the firefox.
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
     
  # For WebRTC (additional):
   sudo apt-get install \
    libglib2.0-dev \
    libssl-dev \
    libvpx-dev \
    yasm
    "
---------------------------------------------------------

STEP 5:

Now all the Dependencies and Modification in Source Code have been completed, so this is the time to start compiling and use your final product. 
