# first-step
My first repository on GitHub

https://docs.github.com/

อะไรคือ Version Control System? ทำไมเราต้องการมัน?
- ใช้เลือก version ที่ prd ได้ ถอยได้
- มีศูนย์กลางของ Source Code
- communication ***
History
- ยุคแรก No Networking ส่งไฟล์หากัน คุยว่าแก้อันไหนอยู่กันการทับ
- ยุคสอง Centralised ต้องพึ่งพา network ทุกครั้งต้องมีการ connect เพิ่อตรวจสอบ (Merge bofore Commit)
- ยุคสาม Distributed ยุคที่เข้าใจ dev ว่าอยากทำงานได้ด้วยการ Commit Version ไว้ที่ตัวเอง (Commit bofore Merge)
วิธีการเก็บ
1. Delta เก็บแต่ละ commit เฉพาะ File ที่ Change ประหยัดเนื้อที่ในการเก็บ แต่เวลาจะควานหาก็ต้องไปดูทั้งหมด
2 DAG เก็บแต่ละ commit ด้วยไฟล์ทั้งหมด เนื้อที่ในการเก็บเยอะ แต่เวลาหาไว
เป้าหมายของ git คือ เร็ว, ง่าย, รอบรับหลาย Branch, fully distributed?????, จัดการ project ขนาดใหญ่ เหมือน linux kernel
จบที่ install git 
