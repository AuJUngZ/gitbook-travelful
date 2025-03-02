# \[DevOps] Initial Pipeline Overview

## Initial Project <a href="#initial-project" id="initial-project"></a>

<figure><img src="../../../.gitbook/assets/image (5).png" alt="" width="375"><figcaption></figcaption></figure>

จากแผนภาพข้างบนการ initial project จะมีการสร้างอยู่ด้วยกันทั้หมด 2 ส่วนคือ

1. Gitlab
2. Jenkins Pipeline

### Jenkins <a href="#jenkins" id="jenkins"></a>

* สร้าง Jobs สำหรับ Request, Provisioning, Destroy Infra สำหรับ Cloud ต่าง ๆ ไม่ว่าจะเป็น Azure , AWS , etc.

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

* สร้าง Job สำหรับ Build Repository ต่าง ๆ เพื่อให้ได้มาซึ่ง Image ที่จะใช้ในการ Deploy ทั้ง Microservices and Frontend
* สร้าง Jobs สำหรับ Deploy ในแต่ละ Environment ของแต่ละ Repository

### Gitlab Repository <a href="#gitlab-repository" id="gitlab-repository"></a>

* ในส่วนของ Gitlab นั้น จะมีการสร้าง Initial Project และ Sub-Project สำหรับงานในงานแต่ละส่วนเอาไว้ โดยชั้นในสุดของ Sub-Project นั้นจะเป็น Repository ซึ่งในที่นี้จะมีการอ้างอิงจากของ Travelful+ ตามที่เห็นด้านล่างดังนี้

```
Travelful+/
├── Frontend/
│   └── Repository/
├── Backend/
│   └── Microservice/
│       └── Repository/
├── Machine Learning/
│   └── Repository/
├── Infrastructure/
│   ├── AWS/
│   │   ├── Repository/
│   └── Azure/
│       ├── Repository/
├── Helm/
│   ├── Frontend/
│       └── Repository/
│   ├── Backend/
│       └── Repository/
│   └── Machine Learning/
│       └── Repository/
└── Configs/
    ├── Frontend/
        └── Repository/
    ├── Backend/
        └── Repository/
    └── Machine Learning/
        └── Repository/
```

## Initial Repository Pipeline <a href="#initial-repository-pipeline" id="initial-repository-pipeline"></a>

<figure><img src="../../../.gitbook/assets/image (8).png" alt="" width="375"><figcaption></figcaption></figure>

จากภาพข้างต้น ตอนที่มีการสร้าง Repository ใน Sub-Project ที่ต้องการนั้นจะมีการสร้าง Stages ให้ตามที่เห็นในภาพ โดยแต่ละ stages จะมีความหมายดังนี้

* Build → เป็นขั้นตอนแรกที่ใช้สำหรับสร้าง (compile) โค้ดจากแหล่งที่มาของโครงการ (source code) ให้เป็น artifact ที่สามารถนำไปใช้งานในขั้นตอนถัดไปได้
* Dev → เป็นสภาพแวดล้อมสำหรับนักพัฒนาทดสอบ code ที่พัฒนา เพื่อให้แน่ใจว่าฟีเจอร์ทำงานได้ตรงตามที่คาดหวัง
* QA → Quality Assurance (QA) ใช้สำหรับการตรวจสอบคุณภาพของระบบ โดยทีม QA จะทำการทดสอบแบบเชิงลึก (functional testing) และ manual testing
* SIT → การทดสอบระบบแบบองค์รวมที่รวมทุกองค์ประกอบของระบบเข้าด้วยกัน เช่น API, Database, และ Third-party Service
* UAT → การทดสอบที่ผู้ใช้งาน (End User) หรือทีมลูกค้าจะเข้ามาตรวจสอบว่าโซลูชันตรงตามความต้องการทางธุรกิจ
* Pre Prod → เป็นสภาพแวดล้อมที่ใกล้เคียงกับ Production มากที่สุด ใช้สำหรับการทดสอบขั้นสุดท้ายก่อนการเผยแพร่
* Prod → เป็นสภาพแวดล้อมสำหรับการใช้งานจริงที่ผู้ใช้สามารถเข้าถึงได้

หากท่านต้องการทราบการทำงานเชิงลึกว่า Pipeline เหล่านี้ทำงานอย่างไรสามารถกดเข้าไปอ่านได้ในบล็อคด่านล่าง

{% content-ref url="pipeline-deploy.md" %}
[pipeline-deploy.md](pipeline-deploy.md)
{% endcontent-ref %}



