# แนวคิดและวิธีการออกแบบ System Architecture On Cloud

แนวคิดในการออกแบบ **System Architecture** ของโปรเจคนี้ใช้ **Hub-and-Spoke Model** ซึ่งเป็นแนวคิดที่ได้รับความนิยมในองค์กรขนาดใหญ่ เนื่องจากช่วยให้การจัดการระบบมีความเป็นระเบียบ และสามารถ Scale ได้ง่าย

#### **โครงสร้างของ Hub-and-Spoke Model**

1. **Hub (ศูนย์กลางของระบบ)**
   * ทำหน้าที่เป็นจุดศูนย์กลางที่ควบคุมการทำงานทั้งหมด
   * ประมวลผลข้อมูล จัดการการเชื่อมต่อ และประสานงานระหว่างส่วนต่าง ๆ
   * มักเป็น Server หลัก, API Gateway หรือ Message Broker และ Core Firewall ของระบบ
2. **Spoke (ส่วนย่อยของระบบ)**
   * เป็นระบบหรือบริการย่อยที่เชื่อมต่อกับ Hub
   * ทำหน้าที่รับ-ส่งข้อมูลและประมวลผลตามความต้องการของผู้ใช้
   * อาจเป็น Frontend, Mobile App, Microservices หรือระบบย่อยอื่น ๆ

การใช้งาน Cloud Services โดยปกติแล้วอาจจะไม่ได้ใส่ใจเรื่อง firewall ของ service เหล่านั้นเท่าไหร่นักแต่เนื่องด้วยแนวคิดนี้ service แต่ละตัวหากจะต้องออก Internet ภายนอกก็จะต้องผ่าน firewall ที่อยู่ใน Hub ของ Architecture นี้ด้วย เช่นเดียวกับกับใช้งาน service หากไม่ได้รับอณุญาติให้ใช้งานก็จะไม่สามารถผ่าน firewall เข้ามาได้เลย

#### ข้อดีของการใช้ Hub-and-Spoke Model

* ระบบมีจุดศูนย์กลางที่ควบคุมการทำงาน ทำให้การบำรุงรักษาง่ายขึ้น
* สามารถเพิ่ม Spoke ได้โดยไม่กระทบระบบหลักมากนัก
* Hub ทำหน้าที่เป็นตัวกลาง ทำให้สามารถควบคุมการเข้าถึงข้อมูลได้ดีขึ้น
