# Apple 

**Code Signing for Canadian Companies.**

## 1. Apple Developer Program Enrollment

- **D-U-N-S Number:** Required for Canadian legal entities. Obtain from Dun & Bradstreet Canada. Ensure your business name/address matches your government registration.
- **Business Documents:** Apple may request official Canadian business documents (e.g., Articles of Incorporation).
- **Legal Entity Name:** Must match your government-registered name.
- **Authorized Enroller:** The person enrolling must be legally authorized to sign for the company.

## 2. Enroll & Set Up

- Register or use an Apple ID.
- Join the [Apple Developer Program](https://developer.apple.com/programs/)
- Submit D-U-N-S and documents, pay annual fee, complete identity checks.

## 3. Obtain Certificates

- Use Keychain Access on Mac to generate a Certificate Signing Request (CSR).
- In the [Apple Developer Portal](https://developer.apple.com/account/resources/certificates/list), issue and download the appropriate signing certificate (e.g., Developer ID or Distribution).
- Install the certificate on your Mac.

## 4. Provisioning Profiles (iOS/macOS non–App Store apps)

- Register App IDs and test devices if needed.
- Create, download, and install provisioning profiles from the Developer Portal.

## 5. Build & Sign Your Application

- **Manual signing example:**  
  ```
  codesign --deep --force --options runtime --sign "Developer ID Application: Your Name (TEAMID)" /path/to/YourApp.app
  ```

## 6. Notarize Your macOS Application

- Submit your signed app for notarization:
  ```
  xcrun altool --notarize-app --primary-bundle-id "com.yourcompany.yourapp" --username "your@appleid.com" --password "app-specific-password" --file YourApp.zip
  ```
- After approval, staple the notarization ticket:
  ```
  xcrun stapler staple /path/to/YourApp.app
  ```

## 7. Verify Signature and Notarization

- Check signature:
  ```
  codesign --verify --deep --strict --verbose=2 /path/to/YourApp.app
  ```
- Check notarization:
  ```
  spctl --assess --type execute --verbose /path/to/YourApp.app
  ```

## 8. Distribute

- **Outside App Store:** Distribute signed, notarized app (e.g., ZIP/DMG).

---

**Summary**:  

Canadian companies must use their exact legal name and D-U-N-S number when enrolling. Code signing and notarization are required for distributing macOS/iOS apps and ensuring integrity and trust.  
[Apple’s notarization guide](https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution) provides further detail.
