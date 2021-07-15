# first-step
My first repository on GitHub

https://docs.github.com/

Day 1
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
Day 2 & Day 3
คำสั่งเบื้องต้น
	git config
	- ตามด้วย --global << ทุกที่ในการใช้ git บนเครื่องนี้ ไม่ใส่คือแค่ folder ที่อยู่
	- ตามด้วย user.name "{user name}"/ user.email "{email address}"
	- ตามด้วย -l << list ทั้งหมด
	git init << ทำ directory ที่อยู่ให้เป็น git โดยการสร้าง folder .git เป็นตัว repository บน local
	เริ่มจากทำความเข้าใจ Workflow ประกอบด้วย
	- working directory อยู่บน folder ที่ทำ แต่ยังไม่อยู่ใน git ต้องใช้คำสั่ง git add
	- staging area อยู่ใน git แต่ยังไม่ได้ commit ต้องใช้คำสั่ง git commit
	- local repository เป็น file ที่ commit แต่ยังไม่ได้ push ต้องใช้คำสั่ง git push
	- remote repository เป็นส่วนที่อยู่บน server
	ตัดมาแค่ local operations ก่อน โดย Life Cycle มีทั้งหมด 4 สถานะจะเป็น
	- Untracked คือ ยังไม่อยู่ใน git
	- Unmodified คือ ไม่มีการเปลี่ยนแปลง
	- Modified คือ มีการเปลี่ยนแปลง
	- Staged คือ อยู่ใน git แล้ว
	git status << เพื่อดูสถานะว่ามีอะไรเปลี่ยนแปลงไหมใน local
	- ทำการสร้าง file (touch {file name}) สถานะจะเป็น Untracked files คือไฟล์มีเพิ่มเข้ามาแต่ยังไม่อยู่ใน git แนะนำ git add เพื่อเปลี่ยนสถานะจาก Untracked ไป Staged
	- ทำการเพิ่ม file ลงใน git (git add {filename}) สถานะจะเป็น Change to be committed คือมีไฟล์ยังไม่ได้ commit จะเปลี่ยนใหม่ แนะนำ git rm เพื่อเปลี่ยนสถานะจาก Staged กลับไปเป็น Untracked
	- ทำการเปลี่ยนแปลงข้อมูลใน file (echo "{content}" > {filename}) สถานะจะเป็น Change to be committed และ Change not staged for commit แนะนำ git add/git restore เพื่อ update สถานะ file ใน Staged
	git diff << ตรวจสอบความเปลี่ยนแปลงระหว่าง Modified กับ Staged
	git commit -m "{message}" << เปลี่ยนสถานะจาก Staged ไป Unmodified
	- ทำการตรวจสอบสถานะหลังจาก commit จะพบว่ายังมีส่วนที่ไม่เท่ากันระหว่าง Modified กับ Staged เนื่องจาก echo แต่ยังไม่ add สถานะจะเป็น Change not staged for commit แนะนำ git add/git restore
	- ทำการ add และเช็คสถานะ จะพบว่าสถานะเป็น Change to be committed
	- สามารถทำการ add พร้อม commit ได้ -a -m แต่จริงๆ ควรแยกเพื่อให้เข้าใน Stage การทำงานมากกว่า
	git rm  {file name}
	- ทำการลบ file (rm {file name}) สถานะจะเป็น Change not staged for commit แนะนำ git add/rm/git checkout เพราะลบ file ทำให้ไม่เท่ากับใน Staged 
	- ทำการลบ file ออกจาก Staged (git rm {file name}) สถานะจะเป็น Change to be committed แนะนำ git reset HEAD <file> เพื่อทำให้ file กลับเข้ามาใน Staged 
	- ทำการ commit เพื่อลบออกจาก git
	git mv {old file name} {new file name} << เปลี่ยนชื่อไฟล์
	ประกอบด้วย
		- mv {old file name} {new file name} เปลี่ยนชื่อไฟล์ 
		- git rm {old file name} ลบ file เก่า
		- git add {new file name} เพิ่ม file ใหม่
	หลังจากนั้นให้ทำการ commit เพื่อให้ git เห็นว่าเป็น file เดียวกัน โดยดูจาก content เดียวกัน แต่ลบ 1 เพิ่ม 1
ทำความเข้าใจ gitignore
	- อยู่ในไฟล์ .gitignore โดยการระบุไฟล์ / ระบุ folder / ระบุไฟล์ใน folder (* หมายถึง ที่นี่ ** หมายถึงทุก folder)
