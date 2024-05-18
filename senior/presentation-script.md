# Script

## Intro

- [x] สวัสดีครับ วันนี้ผมจะมานำเสนอ Senior Project หัวข้อ Usability Improvement ของ Payroll Service ครับ

## Intro 2

- [x] ในยุคปัจจุบันที่เป็นยุค Digital แอพต่าง ๆ ถูกสร้างขึ้นมามากมาย จนบางครั้งก็เป็นเรื่องยากสำหรับผู้ใช้งานในการตัดสินใจเลือกใช้เทคโนโลยี
- [x] หรือในบริบทของบริษัทที่มี Product เป็น Software
- [x] การซื้อขายจะเกิดขึ้นเมื่อผู้ใช้เกิดการยอมรับในเทคโนโลยีเหล่านั้นเท่านั้น
- [x] ซึ่งการยอมรับนั้นจะเกิดขึ้นได้ก็ต่อเมื่อ ผู้ใช้งานพบว่าเทคโนโลยีนั้นมีประโยชน์และใช้งานง่าย

## Case Study Company

- [x] และบริษัทกรณีศึกษาของเรา มี Service 3 ตัว คือ Payroll Attendance และ Workflow
- [x] ในขณะที่ผู้ใช้ของ Attendnace และ Workflow เพิ่มขึ้นอย่างต่อเนื่อง ผู้ใช้ Payroll กลับเพิ่มขึ้นไม่เยอะ เราเลยเลือกสนใจ Service Payroll ครับ
- [x] โดยคุณปีเตอร์ HR อายุ 29 ปี ซึ่งเป็นตัวแทนของผู้ใช้ Payroll กล่าวว่า เขามี 4 task ที่ต้องทำเป็นประจำทุกเดือน
- [x] คือ Register Employee, Update Attendance, Confirm Salary และ Create Document
- [x] และจากการสัมภาษณ์ผู้ใช้งานจริงจำนวน 20 คน เราพบว่า User Emotion มีค่าลดลงในช่วงของการ Confirm Salary

## Usability Testing Scene

- [x] เพื่อวิเคราะห์หาสาเหตุ เราเลยทำ Usability Testing กับ Payroll service ซึ่งประกอบไปด้วย 4 task คือ Register employee, Update attendance, comfirm salary และ create document
- [x] โดย metric ที่ใช้วัดประกอบด้วย time on task, success rate และ, lostness

## Usability Testing Result

- [x] โดยได้ผลลัพธ์ที่สำคัญดังนี้
- [x] Register Employee มี success rate แค่ 55% ส่วนที่ไม่สำเร็จเกิดจาก User กรอกข้อมูลตอนสมัครไม่ครบ
- [x] Update Attendance มี success rate แค่ 45% ส่วนที่ไม่สำเร็จเกิดจาก User แก้ไขข้อมูลผิดเดือน
- [x] Confirm Salary มี lostness สูงถึง 0.71 พบว่าเกิดจากการที่ user พบ error แล้วไม่สามารถแก้ไขได้
- [x] Create Document มี success rate ที่ 100% ครับ
- [x] ซึ่งผลลัพธ์ดังกล่าว สามารถนำมาสรุปเป็น Painpoint ของระบบได้ดังนี้ครับ

## System Painpoint

- [x] การที่ระบบยอมให้ user กรอกข้อมูลไม่ครบแปลว่าระบบยังไม่มี Error Prevention
- [x] และการที่ User เกินครึ่งมองข้าม Drop down list แปลว่าปัจจุบัน Interface ของระบบยังมีความไม่ชัดเจนมากพอ
- [x] และสุดท้ายการที่ user เจอ error และทำให้เขาหลง แปลว่า error message ยังมีความไม่ชัดเจนเช่นกันครับ

## Objective and Scope

- [x] จึงเป็นที่มาของการศึกษาในครั้งนี้ที่จะมุ่งปรับปรุง usability ของ payroll service
- [x] โดยมี scope คือการแก้ไข 3 ปัญหาที่เกิดขึ้น บนเวอร์ชั่น desktop และผู้ทดสอบเป็นคนไทย

## Iterative Design Approach

- [x] ในส่วนของขั้นตอนการทำงาน เราใช้วิธี Iterative Design โดยเริ่มจากการปรับปรุง Workflow ของการทำงานเพื่อเพิ่มประสิทธิภาพของการระบบ

### Register Employee Flow

