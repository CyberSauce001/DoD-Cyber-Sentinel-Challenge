### Difficulty: Easy

### Challenge Info

We've received intelligence that an attacker is hosting flags for others to find. However, it seems that this flag is hosted on a non-standard port. Can you find the service and read the flag?

You will need to SSH into the machine and search for an open port on the localhost. The credentials are:
- **Username:** ctfuser
- **Password:** ctfpassword

**Author:** m4lwhere

To access the machine, use the following SSH command:
```
ssh -p 22631 ctfuser@0.cloud.chals.io
```
-------------------------------------------------------------

First log into the machine with the infomation given above.
Then follow the steps below:

1. Find the IP address of the machine.
2. Use `nmap` to scan for open ports:
   ```
   nmap -sV -Pn -p- -v -T4 {IP address}
   ```
   This scan will take some time. Eventually, it will discover an unknown port, `51147`.

3. To retrieve the flag, you can also use `nc` (netcat) on the discovered port, otherwise the nmap should display the flag for you:
   ```
   nc {IP address} 51147
   ```

The flag is:
```
C1{ch3ck_4ll_p0rts!}
```
