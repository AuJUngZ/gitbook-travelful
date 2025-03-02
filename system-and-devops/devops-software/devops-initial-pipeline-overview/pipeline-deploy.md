# หลักการทำงาน Pipeline Deploy

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Deployment state</p></figcaption></figure>

* การเริ่มต้นการ deploy ในทุก ๆ version จะต้องผ่าน State Build ก่อนเนื่องจากหากไม่ผ่าน State Dev ใน State ต่อ ๆ ไปจะไม่มีการ Build โปรเจคใดทั้งสิ้น นั้นหมายความว่า State Build คือ State ที่จะใช้สร้าง Image ที่จะต้องใช้ Deploy ใน State อื่น ๆ
* เช่น หาก Developer จะลองทำการ Deploy Code Version ล่าสุดที่ Dev Environment ผู้ที่ได้รับหน้าที่ในการ Deploy จะต้องนำ Code Version นั้น ๆ มา Build Image ใน Pipeline Build เพื่อสร้าง Image ก่อนการ Deploy
* หลังจากนั้นหากต้องการ Deploy Image version นั้นที่ State ไหนก็เลือกใช้ Pipeline ตาม State ที่ต้องการแล้วให้เลือก Image ที่จะ Deploy เป็น version ที่ต้องการ

#### หากใช้หลักการแบบนี้จะทำให้สามารถทำ version control ของ Image ได้ทั้งนี้ยังสามารถย้อน version ไปกลับได้อย่างสะดวกหากเกินปัญหากับ Image Version นั้น ๆ

## Note

ใน State Build หลังจาก Build Image เสร็จสิ้น Image จะถูกจัดเก็บไว้ที่ Azure Container registry และ version ของ Image ก็จะถูกเก็บลงใน Database ของระบบ CI/CD ด้วย เพื่อที่จะใช้นำมาใช้ในการเลือก Image ตอน Deploy ต่อไป

