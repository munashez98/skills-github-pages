# BFT Hack The Box

_Today we will be looking at BFT, a Sherlock challenge from Hack The Box which you can find [here](https://app.hackthebox.com/sherlocks/bft/play)._

## Scenario
In this Sherlock, you will become acquainted with MFT (Master File Table) forensics. You will be introduced to well-known tools and methodologies for analyzing MFT artifacts to identify malicious activity. During our analysis, you will utilize the MFTECmd tool to parse the provided MFT file, TimeLine Explorer to open and analyze the results from the parsed MFT, and a Hex editor to recover file contents from the MFT.

## Task 1
**Simon Stark was targeted by attackers on February 13. He downloaded a ZIP file from a link received in an email. What was the name of the ZIP file he downloaded from the link?**

The first step is to use MFTECmd to parse the MFT and write the output to a CSV that we can process in TimeLine Explorer.

![image](https://github.com/user-attachments/assets/21174ef0-19c1-4e39-b6cc-e1433c877741)

As you can see below, the parsing was successful, and the tool output a CSV

![image](https://github.com/user-attachments/assets/f9b986b8-f5ab-4128-bb90-892005c77620)

![image](https://github.com/user-attachments/assets/f8594edf-27de-4d43-91d6-3ccb2d5a7dc0)

To find the file in question we can filter by Extension and look for records that contain ".zip". We are presented with 5 files in question. Looking at the Parent Sequence Numbers we identify Stage-20240213T093324Z-001.zip as the most likely candidate for the answer as it has the number 1.


## Task 2






