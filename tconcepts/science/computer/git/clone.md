# Clone 

**Cloning is when you copy a git repo to your own computer**

## What is cloning?

Cloning is when you copy a git instance - literally cloning it.  
You will typically need to do this in order to alter it.

This example assumes you have these details and that we are using GitHub
and that we are using the SSH protocol which makes pushing changes back
much easier since you do not need to remember your password.

Remember to use your own password and your own repository name.

- **User**: `johno`  
- **Repository name**: `press`

### Steps to Clone the Repository with SSH

1. **Copy the Repository SSH URL**

   Use the SSH URL for the repo. For this example, the URL will be:  
   ```
   git@github.com:johno/press.git
   ```
   > **Note:** You must have your SSH key added to your GitHub account.

2. **Open a Terminal**

3. **Type the Clone Command**

   In your terminal, type:
   ```bash
   git clone git@github.com:johno/press.git
   ```

4. **Press Enter**

5. **Done!**

You’ll now have a folder named `press` with all the repository contents.

