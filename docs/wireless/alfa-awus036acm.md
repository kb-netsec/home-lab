Found a wireless adapter for my Debian lab workstation. I wanted an adapter that had good Linux compatibility with monitor mode and packet injection. 

I plugged it in out of the box and Debian could already see it. Ok, off to a good start. 

```
$ lsusb
Bus 001 Device 063: ID 0e8d:7612 MediaTek Inc. MT7612U 802.11a/b/g/n/ac Wireless Adapter
```

Next I went to https://info.alfa.com.tw/awus036acm 

Went to the Linux support page which had an adorable support table. I've added my own headers here for amusement and also because theirs didn't have any. 

| OS     | Status     | Is it good?
| -------| ---------- | ------------- |
| Kali 2022.2       | Cell 2        |
| Kali 2021.3       | Cell 4        |
| Ubuntu 22.04 | Works out-of-the-box | Good |
| Ubuntu 20.10
| Debian 11.0.3
| Debian 10.7.0
| Raspberry Pi OS (32-bit) (rev 2020-08-20)
| Raspberry Pi OS (32-bit) (rev 2022-04-04)

Support status:

Kali 2022.2	Works out-of-the-box	Good
Kali 2021.3	Works out-of-the-box	Good
Ubuntu 22.04	Works out-of-the-box	Good
Ubuntu 20.10	Works out-of-the-box	Good
Debian 11.0.3	Works	Good
Debian 10.7.0	Works	Good
Raspberry Pi OS (32-bit) (rev 2020-08-20)	Works out-of-the-box	Good
Raspberry Pi OS (32-bit) (rev 2022-04-04)	Works out-of-the-box	Good

