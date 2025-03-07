# บทบาทของทีม Audit

> **Audit Team** มีหน้าที่ตรวจสอบความถูกต้อง ประสิทธิภาพ และความเหมาะสมของโมเดล Machine Learning (ML) ก่อนที่จะนำไปใช้งานจริง ระบบตรวจสอบนี้ช่วยให้มั่นใจว่าโมเดลที่นำไป Deploy มีคุณภาพ และเป็นไปตามข้อกำหนดด้านธุรกิจและเทคนิค

***

### 🔹 **1. ตรวจสอบความถูกต้องของโมเดล (Model Validation & Compliance Check)**

**ตรวจสอบว่าผลลัพธ์ของโมเดลมีความถูกต้องเพียงพอ**

* วิเคราะห์ว่าโมเดล **มีความแม่นยำเพียงพอหรือไม่** โดยพิจารณา **Accuracy, Precision, Recall, F1-score**
* ตรวจสอบว่าโมเดลสามารถ **ให้คำแนะนำที่สอดคล้องกับความต้องการของธุรกิจ**

**ประเมินว่าข้อมูลที่ใช้ฝึกโมเดลมีคุณภาพหรือไม่**

* ตรวจสอบว่า **ชุดข้อมูลที่ใช้ฝึกโมเดลไม่มี Bias หรือความผิดพลาด**
* ทำงานร่วมกับ **ML Creator และ Data Analyst** เพื่อตรวจสอบความถูกต้องของข้อมูล

**กำหนดมาตรฐานการตรวจสอบโมเดล (Audit Standards)**

* ตั้งเงื่อนไขที่ชัดเจนสำหรับการอนุมัติโมเดล เช่น \
  \- ความแม่นยำต้องมากกว่า 85%\
  \- ต้องไม่มี Bias ในการแนะนำสถานที่ท่องเที่ยว\
  \- Latency ของโมเดลต้องไม่สูงเกินไป เป็นต้น

***

### 🔹 **2. ประเมินผลกระทบและความเสี่ยงของโมเดล (Risk & Bias Analysis)**

**ตรวจสอบว่าโมเดลไม่ได้สร้างความเสี่ยงทางธุรกิจ**

* วิเคราะห์ความเป็นไปได้ที่โมเดลให้ **ผลลัพธ์ผิดพลาด (False Positive/False Negative)**
* ตรวจสอบว่าการแนะนำสถานที่ **ไม่มีปัญหาทางจริยธรรม หรือผลกระทบต่อผู้ใช้**

**วิเคราะห์ปัญหา Bias และความเป็นธรรมของโมเดล**

* ตรวจสอบว่าข้อมูลไม่ได้ **มี Bias ที่เกิดจากพฤติกรรมของผู้ใช้หรือความคิดเห็นที่เอียงกระเท่**
* รายงานความเสี่ยงให้กับ **ทีมวิเคราะห์ข้อมูล (Analytics Team) และ ML Creator** เพื่อปรับปรุงโมเดล

**กำหนดแนวทางแก้ปัญหาหากโมเดลมีความผิดพลาด**

* หากพบว่าโมเดล **ไม่ผ่านเกณฑ์มาตรฐาน** → แนะนำการปรับปรุงและส่งกลับไปให้ทีม **ML Creator ฝึกโมเดลใหม่**
* หากโมเดลผ่านเกณฑ์ **สามารถนำไป Deploy บน Azure ML** ได้

***

### 🔹 **3. อนุมัติหรือปฏิเสธโมเดล (Approval & Decision Making)**

**ตัดสินใจว่าโมเดลสามารถนำไปใช้งานได้หรือไม่**

* ถ้าโมเดล **ผ่านการตรวจสอบ** → อนุมัติให้ **Deploy บน Azure ML**
* ถ้าโมเดล **ไม่ผ่านการตรวจสอบ** → รายงานปัญหา **ให้ทีม ML Creator และ Business Analyst**

**ทำเอกสารรายงานการตรวจสอบ (Audit Report)**

* สรุปผลการตรวจสอบโมเดล **(ผ่าน / ไม่ผ่าน / ต้องปรับปรุงจุดใดบ้าง)**
* ให้คำแนะนำเกี่ยวกับ **การแก้ไขจุดบกพร่องของโมเดล**

**ทำงานร่วมกับทีมอื่นเพื่อปรับปรุงโมเดลให้เหมาะสม**

* หากโมเดลต้องปรับปรุง **รายงานปัญหาให้กับ Business Analyst และ ML Creator** เพื่อออกแบบโมเดลใหม่
* ติดตามผลลัพธ์ของโมเดลที่ Deploy แล้ว เพื่อตรวจสอบว่า **ยังคงมีประสิทธิภาพอยู่หรือไม่**

***

## 🎯 **สรุปบทบาทของ Audit Team**

* ตรวจสอบ **Accuracy, Bias, ความแม่นยำ และประสิทธิภาพของโมเดล**
* วิเคราะห์ **ความเสี่ยงและผลกระทบของโมเดลต่อผู้ใช้และธุรกิจ**
* ตัดสินใจว่าโมเดลที่ฝึกเสร็จแล้ว **พร้อมสำหรับการนำไปใช้งานจริงหรือไม่**
* ทำงานร่วมกับ **ML Creator, Data Analyst และ Business Analyst** เพื่อให้มั่นใจว่าโมเดลที่นำไปใช้งานมีคุณภาพดีที่สุด
