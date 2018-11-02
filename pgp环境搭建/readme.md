# windows下使用PGP

1. 下载PGP

https://www.gnupg.org/download/

2. 安装

3. 将pgp加入到path路径中

4. 验证是否安装成功

```bash
C:\Users\zhangzhongjun>gpg --version
gpg (GnuPG) 2.2.10
libgcrypt 1.8.3
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Home: C:/Users/zhangzhongjun/AppData/Roaming/gnupg
Supported algorithms:
Pubkey: RSA, ELG, DSA, ECDH, ECDSA, EDDSA
Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
        CAMELLIA128, CAMELLIA192, CAMELLIA256
Hash: SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
Compression: Uncompressed, ZIP, ZLIB, BZIP2
```

5. 创建公私钥对

> 密码是 zhangzhongjun

```bash
$ gpg --gen-key
gpg: C:/Users/zhangzhongjun/AppData/Roaming/gnupg/trustdb.gpg: trustdb created
gpg: key 531BCDA4F0BB294E marked as ultimately trusted
gpg: directory 'C:/Users/zhangzhongjun/AppData/Roaming/gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as 'C:/Users/zhangzhongjun/AppData/Roaming/gnupg/openpgp-revocs.d\34E845556F6C2B1E6BB552C0531BCDA4F0BB294E.rev'
public and secret key created and signed.

pub   rsa2048 2018-10-30 [SC] [expires: 2020-10-29]
      34E845556F6C2B1E6BB552C0531BCDA4F0BB294E
uid                      ZhangZhongJun <18835109707@163.com>
sub   rsa2048 2018-10-30 [E] [expires: 2020-10-29]
```

6. 发布公钥

> key id就是指纹的最后8个16进制字母

```bash
C:\Users\zhangzhongjun>gpg --keyserver hkp://pool.sks-keyservers.net --send-keys F0BB294E
C:\Users\zhangzhongjun>gpg --keyserver hkp://keyserver.ubuntu.com:11371 --send-keys F0BB294E
```

是否发布成功

```bash
C:\Users\zhangzhongjun>gpg --keyserver hkp://keyserver.ubuntu.com:11371 --recv-keys F0BB294E
```

# 参考文献

https://central.sonatype.org/pages/working-with-pgp-signatures.html