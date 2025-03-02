# บทบาทของทีม Ops

> **Ops Team** เป็นทีมที่รับผิดชอบการดูแลโครงสร้างพื้นฐาน (Infrastructure), การจัดการระบบ MLOps, การตรวจสอบสถานะการฝึกโมเดล และการแก้ไขปัญหาที่อาจเกิดขึ้นระหว่างการฝึกหรือการใช้งานโมเดล (Model Inference) เพื่อให้แน่ใจว่าระบบทำงานได้อย่างต่อเนื่องและมีประสิทธิภาพสูงสุด

***

### 🔹 **1. ดูแลโครงสร้างพื้นฐาน MLOps และระบบจัดเก็บข้อมูล (Infrastructure & Storage Management)**

✅ **บริหารจัดการเซิร์ฟเวอร์และ GPU สำหรับการฝึกโมเดล**

* ดูแล **TrueNAS SCALE RAID-Z2** ที่เป็น **Storage หลัก สำหรับ ML Training Data & Artifacts**
* ตรวจสอบสถานะและประสิทธิภาพของ **AMD MI-100 GPU ที่ใช้ฝึกโมเดล**
* ใช้ **SLURM Task Manager** เพื่อจัดการคิวงาน Training Task

✅ **ตรวจสอบและบริหารระบบเครือข่ายและการเชื่อมต่อระหว่างเซิร์ฟเวอร์**

* ดูแลการสื่อสารระหว่าง **TrueNAS, Training Server, และ Azure ML**
* ตรวจสอบประสิทธิภาพของเครือข่าย **100GbE Interlink ระหว่างเซิร์ฟเวอร์ไฟล์**
* จัดการปัญหาการเข้าถึงไฟล์ **NFS สำหรับ Training Artifacts และ Model Logs**

✅ **จัดการพื้นที่เก็บข้อมูล และแคช (Storage & Caching Optimization)**

* ตรวจสอบการใช้งาน **4× 960GB NVMe SSD Cache (L2ARC & ZIL)**
* บริหาร **ประสิทธิภาพการอ่าน / เขียนข้อมูล (Read-Write Performance Tuning)**
* ตรวจสอบว่า **ไฟล์ที่โมเดลต้องใช้ถูกโหลดเข้าสู่ SSD Cache อย่างเหมาะสม**

***

### 🔹 **2. ตรวจสอบและจัดการการฝึกโมเดล (Model Training Monitoring & Issue Resolution)**

✅ **ตรวจสอบสถานะ Training Task และแก้ไขปัญหาเมื่อเกิดความผิดพลาด**

* ตรวจสอบผ่าน **SLURM Logs และ GPU Utilization Metrics**
* หากการฝึกโมเดลล้มเหลว → แจ้งเตือนผ่าน **Sentry และ Logging System**
* วิเคราะห์และแก้ไขปัญหาเช่น\
  ✅ GPU Memory Overload\
  ✅ การเข้าถึงไฟล์ Training Data ผิดพลาด\
  ✅ กระบวนการ Training ค้าง หรือใช้เวลานานผิดปกติ

✅ **ตั้งค่าและบำรุงรักษาระบบแจ้งเตือน & Monitoring Tools**

* ใช้ **Sentry Alerts & Prometheus** เพื่อตรวจสอบว่าโมเดลทำงานผิดพลาดหรือไม่
* ติดตั้งระบบแจ้งเตือนให้กับ **ML Creator และ Business Analyst** หากพบว่ามี Model Failure

✅ **ตรวจสอบ Log และ วิเคราะห์ Performance Bottleneck**

* วิเคราะห์ **Training Logs, Inference Logs, และ Failover Scenarios**
* ตรวจจับ **Model Performance Issue เช่น Training Convergence Problem หรือ Data Pipeline Slowdown**

***

### 🔹 **3. ตรวจสอบและบริหารโมเดลที่ถูก Deploy (Production Monitoring & Failover Management)**

✅ **ติดตั้งและจัดการโมเดลที่ถูก Deploy บน Azure ML**

* ดูแล **Web API / Batch Inference Performance** ของโมเดลที่ใช้งานจริง
* ทำให้มั่นใจว่าโมเดลสามารถ **Scale ได้ตามจำนวนผู้ใช้งานจริง**
* ตรวจสอบ **Latency ของการร้องขอ API Inference** และปรับจูนให้เหมาะสม

✅ **วิเคราะห์ Model Failure & Troubleshooting เมื่อเกิดปัญหาใน Production**

* หากโมเดลให้คำแนะนำผิดพลาด (Misclassification) → แจ้ง **ML Creator และ Analyst Team**
* หากระบบล่มหรือมีปัญหา → **Rollback หรือ Switch ไปยังโมเดลก่อนหน้าที่เสถียร**

✅ **บริหารจัดการ Disaster Recovery และ High Availability**

* ตั้งค่า **Auto-Recovery หากระบบล่ม**
* ตรวจสอบ Regular Backup & Snapshots ของโมเดลและข้อมูลที่เกี่ยวข้อง
* ดูแล **Failover Plan ของ TrueNAS JBOD และ Training Server เพื่อป้องกันเหตุฉุกเฉิน**

***

## 🎯 **สรุปบทบาทของ Ops Team**

✅ ดูแล **Datacenter, TrueNAS และ AI Training Infrastructure** ให้พร้อมใช้งาน\
✅ จัดการ **SLURM Job Scheduling และแก้ไขปัญหาระหว่างการฝึกโมเดล**\
✅ ใช้ **Sentry & Monitoring Tools** คอยติดตามประสิทธิภาพของโมเดลทั้งระหว่าง Training & Inference\
✅ แก้ไขปัญหาที่เกี่ยวข้องกับ **GPU Training, Storage Access, Failover Management และ API Latency**
