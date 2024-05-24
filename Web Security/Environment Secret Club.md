### Difficulty: Medium

#### Challenge Information:

We've discovered a website that appears to be vulnerable to leaking secrets. Your task is to gather the secrets within the admin account.

 **Author**: m4lwhere
 **Site**: [https://dodcybersentinel-environment-secret-club.chals.io/login](https://dodcybersentinel-environment-secret-club.chals.io/login)

Upon visiting the site, you'll encounter a lengthy text regarding the page. Context clues on the page hint at the use of "git".

By entering any random username and password, you can gain access to the site. Once inside, you'll see a large text resembling SQL injection, but adding secrets won't be helpful.
*Note: I logged in with `a/a` and found the secret key string.*

Let's start by enumerating the `.git` directory on the site. Try both `{url}/git` and `{url}/.git`. The latter should redirect you to a page showing a git folder.

You can use [Git Dumper](https://github.com/arthaud/git-dumper?ref=blog.price.ws) to download the entire repository to your desktop. Once downloaded, navigate into the folder. A useful initial step is to run `ls -la` to check for any hidden files or flags.

Running this command reveals a hidden `.env` file. Inspect this file using `cat .env`.

With the secret key known, verify that it matches the key you saw when logging in.

Next, you'll need the JWT Token. Return to the login page and inspect it.

With some persistence, you'll find a key called `access_token` under 'Application > Local Storage'.

Copy and paste the token into [jwt.io](https://jwt.io/). Modify the code and insert the secret key you found. Change the value of the user to `"admin"`.

Refresh the page, and the flag will be revealed.

**Flag**: `C1{oops_I_l34k3d_my_k3ys!}`

