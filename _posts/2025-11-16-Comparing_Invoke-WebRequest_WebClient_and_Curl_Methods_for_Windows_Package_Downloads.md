---
layout: post
title: Downloading files with Windows PowerShell
subtitle: Comparing Invoke-WebRequest, WebClient, and Curl Methods for Windows Package Downloads
cover-img: assets/img/abstract-technology-background-hi-tech-communication-concept-innovation-background-vector-illustration-free-photo.jpg
thumbnail-img: assets/img/abstract-technology-background-hi-tech-communication-concept-innovation-background-vector-illustration-free-photo.jpg
share-img: assets/img/abstract-technology-background-hi-tech-communication-concept-innovation-background-vector-illustration-free-photo.jpg
tags: [powershell, invoke-webrequest, curl, webclient]
---

# Comparing Invoke-WebRequest, WebClient, and Curl Methods for Windows Package Downloads
## Introduction
Downloading files, such as winget cli from Github, is a common task for IT professionals and enthusiasts. With various tools available on Windows, such as PowerShell’s Invoke-WebRequest, WebClient, and curl (in both PowerShell and Command Prompt), you have multiple options to automate and streamline downloads. This post will guide you through each method, highlighting their usage, nuances, and differences.

## Quick Links
* [Prerequisites](#prerequisites)
* [Method 1: Using Invoke-WebRequest in PowerShell](#method-1-using-invokewebrequest-in-powershell)
* [Method 2: Using WebClient in PowerShell](#method-2-using-webclient-in-powershell)
* [Method 3: Using Curl in PowerShell](#method-3-using-curl-in-powershell)
* [Method 4: Using Curl in Command Prompt](#method-4-using-curl-in-command-prompt)
* [PowerShell Curl vs. Command Prompt Curl](#powershell-curl-vs-command-prompt-curl)

## Prerequisites
* Windows 10 or later (with PowerShell and curl available by default)
* URL to the file you want to download such as [https://github.com/microsoft/winget-cli/releases/download/v1.10.390/Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle](https://github.com/microsoft/winget-cli/releases/download/v1.10.390/Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle)
* Administrative privileges (recommended for installation tasks)

## Method 1: Using Invoke-WebRequest in PowerShell
PowerShell’s Invoke-WebRequest cmdlet is a powerful and straightforward way to download files.
1.	Open PowerShell as Administrator.
2.	Use the following command:
3.	`Invoke-WebRequest -Uri "https://github.com/microsoft/winget-cli/releases/download/v1.10.390/Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle" -OutFile "C:\tmp\winget_cli_installer.msixbundle"`
4.	Replace the URL with the actual download link and the path with your desired location.
This command fetches the file from the specified URL and saves it locally. Invoke-WebRequest is ideal for scripting and automation, supporting authentication, headers, and more.

## Method 2: Using WebClient in PowerShell
The WebClient class provides another way to download files in PowerShell, useful for compatibility with older scripts or when you need more granular control over the download process.
1.	Open PowerShell.
2.	Run the following commands:
3.	`$webClient = New-Object System.Net.WebClient`
4.	`$wc.DownloadFile("https://github.com/microsoft/winget-cli/releases/download/v1.10.390/Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle", "C:\tmp\winget_cli_install.msixbundle")`
5.	Again, adjust the URL and output path as needed.
WebClient is lightweight and works well for simple downloads, but lacks some of the advanced features of Invoke-WebRequest.

## Method 3: Using Curl in PowerShell
Windows ships with curl as a built-in command-line tool. You can use it directly in PowerShell, though it behaves slightly differently compared to Linux or macOS environments.
1.	Open PowerShell.
2.	Run: `curl.exe -o "C:\tmp\winget_cli_install.msixbundle" "https://github.com/microsoft/winget-cli/releases/download/v1.10.390/Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle"`
4.	Note: Use curl.exe instead of just curl to avoid confusion with the PowerShell alias for Invoke-WebRequest.
curl.exe provides robust options for downloads, including resume support, progress bars, and more.

## Method 4: Using Curl in Command Prompt
You can also use curl in the classic Command Prompt (cmd.exe).
1.	Open Command Prompt.
2.	Type: `curl -o "C:\winget_cli_install.msixbundle" "https://github.com/microsoft/winget-cli/releases/download/v1.10.390/Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle"`
In Command Prompt, curl always refers to the executable and does not have conflicting aliases, making it straightforward to use.

### PowerShell Curl vs. Command Prompt Curl
Powershell curl is actually an alias for *Invoke-WebRequest* meaning you would have to change the command to what the *Invoke-WebRequest* expects. 

so instead of `curl.exe -o "C:\tmp\winget_cli_install.msixbundle" "https://github.com/microsoft/winget-cli/releases/download/v1.10.390/Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle"`, your command would be `Invoke-WebRequest -Uri "https://github.com/microsoft/winget-cli/releases/download/v1.10.390/Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle" -OutFile "C:\tmp\winget_cli_installer.msixbundle"`

<!--| Feature | PowerShell (curl) | Command Prompt (curl) |
| --- | --- | --- |
| Command Name | curl (alias for Invoke-WebRequest), curl.exe (actual curl) | curl (actual curl) |
| Behavior | curl is an alias for Invoke-WebRequest unless curl.exe is specified | curl refers directly to curl.exe |
| Recommended Usage | Use curl.exe to avoid conflicts | Use curl directly |
| Advanced Features | All curl features available via curl.exe | All curl features available | -->

## Conclusion
Whether you’re scripting downloads for automation or manually fetching packages, Windows offers several flexible methods. For PowerShell users, Invoke-WebRequest and WebClient offer native options, while curl.exe brings cross-platform consistency. In Command Prompt, curl is straightforward with no alias conflicts. Always ensure you use the correct command for your environment to avoid confusion and get the most out of your download operations.

While any method will download the file, *Invoke-WebRequest* feels like it takes longer to download that using *WebClient* or *CURL* to me. 

## References & Further Reading
* [PowerShell Invoke-WebRequest Command](https://www.bing.com/ck/a?!&&p=b488221d143307f4ad9c9933d93e4fe1d88534e726f6ec44dde0467f0c2d161bJmltdHM9MTc2MzI1MTIwMA&ptn=3&ver=2&hsh=4&fclid=35726a44-6062-6dff-25d4-7ce1613e6cad&psq=powershell+invoke-webrequest&u=a1aHR0cHM6Ly9sZWFybi5taWNyb3NvZnQuY29tL2VuLXVzL3Bvd2Vyc2hlbGwvbW9kdWxlL21pY3Jvc29mdC5wb3dlcnNoZWxsLnV0aWxpdHkvaW52b2tlLXdlYnJlcXVlc3Q_dmlldz1wb3dlcnNoZWxsLTcuNQ)
* [WebClient Class (Systen.Net)](https://www.bing.com/ck/a?!&&p=a475ebac5fd8ff36fb129792c12ea339bb17303781a9f60bfc5ceb6efc5181e4JmltdHM9MTc2MzI1MTIwMA&ptn=3&ver=2&hsh=4&fclid=35726a44-6062-6dff-25d4-7ce1613e6cad&psq=powershell+webclient&u=a1aHR0cHM6Ly9sZWFybi5taWNyb3NvZnQuY29tL2VuLXVzL2RvdG5ldC9hcGkvc3lzdGVtLm5ldC53ZWJjbGllbnQ_dmlldz1uZXQtOS4w)
* [Curl Windows 11](https://curl.se/windows/microsoft.html)


Don’t forget to bookmark and check back for updates.
Community Engagement: Join the conversation on [discord](https://discord.gg/FXzZKZWkgB)
