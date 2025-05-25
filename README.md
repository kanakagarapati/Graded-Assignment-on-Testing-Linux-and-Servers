# Graded-Assignment-on-Testing-Linux-and-Servers

## Task 1

Run `sudo apt update`
<p align="center">
<img width="717" alt="image" src="https://github.com/user-attachments/assets/c9451c3b-4033-4440-ab09-a899d6e8ed34" />
</p>

Run `Sudo apt-get install htop -y` . </br>
After installing i have ran `htop --version` to check the version .
<p align="center">
<img width="506" alt="image" src="https://github.com/user-attachments/assets/4ba0ad58-252f-4f20-8111-2c9f8097191a" />
</p>

Run `sudo nano sys_monitor.sh`. </br>
Add below code block. </br>
```
log_dir="/var/log/sys_monitor"
mkdir -p "$log_dir"

timestamp=$(date +%F_%H-%M-%S)
log_file="$log_dir/sys_report_$timestamp.log"

{
    echo "====== System Monitor Report ======"
    echo "Date: $(date)"
    echo ""

    echo "####CPU and Memory Usage (top)####"
    top -b -n1 | head -n 15
    echo ""

    echo "### Top 10 Memory-Consuming Processes###"
    ps aux --sort=-%mem | head -n 11
    echo ""

    echo "### Disk Usage Summary###"
    df -h
    echo ""

    echo "###Top 5 Largest Directories in / (may take time)###"
    du -h / 2>/dev/null | sort -rh | head -n 5
    echo ""

    echo "====== End of Report ======"
} >> "$log_file"
 ```
<p align="center">
<img width="589" alt="image" src="https://github.com/user-attachments/assets/32a8c5d9-97e3-450f-a521-33fb929a869d" />
</p>
</br>
verify code 
Run 'cat sys_monitor.sh' for verify created .sh file code.</br>

Run 'sudo chmod -x sys_monitor.sh'</br>
Run 'sudo chmod +x sys_monitor.sh'</br>
Run `sudo ./sys_monitor.sh` </br>
run `ls`</br>
<p align="center">
<img width="708" alt="image" src="https://github.com/user-attachments/assets/b310de81-d829-49bc-be60-a9e8d98f83e1" />
</p>
</b>
log results for manual execution 
<p align="center">
<img width="1328" alt="image" src="https://github.com/user-attachments/assets/38a8ceee-b2c0-41ea-8b98-0cd094a5f30a" />
</p>
<p align="center">
<img width="1409" alt="image" src="https://github.com/user-attachments/assets/10467d93-7aa0-4132-a858-8f10f39a4f86" />
</p>

Creating Cron jobs to automate the sys_monitor.sh to run automically. </b>
Run `crontab -e` </b>
selected option 1
<p align="center">
<img width="585" alt="image" src="https://github.com/user-attachments/assets/1085e6f0-09bb-48ef-aa26-6e8c697bdd56" />
</p>

## Task 2
Run `sudo apt update` </b>
<p align="center">
<img width="452" alt="image" src="https://github.com/user-attachments/assets/2d0d2ecc-fa3d-4cc1-97a2-bb0f3f9849d8" />
</p>
<p align="center">
<img width="637" alt="image" src="https://github.com/user-attachments/assets/fcfa0185-48c2-49bf-9232-efcf992d9f51" />
</p>

Run below commands to add sarah user and set password </br> 
`sudo useradd -m -s /bin/bash sarah`
`sudo passwd sarah`
New password: </br>
Retype new password: </br>
passwd: password updated successfully </br>
<p align="center">
<img width="497" alt="image" src="https://github.com/user-attachments/assets/a85adb2a-f182-4188-a2da-44ca6f0b3b97" />
</p>
</br>
Run below commands to add workspace, permission and password expiration policy for SARAH. </br> 
Run ``` sudo mkdir -p /home/sarah/workspace ``` </br>
Run `sudo chown sarah:sarah /home/sarah/workspace` </br>
Run `sudo chown 700 /home/sarah/workspace` </br>
Run `sudo change -M 30 sarah` </br>

Run `sudo chage -M 30 sarah` </br>
Run `sudo chage -l sarah` </br>
below are the results screen.
<p align="center">
<img width="704" alt="image" src="https://github.com/user-attachments/assets/d4dbdb06-d93e-4495-800a-eaff3b292576" />
</p>

similar I have created for Mike </br>
<p align="center">
<img width="704" alt="image" src="https://github.com/user-attachments/assets/a429d31f-2ff8-4f5f-b499-f9bca2e99825" />
</p>

Run `sudo nano /etc/login.def`
<p align="center">
<img width="704" alt="https://github.com/user-attachments/assets/c11e993d-cee0-4c81-80e8-53610a48ef26"/>
</p>
Set below value </br>
PASS_MAX_DAYS  30 </br>
PASS_MIN_DAYS  0 </br>
PASS_WARN_AGE  7 </br> 
and Save it.

Run below commands to set password policy
```
sudo nano /etc/pam.d/common-password
sudo apt install libpam-pwquality
```
<p align="center">
<img width="704" alt="https://github.com/user-attachments/assets/f7aa1f54-46be-4af9-ad6e-27dad0ab26bb"/>
</p>

<p align="center">
<img width="704" alt="https://github.com/user-attachments/assets/df85fcea-da63-437e-bb12-bfc1bb408dbe"/>
</p>







## Task 3




