# Graded-Assignment-on-Testing-Linux-and-Servers

## Task 1 System Monitoring Setup

Run `sudo apt update`
<p align="left">
<img width="717" alt="image" src="https://github.com/user-attachments/assets/c9451c3b-4033-4440-ab09-a899d6e8ed34" />
</p>

Run `Sudo apt-get install htop -y` . </br>
After installing i have ran `htop --version` to check the version .
<p align="left">
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
<p align="left">
<img width="589" alt="image" src="https://github.com/user-attachments/assets/32a8c5d9-97e3-450f-a521-33fb929a869d" />
</p>
</br>
verify code 
Run 'cat sys_monitor.sh' for verify created .sh file code.</br>

Run 'sudo chmod -x sys_monitor.sh'</br>
Run 'sudo chmod +x sys_monitor.sh'</br>
Run `sudo ./sys_monitor.sh` </br>
run `ls`</br>
<p align="left">
<img width="708" alt="image" src="https://github.com/user-attachments/assets/b310de81-d829-49bc-be60-a9e8d98f83e1" />
</p>
</b>
log results for manual execution 
<p align="left">
<img width="1328" alt="image" src="https://github.com/user-attachments/assets/38a8ceee-b2c0-41ea-8b98-0cd094a5f30a" />
</p>
<p align="left">
<img width="1409" alt="image" src="https://github.com/user-attachments/assets/10467d93-7aa0-4132-a858-8f10f39a4f86" />
</p>

Creating Cron jobs to automate the sys_monitor.sh to run automically. </b>
Run `crontab -e` </b>
selected option 1
<p align="left">
<img width="585" alt="image" src="https://github.com/user-attachments/assets/1085e6f0-09bb-48ef-aa26-6e8c697bdd56" />
</p>

## Task 2 User Management and Access Control
Run `sudo apt update` </b>
<p align="left">
<img width="452" alt="image" src="https://github.com/user-attachments/assets/2d0d2ecc-fa3d-4cc1-97a2-bb0f3f9849d8" />
</p>
<p align="left">
<img width="637" alt="image" src="https://github.com/user-attachments/assets/fcfa0185-48c2-49bf-9232-efcf992d9f51" />
</p>

Run below commands to add sarah user and set password </br> 
`sudo useradd -m -s /bin/bash sarah`
`sudo passwd sarah`
New password: </br>
Retype new password: </br>
passwd: password updated successfully </br>
<p align="left">
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
<p align="left">
<img width="704" alt="image" src="https://github.com/user-attachments/assets/d4dbdb06-d93e-4495-800a-eaff3b292576" />
</p>

similar I have created for Mike </br>
<p align="left">
<img width="704" alt="image" src="https://github.com/user-attachments/assets/a429d31f-2ff8-4f5f-b499-f9bca2e99825" />
</p>

Run `sudo nano /etc/login.def`
<p align="left">
<img width="724" alt="image" src="https://github.com/user-attachments/assets/885dd57f-768f-4848-8317-a65944d10de1" />
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
<p align="left">
<img width="887" alt="image" src="https://github.com/user-attachments/assets/45d646d7-3c17-4032-8a2c-c0061cee109b" />

</p>

modified `password requisite pam_pwquality.so retry=3`
<p align="left">
<img width="977" alt="image" src="https://github.com/user-attachments/assets/27d2b0f4-de8d-4349-8f26-aa3e1e0dd57a" />
</p> 
to `password requisite pam_pwquality.so retry=3 minlet=8 ucredit=-1 lcredit=-1 ocredit=-1` as shown in the below screen.
<p align="left">
<img width="802" alt="image" src="https://github.com/user-attachments/assets/cbc97d8e-afee-4f1f-9bdf-837b0cd56f69" />
</p>

Run below command to check human users 
```
awk -F: '$3 >= 1000 && $3 <65534 { print $1 }' /etc/passwd
```
<p align="left">
<img width="452" alt="image" src="https://github.com/user-attachments/assets/5de78703-3d49-41b2-a51d-9228d750bbf7" />
</p>

