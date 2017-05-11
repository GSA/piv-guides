
## Assumptions

These SSH for Linux procedures are intended to be used by System Administrators (SAs) or other IT professionals. 

## Prerequisites

  * A Smart Card reader
  * A PIV card
  * A UNIX/Linux computer correctly configured to use a PIV card for login

## SSH Daemon configuration

  1. No SSH Daemon (SSHD) configuration is required. Place your PIV card's SSH public key in the appropriate authorized_keys file (e.g., /home/[login ID]/.ssh/authorized_keys).

  2. To optionally configure SSHD to allow specific users to access a host via only PIV cards, complete the following steps:

     1. Change the configuration in the **/etc/ssh/sshd_config** file. Then restart the **sshd**.

        ```
		AuthorizedKeysFile /etc/sshd/authorized_keys/%u
		PasswordAuthentication No
        ```

     2. Create the directory: **/etc/sshd/authorized_keys**.

        ```
		mkdir /etc/sshd/authorized_keys
        ```

     3. To allow a specific user access, place the user&#39;s PIV card's SSH public key in the following directory, according to the user name: **/etc/sshd/authorized_keys/[login ID]**. 

> **Note:** To ensure that access requirements are enforced, only a **root user** may modify this directory and its files.

    4. Disable any alternative means of access (i.e., via passwords, as needed.

## Login via SSH

  1. Insert your PIV ID Badge into the Smart Card reader for your computer.
  2. On RHEL and CentOS, run the following commands:
  
        ```
		eval $(ssh-agent)
		ssh-add –s libcoolkeypk11.so
        ```

  3. On other Linux distributions, run

        ```
		eval $(ssh-agent)
		ssh-add –s opensc-pkcs11.so

        ```
  4. Type the PIN when requested at the PIV ID Badge password prompt. 
  
  > **Note:**  The card reader may flash. Do not remove the PIV ID Badge from the card reader until the login process is complete.

  5. Use the following command to list the user&#39;s public SSH key.
  
        ```
		ssh-add –L | egrep  | egrep &#39;ssh-rsa&#39;
        ```

 6. Add this public key to the appropriate authorized_keys file on the remote machine.
 7. The user can now log into the remote machine via the following command:
 
        ```
		ssh &lt;remote-host&gt;
        ```

  > **Note:**  Do not remove the PIV ID Badge from the card reader until the login process is complete.

  > The key will no longer work after removing the PIV ID Badge from the card reader. After replacing the badge, you will have to run a command to restart the card before the keys will once again be available to SSH (ssh-add –e opensc-pkcs11.so ).
