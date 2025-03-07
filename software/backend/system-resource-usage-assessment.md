# ประเมินการใช้งานทรัพยากรระบบ System Resource Usage Assessment

บทนี้นำเสนอการประเมินการใช้งานทรัพยากรของระบบ โดยมุ่งเน้นที่การคำนวณขนาดฐานข้อมูลที่ใช้งานอยู่ในปัจจุบัน การเติบโตของฐานข้อมูลในแต่ละปี และปริมาณธุรกรรมต่อวินาที (TPS) ของซอฟต์แวร์ เพื่อสนับสนุนการวางแผนและบริหารจัดการทรัพยากรสำหรับการสนับสนุนระบบ

โดยจะข้อสันนิษฐานไว้ดังต่อไปนี้

| ข้อ | ข้อสันนิษฐาน                                        | จำนวนสันนิษฐาน          | อ้างอิง                                                                                                                          |
| --- | --------------------------------------------------- | ----------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| a.1 | จำนวนนักท่องเที่ยวต่อปี                             | 1.3 พันล้านคน           | [UNWTO 2023](https://www.unwto.org/tourism-data/global-and-regional-tourism-performance)                                         |
| a.2 | อัตราผู้ใช้งาน Travelful ต่อจำนวนนักท่องเที่ยว      | 1%                      |                                                                                                                                  |
| a.3 | จำนวนทริปต่อคนต่อปี                                 | 1 ทริปต่อคนต่อปี        |                                                                                                                                  |
| a.4 | จำนวนของสถานที่เที่ยวจากการเที่ยวหนึ่งวัน           | 7 สถานที่ต่อวัน         | [Schneider 2013](https://www.researchgate.net/publication/236666207_Unravelling_daily_human_mobility_motifs)                     |
| a.5 | จำนวนวันต่อทริป                                     | 5 วันต่อทริป            | [Statista Research Department 2024](https://www.statista.com/statistics/1472338/average-stay-leisure-trips-worldwide-by-market/) |
| a.6 | จำนวนการเปิดแอปพลิเคชั่นต่อสถานที่ท่องเที่ยว        | 5 ครั้งต่อสถานที่       |                                                                                                                                  |
| a.7 | จำนวนสิ่งของที่ต้องเตรียมสำหรับแต่ละทริป            | 14 สิ่งของต่อทริป       |                                                                                                                                  |
| a.8 | จำนวน Transactions ต่อการเปิดแอปพลิเคชั่นหนึ่งครั้ง | 10 Transaction ต่อครั้ง |                                                                                                                                  |
| a.9 | TPS (Transactions per second) Spike Ratio           | 2                       |                                                                                                                                  |

และอ้างอิงจาก Schema ของฐานข้อมูล จะได้ขนาดของแต่ละ Record ดังนี้

| ข้อ | ประเภทข้อมูล                  | ขนาดข้อมูล |
| --- | ----------------------------- | ---------- |
| b.1 | ขนาดข้อมูลผู้ใช้งาน           | 1.6 kB     |
| b.2 | ขนาดข้อมูล `user_goals`       | 475 B      |
| b.3 | ขนาด `trip_loc`               | 76 B       |
| b.4 | ขนาด `trip_items`             | 106 B      |
| b.5 | ขนาดรูปภาพโปรไฟล์ (สันนิษฐาน) | 50 kB      |

โดยจากข้อูลทั้งหมด เราจะสามารถอนุมานข้อมูลที่เหลือได้ดังนี้

| ข้อ | ข้ออนุมาน                      | ผลการอนุมาน                     | หลักฐานการอนุมาน        |
| --- | ------------------------------ | ------------------------------- | ----------------------- |
| c.1 | จำนวนของผู้ใช้งาน              | 13 ล้านคน                       | (a.1) (a.2)             |
| c.2 | จำนวนสถานที่ท่องเที่ยวต่อทริป  | 35 สถานที่ต่อทริป               | (a.3) (a.4) (a.5)       |
| c.3 | จำนวนของสถานที่ท่องเที่ยวต่อปี | 455 พันล้านสถานที่ต่อปี         | (c.1) (c.2)             |
| c.4 | จำนวนการเปิดแอปพลิเคชั่นต่อปี  | 2.275 พันล้านครั้งต่อปี         | (a.6) (c.3)             |
| c.5 | จำนวน Transactions ต่อปี       | 22.75 พันล้าน Transaction ต่อปี | (a.8) (c.4)             |
| d.1 | ขนาดข้อมูลผู้ใช้งาน รวม        | 20.8 GB                         | (b.1) (c.1)             |
| d.2 | ขนาดข้อมูล `user_goals` รวม    | 6.2 GB ต่อปี                    | (b.2) (c.1)             |
| d.3 | ขนาด `trip_loc` รวม            | 34.6 GB ต่อปี                   | (b.3) (c.3)             |
| d.4 | ขนาด `trip_items` รวม          | 19.3 GB ต่อปี                   | (a.3) (a.7) (b.4) (c.1) |

ซึ่งจำสามารถสรุปได้ว่า

| ข้อสรุป                                 | จำนวน         | หลักฐานการอนุมาน  |
| --------------------------------------- | ------------- | ----------------- |
| TPS (Transaction per second)            | 721 tps       | (c.5)             |
| Peak TPS                                | 1442 tps-max  | (a.9) (c.6)       |
| ขนาดฐานข้อมูลเริ่มต้น (ข้อมูลผู้ใช้งาน) | 20.8 GB       | (d.1)             |
| อัตราการเพิ่มขนาดฐานข้อมูล (ข้อมูลทริป) | 60.1 GB ต่อปี | (d.2) (d.3) (d.4) |
| ขนาดหน่วยเก็บความจำ (รูปภาพโปรไฟล์)     | 650 GB        | (c.1) (b.5)       |
