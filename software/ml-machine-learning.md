# การประยุกต์ใช้ ML (Machine Learning)

<figure><img src="../.gitbook/assets/Travelful+ #261492final.png" alt=""><figcaption></figcaption></figure>

ในโปรเจคนี้เรามีการใช้ AI ในการ Classification review แต่ละ review ว่ามีการพูดถึงไลฟ์สไตล์ใดบ้างเป็นส่วนใหญ่ เช่น สายกิน, สาย shop, มรดกและวัฒนธรรม, ถ่ายรูป, ชมวิว, ทะเล, Adventure ฯลฯ เพื่อเป็นหนึ่งในข้อมูลที่ช่วยให้ Algorithm ที่ใช้ในการสร้างแผนอัตโนมัติ สามารถตัดสินใจเลือกสถานที่ที่จะเข้าไปอยู่ในแผนได้เหมาะสมขึ้น โดยการพัฒนาจะมีการใช้ FacebookAI/xlm-roberta-base ในการช่วง embed review ในอยู่ในรูปของตัวเลขเพื่อให้สามารถใช้ Neural Network ในการทำ Classification ได้แม่นยำขึ้น