Day 4
เพิ่ม SSH Key บน Github
- Gen Key ก่อน ผ่าน ssh-keygen
วิธีการเอาจาก Remote มาไว้ local (ดูได้ใน gitlab)
- Create a new repository > git clone {url}
- Push an existing folder > git init --initial-branch=main, get remote add origin {url}, git add ., git commit -m "{comment}", git push -u origin main
- Push an existing Git repository > get remote add origin {url}, git push -u origin --all, git push -u origin --tags
ดูการเปลี่ยนแปลงผ่าน git log
เอาไฟล์ขึ้น git push
เอาลงมา git pull
Day 5
https://siamchamnankit.co.th/%E0%B8%A5%E0%B8%AD%E0%B8%87%E0%B8%AA%E0%B8%A3%E0%B8%B8%E0%B8%9B-%E0%B8%81%E0%B8%8F%E0%B8%82%E0%B8%AD%E0%B8%87%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%AD%E0%B8%AD%E0%B8%81%E0%B9%81%E0%B8%9A%E0%B8%9A-uris-%E0%B8%88%E0%B8%B2%E0%B8%81%E0%B8%AB%E0%B8%99%E0%B8%B1%E0%B8%87%E0%B8%AA%E0%B8%B7%E0%B8%AD-rest-api-design-rulebook-1fb2e3a7258f
https://siamchamnankit.co.th/%E0%B8%A5%E0%B8%AD%E0%B8%87%E0%B8%AA%E0%B8%A3%E0%B8%B8%E0%B8%9B-%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%AD%E0%B8%AD%E0%B8%81%E0%B9%81%E0%B8%9A%E0%B8%9A-%E0%B9%80%E0%B8%A5%E0%B8%B7%E0%B8%AD%E0%B8%81%E0%B9%83%E0%B8%8A%E0%B9%89-http-methods-%E0%B9%81%E0%B8%A5%E0%B8%B0-response-code-%E0%B8%82%E0%B8%AD%E0%B8%87-rest-api-a5329a59e334
https://github.com/up1/course-web-api
server side render ให้ server gen html
- server ทำงานหนัก
- ต้อง ren ใหม่เสมอที่ srver
server side render+jquery ติดภาษา แกะออกยากเพราะยิดติดภาษา
modern web application
API คือ Aplllication Programming Interface
>> JAVA RMI Protocal, 
Web API
REST API - https://iamgique.medium.com/restful-api-%E0%B8%81%E0%B8%B1%E0%B8%9A-rest-api-%E0%B8%95%E0%B9%88%E0%B8%B2%E0%B8%87%E0%B8%81%E0%B8%B1%E0%B8%99%E0%B8%99%E0%B8%B0%E0%B8%A3%E0%B8%B9%E0%B9%89%E0%B8%A2%E0%B8%B1%E0%B8%87-2c70c42990e3
GraphQL - ยอมให้ query ผ่าน
Webhook - ลงทะเบียน

HTML > XML > 
NEWMAN ไปหามา ติดตั้งที่เครื่อง
REST vs RESTful > https://iamgique.medium.com/restful-api-%E0%B8%81%E0%B8%B1%E0%B8%9A-rest-api-%E0%B8%95%E0%B9%88%E0%B8%B2%E0%B8%87%E0%B8%81%E0%B8%B1%E0%B8%99%E0%B8%99%E0%B8%B0%E0%B8%A3%E0%B8%B9%E0%B9%89%E0%B8%A2%E0%B8%B1%E0%B8%87-2c70c42990e3
DAY 6
jsonplaceholder << เวปที่ทำมาดี 
ลง JSON Viewer << Extension บน Chrome
API Gateway << https://siamchamnankit.co.th/%E0%B8%A5%E0%B8%AD%E0%B8%87%E0%B8%AA%E0%B8%A3%E0%B8%B8%E0%B8%9B-microservices-pattern-the-api-gateway-eeb6ca40238
Allow Origin ???

ว่าด้วยเรื่องสถาปตกรรม Software
1. User login ไปยัง Server เอ้าไม่มี Security ทำไงดี อ่ะ session คือคำตอบ
2. User login ไปยัง Server เช็ค Authority แล้วก็เก็บ Session ไว้ที่ Server Return Session ID กลับไปหาให้ฝั่งลูกค้า หลังจากนั้นการ Request มาก็ส่ง Session ID มาด้วย มาเช็ค Session Timeout แทน เอ้าลูกค้าเยอะขึ้นเพิ่มเครื่องดีกว่า LoadBalancer คือคำตอบ
3. User login ไปยัง LoadBalancer เพื่อกระจายให้แต่ละเครื่องดูแลลูกค้าแต่ละคน เอ้าเครื่องตายทำไง ลูกค้าต้อง login ใหม่ Sticky(Session/IP) หรือการแยก Front End / Back End คือคำตอบ 

ยุคของ FE BE
????
????
????
????
????
????
????


DAY 7
