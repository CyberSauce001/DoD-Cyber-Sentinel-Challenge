### Difficulty: Medium

**Challenge Info:**

We've been alerted that something's been stolen from our network, but none of our sensors found anything out of the ordinary. Can you find if a flag was stolen from our network in the attached packet capture?

**Author:** m4lwhere  
**Package Link:** [Download the package](https://github.com/CyberSauce001/DoD-Cyber-Sentinel-Challenge/blob/main/Forensics/packages/exfiltrated.pcap)

To solve this challenge, follow these steps:

**Step-by-Step Solution:**

1. **Download and Analyze the PCAP:**
   - Download the provided PCAP file.

2. **Choose Your Tool:**
   - You can use either `tshark` or `Wireshark` to analyze the packet capture.

3. **Identify Suspicious Traffic:**
   - Look for unusual patterns in the packet capture. Notably, you'll see that `data.exfiltrated.com` has a subdomain with a long string of uppercase letters.
   - This string is likely encoded in Base32.

4. **Filter the Traffic:**
   - **Using tshark:** Run the following command to filter the traffic:
     ```sh
     tshark -r exfiltrated.pcap -Y 'dns.qry.name contains "exfiltrated.com" && ip.src == 192.168.40.73' -T fields -e dns.qry.name | awk -F'.' '{print $1}' | tr -d '\n'
     ```
   - **Using Wireshark:** 
     - Open the PCAP file in Wireshark.
     - Apply a display filter for `dns.qry.name contains "exfiltrated.com"` and `ip.src == 192.168.40.73`.
     - Export the filtered data to a CSV file.
     - Use `grep` and a delimiter to extract only the Base32 code.

5. **Decode the Base32 String:**
   - Use [CyberChef](https://gchq.github.io/CyberChef/) to decode the extracted Base32 string.
   - The decoded string will be a JPG image.

6. **Extract the Flag:**
   - Open the decoded image to find the flag.

**Flag:**
   - The flag is `C1{dns_3xfil7r4t3d!}`.

