# Linphone User Guide

## Introduction

Linphone is an open-source Voice Over Internet Protocol (VoIP) software that enables free communication over the internet. It supports voice and video calls, messaging, and presence features across multiple platforms such as Windows, macOS, Linux, iOS, and Android. Linphone utilizes the Session Initiation Protocol (SIP) to establish and manage communication sessions, making it a versatile tool for personal and professional use.

## Installation on Linux (Ubuntu)

### Update Package Lists

Before installing Linphone, update your package lists to access the latest versions of available software:

```bash
sudo apt-get update
```

### Install Linphone

Install Linphone from the default repositories:

```bash
sudo apt-get install linphone -y
```

## Configuration

After installing Linphone, configure it by setting up a SIP account to start making or receiving calls.

### Launch Linphone

Start Linphone from the applications menu or by executing `linphone` in the terminal.

### Set Up a SIP Account

Upon opening Linphone for the first time, you may be prompted to set up a SIP account. You can create a new account with Linphone or use an existing one. Enter your SIP username, password, and the server domain.

### Configure Audio and Video Settings

Adjust audio and video settings under **Settings** > **Preferences** in the Linphone application, including selecting preferred devices and codecs.

### Making and Receiving Calls

Make calls by entering the SIP address of the contact and pressing the call button. Linphone automatically notifies you of incoming calls when running.

## Documentation

For detailed guides and additional resources, visit:

- **Official Website:** [https://www.linphone.org](https://www.linphone.org)
- **Wiki and Documentation:** [https://wiki.linphone.org](https://wiki.linphone.org)

## Advanced Configuration and Usage

### Contacts Management

- **Adding Contacts:** Navigate to the contacts section and enter their SIP address.
- **Import/Export Contacts:** Useful for managing contacts across multiple devices or for backup.

### Messaging

Send instant messages and files through the chat interface.

### Multi-Call and Conference

Handle multiple calls or merge them into a conference call for group discussions.

### Security Features

- **Encryption:** Supports end-to-end encryption for secure communications.
- **SIP TLS:** Uses TLS with SIP for encrypted signaling.
- **SRTP:** Enables SRTP for encrypted voice and video data.

### Customization and Preferences

- **Custom Ring Tones:** Customize ring tones for different contacts.
- **Answering Machine:** Receive voice messages when unable to take calls.
- **Network Settings:** Adjust settings like STUN, TURN, and ICE for optimal connectivity.

### Troubleshooting and Support

- **Logging:** The application provides logging features for troubleshooting.
- **Community and Forums:** Access the Linphone community and support forums for help.

## Staying Updated

- **Software Updates:** Regular updates ensure access to the latest features and security patches.
- **Following Development:** Follow the project on GitHub or subscribe to the mailing list for insights.

## Conclusion

Linphone offers a secure, reliable, and feature-rich communication experience. By leveraging its advanced features and ensuring proper configuration, users can enjoy a versatile VoIP solution for both personal and professional needs.
