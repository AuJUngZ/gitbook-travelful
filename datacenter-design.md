# Datacenter Design

### **🏢 1. ภาพรวมดาต้าเซ็นเตอร์**

✅ **องค์ประกอบหลัก**

* **ML Server**: **เซิร์ฟเวอร์ประมวลผล GPU ประสิทธิภาพสูง** สำหรับฝึกโมเดล AI
* **Storage Server (TrueNAS)**: **ระบบจัดเก็บไฟล์บนเครือข่าย (NFS/SMB)** สำหรับ **ข้อมูล, ML Logs และเอกสารขององค์กร**
* **JBOD Expansion**: ขยายพื้นที่เก็บข้อมูลด้วย **12× 12TB Seagate Exos HDDs**
* **General Server**: รองรับ **เวิร์กโหลดทั่วไป, ระบบภายใน และ API Hosting**

✅ **ต้นทุนรวมโดยประมาณ**\
**ML + General Server + ระบบ Storage ≈ 29,432 ดอลลาร์ (\~1,005,000 บาท)**

***

### **🖥️ 2. โครงสร้างพื้นฐานการประมวลผล (AI Training & Workloads ต่าง ๆ)**

#### 🔹 **ML Training Server (เซิร์ฟเวอร์ประมวลผล AI หลัก)**

📌 **สเปคฮาร์ดแวร์**

* **รุ่น**: **Thinkmate GPX QS4-12E2-4GPU**
* **CPU**: **AMD EPYC 7313P** (16 คอร์ 32 เทรด, 3.00GHz)
* **GPU**: **AMD Instinct MI100 (32GB HBM2, PCIe 4.0 x16)**
* **RAM**: **8× 8GB DDR4 RDIMM ECC (PC4-25600 3200MHz)**
* **Storage**: **800GB Kioxia NVMe SSD**
* **Networking**: **10GbE (Broadcom P210P - PCIe 3.0 x8, 2× SFP+)**

📌 **ความสามารถในการฝึกโมเดล**

| **Configuration**    | **7B x 2** | **14B x 1** |
| -------------------- | ---------- | ----------- |
| Precision            | bfloat16   | float16     |
| Parameters (B)       | 7          | 14          |
| Bytes per Param      | 0.5        | 0.5         |
| Training Factor      | 3          | 3           |
| Model Memory (GB)    | 11         | 21          |
| Dataset Size (GB)    | 10         | 10          |
| GPU Requirement (GB) | 21         | 31          |

🛠️ **การใช้งานหลัก**\
✔️ **ฝึกโมเดล AI** ด้วย GPU ขั้นสูง\
✔️ **รองรับการประมวลผลชุดข้อมูลขนาดใหญ่**\
✔️ **นำโมเดลที่ฝึกแล้วไป Deploy บน Azure ML**

💰 **ต้นทุนรวม**: **13,886 ดอลลาร์ (\~474,500 บาท)**

***

#### 🔹 **General Compute Server**

📌 **สเปคฮาร์ดแวร์**

* **รุ่น**: **CloudDC A+ Server AS-1015CS-TNR**
* **CPU**: **AMD EPYC 9124 (16C/32T, 3.00GHz, 64MB Cache)**
* **RAM**: **16GB DDR5 4800MHz ECC RDIMM ×2**
* **Storage**: **2× 240GB SATA SSD (RAID-1 for OS)**
* **Networking**: **Supermicro 10GbE Adapter (2× SFP+)**

🛠️ **การใช้งานหลัก**\
✔️ **ให้บริการ API และ Backend ต่าง ๆ**\
✔️ **จัดการเวิร์กโหลด CI/CD และ Automation Workflow**\
✔️ **Load-balancing สำหรับ Model Inference API บน Azure ML**

💰 **ต้นทุนรวม**: **3,756 ดอลลาร์ (\~128,300 บาท)**

***

### **💾 3. โครงสร้างระบบจัดเก็บข้อมูล (Enterprise File Server & ML Data Management)**

#### 🔹 **TrueNAS-Based Storage Server (ระบบ ZFS RAID-Z2)**

📌 **สเปคฮาร์ดแวร์**

* **ชิ้นส่วนหลัก**: **Supermicro CSE-826BE2C-R802JBOD (2U JBOD Expansion)**
* **Storage Controller**: **SAS 12Gbps Backplane พร้อม Dual Expanders**
* **ดิสก์ไดรฟ์**:
  * **12× Seagate Exos 12TB HDDs (ST12000NM0007, 7200RPM, SAS 12Gbps)**
  * **Raw Storage:** **144TB (12× 12TB HDDs)**
  * **Usable (RAID-Z2):** **≈96TB**
* **Cache Drives:**
  * **4× 960GB NVMe SSDs (2× Read Cache L2ARC, 2× Write Log ZIL)**
* **Security:** **AES-256-GCM Encryption** + **RBAC Permissions**

🛠️ **การใช้งานหลัก**\
✔️ **เป็นระบบจัดเก็บข้อมูลหลักสำหรับการฝึก AI และไฟล์องค์กร**\
✔️ **เร็วขึ้นด้วย NVMe Caching สำหรับเวิร์กโหลด AI**\
✔️ **สำรองข้อมูลอัตโนมัติด้วย ZFS Snapshots**

💰 **ต้นทุนรวม**: **11,790 ดอลลาร์ (\~402,800 บาท)**

***

### **🌎 4. การเชื่อมต่อเครือข่ายและการขยายระบบ**

📌 **โครงสร้างเครือข่าย**

* **Primary Interconnect:** **100GbE**
* **Storage Access:** **Dual-port 100GbE บน TrueNAS และ ML Server**
* **Load Balancing สำหรับ API Inference:** **Azure ML Deployment API**

📌 **การขยายระบบในอนาคต**\
✔️ **สามารถเพิ่มเซิร์ฟเวอร์ไฟล์ได้โดยใช้ JBOD Expansion**\
✔️ **รองรับการเพิ่ม GPU Node โดยใช้ InfiniBand หรือ 100GbE**\
✔️ **อาจใช้ Cloud-based AI training หากมีงานขนาดใหญ่เกินกว่าทรัพยากรในองค์กร**

***

### **🔒 5. ความปลอดภัยและการจัดการสิทธิ์การเข้าถึง**

📌 **มาตรการความปลอดภัย**

* **การเข้ารหัส:** **AES-256-GCM บน Storage ทั้งหมด**
* **การควบคุมสิทธิ์ (RBAC)**

***

### **📌 6. ระบบสำรองและรองรับความผิดพลาด (Redundancy & High Availability)**

| **Component**         | **กลยุทธ์สำรอง & ป้องกันความผิดพลาด**                        |
| --------------------- | ------------------------------------------------------------ |
| **Storage (TrueNAS)** | **RAID-Z2 (ป้องกัน HDD เสีย 2 ลูก พร้อมกัน), JBOD Failover** |
| **Network**           | **มี 100GbE ลิงก์สำรอง + Dual NICs**                         |
| **Inference API**     | **ใช้ Azure ML ซึ่งรองรับ Auto Scaling**                     |

***

### **📢 สรุปและบทสรุป**

✅ **รองรับการฝึก AI ด้วย GPU AMD MI100**\
✅ **Storage RAID-Z2 รองรับความปลอดภัยของข้อมูล**\
✅ **ขยายได้ง่ายด้วย JBOD และ 100GbE Interlink**\
✅ **Failover รองรับเซิร์ฟเวอร์สำรองในกรณีฉุกเฉิน**
