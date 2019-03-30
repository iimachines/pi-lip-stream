Wonder Media Productions - internal setup steps

* [Install .NET Core 2.2 on Windows 10](https://dotnet.microsoft.com/download/dotnet-core/2.2)

* [Install .NET Core 2.2 on Raspberry PI](https://www.hanselman.com/blog/InstallingTheNETCore2xSDKOnARaspberryPiAndBlinkingAnLEDWithSystemDeviceGpio.aspx)

* [Give each PI a unique network name](https://thepihut.com/blogs/raspberry-pi-tutorials/19668676-renaming-your-raspberry-pi-the-hostname)
  - `sudo nano /etc/hostname` => change name 
  -  `sudo nano /etc/hosts` => change name
  -  `hostname` => test name
  - I used `rp3` for my PI

* [Install remote debugging and deployment tools](https://github.com/Microsoft/MIEngine/wiki/Offroad-Debugging-of-.NET-Core-on-Linux---OSX-from-Visual-Studio)
  - To synchronize files between the PI and Windows 10, I shared the `PiLipClient\bin` folder as `pi-lip-client`. 
     - I had to create a non-Microsoft-account local user (I called it `STS`) to get this working
     - On the PI:
        - `sudo apt-get install cifs-utils`
        - `sudo mkdir /mnt/pi-lip-client`
        - `sudo mount -t cifs //<WINDOWS_COMPUTER_NAME>/pi-lip-client /mnt/pi-lip-client -o username=STS,dir_mode=0777,file_mode=0777,serverino,sec=ntlmssp`  
        - The build code will be synchronized using the command `rsync -rtv -aR /mnt/pi-lip-client/ ~/Desktop/pi-client/bin`
        - On Windows, assuming you created you private SSH key as `usr\private-key.ppk`, we execute this command using `"c:\Program Files\PuTTY\plink.exe" -i usr\private-key.ppk pi@rp3 -batch -T "rsync -rtv -a /mnt/pi-lip-client/ ~/Desktop/pi-lip-client"`
   - *Note that I was unable to start the debugger with Visual Studio 2017 as described in the article*

* [Install remote debugging and deployment tools for VSCode](https://www.hanselman.com/blog/RemoteDebuggingWithVSCodeOnWindowsToARaspberryPiUsingNETCoreOnARM.aspx)



        
