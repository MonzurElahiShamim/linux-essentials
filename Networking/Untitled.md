 
 ```bash
# ssh-keygen -y -f file_name.pem > file_name.pub  
#cloud-config  
cloud_final_modules:  
- [users-groups,always]  
users:  
  - name: rizwan  
    groups: [ wheel ]  
    sudo: [ "ALL=(ALL) NOPASSWD:ALL" ]  
    shell: /bin/bash  
    ssh-authorized-keys:  
    - <SSH_PUB_KEY>
```


network design whitepaper
