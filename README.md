# ระบบติดตามการโจมตีรูปแบบ Ping of Death
## Link to Youtube
[ระบบแจ้งเตือนการเข้า-ออกโรงเรียน (Attendance System)](https://youtu.be/BAh69DkOwuc?si=MIl8_Ys98mKSaYL-)
## สมาชิกในกลุ่ม
- 64102122 จิรภัทร จิตรภักดี
- 64102080 จิรกิตติ์ เอียดเหตุ 
- 64104532 ณัฐนันท์ ทองมาก
- 64125354 ภีรภัทร บุญสุวรรณ
- 64125735 ธนวัฒน์ กองสีสังข์
- 64110455 ภัครศักดิ์ ผลสนอง 
## หน้าเว็บไซต์การแสดงผลกราฟ
กราฟติดตามการโจมตีรูปแบบ Ping of Death
![Screenshot 2024-04-07 203718 (1)](https://github.com/TOEYJIRAKIT/Cyber-Security---Project/assets/110581279/365b39c2-5159-465c-8559-b9995c4f1ebe)
## Ping of Death Command
<code>sudo hping3 --icmp --flood --spoof <spoofed_ip> <target_ip></code>
## โครงสร้างข้อมูล
```json
{
    "input_interface": "wlp2s0",
    "code": "0",
    "dst": "172.28.1.60",
    "attack_type": "Ping of Death",
    "src": "172.28.1.63",
    "type": "8",
    "ttl": "64",
    "tags": [],
    "hostname": "itd-Macmini8",
    "@timestamp": "2024-04-07T11:42:54.570Z",
    "len": "28",
    "prec": "0x00",
    "port": 35324,
    "proto": "ICMP",
    "@version": "1",
    "host": "172.18.0.1",
    "mac_dst": "dc:a4:ca:e9:a6:db",
    "mac_src": "70:9c:d1:84:a0:df",
    "tos": "0x00",
    "id": [
        "3608",
        "25180"
    ],
    "seq": "512",
    "timestamp": "Apr  7 18:42:54"
}
```
## ตัวอย่างการทำงาน
![Screenshot 2024-04-07 204434 (1)](https://github.com/TOEYJIRAKIT/Cyber-Security---Project/assets/110581279/a0723a82-7174-45d8-adfa-f165d89999e5)
