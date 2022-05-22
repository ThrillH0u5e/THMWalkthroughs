# GamingRoom

Target IP 10.10.53.164 

curl [http://ip/10.10.53.164/dict.lst](http://ip/uploads/dict.lst) > pwlist.txt

gobuster dir -u 10.10.53.164 -w /usr/share/wordlists/dirb/common.txt -t 200

/secret directory found!

RSA Key:

```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,82823EE792E75948EE2DE731AF1A0547

T7+F+3ilm5FcFZx24mnrugMY455vI461ziMb4NYk9YJV5uwcrx4QflP2Q2Vk8phx
H4P+PLb79nCc0SrBOPBlB0V3pjLJbf2hKbZazFLtq4FjZq66aLLIr2dRw74MzHSM
FznFI7jsxYFwPUqZtkz5sTcX1afch+IU5/Id4zTTsCO8qqs6qv5QkMXVGs77F2kS
Lafx0mJdcuu/5aR3NjNVtluKZyiXInskXiC01+Ynhkqjl4Iy7fEzn2qZnKKPVPv8
9zlECjERSysbUKYccnFknB1DwuJExD/erGRiLBYOGuMatc+EoagKkGpSZm4FtcIO
IrwxeyChI32vJs9W93PUqHMgCJGXEpY7/INMUQahDf3wnlVhBC10UWH9piIOupNN
SkjSbrIxOgWJhIcpE9BLVUE4ndAMi3t05MY1U0ko7/vvhzndeZcWhVJ3SdcIAx4g
/5D/YqcLtt/tKbLyuyggk23NzuspnbUwZWoo5fvg+jEgRud90s4dDWMEURGdB2Wt
w7uYJFhjijw8tw8WwaPHHQeYtHgrtwhmC/gLj1gxAq532QAgmXGoazXd3IeFRtGB
6+HLDl8VRDz1/4iZhafDC2gihKeWOjmLh83QqKwa4s1XIB6BKPZS/OgyM4RMnN3u
Zmv1rDPL+0yzt6A5BHENXfkNfFWRWQxvKtiGlSLmywPP5OHnv0mzb16QG0Es1FPl
xhVyHt/WKlaVZfTdrJneTn8Uu3vZ82MFf+evbdMPZMx9Xc3Ix7/hFeIxCdoMN4i6
8BoZFQBcoJaOufnLkTC0hHxN7T/t/QvcaIsWSFWdgwwnYFaJncHeEj7d1hnmsAii
b79Dfy384/lnjZMtX1NXIEghzQj5ga8TFnHe8umDNx5Cq5GpYN1BUtfWFYqtkGcn
vzLSJM07RAgqA+SPAY8lCnXe8gN+Nv/9+/+/uiefeFtOmrpDU2kRfr9JhZYx9TkL
wTqOP0XWjqufWNEIXXIpwXFctpZaEQcC40LpbBGTDiVWTQyx8AuI6YOfIt+k64fG
rtfjWPVv3yGOJmiqQOa8/pDGgtNPgnJmFFrBy2d37KzSoNpTlXmeT/drkeTaP6YW
RTz8Ieg+fmVtsgQelZQ44mhy0vE48o92Kxj3uAB6jZp8jxgACpcNBt3isg7H/dq6
oYiTtCJrL3IctTrEuBW8gE37UbSRqTuj9Foy+ynGmNPx5HQeC5aO/GoeSH0FelTk
cQKiDDxHq7mLMJZJO0oqdJfs6Jt/JO4gzdBh3Jt0gBoKnXMVY7P5u8da/4sV+kJE
99x7Dh8YXnj1As2gY+MMQHVuvCpnwRR7XLmK8Fj3TZU+WHK5P6W5fLK7u3MVt1eq
Ezf26lghbnEUn17KKu+VQ6EdIPL150HSks5V+2fC8JTQ1fl3rI9vowPPuC8aNj+Q
Qu5m65A5Urmr8Y01/Wjqn2wC7upxzt6hNBIMbcNrndZkg80feKZ8RD7wE7Exll2h
v3SBMMCT5ZrBFq54ia0ohThQ8hklPqYhdSebkQtU5HPYh+EL/vU1L9PfGv0zipst
gbLFOSPp+GmklnRpihaXaGYXsoKfXvAxGCVIhbaWLAp5AybIiXHyBWsbhbSRMK+P
-----END RSA PRIVATE KEY-----
```

chmod 400 - id_rsa 

Inspect Page source on website:

`<!-- john, please add some actual content to the site! lorem ipsum is horrible to look at. -->`

I took this as a hint to use john the ripper. 

python3 /usr/share/john/ssh2john.py id_rsa > id_rsa.hash

john id_rsa.hash

![Screen Shot 2022-05-22 at 12.49.58 PM.png](GamingRoom%207dad8e9817ce49f3a4e1798acbf9451e/Screen_Shot_2022-05-22_at_12.49.58_PM.png)

ssh pw: letmein

![Screen Shot 2022-05-22 at 12.51.11 PM.png](GamingRoom%207dad8e9817ce49f3a4e1798acbf9451e/Screen_Shot_2022-05-22_at_12.51.11_PM.png)

First flag found.

from John@exploitable I ran

find / -perm -u=s -type f 2>/dev/null

![Screen Shot 2022-05-22 at 12.54.38 PM.png](GamingRoom%207dad8e9817ce49f3a4e1798acbf9451e/Screen_Shot_2022-05-22_at_12.54.38_PM.png)

first I went to GTFO bins to see if mount showed anything but you need sudo privileges

Googled lxc-user-nic and found: 

[https://steflan-security.com/linux-privilege-escalation-exploiting-the-lxc-lxd-groups/](https://steflan-security.com/linux-privilege-escalation-exploiting-the-lxc-lxd-groups/)

This article basically gives you the blueprint for a linux container build. 

Upload as a tar.gz file to the attack machine with root file system installed

We’re essentially uploading a built container that contains root access. When mounted this containers root access is attached to any are root has access to on target machine. This tripped me up a little when looking for the root flag.

tar.gz file - configuration for building container with root access. 

root in container on target machine but technically not root on the target machine.

![Screen Shot 2022-05-22 at 1.11.11 PM.png](GamingRoom%207dad8e9817ce49f3a4e1798acbf9451e/Screen_Shot_2022-05-22_at_1.11.11_PM.png)

Second Flag Found.