### Difficulty: Easy

**Challenge Info:**

We received this memo from the supervisor, but it has some serious issues. Can you figure it out?  
**Author:** nord  
**Package Link:** [Download the package](Filing Problem - memo)

To solve this challenge, follow these steps:

**Step-by-Step Solution:**

1. **Download the Package:**
   - Download the provided package. You might notice that you're unable to open the file because it has an unknown file format.

2. **Use a Hex Editor:**
   - Go to [HexEd.it](https://hexed.it/) and import the package file.
   - Skim through the hex data. You'll notice patterns that suggest it's a PDF file. A common method to identify a PDF is searching for '16 0 obj' in Google, which indicates a PDF structure.
   - Additionally, look for the hex sequence `0D 0A 25 25 45 4F 46 0D 0A`, which corresponds to the PDF trailer `..%%EOF..`.

3. **Convert to PDF:**
   - Save the file with a `.pdf` extension (e.g., `file.pdf`) to convert it to a readable PDF format.

4. **Read the PDF:**
   - Open the converted PDF. The content might appear redacted.
   - Copy the entire text from the PDF and paste it into a text editor of your choice.

5. **Find the Flag:**
   - Carefully read through the text in the text editor to find the hidden flag.

**Flag:**
   - The flag is `C1{c0rrup7ion_4nd_r3dac7tion}`.

