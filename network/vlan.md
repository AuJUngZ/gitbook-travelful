# VLAN

ในด้านการออกแบบ VLAN ภายในบริษัท จะแบ่ง VLAN ตาม Department ภายในบริษัท โดยมีข้อดีคือ\
1\. เพิ่มความปลอดภัยในการส่งข้อมูล ลดความเสี่ยงการส่งข้อมูลระหว่างแผนกที่ไม่เกี่ยวข้องกัน\
2\. รองรับการทำ Quality of Service โดยสามารถกำหนด Priority และ Bandwidth ในแต่ละแผนกได้\
3\. รองรับการใช้งาน Wifi ที่แยก SSID ตามแผนก

โดยได้แบ่งตาม Department ดังนี้

| VLAN | VLAN Name                    | Subnet           | Type          | Number of Users | Number of Devices |
| ---- | ---------------------------- | ---------------- | ------------- | --------------- | ----------------- |
| 10   | Financial Department         | 192.168.10.0/24  | LAN, Wireless | 5               | 10                |
| 20   | Marketing                    | 192.168.20.0/24  | LAN, Wireless | 5               | 20                |
| 30   | IT Department                | 192.168.30.0/24  | LAN, Wireless | 20              | 60                |
| 40   | Management Department        | 192.168.40.0/24  | LAN, Wireless | 5               | 10                |
| 50   | Serucity Controller and CCTV | 192.168.60.0/24  | LAN, Wireless | -               | 20                |
| 60   | Content Creator              | 192.168.50.0/24  | LAN, Wireless | 5               | 20                |
| 70   | Conference and Meeting       | 192.168.70.0/24  | LAN, Wireless | 10              | 20                |
| 100  | Reception (Guest)            | 192.168.100.0/24 | Wireless      | 50              | 80                |
| 150  | Data Center                  | 192.168.150.0/24 | LAN           | -               | 4                 |
