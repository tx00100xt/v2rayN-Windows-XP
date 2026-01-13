# v2rayN Windows XP

A GUI client for Windows XP, support v2ray-core with protocols Shadowsocks, VLESS, VMess.

## How to use

To use the v2rayN program, you need to install [NET Framework 4.0](https://www.microsoft.com/en-my/download/details.aspx?id=17718)

Go to [Release](https://github.com/tx00100xt/v2rayN-Windows-XP/releases) section and download archive with binaries files. Unpack the downloaded archive to any location.  
Go to the directory with the unpacked archive and run v2rayN.exe

![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/900.png)

After launching, the v2rayN icon appears in the system tray. Click on it to open the main program window.

You can add server links using the program menu and the clipboard:

![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/901.png)
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/902.png)
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/903.png)

After add server links click needed server on table and choose "Set as active server (Enter)"

![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/904.png)

In the program's information window, you'll see the service and v2ray core startup status.  
Further information about connections and program operation will be displayed there.

![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/905.png)

# Building v2rayN and v2ray core from source

The application is built in two stages. The first stage builds the GUI using NET Framework 4.0  
and Visual Studio 2015 (recommended). Windows 7 or higher is recommended for this build.  
The second stage builds the application in Windows XP, using the native Go language for Windows XP  
and trusted root certificates installed for downloading and processing Go mods.

## First stage build

1. Download and Install [Visual Studio 2015 Community Edition] or higher.
2. Clone this repo or use the source code archive at the recommended path:
**"C:\Users\<user>\Documents\Visual Studio 2015\Projects\"**
```powershell
cd "C:\Users\<user>\Documents\Visual Studio 2015\Projects\"
git clone https://github.com/tx00100xt/v2rayN-Windows-XP.git
```
3. Open Visual Studio 2015 and choose solution:
**"C:\Users\<user>\Documents\Visual Studio 2015\Projects\v2rayN-Windows-XP\v2rayN.sln"**
4. Select Release x86 and compile it.

After building, you will get the output files:
```powershell
bin\Release\v2rayN.exe
bin\Release\zh-Hans\v2rayN.resources.dll
```
## Second stage build

<span style="color:blue">**The first thing you need to do is install trusted root certificates.**</span>.

1. Download the GlobalSign **Root-R1** certificate to an accessible location:  
[GlobalSign Root Certificates](https://support.globalsign.com/ca-certificates/root-certificates/globalsign-root-certificates)

2. Click **Start > Run**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/951.png)

3. Type **MMC** and press **OK**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/952.png)

4. Click on **File  > Add / Remove Snap-In**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/953.png)

5. Click **Add**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/954.png)

6. Under **Snap-in**, double click on **Certificates**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/955.png)

7. Click **Computer Account > Next**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/956.png)

8. Choose **Local Computer > Finish**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/957.png)

9. Click **Close.**  

10. Click **OK** to exit the snap-in window.  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/958.png)

11. Click **[+] next to Certificates > Trusted Root Certification Authorities > Certificates**  

12. Right click on **Certificates** and select **All Tasks > Import**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/959.png)

13. Click **Next**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/960.png)

14. Click **Browse**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/961.png)

15. Select **Root-R1.crt** downloaded in step <span style="color:red">**1**.</span>.  
Press **Open** and **Next** to continue.  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/962.png)

16. Click **Next**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/963.png)

17. Click **Finish**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/964.png)

17. Press **OK**  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/965.png)

### NOTE:

If you do not install trusted root certificates, you will receive an error during build:

```powershell
tls: failed to verify certificate: x509: certificate signed by unknown authority
```
For a large number of mods, when executing the command:
```powershell
go mod download
```
After install trusted root certificates, you can install the Go language compiler and start building the V2ray core.

Download the Go compiler [go-386.zip](https://github.com/BieHDC/go-backports/releases/download/2023_02_12_120/go-386.zip) for Windows XP from the repo: https://github.com/BieHDC/go-backports
Unpack this archive on disk **"C:\ "** . Add the path to the Go compiler **"C:\go\bin"** to the PATH environment variable.
Also put the source code of **"v2rayN-Windows-XP"** on the **"C:\ "** disk.
Open a terminal and use the following commands to build **v2ray.exe** and **v2ctl.exe**

```powershell
cd C:\v2rayN-Windows-XP\v2ray-core
go mod download
go build -o v2ray.exe -trimpath -ldflags "-s -w -buildid=" ./main
go build -o v2ctl.exe -trimpath -ldflags "-s -w -buildid=" -tags confonly ./infra/control/main
```
The final build will contain the following files:
```powershell
v2rayN\v2rayN.exe
v2rayN\v2ray.exe
v2rayN\v2ctl.exe
v2rayN\config.json
v2rayN\geoip.dat
v2rayN\geosite.dat
v2rayN\zh-Hans\v2rayN.resources.dll
```
You can download the completed archive containing these files in the [Release](https://github.com/tx00100xt/v2rayN-Windows-XP/releases) section.
You can run executable file v2ray.exe from the command line without using GUI.  
![v2rayN-WinXP](https://raw.githubusercontent.com/tx00100xt/v2rayN-Windows-XP/main/images/970.png)

By default, the listen address **127.0.0.1:10808** is used.

## Links

https://github.com/2dust/v2rayN  
https://github.com/v2ray/v2ray-core  

[Visual Studio 2015 Community Edition]: https://go.microsoft.com/fwlink/?LinkId=615448&clcid=0x409 "Visual Studio 2015 Community Edition"
