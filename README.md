# TOTP auth tool

## Prepare:

1. Install depencenies:
  - [oath toolkit](https://www.nongnu.org/oath-toolkit/): `brew install oath-toolkit`
  - [openssl](https://www.openssl.org/): `brew install openssl`
2. Encrypt your TOTP tokens. for every token, do:
  - `echo $TOTPTOKEN | openssl aes-256-cbc -salt > ~/.totp_enc_$TOTPNAME` where `$TOTPTOKEN` ist the token you get from your TOTP provider (e.g. MSI) and `$TOTPNAME` is a name you can choose freely
  - Enter your password twice
  - optional: execute `cat ~/.totp_enc_$TOTPNAME | openssl aes-256-cbc -d` and enter your password to check if encryption succeeded

## Usage:

The TOTP Auth application checks for files in `~` matching `.totp_enc_*`. If there is more than one finding, it lets you choose which one you'd like to use.   
Then you have to enter your password, so that the application can decrypt the token and create a OTP with the `oathtool` command (which is `oathtool --totp -b $TOKEN`.   
If the request succeeds, the application will copy the received OTP into the Clipboard and displays it as a desktop notification.
If someting fails, a notification holding additional information is shown.

## Contact

thomas.liebeskind@gmail.com