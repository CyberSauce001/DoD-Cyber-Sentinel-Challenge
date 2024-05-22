### Difficulty: Easy

**Challenge Info:**

Our intelligence team received an anonymous tip that our website is leaking secrets. It appears that an insider threat has implanted an encoded message on our index.html landing page. We need your help to find and decode this message! 

To protect our agency, we have taken the webpage down but saved it to a Docker instance so you can interact with the site and figure this out for us. 

**Author:** r0m

**Package Link:** [Download the package](https://github.com/CyberSauce001/DoD-Cyber-Sentinel-Challenge/blob/main/Networking%20%26%20Reconnaissance/Packages/Header%20Hinterlands.zip)

**Instructions:**

1. **Set Up Docker:**
   - If you haven't already, set up Docker on your machine.
   - Load the Docker file through your terminal with the following commands:
     ```sh
     docker load -i {filename}.tar
     docker images
     docker run -d -p 1234:80 {image_id}
     docker ps
     ```
   - Replace `{filename}.tar` with the actual filename and `{image_id}` with the appropriate image ID from the `docker images` output.

2. **Access the Local Website:**
   - Open your web browser and go to `http://localhost:1234` (or whatever port you used).

3. **Inspect HTTP Headers:**
   - Run the following `curl` command to fetch the HTTP headers:
     ```sh
     curl -sI http://localhost:1234
     ```
   - Look for a header named `X-Syndicate-Command` which contains a Base64 encoded string.

4. **Decode the Base64 String:**
   - Use [CyberChef](https://gchq.github.io/CyberChef/) to decode the Base64 string.
   - Paste the Base64 encoded string into CyberChef and apply the "From Base64" operation to reveal the hidden message.

**Flag:**
   - The decoded message will reveal the flag: `C1{am@z1ng_wh@t_u_c@n_h1d3_1n_h3@d3rs}`.


