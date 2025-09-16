# Billing

[Try Hack Me Room](https://tryhackme.com/room/billing)

# Room Details:
> Gain a shell, find the way and escalate your privileges <br />
  <b>Note</b>: Bruteforcing is out of scope for this room <br />

# Tools Used: 
  • nmap <br />
  • dirbuster <br />
  • metasploit <br />
  • fail2ban <br />

# Analysis

1. Starting off I used nmap to do a scan but unfortunately I didn’t get much results. <br />
        ◦ -F options indications that it should scan in Fast Mode which scans fewer ports than the   default scan.<br />
        ◦ -Pn option indicates treatsts all hosts as if they were online and skips the host discovery.
<img width="1279" height="434" alt="Screenshot from 2025-08-21 13-39-18" src="https://github.com/user-attachments/assets/21592f7c-2c63-4671-bd3c-c13f9289a1a7" />

2. Editing the nmap scan I got the following, showing more details about the website available. <br />
        ◦ -Pn option indicates treatsts all hosts as if they were online and skips the host discovery.<br />
        ◦ -sV option tells nmap to probe for open ports and get the versions/service info.<br />
        ◦ -p 22,80,3306 option advises nmap to scan these specific ports.<br />
        
<img width="1295" height="639" alt="Screenshot from 2025-08-21 13-43-59" src="https://github.com/user-attachments/assets/1f198bd2-ff01-431d-8088-7da44e75863a" />

3. Navigating to the website we have a sign in <br />

<img width="1715" height="1054" alt="Screenshot from 2025-08-21 13-44-14" src="https://github.com/user-attachments/assets/f614df49-473b-4094-98d4-56013814e1e8" />

4. To check to see if there are any other directories available I’ll use Dirbuster. <br />

<img width="1294" height="911" alt="Screenshot from 2025-08-21 13-47-14" src="https://github.com/user-attachments/assets/b0ddb7e1-cdb9-4b05-b89a-63d28e3617ec" />

5. Unfortunately the results weren’t great as there was no other available directories. <br />
<img width="1294" height="911" alt="Screenshot from 2025-08-21 13-48-50" src="https://github.com/user-attachments/assets/d11ba520-0da5-451b-9813-8689b7f8d297" />

6. Instead I will try to use Metasploit to access the website by using the search function in Metasploit I was able to find a vulnerability using an Remote Code Execution (RCE) with Magnus software. <br />
       ◦ By using the search option we’re able to search the entire metasploit database for any keywords that match. <br />
       ◦ In this case the expliot is listed as 0, to select it we use the command use 0 <br />
       
<img width="1703" height="1092" alt="Screenshot from 2025-08-21 13-56-09" src="https://github.com/user-attachments/assets/ef3755d4-dea7-43ba-9eb7-464f155319cc" />

7. Using the show info command I can see more detailed on the RCE to be used. <br />

<img width="1703" height="1092" alt="Screenshot from 2025-08-21 13-57-10" src="https://github.com/user-attachments/assets/3aeaab1e-b11b-4180-9fe3-473dc8dd63ed" />

8. Next I need to set the target host (RHOSTS) and the local host (LHOST) for the payload then type in run to start it. Once we gained access I can initialise a shell. I then use a short python command to import the Putty program and start up the shell which gives me command line access. <br />
<img width="1395" height="642" alt="Screenshot from 2025-08-21 16-30-51" src="https://github.com/user-attachments/assets/84e987f8-d612-4a94-986d-d6af8ab119cd" />

9. Once in the system we can check the directory for any information or files available and sure enough we have our first file “user.txt”.

<img width="1542" height="711" alt="Screenshot from 2025-08-21 14-06-07" src="https://github.com/user-attachments/assets/e9460f75-9580-4d37-b3cf-1742fccd14ad" />

10. Using the cat function we can see our first flag. <br />

<img width="1498" height="71" alt="Screenshot from 2025-08-21 14-09-18" src="https://github.com/user-attachments/assets/89195cb9-3714-4074-aa07-5d71ea994c5a" />

11. Using the sudo -l command, which can be used as priviledge escalations paths which shows me that the systems are using Fail2Ban <br />
        ◦ Fail2Ban is a program used to prevent brute force attacks. It does this by scanning log files such as /var/log/auth.log and then bans IP’s based on their failed attempts. It then updates the firewall and rejects connections based on the configured time. <br />

<img width="1462" height="392" alt="Screenshot from 2025-08-21 16-33-34" src="https://github.com/user-attachments/assets/57c18d28-420a-4550-a245-585753ba4084" />

12. First I’ll check to see the version Fail2Ban is using then check to see if it’s running.

<img width="1499" height="202" alt="Screenshot from 2025-08-21 16-36-52" src="https://github.com/user-attachments/assets/72648d42-074c-4998-99b6-79d80fd783bc" />

<img width="1503" height="342" alt="Screenshot from 2025-08-21 16-37-49" src="https://github.com/user-attachments/assets/070631c3-dcab-4f28-982f-8bd1b7f0523b" />

13. Next I’ll change my current directory to the fail2ban directory and use ls -al function to see what files are available. <br />
        ◦ ls command will list what is available in that directory <br />
        ◦ -al is two commands <br />
            ▪ a will show hidden files <br />
            ▪ l will give the long list including any file attributes (permissions)<br />

<img width="1451" height="65" alt="Screenshot from 2025-08-21 16-46-59" src="https://github.com/user-attachments/assets/303696e8-cf23-4485-8f8a-3e32bd8994e6" />

<img width="1441" height="475" alt="Screenshot from 2025-08-21 16-47-11" src="https://github.com/user-attachments/assets/07dcb2e9-8d06-4e67-9aa4-dbe19c470910" />

14. I’ll check the status of fail2ban and can see that there is 8 jails which means there are 8 configurations on fail2ban set up.  <br />

<img width="1692" height="216" alt="Screenshot from 2025-08-21 16-50-33" src="https://github.com/user-attachments/assets/3afdaad3-d8f8-417f-a0b2-9056aca9e963" />

15. Before we get into that we’ll restart the system: <br />

<img width="1670" height="240" alt="Screenshot from 2025-08-21 17-07-01" src="https://github.com/user-attachments/assets/b3c76f34-51d3-49ee-88d9-e1c76b799ea0" />

16. Next I’m going to use Rsync function. Breaking this down shows: <br />
        ◦ rsync → a fast, efficient tool for copying and synchronizing files/directories.<br />
        ◦ -a (archive mode) → preserves file permissions, timestamps, symbolic links, and directory structure.<br />
        ◦ -v (verbose) → shows detailed output of what is being copied.<br />
        ◦ /etc/fail2ban/ → the source directory, which contains Fail2ban’s configuration files (like jail.conf, jail.local, filters, etc.).<br />
        ◦ /tmp/fail2ban/ → the destination directory, where the files will be copied.<br />
          
	In essence it copies the contents into a temp system locations which is more writeable and 	accessible than the normal locations <br />

 <img width="1708" height="698" alt="Screenshot from 2025-08-21 17-08-07" src="https://github.com/user-attachments/assets/a80d838b-a4c9-4b73-b19a-06f6cfe72bbb" />

17. Finally since the files have been synced to a temp location we’ll change to the temp directory. Running the ./bash -p preserves the UID and GID giving us root access in that shell.  Now I should be access the root file and then obtain out root.txt flag. <br />

<img width="1696" height="532" alt="Screenshot from 2025-08-21 17-06-29" src="https://github.com/user-attachments/assets/79736c1f-c998-40d3-91cb-719f2500b27c" />

