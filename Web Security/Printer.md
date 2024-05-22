### Difficulty: Easy

**Challenge Info:**

I've been trying to access the control panel for my multifunction printer but can't remember the password. Can you help me log in?  
**Author:** Tsuto  
**Site:** [Printer Control Panel](https://web-printer-t34jla4lcq-uc.a.run.app/)

To solve this challenge, you'll need to explore the webpage and use `gobuster` to discover additional pages.

**Steps to Follow:**

1. **Run Gobuster**: Use the following command to scan for hidden directories:
   ```sh
   gobuster dir -u https://web-printer-t34jla4lcq-uc.a.run.app/ -w /usr/share/wordlists/{your_wordlist}
   ```
   - You can use the default wordlists that come with Kali Linux or download SecLists for more options.

2. **Finding hidden index**: Gobuster should reveal a `robots.txt` file. Access it by appending it to the URL:
   ```
   https://web-printer-t34jla4lcq-uc.a.run.app/robots.txt
   ```
   This file indicates that `/notes.txt` is disallowed from being indexed.

3. **Access notes.txt**: Navigate to the notes file:
   ```
   https://web-printer-t34jla4lcq-uc.a.run.app/notes.txt
   ```
   Here, you'll find the password: `fAES5I64X1EL`.

4. **Retrieve the Flag**: Use the password to log in and you will see the flag:
   ```
   C1{p1nt1ng_fl4g5}
   ```

**Notes:**

- It might take some time to find the correct wordlist that identifies `robots.txt` or `notes.txt`. Start by manually checking common filenames like `robots.txt` or `secrets.txt`.
- Using a comprehensive wordlist like `directory-list-2.3-medium.txt` can help you save time during your scan.

Good luck!
