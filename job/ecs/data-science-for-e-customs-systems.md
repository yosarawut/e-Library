# Data Science for e-Customs Systems

## Data Science for e-Customs Systems

## เป้าหมายที่จะนำมาแก้ปัญหาในด้านใดบ้าง

1. การนำเข้าข้อมูล \( import data \) ให้สะดวก ยืดหยุ่น มีความหลากหลาย 
2. ช่วยตรวจสอบการทำงาน ลดข้อผิดพลาด
3. ความรู้ข่าวสาร ประกาศกฎหมาย ข้อมูลที่แตกต่าง เพื่อความได้เปรียบทางธุรกิจ
4. Data Visualization ต่อยอดจาก Report ของเดิม เพื่อให้จบกระบวนการทำงาน อาจจะลองนำแนวคิด Privot table มาปรับใช้

   ==**Detail**==

### 1. การนำเข้าข้อมูล

### 2. ช่วยตรวจสอบการทำงาน ลดข้อผิดพลาด

* check digit 
  * Bank Account
  * ID Card
  * Container No.
* EXAM ใบอนุญาต ให้นำ excel เข้าในระบบเพื่อตรวจสอบ

### 3. ความรู้ข่าวสาร

* Permission แจ้งว่าเดือนนี้ มีพิกัดใดที่ตรวจสอบเพิ่มขึ้น / มีการเอาออก / มีการเปลี่ยนแปลง

### 4. Data Visualization

#### Example

