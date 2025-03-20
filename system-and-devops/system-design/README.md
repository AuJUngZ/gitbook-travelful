# \[System] System Design

## System Design Ideas

เนื่องจาก Project มีหลาย ๆ ส่วนที่ต้องทำงานร่วมกันทั้งส่วนของ Application , Web site และ AI ซึ่งการที่จะทำให้องค์กระกอบเหล่านี้ทำงานร่วมกันได้อยากราบรื่นจึงต้องอาศัยการออกแบบที่ดี และเข้ากันได้ของทั้งระบบ ดังนั้นในหัวข้อนี้จึงจะอธิบาย ideas ของการ design ระบบทั้งหมด ซั่งจะแบ่งออกเป็นสองส่วนหลัก ๆ คือ

* On Cloud : Project นี้เลือกที่จะใช้ Cloud ของ Microsoft ที่ชื่อว่า Azure เพื่อใช้ในการ deploy services ทั้งหมดที่ project ต้องมี และองค์ประกอบอื่น ๆ ที่จำเป็นเช่น
  * Storage account
  * Database services
  * AKS (Azure Kubernetes Service)
  * Gateway
  * Vm (Virtual Machine)
* On Premise : ในส่วนของ On Premise หรือเรียกง่าย ๆ คือ data center ของเราเองจะใช้ในการเก็บ sensitive data ต่าง ๆ ยกตัวอย่างเช่น ข้อมูลที่ต้องใช้ในการ Train ML Model ทั้งนี้เมื่อพูดถึงการ train AI Model แล้วนั้นเราก็จะใช้ On Premise data center ในการ Train ด้วยเช่นกัน ในส่วนของรายละเอียดของ Data Center และ MLOps จะได้อธิบายอยู่ในส่วนต่อ ๆ ไป

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

