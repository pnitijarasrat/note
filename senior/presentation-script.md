# Script

## Intro

- [ ] สวัสดีครับ วันนี้ผมจะมานำเสนอ Senior Project หัวข้อ Usability Improvement ของ Payroll Service ครับ

## Intro 2

- [ ] ในยุคปัจจุบันที่เป็นยุค Digital แอพต่าง ๆ ถูกสร้างขึ้นมามากมาย จนบางครั้งก็เป็นเรื่องยากสำหรับผู้ใช้งานในการตัดสินใจเลือกใช้เทคโนโลยี
- [ ] หรือในบริบทของบริษัทที่มี Product เป็น Software
- [ ] การซื้อขายจะเกิดขึ้นเมื่อผู้ใช้เกิดการยอมรับในเทคโนโลยีเหล่านั้นเท่านั้น
- [ ] ซึ่งการยอมรับนั้นจะเกิดขึ้นได้ก็ต่อเมื่อ ผู้ใช้งานพบว่าเทคโนโลยีนั้นมีประโยชน์และใช้งานง่าย

## Case Study Company

- [ ] และบริษัทกรณีศึกษาของเรา มี Service 3 ตัว คือ Payroll Attendance และ Workflow
- [ ] ในขณะที่ผู้ใช้ของ Attendnace และ Workflow เพิ่มขึ้นอย่างต่อเนื่อง ผู้ใช้ Payroll กลับเพิ่มขึ้นไม่เยอะ เราเลยเลือกสนใจ Service Payroll ครับ
- [ ] โดยคุณปีเตอร์ HR อายุ 29 ปี ซึ่งเป็นตัวแทนของผู้ใช้ Payroll กล่าวว่า เขามี 4 task ที่ต้องทำเป็นประจำทุกเดือน
- [ ] คือ Register Employee, Update Attendance, Confirm Salary และ Create Document
- [ ] และจากการสัมภาษณ์ผู้ใช้งานจริงจำนวน 20 คน เราพบว่า User Emotion มีค่าลดลงในช่วงของการ Confirm Salary

## Usability Testing Scene

- [ ] เพื่อวิเคราะห์หาสาเหตุ เราเลยทำ Usability Testing กับ Payroll service ซึ่งประกอบไปด้วย 4 task คือ Register employee, Update attendance, comfirm salary และ create document
- [ ] โดย metric ที่ใช้วัดประกอบด้วย time on task, success rate และ, lostness

## Usability Testing Result

- [ ] โดยได้ผลลัพธ์ที่สำคัญดังนี้
- [ ] Register Employee มี success rate แค่ 55% ส่วนที่ไม่สำเร็จเกิดจาก User กรอกข้อมูลตอนสมัครไม่ครบ
- [ ] Update Attendance มี success rate แค่ 45% ส่วนที่ไม่สำเร็จเกิดจาก User แก้ไขข้อมูลผิดเดือน
- [ ] Confirm Salary มี lostness สูงถึง 0.71 พบว่าเกิดจากการที่ user พบ error แล้วไม่สามารถแก้ไขได้
- [ ] Create Document มี success rate ที่ 100% ครับ
- [ ] ซึ่งผลลัพธ์ดังกล่าว สามารถนำมาสรุปเป็น Painpoint ของระบบได้ดังนี้ครับ

## System Painpoint

- [ ] การที่ระบบยอมให้ user กรอกข้อมูลไม่ครบแปลว่าระบบยังไม่มี Error Prevention
- [ ] และการที่ User เกินครึ่งมองข้าม Drop down list แปลว่าปัจจุบัน Interface ของระบบยังมีความไม่ชัดเจนมากพอ
- [ ] และสุดท้ายการที่ user เจอ error และทำให้เขาหลง แปลว่า error message ยังมีความไม่ชัดเจนเช่นกันครับ

## Objective and Scope

- [ ] จึงเป็นที่มาของการศึกษาในครั้งนี้ที่จะมุ่งปรับปรุง usability ของ payroll service
- [ ] โดยมี scope คือการแก้ไข 3 ปัญหาที่เกิดขึ้น บนเวอร์ชั่น desktop และผู้ทดสอบเป็นคนไทย

## Iterative Design Approach

- [ ] ในส่วนของขั้นตอนการทำงาน เราใช้วิธี Iterative Design โดยเริ่มจากการปรับปรุง Workflow ของการทำงานเพื่อเพิ่มประสิทธิภาพของการระบบ
- [ ] จากนั้นจึงทำการ Design Interface เพื่อปรับปรุง Interaction Cost ระหว่าง User กับ ระบบ

## System Implementation

- [ ] ในการพัฒนาระบบ เราใช้ React และ Antd libray ในการพัฒนา frontend และใช้ Nodejs สำหรับ backend โดยใช้ database ของ mongodb
- [ ] จากนั้นนำไป deploy บนเว็ปไซต์ชื่อ render
- [ ] เพื่อให้ user สามารถเข้ามาใช้งานจากที่ไหนก็ได้

## System Validation

- [ ] ในส่วนของการทดสอบระบบ เราเลือกผู้ใช้งานที่มีอายุ 20-40 ปี ที่มีประสบการณ์ในการทำ Payroll แต่ว่าไม่เคยใช้ service ของบริษัทกรณีศึกษามาก่อน
- [ ] โดยให้ผู้เข้าร่วมทำ 4 task คือ register employee, update attendance , Confirm salary และ create document
- [ ] และวัด 3 metric คือ time on task, success rate และ lostness

## Usability Testing Result Register Employee

- [ ] จากผลการทดสอบพบว่า register employee มี average time on task ลดลงเหลือเพียง 184 วินาที
- [ ] มี success rate สูงขึ้นจน 100% และไม่มีการกรอกข้อมูลไม่ครบอีก
- [ ] และมี lostness เพียง 0.07

## Usability Testing Result Update Attendance

- [ ] update attendance มี average time on task เหลือ 98 วินาที
- [ ] มี success rate สูงขึ้นจน 100% เช่นกัน และไม่มีการแก้ไขข้อมูลผิดเดือน
- [ ] แต่ design ใหม่มี lostness สูงขึ้นเล็กน้อย

## Usability Testing Result Confirm Salary

- [ ] จาก design ใหม่ ประกอบกับการทำให้มั่นใจว่าข้อมูลต่าง ๆ นั้นครบถ้วนตั้งแต่ขั้นตอน register นั้นทำให้ user ไม่พบเจอ error เลย จนทำให้ lostness เหลือเพียง 0.1 -
- [ ] เป็นผลให้ average time on task ลดลงเหลือเพียง 39 วินาที
- [ ] และมี success rate ที่ 100%

## Usability Testing Result Confirm Salary

- [ ] create document มี average time on task เหลือเพียง 42 วินาที
- [ ] ในส่วนของ success rate ยังคงเดิมที่ 100%
- [ ] และ lostness ลดลงเล็กน้อย
