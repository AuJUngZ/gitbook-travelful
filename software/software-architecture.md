# โครงสร้างซอฟต์แวร์ (Software Architecture)

<figure><img src="../.gitbook/assets/Travelful+ #2614924 (4).png" alt=""><figcaption></figcaption></figure>

โครงสร้างของซอฟต์แวร์ในภาพรวมจะแบ่งออกเป็น 4 layers ได้แก่

1. แอปพลิเคชันมือถือ
2. ระบบจัดการข้อมูล
3. ระบบที่ใช้ในการสร้างแผนการท่องเที่ยว
4. ส่วนบริการอื่นๆ

## แอปพลิเคชันมือถือ

ในโปรเจคนี้เราจะทำการพัฒนาแอปพลิเคชันมือถือ โดยใช้ภาษา Kotlin และ Swift ซึ่งจะเป็นการแยกพัฒนาสำหรับแต่ละระบบปฏิบัติการไปเลย

## ระบบจัดการข้อมูล

การจัดการข้อมูลจะถูกแบ่งออกเป็น 4 services ตามประเภทของข้อมูลที่จะต้องจัดการ ได้แก่

* **Goal Management Service** ทำการจัดการกับข้อมูลเป้าหมายการท่องเที่ยวของผู้ใช้
* **Plan Management Service** ทำการจัดการกับแผนการท่องเที่ยวของผู้ใช้
* **User Service** ทำการจัดการกับข้อมูลส่วนตัวของผู้ใช้
* **Community Service** ทำการจัดการกับเนื้อหาต่างๆ ที่อยู่ภายในระบบ community

## ระบบที่ใช้ในการสร้างแผนการท่องเที่ยว

ระบบนี้จะมีการดึงข้อมูลมาจาก Goal Management Service และ Community Service เพื่อใช้ในการสร้างแผนแล้วนำไปเก็บไว้ใน Plan Management Service

<figure><img src="../.gitbook/assets/Travelful+ #2614924 (5).png" alt=""><figcaption></figcaption></figure>

## ส่วนบริการอื่นๆ

ซอฟต์แวร์ของเราจะมีการเรียกใช้บริการและข้อมูลจากซอฟต์แวร์อื่นๆ เช่น ข้อมูลสถานที่ แผนที่ และรีวิว