* [_**esquisse**_](https://github.com/dreamRs/esquisse) 
* เป็น Interactive ที่มีความยืดหยุ่น ผู้ใช้งานสามารถเลือกข้อมูล กำหนดค่าต่าง ๆ ได้หลากหลายและเป็นอิสระ เพื่อให้รองรับกับ requirement ที่หลากหลาย 

This addin allows you to interactively explore your data by visualizing it with the [ggplot2](https://github.com/tidyverse/ggplot2) package. It allows you to draw bar plots, curves, scatter plots, histograms, boxplot and [sf](https://github.com/r-spatial/sf) objects, then export the graph or retrieve the code to reproduce the graph.

See online documentation : [https://dreamrs.github.io/esquisse/index.html](https://dreamrs.github.io/esquisse/index.html)

![enter image description here](https://github.com/dreamRs/esquisse/raw/master/man/figures/esquisse.gif)

### ข้อมูลเพิ่มเติม

#### Anatomy of Credit Card Number ความหมายของเลขบัตรเครดิต

เลขบัตรเครดิต/เดบิตกัน เลขบัตรเครดิตที่เห็นยาว ๆ กันนั้นประกอบด้วย 2 ส่วนใหญ่ ๆ ด้วยกันคือ BIN กับ PAN

**"ส่วนแรก BIN"**

ตัวเลข 6 ตัวแรกเรียกว่า Issuer หรือ Bank Identification Number\(IIN หรือ BIN\) พัฒนาขึ้นมาโดย International Organization for Standardization \(ISO\) มี American Bankers Association เป็นหน่วยงานจัดสรรหมายเลข IIN

เลขตัวแรกของ IIN เรียกว่า Major Industry Identifier \(MII\) เป็นตัวบ่งบอก ประเภทของธุรกิจที่ออกบัตร โดย IIN ทั้ง 6 ตัวจะบอกถึง Card Brand, Issuing Bank, Card Type, Card Level, Country, Bank's website และ Customer Care Line

**"ส่วนที่สอง PAN"**

ตัวเลขบัตรเครดิตที่เหลือเรียกว่า Primary Account Number \(PAN\) จะจำเพาะต่อผู้ถือบัตรแต่ละคน โดยตัวเลขสุดท้ายของ PAN เรียกว่า Check digit\(?\) เอาไว้ตรวจสอบว่าเลขบัตรเครดิตนั้นถูกต้องหรือไม่? ตัวเลขถัดมาทางซ้ายก็จะรัน 1, 2, 3,... ตามลำดับการอนุมัติบัตรครับ ดังนั้นถ้าเลข 8 ตัวท้ายของบัตรเป็น 0000 077x ก็คือบัตรอนุมัติเป็นคนที่ 77 นั่นเองครับ

แต่ถ้าเป็นสำนัก TMB, BBL, AEON จะไม่ใช้วิธีการเรียงลำดับดังกล่าว แต่จะกำหนดเลขบัตร 4 ตัวท้ายเป็นรูปแบบที่ตายตัว คือ

X00X หรือ X01X สำหรับ TMB  
X11X-X14X สำหรับ BBL และ  
XX0X สำหรับ AEON ครับ

ถ้าจะเรียงลำดับให้ดูที่หลัก 8-13 หรือ 8-14 แทนครับ ตัวอย่าง ของ TMB เป็น 4050 1617 0001 100X อันนี้จะเป็นการออกบัตรในลำดับที่ 11 ของ Series นั้นๆ \(ตัดหลักที่ 14-16 ออกไป\)

**"Check digit"**

Check digit\(?\) ได้มาจากการใช้ Luhn algorithm \(เทคนิคของผมคือจำว่า คูณสอง ลบเก้า คูณเก้า\) ตัวอย่างเช่นบัตร MasterCard เลข 16 หลักคือ 5237 1645 0365 554\(?\) มาคำนวณ Luhn algorithm กันดูว่าเลขสุดท้ายควรเป็นเลขอะไร?

ขั้นแรก จาก Check digit\(?\) ไล่ย้อนมาทางซ้ายมือให้คูณที่ตัวเลขตัวเว้นตัวด้วย 2 ตัวที่เว้นไว้ไม่ต้องคูณอะไรดังนี้  
\(5x2\) 2 \(3x2\) 7 \(1x2\) 6 \(4x2\) 5 \(0x2\) 3 \(6x2\) 5 \(5x2\) 5 \(4x2\) ค่าที่คูณได้คือ \(10\) 2 \(6\) 7 \(2\) 6 \(8\) 5 \(0\) 3 \(12\) 5 \(10\) 5 \(8\)

ขั้นที่สอง ถ้าผลคูณในวงเล็บเกิน 9 ให้ลบออกด้วย 9 จะได้เป็น  
\(1\) 2 \(6\) 7 \(2\) 6 \(8\) 5 \(0\) 3 \(3\) 5 \(1\) 5 \(8\)

ขั้นที่สาม นำตัวเลขทั้งหมดบวกรวมกัน จะได้เป็น  
\(1\)+ 2+ \(6\)+ 7+ \(2\)+ 6+ \(8\)+ 5+ \(0\)+ 3+ \(3\)+ 5+ \(1\)+ 5+ \(8\) = 62

ขั้นสุดท้าย นำผลรวมที่ได้คูณด้วย 9 ได้ผลลัพธ์เท่าไหร่ ตัวเลขสุดท้ายคือ Check digit\(?\) นั่นคือ  
62x9 = 558 แสดงว่า check digit คือเลข 8 นั่นเอง \(แสดงว่าเลขบัตรดังกล่าวคือ 5237 1645 0365 5548 \)

**หมายเหตุ** เวลาซื้อของออนไลน์ถ้าเราพิมพ์เลขบัตรถูกต้องจะขึ้นเครื่องหมายถูกสีเขียวเพราะตรวจสอบด้วย Luhn algorithm นั่นเองครับ

ดูภาพประกอบ&gt;&gt;&gt; [https://bit.ly/2IuuzbK](https://goo.gl/aDWVoh)

#### บัตรประชาชน

1. ตัวเลขบนบัตรประชาชนจะมีทั้งหมด 13 หลัก นำเลขใน 12 หลักแรก มาคูณกับเลขประจำตำแหน่ง \(เลขประจำหลักได้แก่ 13 บวก 1 ลบด้วยตำแหน่งที่\) ส่วนเลขหลัก 13 ที่ใช้ในการคำนวณคือจำนวนตัวเลขทั้งหมดที่ต้องการตรวจสอบ  
2. หลังจากนั้นเอาผลคูณของทั้ง 12 หลักมารวมกัน แล้ว modulation \(การหารเอเศษ\) ด้วย 11  
3. เอาเศษที่ได้จากการหารในข้อ 2 มาลบด้วย 11 เท่านี้ก็ได้เลขที่เป็น Check Digit แล้ว \(ถ้าผลจากข้อ 2 ได้ 10 ให้เอาเลขหลักหน่วยเป็น Check Digit ก็คือ 0 นั้นเอง\)  

   ตัวอย่าง 1-2345-67890-12-9  

   นำไปคูณเลขประจำตำแหน่ง \(1_13\)+\(2_12\)+\(3_11\)+\(4_10\)+\(5_9\)+\(6_8\)+\(7_7\)+\(8_6 \)+\(9_5\)+\(0_4\)+\(1_3\)+\(2_2\) = 352  

   modulation 11 .... 352%11= 0  

   นำ 11 ตั้งแล้วลบด้วย 0 11 - 0 = 11 เอาเลขหลักหน่วย ดังนั้น Check Digit คือ 1  

   อ้าว... นี้มันเลขที่บัตรประชาชนไม่ถูกต้องนี้ ที่ถูกต้องคือ 1-2345-67890-12-1  

โดยหลักการคำนวนนี้ สามารถใช้กับเลข 10 หลักอย่างเลขที่บัญชีได้อีกด้วย

ตัวอย่าง 123-4-56789-6  
นำไปคูณเลขประจำตำแหน่ง \(1_10\)+\(2_9\)+\(3_8\)+\(4_7\)+\(5_6\)+\(6_5\)+\(7_4\)+\(8_3\)+\( 9\*2\) = 210  
modulation 8 .... 210%8= 2  
นำ 8 ตั้งแล้วลบด้วย 2.... 8 - 2 = 6 เอาเลขหลักหน่วย ดังนั้น Check Digit คือ 6 อ้าว... นี้มันเลขที่บัญชีที่ถูกต้อง

**ความหมายของเลขหลักต่าง ๆ**

**หลักที่ 1** หมายถึง ประเภทบุคคล มีแปดประเภท **หลักที่ 2-5** หมายถึง รหัสสำนักทะเบียนที่มีชื่อในทะเบียนบ้านนั้นๆ **หลักที่ 6-10** หมายถึง กลุ่มที่บุคคล แต่ละประเภท ตามหลักที่ 1 หรือเล่มที่ของสูติบัตร **หลักที่ 11-12** หมายถึง ลำดับที่ของบุคคลในแต่ละกลุ่มประเภท ตามระบบทะเบียนบ้าน หรือหมายถึง ใบที่ของสูติบัตร ในแต่ละเล่ม **หลักที่ 13** หมายถึง เลขตรวจสอบความถูกต้อง \(CHECK DIGIT\) ของเลขประจำตัวประชาชน 12 หลักแรก ว่าถูกต้องหรือไม่ เช่น เป็นเลขที่เขียนผิด หรือเป็นเลขปลอมหรือไม่ โดยตรวจสอบและคำนวณด้วยเครื่องคอมพิวเตอร์.. [http://dop.rta.mi.th/pid13.htm](http://dop.rta.mi.th/pid13.htm)

[Source :](http://musicjusk.blogspot.com/2010/04/blog-post_10.html)

## ECS Mobile App Service

![enter image description here](https://gitlab.com/yosarawut/e-library/raw/master/Document/Job/ECS/img/Screen_Shot_2562-09-09_at_09.22.42.png?inline=false) ==เสนอเพิ่มเติม==

* Ref. file ของกรมศุลกากร เช่น ใบอนุญาต/ใบรับรอง , รหัสยกเว้นไม่ต้องมีใบอนุญาต/ใบรับรอง, หน่วยหีบห่อ, หน่วยของปริมาณ, รหัสด่านศุลกากร ฯลฯ \(มีรายละเอียดว่าอัพเดทล่าสุดเมื่อวันที่เท่าไหร่ + แจ้งให้ทราบว่า มีการเปลี่ยนแปลง เพิ่ม-ลด-แก้ไข ในส่วนใดบ้างเมื่อเทียบกับข้อมูลก่อนหน้า\)

