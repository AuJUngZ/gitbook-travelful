# System Design with MLOps

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## Note

* ภาพที่แสดงข้างต้นในส่วนของ system on cloud จะถูก simplify ให้เข้าใจง่ายและมีการซ้อนรายละเอียดบางอย่างเช่น Design pattern Hub and Spoke ที่ได้ถูกนำมาใช้ในการ design system on cloud ด้วย
* ในส่วนของ on premise ที่ได้แสดงไว้ในภาพข้างต้นเป็นการแสดงกรบวณการทำงานของ MLOps เพื่อใช้ในการ Training ML Model เพื่อนำมาใช้ใน Product ของเรา ซึ่งในรายละเอียดเพิ่มเติมสำหรับเนื้อหา MLOps สามารถดูได้จากที่นี้ [Broken link](broken-reference "mention")

### ความเชื่อมโยงระหว่าง On Premise กับ On Cloud

* จากแผนภาพที่แสดงข้างต้นจะเห็นได้ว่าความเชื่อมโยงของทั้งสอง System จะเชื่อมโยงกันที่ Azure ML กล่าวคือ ระบบ On Cloud ของเราจะใช้ในการ Deploy Service ทั้งหมดที่ Product จะต้องใช้ไม่ว่าจะเป็น Backend Frontend และอื่น ๆ เพื่อที่จะสามารถทำให้ผู้ใช้งานสามารถเข้าถึงบริการของเราได้อย่างทั่วถึงและรวดเร็ว ดังนั้นจึงเลือกใช้ระบบ Cloud ในการ Deploy สิ่งเหล่านี้
* ในส่วนของ On Premise เราจะมี Data center ที่ใช้สำหรับการประมวลผล ML Model โดยเฉพาะเพื่อความเป็นส่วนตัวของข้อมูลของลูกค้า อีกทั้งในระยะยาวยังสามารถประหยัดค่าใช้จ่ายต่าง ๆ เพื่อที่จะใช้ในการพัฒนา ML Model ในอนาคตอีกด้วย
* ดังนั้นแล้วเมื่อ On Premise ประมวลผลจนได้ ML Model มาตัวของ ML Model ก็จะถูก Deploy บน Cloud ไม่ต่างจาก service อื่น ๆ ที่ได้กล่าวมา

