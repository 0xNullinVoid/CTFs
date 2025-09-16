# Takeover 

[Try Hack Me Room](https://tryhackme.com/room/takeover) 

# Room Details:
> Hello there, <br />
I am the CEO and one of the co-founders of futurevera.thm. In Futurevera, we believe that the future is in space. We do a lot of space research and write blogs about it. We used to help students with space questions, but we are rebuilding our support. <br />
>
> Recently blackhat hackers approached us saying they could takeover and are asking us for a big ransom. Please help us to find what they can takeover. <br />
Our website is located at https://futurevera.thm <br />
>
> Hint: Don't forget to add the MACHINE_IP in /etc/hosts for futurevera.thm ; )
# Tools Used: 
  - dirbuster

# Analysis

1. From observation of the introduction I can see that they are rebuilding their support. Having a look in the /etc/host directory I can see that they have an IP address of their website as mentioned in the introduction of 10.10.60.229.

2. I added in the support domain for futurevera.thm just beside the website so we can gain access to that site. 
   <img width="365" height="154" alt="3 Add_IP_to_Hosts_File" src="https://github.com/user-attachments/assets/d8805e5f-7ca9-4adb-ab23-f3e70306cb6d" />

3. Then entering in the website link “futurevera.thm” I was presented with an error and after checking the certifications and the source codes we can’t find anything.

<img width="628" height="478" alt="4 Nothing_In_Certs" src="https://github.com/user-attachments/assets/eee50b31-2185-4101-b447-24b11d0731c7" />

4. I attempted to find any other directories using the tool DirBuster which brute forces websites to find other directories and files. In this case I used their website name and use a common wordlist text file from the /wordlists/dirb directory on my Kali Linux machine.

<img width="574" height="406" alt="4 1 DirBuster" src="https://github.com/user-attachments/assets/e3e0fccb-83bb-4cc0-90fb-8ddaadd6c0b9" />

5. After running DirBuster it seems like I didn’t find anything of interest
<img width="578" height="413" alt="4 2 Nothing_Found_In_DirBuster" src="https://github.com/user-attachments/assets/c3bc4e06-3466-462b-8834-52b8a11871e6" />

6. Returning to our browser, I was noted that the support link wasn’t working due to the incorrect protocol, was using http when https should be used to visit this site.

<img width="794" height="483" alt="5 Support_Link" src="https://github.com/user-attachments/assets/cf3d0de5-1f4c-49ff-88a6-770c175b467c" />

7. From here, checked out the certificate for this link and found and interesting DNS name.
<img width="1213" height="731" alt="6 Support_Cert_Alt_Domain" src="https://github.com/user-attachments/assets/815f4f3f-9085-4ebb-b4e9-e6f2702deaf6" />


8. Adding this secret domain name to the /etc/host file

<img width="1205" height="303" alt="7 Add_to_Hosts_File" src="https://github.com/user-attachments/assets/cc5b1c82-b696-4a29-84a7-7ed9978b0a1f" />


9. Redirecting to the secret website via this link
<img width="1207" height="62" alt="8 HTTP_Address" src="https://github.com/user-attachments/assets/2045e408-f7c7-4fa4-ac7f-23ffd2a6b5ee" />


10. Once loaded was prompt with an error to the website, however the flag appears in the url box for the browser. 
<img width="1993" height="961" alt="9 Flag" src="https://github.com/user-attachments/assets/d48017c3-ac4e-49b6-af90-e1b8b96eb65e" />


