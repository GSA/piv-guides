The information in this record is targeted to those who are comfortable performing high-level IT tasks.

**Prerequisites**

- A Smart Card reader.
- A PIV ID Badge
- A UNIX/Linux computer correctly configured to use the PIV ID Badge for login.

**SSH Daemon Configuration**
No further SSH Daemon (SSHD) configuration is required. The user&#39;s PIV ID Badge SSH public key can be placed in the appropriate authorized\_keys file (e.g., /home/cmonster/.ssh/authorized\_keys) as needed.

SSHD can be configured to only allow specific users access to a host only via PIV ID Badges. To perform this action, complete the following steps.

1. Change the following configuration in the /etc/ssh/sshd\_config file:
```
      AuthorizedKeysFile /etc/sshd/authorized\_keys/%u
      PasswordAuthentication No
```      
2. Restart sshd.
3. Create the directory: /etc/sshd/authorized\_keys
mkdir /etc/sshd/authorized\_keys

To allow access for a particular user:

Place the user&#39;s PIV ID Badge SSH public key in that directory according to the user name:

/etc/sshd/authorized\_keys/cmonster

**Note:**  This directory and files should only be modifiable by root, thus enforcing the access requirements.

Alternative means of access (i.e., via passwords) should be disabled as needed.

**Logging In via SSH**

1. Insert your PIV ID Badge into the Smart Card reader for your computer.
2. On RHEL and CentOS, run the following commands:
```
      eval $(ssh-agent)
      ssh-add –s libcoolkeypk11.so
```
3. On other distributions, run
```
     eval $(ssh-agent)
     ssh-add –s opensc-pkcs11.so

```
4. Type the PIN when requested at the PIV ID Badge password prompt. 
**Note:**  The card reader may flash. Do not remove the PIV ID Badge from the card reader until the login process is complete.
5. Use the following command to list the user&#39;s public SSH key.
```
     ssh-add –L | egrep  | egrep &#39;ssh-rsa&#39;
```
6. Add this public key to the appropriate authorized\_keys file on the remote machine.
7. The user can now log into the remote machine via the following command:
```
     ssh &lt;remote-host&gt;
```
**Note:**  Do not remove the PIV ID Badge from the card reader until the login process is complete.

The key will no longer work after removing the PIV ID Badge from the card reader. After replacing the badge, you will have to run a command to restart the card before the keys will once again be available to SSH (ssh-add –e opensc-pkcs11.so ).
