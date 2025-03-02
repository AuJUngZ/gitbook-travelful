# \[DevOps] Infra Provisioning Pipeline

## ขั้นตอนการทำ Infra provisioning <a href="#infra-provisioning" id="infra-provisioning"></a>

1. ก่อนที่ในแต่ละโปรเจคจะขอสร้าง service ต่าง ๆ ในแต่ละ cloud นั้นจะต้องมากดขอ Request Catalog ที่จะใช้ก่อนเช่นหากต้องการที่จะสร้าง DB ก็จะต้องมา Request Catalog ที่ใช้ในการ Provision DB ก่อน
2. หลังจากที่ Request สำเสร็จจะปรากฏ Repository สำหรับ Config spec ต่าง ๆ ของ service ที่ได้ Request มา
3. Config ตามต้องการ Base on Parameter ที่มีให้
4. หลังจาก Config เรียบร้อยก็จะเป็นการเริ่ม Provision ทำได้โดยการ Run Pipeline Provision เพื่อทำการสร้าง Service นั้นมา ซึ่งหลักการทำงานจะเป็นดังนี้
   1. Jenkins จะเข้าไปอ่าน Config Service ใน Project นั้น ๆ เพื่อที่จะนำไป apply กับคำสั่ง terraform
   2. Jenkins จะ execute terraform command
   3. Jenkins จะทำการเก็บ State file ของ Service นั้น ๆ ใน Storage account เนื่องจากเป็น file ที่สำคัญสำหรับ Terraform หากสูญหายจะทำให้การเปลี่ยนแปลงและแก้ Config นั้นทำได้ยากหรือทำไม่ได้
