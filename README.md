### DBC2 is DropboxC2
  
DBC2 (DropboxC2) is a modular post-exploitation tool, composed of an agent, a controler, running on any machine, and some modules.
  
To start the image in interactive mode:
  
`docker run --rm -ti arno0x0x/dbc2`
  
If you want to save the accesstoken and master key, edit the /dbc2/config.py file in the container or simply copy the desired config.py file from the host to the container.

Project official repository is here: [DBC2 on GitHub](https://github.com/Arno0x/DBC2)

Security Aspects
-----------

DBC2 controller requires a master password to be given when it starts. This password is then derived into a 128 bits master key by the use of the PBKDF function from the pyscrypt library. The master key is then base64 encoded and can (*optionnal*) be saved in the config file.

DBC2 performs end-to-end encryption of data using the master key with AES-128/CBC mode. Data exchanged between the agent and the controller flows through the Dropbox servers so while the transfer itself is encrypted, thanks to HTTPS, it had to be end-to-end encrypted to protect the data while at rest on the Dropbox servers.

DBC2 also performs obfuscation of the stages and the modules by the use of some XOR encryption, which is dumb encryption but is enough to simply obfuscate some well known and publically available piece of codes. The key used to perform XOR encryption is a SHA256 hash of the master key.