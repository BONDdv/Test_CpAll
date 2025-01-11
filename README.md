# ระบบจัดการสินค้า (Product Management System)

โปรเจกต์นี้เป็นระบบจัดการสินค้า โดยใช้ **MySQL** เป็นฐานข้อมูลในการจัดเก็บข้อมูลสินค้า เช่น การเพิ่มสินค้า, แก้ไขสินค้า, และแสดงรายการสินค้า โดยใช้ **Prisma ORM** ในการเชื่อมต่อและจัดการฐานข้อมูล MySQL

### 1. Clone หรือดาวน์โหลดโปรเจกต์

```
git clone https://github.com/username/repository-name.git
cd repository-name 
```
### 2. การติดตั้ง Dependencies

2.1 ติดตั้ง dependencies ของ Frontend:
```
cd frontend
npm install
```

2.2 ติดตั้ง dependencies ของ Backend:
```
cd backend
npm install
```


### 3. การตั้งค่า .env

3.1 ตั้งค่าใน Frontend (frontend/.env):
ตรวจสอบให้แน่ใจว่าไฟล์ .env ในโฟลเดอร์ Frontend มีการตั้งค่าตัวแปร VITE_API_URL ที่เชื่อมต่อกับ Backend อย่างถูกต้อง
```
VITE_API_URL=http://localhost:8001/api
```
3.2 ตั้งค่าใน Backend (backend/.env):
สร้างไฟล์ .env ในโฟลเดอร์ Backend หรือเพิ่มค่าต่อไปนี้หากไฟล์ .env มีอยู่แล้ว เพื่อเชื่อมต่อกับฐานข้อมูล MySQL และใช้ Prisma

```
PORT=8001
DATABASE_URL="mysql://your_mysql_username:your_mysql_password@localhost:3306/your_database_name"
```
**หมายเหตุ**
```
your_mysql_username: ชื่อผู้ใช้งาน MySQL ของคุณ 
your_mysql_password: รหัสผ่านของผู้ใช้งาน MySQL
your_database_name: ชื่อฐานข้อมูลที่คุณสร้างขึ้นใน MySQL
```


### 4. การตั้งค่าฐานข้อมูล MySQL

4.1 การสร้างฐานข้อมูลใน MySQL
ก่อนที่จะรันโปรเจกต์ คุณต้องสร้างฐานข้อมูลใน MySQL ให้ตรงกับชื่อที่ตั้งในไฟล์ .env โดยใช้คำสั่ง SQL ดังนี้:
```
CREATE DATABASE your_database_name;
```
4.2 การติดตั้ง Prisma และการสร้าง Schema
หลังจากสร้างฐานข้อมูลแล้ว ให้ติดตั้ง Prisma CLI และสร้างการเชื่อมต่อไปยังฐานข้อมูล MySQL
```
cd backend
npx prisma migrate dev --name init
```
คำสั่งนี้จะใช้ Prisma เพื่อสร้างตารางในฐานข้อมูลของคุณตามที่กำหนดในไฟล์ schema.prisma ซึ่งจะถูกสร้างขึ้นโดยอัตโนมัติเมื่อคุณติดตั้ง Prisma

### 5. การรันโปรเจกต์

5.1 รัน Backend:
```
cd backend
npm start
```
Backend จะเริ่มต้นที่พอร์ต 8001 และเชื่อมต่อกับ MySQL โดยอัตโนมัติ หากการเชื่อมต่อสำเร็จจะมีข้อความแสดงบนคอนโซลว่าเชื่อมต่อฐานข้อมูลได้

5.2 รัน Frontend:
```
cd frontend
npm run dev
```

Frontend จะเริ่มต้นที่พอร์ต 5173 โดยจะเชื่อมต่อกับ API ที่อยู่ใน Backend (ตามที่ตั้งใน .env)


### 6. การทดสอบ
```
เปิดเว็บบราวเซอร์ไปที่ http://localhost:5173 เพื่อเข้าถึง Frontend
ลองเพิ่ม, แก้ไข, และดูรายการสินค้าผ่าน Frontend
ตรวจสอบข้อมูลที่ถูกเพิ่ม/แก้ไขใน MySQL ผ่านคำสั่ง SQL หรือ MySQL Workbench
```
### โครงสร้างโปรเจกต์
**Backend** (Node.js/Express + Prisma):
```
backend/: โฟลเดอร์ที่เก็บไฟล์ของ Backend
prisma/: โฟลเดอร์ที่เก็บไฟล์ Prisma
schema.prisma: ไฟล์กำหนดโครงสร้างฐานข้อมูลของคุณ
server.js: ไฟล์หลักในการตั้งค่าเซิร์ฟเวอร์ Node.js
db.js: ไฟล์ตั้งค่าการเชื่อมต่อ MySQL ผ่าน Prisma
models/: โฟลเดอร์เก็บโมเดลของ Prisma (ใช้ในการเชื่อมต่อและจัดการข้อมูล MySQL)
```
**Frontend** (React):
```
frontend/: โฟลเดอร์ที่เก็บไฟล์ของ Frontend
src/: โฟลเดอร์เก็บไฟล์ซอร์สโค้ด React
.env: ไฟล์ตั้งค่าที่เก็บตัวแปร VITE_API_URL สำหรับเชื่อมต่อกับ Backend
```