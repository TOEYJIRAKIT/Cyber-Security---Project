# ระบบการติดตามการโจมตีรูปแบบ Ping of Death
## Link to youtube
[ระบบแจ้งเตือนการเข้า-ออกโรงเรียน (Attendance System)](https://youtu.be/BAh69DkOwuc?si=MIl8_Ys98mKSaYL-)
## สมาชิกในกลุ่ม
- 64102122 จิรภัทร จิตรภักดี
- 64102080 จิรกิตติ์ เอียดเหตุ 
- 64104532 ณัฐนันท์ ทองมาก
- 64125354 ภีรภัทร บุญสุวรรณ
- 64125735 ธนวัฒน์ กองสีสังข์
- 64110455 ภัครศักดิ์ ผลสนอง 
## หน้าเว็บไซต์การแสดงผลกราฟ
กราฟการติดตามการโจมตีรูปแบบ Ping of Death
![Screenshot 2024-04-07 203718 (1)](https://github.com/TOEYJIRAKIT/Cyber-Security---Project/assets/110581279/365b39c2-5159-465c-8559-b9995c4f1ebe)
## Ping of Death Command
<p align="center">
    <code>sudo hping3 --icmp --flood --spoof <spoofed_ip> <target_ip></code>
</p>
#### Process Layer ทำหน้าที่เก็บข้อมูล โดยฐานข้อมูลจะถูกเก็บเป็น Json Server และมีตัวกลางในการเชื่อมต่อกับฝั่ง Web โดยใช้ Flask
#### Frontend Layer ทำหน้าที่แสดงผลต่างๆที่ได้จาก RFID sensor เช่น uid , studentid , firstname , lastname , position , timestamp , status, id เป็นต้น

แสดงสถาปัตยกรรมซอฟต์แวร์ (Software Architecture)
![image](https://github.com/TOEYJIRAKIT/IOT-MiniProject/assets/110581279/27c4a44d-e4de-4dcf-af2b-b90ca1ab6e14)

#### Collect Layer 
- Arduino UNO Wifi ใช้ในการรับค่าข้อมูลจาก RFID sensor เพื่อส่งไปให้ NodeMCU 1.0
- NodeMCU 1.0 ใช้สำหรับในการรับค่าจาก Arduino UNO Wifi และนำส่งข้อมูลที่ได้ไปยัง MQTT
#### Process Layer 
- MQTT ใช้รับข้อมูลจาก NodeMCU 1.0 และส่งข้อมูล ไปยัง Flask
- Flask ใช้รับข้อมูลจาก JSON และส่งไปแสดงผลใน Web
- JSON ใช้เป็น database ที่ใช้ในการเก็บข้อมูลนักศึกษาที่เข้า-ออก
#### Frontend Layer 
- Web แสดงผลผ่านเว็บไซต์ข้อมูลนักศึกษาที่เข้า-ออกจาก Flask ที่ส่งมา
- LINE Notify ส่งแจ้งเตือนข้อมูลนักศึกษาที่เข้า-ออกไปยังไลน์ผู้ปกครอง
- OLED Display แสดงผลข้อมูลนักศึกษาที่เข้า-ออกผ่านหน้าจอว่า SUCCESS หรือไม่ถ้าเป็นนักศึกษาที่ไม่รู้จักจะแสดง UNKNOWN

### Data Stucture
โครงสร้างข้อมูลถูกเก็บด้วย JSON โดยประกอบด้วยข้อมูลดังนี้ uid , studentid , firstname , lastname , position , timestamp , status, id ดังตัวอย่างตามลำดับ ที่ถูกจัดเก็บใน Module ชื่อ users 
#### โครงสร้างข้อมูล :
```json
{
  "users": [
    {
      "uid": "2",
      "studentid": "64125735",
      "firstname": "ธนวัฒน์",
      "lastname": "กองสีสังข์",
      "position": "นักศึกษา",
      "timestamp": "20:15:40",
      "status": "เข้า",
      "id": 1
    },
    {
      "uid": "3",
      "studentid": "64102080",
      "firstname": "จิรกิตติ์",
      "lastname": "เอียดเหตุ",
      "position": "นักศึกษา",
      "timestamp": "20:15:43",
      "status": "ออก",
      "id": 2
    }
  ]
}
```
### Data Dictionary
| Attribute | Description | Data Type | Example |
|--------------------|--------------------|--------------------|--------------------|
| uid  |  รหัสประจำผู้ใช้งาน  | String   | 2   |
| studentid  |รหัสนักเรียน  | String   | 64125735 |   
| firstname  | ชื่อ  | String   | ธนวัฒน์   |
| lastname  |  นามสกุล  | String   | กองสีสังข์   |
| position  |ตำแหน่ง  | String   | นักศึกษา   |
| timestamp  | เวลา  | String   | 20:15:43   |
| status  | สถานะ  | String   | เข้า   |
| id  | รหัสลำดับผู้ใช้  | int   | 1   |
## การพัฒนาระบบ
### เครื่องมือ
- Arduino UNO+WiFi R3 ATmega328P+ESP8266 Web Server Wifi ใช้สำหรับอ่านค่า Sensor และติดตั้งอุปกรณ์ 
- RFID Sensor ทำหน้าที่เป็นตัวอ่านบัตรที่สแกนเข้ามา 
- OLED Display ใช้สำหรับแสดงข้อมูลส่วนตัวของผู้สแกนบัตร
- Jumper Wire สายไฟใช้สำหรับเชื่อมต่อ Sensor เข้ากับตัวบอร์ด
- Key Tag สำหรับแสกนเพื่อส่งข้อมูลบัตรไปยัง Sensor แสกน
### ภาษาโปรแกรม 
- ภาษา C ใช้สำหรับเขียนคำสั่งลงไปยังบอร์ดเพื่อที่จะสามารถรับค่าและส่งค่าข้อมูลได้
- Json ทำหน้าที่เป็น Json Server เพื่อเก็บข้อมูลและส่งข้อมูลไปยังหน้าเว็บ 
- JavaScript ทำหน้าเป็นตัวดึงข้อมูลจาก Json Server เพื่อแสดงข้อมูลที่มีการเก็บบน Json Server มาแสดงบนหน้าเว็บ
- HTML ใช้สำหรับการพัฒนาหน้าเว็บ และเพื่อตบแต่งความสวยงานของหน้าเว็บและแสดงข้อมูลที่มีการดึงมาโดย JavaScript
### ไลบรารี
- SPI.h: ไลบรารีสำหรับการสื่อสารผ่าน Serial Peripheral Interface (SPI) ซึ่งใช้ในการเชื่อมต่อกับอุปกรณ์อื่น ๆ ที่รองรับ SPI เช่น จอ OLED
- Wire.h: ไลบรารีสำหรับการสื่อสารผ่าน I2C (Inter-Integrated Circuit) ซึ่งใช้ในการเชื่อมต่อกับอุปกรณ์ I2C อื่น ๆ เช่น ม็อดูล RFID
- Adafruit_GFX.h: ไลบรารีนี้เป็นไลบรารีที่สร้างขึ้นมาเพื่อให้การเขียนกราฟิกบนจอ LCD หรือ OLED ง่ายขึ้น โดยมีคลาสพื้นฐานสำหรับการวาดรูปแบบต่าง ๆ บนจอ
- Adafruit_SSD1306.h: ไลบรารีนี้เป็นไลบรารีสำหรับจอ OLED ที่ใช้ควบคุมด้วยชิพ SSD1306 ซึ่งจะทำให้คุณสามารถสร้างและแสดงข้อมูลต่าง ๆ บนจอ OLED
- MFRC522.h: ไลบรารีสำหรับการใช้งาน RFID (Radio-Frequency Identification) โดยใช้ชิพ MFRC522 ซึ่งสามารถอ่านข้อมูลจาก RFID card หรือ tag
- ESP8266WiFi.h: ไลบรารีสำหรับการเชื่อมต่อ WiFi ใน ESP8266
- NTPClient.h: ไลบรารีสำหรับการซิงค์เวลาจาก NTP (Network Time Protocol) server
- WiFiUdp.h: ไลบรารีสำหรับการใช้งาน UDP ในการเชื่อมต่อ WiFi
- PubSubClient.h: ไลบรารีสำหรับการเข้ารหัสและส่งข้อมูลผ่าน MQTT (Message Queuing Telemetry Transport) protocol
- TridentTD_LineNotify.h: ไลบรารีสำหรับการส่งข้อความผ่าน Line Notify API
## การทดสอบ
### สถานการณ์ 1 ทดสอบการสแกนบัตรผ่าน RFID ด้วยบัตรที่มีข้อมูลในระบบ 
- ตัวแปรต้น: บัตรที่เคยมีการบันทึกข้อมูลผู้ใช้
- ตัวแปรตาม: ผลลัพธ์การอ่านค่าและการแสดงผลข้อมูล
- ตัวแปรควบคุม: โค้ดสำหรับการอ่านบัตรผ่าน RFID Sensor, OLED Display, Key tag
- ผลการทดลอง: ![411950731_1278126119679940_1025604557624947419_n](https://github.com/TOEYJIRAKIT/IOT-MiniProject/assets/110581279/937fa408-c1ff-4490-8df2-835b1f327a6c)

### สถานการณ์ 2 ทดสอบการสแกนบัตรผ่าน RFID ด้วยบัตรที่ไม่มีข้อมูลในระบบ 
- ตัวแปรต้น: บัตรที่ไม่เคยมีการบันทึกข้อมูลผู้ใช้
- ตัวแปรตาม: ผลลัพธ์การอ่านค่าและการแสดงผลข้อมูล
- ตัวแปรควบคุม: โค้ดสำหรับการอ่านบัตรผ่าน RFID Sensor, OLED Display, Key tag
- ผลการทดลอง: ![409711670_725107342563807_3125771315398492763_n](https://github.com/TOEYJIRAKIT/IOT-MiniProject/assets/110581279/c837699d-fabb-4724-983b-86ad8e897e8e)


## สรุปผลการทดสอบ
สรุปได้ว่าโครงงานนี้สามารถตอบโจทย์วัตถุประสงค์ได้ คือ 1) สามารถสร้างตารางเก็บบันทึกข้อมูลการเข้า-ออกโรงเรียนของนักเรียนแสดงผลบนเว็บไซด์ได้ 2) สามารถสร้างระบบแจ้งเตือนการเข้า-ออกโรงเรียนของนักเรียนส่งไปยังผู้ปกครองผ่านระบบ LINE Notify ได้ตามจุดมุ่งหมายที่วางไว้
