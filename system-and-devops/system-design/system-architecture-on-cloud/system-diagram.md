# System Diagram

<figure><img src="../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p>system Diagram</p></figcaption></figure>

## ภาพรวมของระบบ (Overview)

แผนภาพนี้แสดงให้เห็นโครงสร้างระบบที่ใช้ **Azure Kubernetes Service (AKS)** และ **Azure Services** ต่าง ๆ โดยมีการแบ่งออกเป็น 2 ส่วนหลัก ๆ ได้แก่:

1. **Hub** – ศูนย์กลางของเครือข่าย
2. **Spoke** – ส่วนของ Workload ที่ใช้งานจริง

**Hub จะเชื่อมต่อกับ Spoke ผ่านการ Peering** เพื่อให้การส่งข้อมูลมีความปลอดภัยและสามารถควบคุมการเข้าถึงได้

## องค์ประกอบของระบบ

### **Hub (เครือข่ายกลาง)**

* **VPN Gateway** – ใช้สำหรับเชื่อมต่อเครือข่าย private network ใน cloud เพื่อใช้งานหรือ config
* **Azure Bastion** – ใช้สำหรับเข้าถึง Virtual Machines อย่างปลอดภัยโดยไม่ต้องเปิดพอร์ต RDP/SSH
* **Azure Firewall** – เป็นตัวควบคุมการเข้าถึงเครือข่าย ป้องกันทราฟฟิคที่ไม่ได้รับอนุญาตของระบบใหญ่รวมทั้ง service ต่าง ๆ

### Spoke (Workload ที่ใช้งานจริง)

#### **Azure Services**

* มีบริการฐานข้อมูลและการจัดเก็บข้อมูล ได้แก่:
  * **Cosmos DB** – ฐานข้อมูล NoSQL ที่รองรับการขยายตัวสูง
  * **Redis** – ระบบ Cache ที่ช่วยเพิ่มประสิทธิภาพของระบบ
  * **Blob Storage** – ใช้เก็บข้อมูลที่ไม่มีโครงสร้าง เช่น รูปภาพ วิดีโอ
  * **PostgreSQL** – ฐานข้อมูลหลักของระบบ

#### **Azure Application Gateway**

* มี **WAF (Web Application Firewall)** ป้องกันการโจมตี เช่น SQL Injection, XSS
* เป็น Load Balancer สำหรับรับส่งทราฟฟิกไปยัง **Azure Kubernetes Service (AKS)**

#### **Azure Kubernetes Service (AKS)** แบ่งออกเป็น 3 Namespace หลัก:

* **Namespace Utils** – สำหรับ Monitoring & Logging เช่น **Grafana, Prometheus, Kibana, Elastic, Logstash**
* **Namespace Frontend** – แบ่งเป็น 2 ส่วนคือ **User และ Admin** โดยใช้ Ingress Controller ในการรับ traffic
* **Namespace Backend** – ใช้ **Kong API Gateway** เป็นตัวกลางสำหรับให้บริการ Backend Service และใช้ **Istio** สำหรับ Service Mesh เพื่อ Route Communication ระหว่าง Backend Service ด้วยกันเอง

### **การทำงานของระบบ**

1. ผู้ใช้จาก **Public Internet** เข้าถึงระบบผ่าน **Azure Application Gateway** ซึ่งมี WAF คอยป้องกันการโจมตี
2. จากนั้นจะถูกส่งต่อไปยัง **Ingress Controller** ของ AKS
3. ถ้าเป็นฝั่ง **Frontend** ระบบจะส่งไปยัง User หรือ Admin ตาม URL ที่ร้องขอ
4. ถ้าเป็นฝั่ง **Backend** ระบบจะส่งไปที่ **Kong API Gateway** และให้ Kong ทำหน้าที่ส่งต่อไปยัง **Service 1, 2, 3** ที่อยู่ใน **Service Mesh ของ Istio โดยที่ภายในแต่ละ Service ก็สามารถสื่อสารกันได้โดยตรงผ่าน Service Mesh**
5. ระบบจะใช้ Azure Services เช่น CosmosDB, Redis, และ Blob Storage เพื่อเก็บข้อมูล และสามารถเข้าถึง **Key Vault** เพื่อดึง Credentials ต่าง ๆ ได้อย่างปลอดภัย

