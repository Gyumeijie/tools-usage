# Synopsis

```bash
$ openssl enc -ciphername [options]
```


## Cipher alogorithms

To get a list of available ciphers you can use the ***list-cipher-algorithms*** command

```
$ openssl list-cipher-algorithms

AES-128-CBC
AES-128-CFB
AES-128-CFB1
AES-128-CFB8
AES-128-CTR
AES-128-ECB
...
```
```bash
Valid ciphername values:

 -aes-128-cbc       -aes-128-cfb       -aes-128-cfb1            
 -aes-128-cfb8      ...          
 ```

## Options

-in ***filename***
> This specifies the input file.

-out ***filename***
> This specifies the output file. It will be created or overwritten if it already exists.

-e or -d
> This specifies whether to encrypt (***-e***) or to decrypt (***-d***). Encryption is the default.

-iv ***IV*** :deciduous_tree:
> This specifies the ***initialization vector*** IV as hexadecimal number. If not explicitly given it will be derived from the password.

-K ***key*** :deciduous_tree:
> This option allows you to set the key used for encryption or decryption. This is the key directly used by the cipher algorithm. If no key is given OpenSSL will derive it from a password.

-salt, -nosalt, -S ***salt*** :deciduous_tree:
> These options allow to switch salting on or off. With -S salt it is possible to explicitly give its value (in hexadecimal).

-p, -P
> Additionally to any encryption tasks, this ***prints*** the `key`, `initialization vector` and `salt value` (if used). 

-pass ***arg***
> This specifies the password source. Possible values for ***arg*** are `pass:password` or `file:filename`, where password is your password and filename file containing the password.

## Examples

```bash
$ cat text.plain
Gyumeijie
```
### Encryption

```bash
$ openssl enc -aes-256-cbc -pass pass:password -nosalt  -p  -in text.plain -out secrete.enc
key=5F4DCC3B5AA765D61D8327DEB882CF992B95990A9151374ABD8FF8C5A7A0FE08
iv =B7B4372CDFBCB3D16A2631B59B509E94
```
### Decryption

```bash
$ openssl enc -d -aes-256-cbc -K '5F4DCC3B5AA765D61D8327DEB882CF992B95990A9151374ABD8FF8C5A7A0FE08' -iv 'B7B4372CDFBCB3D16A2631B59B509E94'  -in  secrete.enc
Gyumeijie
```