Run `cat /etc/passwd`
<p align="left">
<img width="1076" alt="image" src="https://github.com/user-attachments/assets/0e94ba8d-8a85-4816-b00a-99ccd9c48779" />
</p>

## Task 3 Backup Configuration for Web Servers
Run below commands to create automatic backup for SARAH. </br>

```
sudo mkdir -p /backups
sudo chmod 700 / backups 
sudo nano /home/sarah/apache_backup.sh
```

Add below code in apache_backup.sh file  </br>

```
#!/bin/bash
# Backup Apache file
DATE=$(date +%F)
BACKUP_FILE="/backups/apache_backup_${DATE}.tar.gz"
LOG_FILE="/backups/apache_backup_${DATE}.10g"
# Create backup
tar -czf "$BACKUP_FILE" /etc/httpd/ /var/www/html/ 2>> "$LOG_FILE"
# Verify backup
{
echo "Backup verification for Apache - $DATE" echo "Contents of $BACKUP_FILE:"
tar -tzf "$BACKUP_FILE"
} > "$LOG_FILE" 2>&1
```

Run `sudo cat /home/sarah/apache_backup.sh` to validate script file.</br>
<p align="left">
<img width="889" alt="image" src="https://github.com/user-attachments/assets/8a07d883-61d2-48c3-9ba8-8b5bce762cff"/>
</p>

Run below commands to make sh file as executable and add cron scheduler</br>

```
sudo chmod +x /home/sarah/apache_backup.sh
sudo crontab -u sarah -e
```

<p align="left">
<img width="954" alt="image" src="https://github.com/user-attachments/assets/4b9ffbcc-6491-485b-8f1d-470f354453e5" />
<img width="890" alt="image" src="https://github.com/user-attachments/assets/4068b1a4-d4dd-484f-b991-af9f9774ecf9" />
</p>

Now creating backup for Mike to backup Nginx files </br>
<p align="left">
<img width="1109" alt="image" src="https://github.com/user-attachments/assets/db93957e-dfd1-47c3-bce9-059e502a0bf7" />
</p>

below is the code </br>

```
#!/bin/bash
# Backup Nginx files for Mike

DATE=$(date +%F)
BACKUP_FILE="/backups/nginx_backup_${DATE}.tar.gz"
LOG_FILE="/backups/nginx_backup_${DATE}.log"

# Create backup
tar -czf "$BACKUP_FILE" /etc/nginx/ /usr/share/nginx/html/ 2>> "$LOG_FILE"

# Verify backup
{
  echo "Backup verification for Nginx - $DATE"
  echo "Contents of $BACKUP_FILE:"
  tar -tzf "$BACKUP_FILE"
} >> "$LOG_FILE" 2>&1
```

validate script </br>
<p align="left">
<img width="411" alt="image" src="https://github.com/user-attachments/assets/4abc4155-bafe-450c-b595-18d0e39b066f" />
</p>

Run Below commands to make it executable file and set cron scheduler </br>

```
sudo chmod +x /home/mike/nginx_backup.sh
sudo crontab -u mike -e
```

<p align="left">
<img width="805" alt="image" src="https://github.com/user-attachments/assets/34df5393-35f0-48db-a676-9faa4e604206" />
</p>

checking backups </br>
<p align="left">
<img width="452" alt="image" src="https://github.com/user-attachments/assets/ac5d3868-b6c9-4e57-a882-6d5db2296cd6" />
</p>
<p align="left">
<img width="452" alt="image" src="https://github.com/user-attachments/assets/6eac8a03-168f-40af-94bd-86318165f489" />
</p>

Ran below commands</br>

```
cd ..
ls
cd backups
ls -ld /backups
ls -l /backups
sudo chmod 755 /backups
cd backups
ls
````

Back Results for SARAH</br>
<p align="left">
<img width="452" alt="image" src="https://github.com/user-attachments/assets/cf2d08d7-4355-4ee2-8770-889396f61ae8" />
</p>
Back Results for MIKE</br>
<p align="left">
<img width="452" alt="image" src="https://github.com/user-attachments/assets/218c7ed8-b5e8-46b6-9a22-c6202f9a3f61" />
</p>














