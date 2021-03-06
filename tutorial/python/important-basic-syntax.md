# ไวยกรณ์พื้นฐานที่จำเป็นอย่างยิ่งต้องจดจำ \(Important basic syntax\)

ไวยกรณ์ต่าง ๆ ที่จะกล่าวต่อไปนี้ ขอให้ผู้อ่านจดจำ และท่องให้ขึ้นใจ เพราะมันจะทำให้การเขียนโปรแกรมไม่มีอุปสรรค

## Case sensitivity

การตั้งชื่อตัวแปร ตัวใหญ่ และตัวเล็กถือว่าเป็นคนละตัวแปร เช่น Number และ number ไม่ใช่ตัวแปรตัวเดียวกัน

## Space and tabs don’t mix

ไพธอนมองว่า space และ tabs มีความหมายไม่เหมือนกัน ดังนั้นเวลาเขียนโปรแกรมอย่าผสมระหว่าง space และ tabs เข้าด้วยกันให้เลือกเอาอย่างใดอย่างหนึ่งเท่านั้น

## Objects \(วัตถุ\)

ไพธอนถูกสร้างขึ้นภายใต้แนวคิดการโปรแกรมเชิงวัตถุ ดังนั้นเมื่อเราเรียกใช้งานคลาสใด ๆ ก็ตามถือว่าเป็นวัตถุตามแนวความคิดแบบโปรแกรมเชิงวัตถุ \(การโปรแกรมเชิงวัตถุจะกล่าวในบทที่ 11 \) ดังนั้นเมื่อใดก็ตามที่มีการสร้างวัตถุและต้องการเข้าถึงแอตทริบิวต์ \(Attribute\) หรือฟังชัน \(Function\) ใดๆ ในวัตถุต้องใช้`“ ”` แล้วตามด้วยเครื่องหมาย `( )` แต่ถ้าอ้างถึงตัวแปรไม่ต้อง มี \( \) เช่น เมื่อต้องการเปลี่ยนค่าสตริง `'Pop'`เป็นตัวอักษรตัวใหญ่ทั้งหมด ทำได้โดยเรียกใช้คลาส upper ในไลบรารีของไพธอน ดังนี้ `'Pop'.upper()`

## Scope

ในการพัฒนาโปรแกรมขนาดใหญ่ ที่มีโปรแกรมเมอร์มากกว่า 1 คน อาจจะประสบปัญหาเรื่องการประกาศตัวแปรที่ซ ้ากันได้ ดังนั้นเพื่อให้การเข้าถึงและใช้งานตัวแปรเป็นไปอย่างถูกต้องโดยไม่มีข้อผิดพลาด แนะนำให้ผู้เขียนโปรแกรมใช้งานในลักษณะของฟังชันจะดีกว่า โดยมีการส่งค่าตัวแปรไปในฟังชัน และคืนค่าที่คำนวณเรียบร้อยแล้วกลับมา จะไม่ทำให้ประสบปัญหาเรื่องของการอ้างตัวแปรดังที่กล่าวมาแล้ว

## Namespaces

คือพื้นที่ที่ใช้เก็บตัวแปรของระบบที่สร้างไว้ให้เราโดยที่เราไม่รู้ และตัวแปรต่าง ๆ ที่เราสร้างขึ้นมาทีหลัง เราสามารถขอดูข้อมูลที่เก็บอยู่ใน Namespaces ได้โดยใช้คำสั่ง `dir()` ซึ่งเป็น `built-in function` ที่มีอยู่ในไพธอน ซึ่งถ้าเรายังไม่ได้ประกาศตัวแปร หรือฟังชันใดๆ ในโรแกรมจะปรากฎรายการของตัวแปรที่ระบบสร้างไว้ให้ 6 ตัวคือ`'__builtins__', '__doc__', '__file__', '__loader__', '__name__', '__package__'`

ถ้าต้องการดูประเภทของตัวแปรเหล่านี้ว่าเป็นชนิดอะไร สามารถเรียกดูได้โดยใช้คำสั่ง `type()` เช่น `type (__builtins__)` ชนิดของตัวแปรที่ปรากฎคือ`<class 'module'>`หรือ `type (__doc__)` ชนิดของตัวแปรที่ปรากฎคือ `<class 'NoneType'>` เมื่อตัวแปรเป็นชนิด module

เราสามารถดูข้อมูลภายในโมดูลเหล่านั้นได้ด้วยคำสั่ง `dir( )` เช่น `dir(__builtins__)` ผลที่ได้ คือชื่อของฟังชัน หรือคลาสที่อยู่ภายในทั้งหมดออกมา ดังนี้ `['ArithmeticError', 'AssertionError', 'AttributeError',…., 'zip']` ในแต่ละ `Namespaces` เปรียบเสมือนเป็นคลัง หรือตู้คอนเทนเนอร์สำหรับเก็บข้อมูลต่างๆ ลงไป ดังนั้นแต่ละโปรแกรมจะถูกเก็บแยกออก จากกันโดยอิสระ

