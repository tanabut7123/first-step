# Test Technique

## การทำ Decision Table Testing

กรณีที่หน้าจอมีการกำหนดให้กรอกค่าดังนี้

- Name ต้องกรอกเสมอ

- Age 18 ปีขึ้นไป และไม่เกิน 100 ปี

จากตัวอย่างข้อมูลมีอยู่ 2 ประเภท

- Equivalence Partitioning คือมีค่าตายตัวชัดเจน เช่น Name มีความเป็นไปได้แค่กรอกหรือไม่กรอกเท่านั้น

- Boundary Value Analysis คือมีขอบเขตของแต่ละกลุ่ม

![Boundary value analysis](image/Boundary%20value%20analysis.jpg)

ทำการแยกเคสของข้อมูลที่จะทำการทดสอบ

1.กรณีไม่รู้ภายใน ก็ทำการแยกเคสแบบไม่คำนึงถึงภายใน Software(ฺBlack Box Testing)

|Case|Name|Age|Output|
|--|--|--|--|
|1|Not Null|19|Pass|
|2|Not Null|99|Pass|
|3|Not Null|18|Pass|
|4|Not Null|100|Pass|
|5|Not Null|17|Not Pass|
|6|Not Null|101|Not Pass|
|7|Null|19|Not Pass|
|8|Null|99|Not Pass|
|9|Null|18|Not Pass|
|10|Null|100|Not Pass|
|11|Null|17|Not Pass|
|12|Null|101|Not Pass|

2.กรณีรู้ภายใน ก็ทำการแยกเคสแบบคำนึงถึงภายใน Software(White Box Testing) กรณีที่ Software เป็นดังภาพ

![Flow Chart](image/Flow%20Chart.jpg)

|Case|Name|Age|Output|
|--|--|--|--|
|1|Not Null|19|Pass|
|2|Null|X|Not Pass|
|3|Not Null|19|Pass|
|4|Not Null|18|Pass|
|5|Not Null|100|Pass|
|6|Not Null|17|Not Pass|
|7|Not Null|101|Not Pass|

เพิ่มเติมหลักการวิเคราะห์ข้อมูลอีกประเภทนึงคือ State Transition

![State Transition](image/State%20Transition.jpg)

แยก Unit Test ออกมาเป็น 4 Case

- State None > Action Create > State Draft

- State Draft > Action Send > State Approve

- State Approve > Action Return > State Draft

- State Approve > Action OK > State Complete

หลังจากนั้นทำการเทสเป็น Scenario ตาม State ดังนี้

- None > Draft > Approve > Complete

- None > Draft > Approve > Draft > Approve > Complete
