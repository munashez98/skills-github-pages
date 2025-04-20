# BFT Hack The Box

_Today we will be looking at BFT, a Sherlock challenge from Hack The Box which you can find [here](https://app.hackthebox.com/sherlocks/bft/play)._

## Scenario
In this Sherlock, you will become acquainted with MFT (Master File Table) forensics. You will be introduced to well-known tools and methodologies for analyzing MFT artifacts to identify malicious activity. During our analysis, you will utilize the MFTECmd tool to parse the provided MFT file, TimeLine Explorer to open and analyze the results from the parsed MFT, and a Hex editor to recover file contents from the MFT.

## Task 1
**Simon Stark was targeted by attackers on February 13. He downloaded a ZIP file from a link received in an email. What was the name of the ZIP file he downloaded from the link?**

The first step is to use MFTECmd to parse the MFT and write the output to a CSV that we can process in TimeLine Explorer.

![image](https://github.com/user-attachments/assets/3e369662-4f86-44f3-a0b6-dffa553f3dce)

As you can see below, the parsing was successful, and the tool output a CSV

![image](https://github.com/user-attachments/assets/f9b986b8-f5ab-4128-bb90-892005c77620)

![image](https://github.com/user-attachments/assets/f8594edf-27de-4d43-91d6-3ccb2d5a7dc0)

To find the file in question we can filter by Extension and look for records that contain ".zip". We are presented with 5 files in question. Looking at the Parent Sequence Numbers we identify Stage-20240213T093324Z-001.zip as the most likely candidate for the answer as it has the number 1.


## Task 2
**Examine the Zone Identifier contents for the initially downloaded ZIP file. This field reveals the HostUrl from where the file was downloaded, serving as a valuable Indicator of Compromise (IOC) in our investigation/analysis. What is the full Host URL from where this ZIP file was downloaded?**

To find the zone identifier we can remove the .zip filter and search for file names that contain "stage". From this we can find the corresponding zone identifier file including the host URL.

![image](https://github.com/user-attachments/assets/356192b3-8bdf-4444-b519-76d94ed7e2e5)

## Task 3 

**What is the full path and name of the malicious file that executed malicious code and connected to a C2 server?**
Again, we clear the filters and proceed to apply a filter for files that have "stage" on the Parent Path 

![image](https://github.com/user-attachments/assets/664e6c5b-703f-4ca8-88d3-843174f9625b)

From examining the paths here and the associated files, we can see that the only one that can satisfy the criteria is invoice.bat. Putting the path and file name together we get the full path C:\Users\simon.stark\Downloads\Stage-20240213T093324Z-001\Stage\invoice\invoices and file name invoice.bat.

## Task 4 

**Analyze the $Created0x30 timestamp for the previously identified file. When was this file created on disk?**
This task is simple as we merely need to look ath the Created0x30 column to get 2024-02-13 16:38:39

![image](https://github.com/user-attachments/assets/83057033-0088-4634-9566-956dce514f18)

## Task 5
**Finding the hex offset of an MFT record is beneficial in many investigative scenarios. Find the hex offset of the stager file from Question 3.**

To do this we obtain the entry number of 23436 and multiply by 1024 to get the decimal representation which works out to be  23,998,464

![image](https://github.com/user-attachments/assets/b70de573-f2bd-4b62-8baf-38fbe0141d27)


![image](https://github.com/user-attachments/assets/34524bcb-3c42-4761-b05d-d6663fb94feb)

Converting this decimal value to Hex we get the value 16E3000

![image](https://github.com/user-attachments/assets/141c1fc5-83e0-4282-9dad-c3bd7aeb3f5a)


## Task 6

**Each MFT record is 1024 bytes in size. If a file on disk has smaller size than 1024 bytes, they can be stored directly on MFT File itself. These are called MFT Resident files. During Windows File system Investigation, its crucial to look for any malicious/suspicious files that may be resident in MFT. This way we can find contents of malicious files/scripts. Find the contents of The malicious stager identified in Question3 and answer with the C2 IP and port.**

To accomplish this, we import our $MFT record to HxD or any other hex editor of your choice. Next, we use the Go to function Ctrl-G and type in the offset 16E3000.

![image](https://github.com/user-attachments/assets/b15242a1-b08b-48ea-b915-99692c8f73b7)

We then look for any network-related addresses and find the address "http[:]//43[.]204[.]110[.]203[:]6666", From this we can infer that the C2 is at the address 43.204.110.203:6666.

![image](https://github.com/user-attachments/assets/1d262525-1bce-4c2d-9999-d24c870a02b1)