ดังนั้นอาจจะเรียก Namespaces ว่าเหมือนกับ Scope ก็ได้ เมื่อใดก็ตามที่เราสร้างตัวแปร หรือฟังชัน ตัวแปรที่สร้างขึ้นก็จะถูกเก็บอยู่ในพื้นที่ของ Namespaces ทั้งหมด เมื่อเราทำการนำเข้าคลาสใดๆ เข้ามาใช้งานในโปรแกรมด้วยการใช้`import` คลาสต่าง ๆ เหล่านั้นก็จะมาปรากฎใน Namespaces ด้วย เช่น import math จากนั้นใช้คำสั่ง `dir()` ผลลัพธ์ที่ได้คือ `['__builtins__', '__doc__', '__loader__', '__name__', '__package__', 'math', 'x']`

ถ้าผู้เขียนโปรแกรมต้องการทราบรายละเอียดของฟังชัน หรือ เมธอต \(Method\) ในคลาส`math` ให้ใช้คำสั่ง `dir(math)` ถ้าผู้เขียนโปรแกรมต้องการทราบการทำงานในแต่ละฟังชันของ math ว่าทำงานอย่างไร สามารถทำได้โดยใช้ฟังชัน print ตามด้วยชื่อคลาส.เมธอต เช่น `print (math.pow)` หรือ `print (math.pi)` เป็นต้น

## Colons

ไพธอนตัดเครื่องหมายแสดงขอบเขตของข้อมูล `{…}`ทิ้งไป แล้วใช้ : ร่วมกับการเขียนโปรแกรมด้วยการย่อหน้าแทน โดยเริ่มจากคอลัมภ์ที่ 1 เสมอดังนั้นอย่าลืม : หลังคำสั่ง`if, for, while, def` เป็นอันขาด

## Blank lines

เมื่อจำเป็นต้องเขียนคำสั่งที่มีความยาวมากๆ ไม่หมดใน 1 บรรทัด ให้ใช้เครื่องหมาย`\` ตามด้วย`enter`เช่น

```python
print ('This is a really long lines \  
but we can make it across \  
multiple lines')
```

หรือ

```python
x = 4 * 5 - 5 + \  
6 + 8 \  
+ 5 % 2  
print(x)
```

## Lines and Indentation

ไพธอนไม่ใช้เครื่องหมาย`{…}`ในการกำหนดขอบเขต เหมือนในภาษาซี ไพธอนใช้การเยื้อง หรือย่อหน้าแทน ดังนั้นผู้เขียนโปรแกรมจะต้องระวังการเยื้องหน้าให้ดี จากตัวอย่างต่อไปนี้

**ตัวอย่างที่ 1**

```python
if True:  
    print ("True")  
else:  
    print ("Answer")
    print ("False")
```

**ตัวอย่างที่ 2**

```text
if True:  
    print ("Answer")  
    print ("True")  
else:  
    print ("Answer")
print ("False")
```

โปรแกรมตัวอย่างที่ 1 จะไม่เกิด ข้อผิดพลาด เพราะว่าคำสั่งหลัง else ย่อหน้าตรงกัน  
โปรแกรมตัวอย่างที่ 2 จะเกิดข้อผิดพลาด เพราะว่าคำสั่งหลัง else ย่อหน้าไม่ตรงกัน

## Multi-line statements

แต่ละคำสั่งของไพธอนส่วนใหญ่จบลงด้วยการขึ้นบรรทัดใหม่ \(new line\) แต่ผู้เขียนโปรแกรมสามารถใช้เครื่องหมาย`\`เพื่อเชื่อมคำสั่งได้ เช่น

```python
total = item_one + \ #item_one = "one"
item_two + \ #item_two = "two" 
item_three #item_three = "three"
```

**OUTPUT**

```python
one two three
```

สำหรับข้อมูลในเครื่องหมาย `[…], {…}` หรือ`(…)` ไม่จำเป็นต้องใช้เครื่องหมาย `\`เช่น

```python
days = ['Monday', 'Tuesday', 'Wednesday',  
'Thursday', 'Friday']
```

## Quotation in Python

ไพธอนใช้เครื่องหมาย`' (single quote), " (double quote)`ในการแสดงค่าของสตริง แต่เครื่องหมาย`""" (triple quote)`สามารถใช้เชื่อมต่อสตริงแบบหลาย ๆ บรรทัดได้ เช่น

```python
word = 'word'  
sentence = "This is a sentence."  
paragraph = """This is a paragraph. It is  made up of multiple lines and  
sentences."""  
print(paragraph)
```

**OUTPUT**

```text
This is a paragraph. It is  made up of multiple lines and sentences.
```

## Waiting for the user

บ่อยครั้งที่ผู้เขียนโปรแกรมต้องการให้โปรแกรมหยุดรอก่อนโปรแกรมทำงานเสร็จ โดยขึ้นข้อความว่า “Press the enter key to exit.” สามารถใช้ `\n\n` ใส่ไว้ก่อนข้อความ ดังนี้

```python
input("\n\nPress the enter key to exit.")
```

## Multiple statements on a single line

ผู้เขียนโปรแกรมสามารถใช้เครื่องหมาย ; เพื่อสั่งให้สามารถรันหลายๆ คำสั่งได้ในบรรทัดเดียวกันได้

```python
import sys; x = 'Python'; sys.stdout.write(x + ' \n')
```

**OUTPUT**

```text
Python  
7
```

> [Source : ](https://).

