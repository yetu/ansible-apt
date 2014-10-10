[![Build Status](https://travis-ci.org/yetu/ansible-unattended.svg?branch=master)](https://travis-ci.org/yetu/ansible-unattended)

Ansible Unattended Role
==================

Ansible unattended upgrades does automatic package updates on debian systems (tested on vagrant ubuntu 12.04).
for more info check [https://help.ubuntu.com/12.04/serverguide/automatic-updates.html](https://help.ubuntu.com/12.04/serverguide/automatic-updates.html)



##Variables 
  All the default variables are located **defaults/main.yml**. Mostly you would need to configure the following variables. 

   - *unattended_blacklist:* Array of packages to not update (set [ ] for empty list) 

       ```unattended_blacklist: [ vim;, libc6; ]```
  
   - *unattended_origins:*  Upgrade packages from these (origin:archive) pairs

    ```
    unattended_origins      :
        security  : true
        updates   : false
        proposed  : false
        backports : false
    ```
    
   - *unattended_autofix:* Allows you to control if on a unclean dpkg exit will automatically run dpkg --force-confold --configure -a

    ```unattended_autofix : true```  
    
    
   - *unattended_steps:* Split the upgrade into the smallest possible chunks 

    ```unattended_steps: false```  
    
    
   - *unattended_shutdown:* Install all unattended-upgrades when the machine is shuting down instead of doing it in the background.
    
    ```unattended_shutdown: false```

   - *unattended_mail:* Send email to this address. (set false to disable emails)

    ```unattended_mail: root```
    
   - *unattended_mail_error:* Get emails only on errors. Default is to always send a mail if unattended_mail is set

    ```unattended_mail_error: false```      

   - *unattended_remove_unused:* Automatic removal of new unused dependencies after the upgrade

    ```unattended_remove_unused: false```      

   - *unattended_automatic_reboot:* Automatically reboot *WITHOUT CONFIRMATION* if packages require that

    ```unattended_automatic_reboot: false```    

   - *unattended_automatic_reboot:* Use apt bandwidth limit feature, Set to Integer representing kb/sec limit else false

    ```unattended_download_limit: 200```


##Configure
You can configure your variables in ansible with one of the following

 * Create a variable in host/group variables directory. (recommended)
 * Editing var/main.yml
 * Run ansible-playbook with -e
 * Edit the default/main.yml (not recommended)



##Test
* Running ```sudo unattended-upgrade --dry-run -d``` should work with no error and simulate installing updates


