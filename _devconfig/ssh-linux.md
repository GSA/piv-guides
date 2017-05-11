
## Assumptions

These SSH for Linux procedures are intended for use by System Administrators (SAs) or other IT professionals. 

## Prerequisites

  * A Smart Card reader
  * A PIV card
  * A UNIX/Linux computer correctly configured to use a PIV card for login

## configure SSH Daemon

  1. No SSH Daemon (SSHD) configuration is required. Place your **PIV card's SSH public key** in the appropriate authorized_keys file (e.g., /home/[login ID]/.ssh/authorized_keys).

  2. To optionally configure SSHD so that specific users may access a host via only their PIV cards, complete the following steps:

     1. Change the configuration in the **/etc/ssh/sshd_config** file. Then restart the **sshd**.

        ```
		AuthorizedKeysFile /etc/sshd/authorized_keys/%u
		PasswordAuthentication No
        ```

     2. Create the directory: **/etc/sshd/authorized_keys**.

        ```
		mkdir /etc/sshd/authorized_keys
        ```

     3. To allow only one user to have such access, place the user&#39;s PIV card's SSH public key in the following directory, according to the user name: **/etc/sshd/authorized_keys/[login ID]**. (**Note:** To ensure that access requirements are enforced, only a **root user** may modify this directory and its files.)  

     4. Disable any alternative means of access (i.e., via passwords, as needed.


## Log in via SSH

  1. Insert your PIV card into your computer's the card reader.
  2. On **RHEL** and **CentOS**, run the following commands:
  
        ```
		eval $(ssh-agent)
		ssh-add –s libcoolkeypk11.so
        ```

  3. On other Linux distributions, run the following commands:

        ```
		eval $(ssh-agent)
		ssh-add –s opensc-pkcs11.so
        ```

  4. At the PIV card password prompt, enter your PIN. 
  
  > **Note:**  The card reader may flash. **Do not** remove the PIV card until the login process has been completed.

  5. Use the following command to list the user&#39;s public SSH key:
  
        ```
		ssh-add –L | egrep  | egrep &#39;ssh-rsa&#39;
        ```

 6. Add the user's public SSH key to the appropriate authorized_keys file on the remote machine.
 7. The user will now be able to log into the remote machine by using the following command:
 
        ```
		ssh &lt;remote-host&gt;
        ```

  > **Note:**  Do not remove the PIV card from the card reader until the login process has been completed. The key will no longer work after removing the PIV ID Badge from the card reader. After replacing the PIV card, run a command to restart the card before the keys will once again be available to SSH. 
  
    ```
		ssh-add –e opensc-pkcs11.so
    ```
