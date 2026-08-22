# Microsoft

## Steps for Getting an Application Cryptographically Signed for Microsoft Windows

### 1. **Obtain a Code Signing Certificate**

#### a. **Choose a Certificate Authority (CA):**
   - Research and select a reputable Certificate Authority that is trusted by Microsoft Windows (e.g., DigiCert, Sectigo/Comodo, GlobalSign, GoDaddy).
   - Decide whether you need an Organization/Enterprise-validated certificate (OV/EV) or an Individual one. For drivers and higher trust, EV is required.

#### b. **Verify Your Identity:**
   - Submit required identification documents and business verification materials as requested by the CA.
   - The CA will authenticate your information (this step can take a few days).

#### c. **Receive/Download Your Certificate:**
   - After successful verification, you will be able to download your code signing certificate and the associated private key, or install it using the CA's tools.

---

### 2. **Prepare Your Application for Signing**

#### a. **Build/Compile Your Application:**
   - Make sure your application is finalized and ready for distribution (EXE, DLL, MSI, etc.).
   - If signing an installer, build your installer package.

---

### 3. **Install Code Signing Tools**

#### a. **Install Microsoft SignTool:**
   - SignTool is included in the Windows SDK, which can be downloaded from Microsoft:
     [Windows SDK Download](https://developer.microsoft.com/en-us/windows/downloads/windows-sdk/)
   - Install the SDK tools on your build/signing machine.

#### b. **Import Certificate:**
   - Import your code signing certificate into the appropriate certificate store on your signing machine, or have your PFX file available (password-protected).

---

### 4. **Sign the Application**

#### a. **Use SignTool to Sign the Binary:**
   - Open a Command Prompt.
   - Run the following command (update paths and names as appropriate):

     ```
     signtool sign /f YourCertificate.pfx /p yourPassword /tr http://timestamp.digicert.com /td sha256 /fd sha256 YourApp.exe
     ```

   - Options explained:
     - `/f`: The path to your certificate file (PFX)
     - `/p`: The password for the certificate (if required)
     - `/tr`: URL to a timestamp server (important for persistent signatures)
     - `/td`: Digest algorithm for the timestamp
     - `/fd`: File digest algorithm (use SHA256)
     - `YourApp.exe`: The application file you want to sign

#### b. **(Optional) Sign Catalog Files/MSI Installers:**
   - For MSI: Use the same `signtool` command on the `.msi` file.
   - For drivers: You may need to create and sign a `.cat` catalog file.

---

### 5. **Verify the Signature**

#### a. **Check Signature Status:**
   - Right-click the signed file, select **Properties > Digital Signatures** to check signature validity in Windows Explorer.
   - Or, use `signtool verify`:

     ```
     signtool verify /pa /v YourApp.exe
     ```

   - Ensure the signature is valid and timestamped.

---

### 6. **Distribute Your Signed Application**

#### a. **Release Your Application:**
   - You can now distribute the signed application to users, confident that Windows will recognize the signature and warn less about "unknown publisher."

#### b. **(Optional) Submit to Microsoft SmartScreen Reputation:**
   - For new publishers, initial downloads may still warn users. As the app gets downloaded/installed by more users, SmartScreen reputation will build up.

---

## **Summary**

Cryptographically signing your application for Windows ensures users can trust the origin and integrity of your executable. You need a code signing certificate, the application you want to sign, access to Microsoft's signing tools, and a timestamp server to ensure signatures remain valid over time.