- [ ] ใน flow การทำงานเดิมนั้น user จะต้องกรอกข้อมูลทั้งหมด 2 หน้า และฟอร์มที่จำเป็นต้องกรอกก็ยังกระจายอยู่ไม่เป็นระเบียบ
- [ ] เราจึงปรับปรุงใหม่โดยการควบรวม 2 หน้าเข้าด้วยกัน และแบ่งกลุ่มฟอร์มออกเป็นจำเป็นต้องกรอก กับสามารถกรอกทีหลังได้
- [ ] ได้ flow ใหม่ หน้าตาดังนี้ โดยประสิทธิภาพรวมของระบบเพิ่มขึ้น 20%

### Update Attendance Flow

- [ ] สำหรับ update attendance จากเดิมที่ user ต้องแก้ไขข้อมูลทีละคนทำ จะเห็นว่ามี loop การทำงานซ้ำซ้อนไปมาระหว่าง 2 หน้า
- [ ] ดังนั้นเราจึงปรับปรุงโดยการให้ user เลือกพนักงานทั้งหมดก่อน แล้วค่อยไปแก้ไขทีเดียวอีกทั้ง user ยังสามารถเลือกแก้ไขเฉพาะประเภทการเข้างานที่ต้องการได้อีกด้วย
- [ ] จะทำให้ loop ของการทำงานจะเหลือเพียงแค่การเลือกพนักงานเท่านั้น
- [ ] ซึ่งประสิทธิภาพของระบบจะเพิ่มขึ้นตามปริมาณพนักงานที่แก้ไขต่อครั้ง ดังตารางต่อไปนี้

### Confirm Salary Flow

- [ ] สำหรับ Confirm Salary มี flow การทำงานที่ตรงไปตรงมาอยู่แล้ว จึงไม่ได้มีการปรับปรุงอะไร

### Create Document Flow

- [ ] เช่นเดียวกันกับ Update Attendance, Create document เดิมนั้นสามารถสร้างเอกสารได้ทีละชนิด นั่นทำให้ user ต้องกลับไปมาระหว่าง 2 หน้าในการสร้างเอกสาร
- [ ] เราจึงปรับปรุงโดยการให้ user เลือกเอกสารที่ต้องการก่อนแล้วค่อยสร้างทีเดียว
- [ ] ทำให้ flow ใหม่มี loop การทำงานแค่ตอนเลือกเอกสารเท่านั้น
- [ ] โดยประสิทธิภาพของการทำงานก็จะแปรตามชนิดของเอกสารที่สร้างต่อครั้ง ดังแสดงในตารางต่อไปนี้

## System Implementation

- [x] จากนั้นจึงทำการ Design Interface เพื่อปรับปรุง Interaction Cost ระหว่าง User กับ ระบบ
- [x] ในการพัฒนาระบบ เราใช้ React และ Antd libray ในการพัฒนา frontend และใช้ Nodejs สำหรับ backend โดยใช้ database ของ mongodb
- [x] จากนั้นนำไป deploy บนเว็ปไซต์ชื่อ render
- [x] เพื่อให้ user สามารถเข้ามาใช้งานจากที่ไหนก็ได้

## System Validation

- [x] ในส่วนของการทดสอบระบบ เราเลือกผู้ใช้งานที่มีอายุ 20-40 ปี ที่มีประสบการณ์ในการทำ Payroll แต่ว่าไม่เคยใช้ service ของบริษัทกรณีศึกษามาก่อน
- [x] โดยให้ผู้เข้าร่วมทำ 4 task คือ register employee, update attendance , Confirm salary และ create document
- [x] และวัด 3 metric คือ time on task, success rate และ lostness

## Usability Testing Result Register Employee

- [x] จากผลการทดสอบพบว่า register employee มี average time on task ลดลงเหลือเพียง 184 วินาที
- [x] มี success rate สูงขึ้นจน 100% และไม่มีการกรอกข้อมูลไม่ครบอีก
- [x] และมี lostness เพียง 0.07

## Usability Testing Result Update Attendance

- [x] update attendance มี average time on task เหลือ 98 วินาที
- [x] มี success rate สูงขึ้นจน 100% เช่นกัน และไม่มีการแก้ไขข้อมูลผิดเดือน
- [x] แต่ design ใหม่มี lostness สูงขึ้นเล็กน้อย

## Usability Testing Result Confirm Salary

- [x] จาก design ใหม่ ประกอบกับการทำให้มั่นใจว่าข้อมูลต่าง ๆ นั้นครบถ้วนตั้งแต่ขั้นตอน register นั้นทำให้ user ไม่พบเจอ error เลย จนทำให้ lostness เหลือเพียง 0.1 -
- [x] เป็นผลให้ average time on task ลดลงเหลือเพียง 39 วินาที
- [x] และมี success rate ที่ 100%

## Usability Testing Result Confirm Salary

- [x] create document มี average time on task เหลือเพียง 42 วินาที
- [x] ในส่วนของ success rate ยังคงเดิมที่ 100%
- [x] และ lostness ลดลงเล็กน้อย
