# บทบาทของ Data Analysts

> **Data Analysts** มีหน้าที่วิเคราะห์ข้อมูลจากหลายแหล่ง รวมถึง **ข้อมูลที่ระบบ ML ใช้ฝึก, ข้อมูลผู้ใช้งานจริง, และข้อมูลแจ้งเตือนจาก Sentry** เพื่อตรวจสอบและปรับปรุงโมเดล Machine Learning (ML) ให้มีความแม่นยำสูงสุด

***

### 🔹 **1. วิเคราะห์ข้อมูลและเตรียมชุดข้อมูลสำหรับโมเดล (Data Preparation & Feature Engineering)**

**รวบรวมและตรวจสอบคุณภาพของข้อมูล (Data Collection & Preprocessing)**

* รวมข้อมูลจาก **Web Scraping, Third-Party Vendors, In-App Reviews** และ **Sentry Logs**
* ทำความสะอาดข้อมูล **ลบข้อมูลซ้ำ, ตรวจสอบ Missing Data, และกำจัด Outliers**

**ออกแบบ Feature Engineering เพื่อเพิ่มประสิทธิภาพโมเดล**

* แปลงข้อมูล **Sentiment Analysis** เป็นค่าที่ใช้ในการแนะนำสถานที่ผ่าน **NLP Embedded Features**
* สร้างฟีเจอร์พิเศษ เช่น **คะแนนความนิยมของสถานที่, อัตราการเข้าชม, และแนวโน้มพฤติกรรมผู้ใช้**

**วิเคราะห์ Bias และความผิดปกติของข้อมูล (Data Bias & Anomaly Detection)**

* ตรวจสอบว่าโมเดล **มี Bias ที่เกิดจากข้อมูล Input หรือไม่**
* วิเคราะห์ข้อมูลจาก **Sentry Logs เพื่อค้นหาจุดที่โมเดลให้ผลลัพธ์ผิดพลาดเป็นประจำ**

***

### 🔹 **2. ติดตามและวิเคราะห์ประสิทธิภาพของโมเดล (Model Performance Monitoring & Sentry Log Analysis)**

**วิเคราะห์ผลการทำงานของโมเดลที่ใช้งานจริง**

* ติดตาม **Accuracy, Precision, Recall, Latency, และ Prediction Errors**
* วิเคราะห์ Feedback ของผู้ใช้เกี่ยวกับ **คำแนะนำที่โมเดลให้**

**วิเคราะห์ปัญหา Model Drift และ Performance Degradation**

* ตรวจสอบข้อมูลจาก **Sentry Logs** ว่าโมเดลมี **Error Rate ที่สูงผิดปกติหรือไม่**
* วิเคราะห์แนวโน้มของข้อมูลใหม่ที่อาจทำให้โมเดล **ล้าหลัง หรือให้คำแนะนำได้ไม่แม่นยำ**

**สร้าง Dashboard & Report สำหรับติดตามประสิทธิภาพของโมเดล**

* รวมข้อมูลจาก **Sentry Logs, Azure ML Metrics, และ Business Analysts**
* สร้าง Data Visualization ด้วย **Power BI, Tableau หรือ Python Dash**

***

### 🔹 **3. ใช้ข้อมูล Sentry Logs ในการสนับสนุนการตัดสินใจฝึกโมเดลใหม่ (Retraining Decision)**

**กำหนดเงื่อนไขสำหรับการฝึกโมเดลใหม่**

* หาก **Sentry Logs แสดงข้อผิดพลาดของโมเดลในระดับสูง หรือความแม่นยำลดลง** → แนะนำให้ฝึกโมเดลใหม่
* วิเคราะห์ว่าโมเดลต้องการ **Feature หรือ Dataset ใหม่ เพื่อแก้ปัญหาจาก Error Logs**

**ทำงานร่วมกับ ML Creator เพื่อปรับปรุงโมเดล**

* วิเคราะห์ **Feature Engineering ใหม่ ๆ** ที่ช่วยลด Error ใน Sentry Logs
* เสนอแนวทางการปรับค่า **Hyperparameter หรือการเปลี่ยนแปลง Model Architecture**

**ให้คำแนะนำกับ Business Analyst & Audit Team**

* รายงานว่า **ข้อมูล Error จาก Sentry ส่งผลต่อการให้คำแนะนำของโมเดลอย่างไร**
* เสนอแนวทางปรับปรุง Business Rules ให้รองรับแนวโน้มพฤติกรรมผู้ใช้และโมเดลที่ปรับปรุงใหม่

***

## **สรุปบทบาทของ Data Analysts**

* รวบรวม, วิเคราะห์ และทำความสะอาดข้อมูล ทั้ง **ข้อมูลลอจิกของโมเดลและข้อมูลแจ้งเตือนจาก Sentry**
* ตรวจสอบ **Model Performance และ Error จาก Sentry Logs** เพื่อลดปัญหาของโมเดลที่ Deploy ไปใช้งาน
* วิเคราะห์ว่าโมเดลควรถูกฝึกใหม่หรือไม่ โดยใช้ข้อมูลจาก **Real-World Performance & Sentry Logs**
* ทำงานร่วมกับ **ML Creator, Business Analyst และ Audit Team** เพื่อวางแผนปรับปรุงและปรับใช้โมเดลอย่างมีประสิทธิภาพ
