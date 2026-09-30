# SEAS
School Equipment Accounting System
# คู่มือการติดตั้งและใช้งาน: ระบบบัญชีครุภัณฑ์โรงเรียน v2.0

ระบบเว็บแอปพลิเคชันบริหารจัดการและทะเบียนควบคุมครุภัณฑ์โรงเรียน  
**Tech Stack:** Google Apps Script + HTML/Tailwind CSS + Google Sheets  
**ฟรีทั้งหมด** — ไม่มีค่าโฮสติ้ง ไม่ต้องเช่า Server

---

## 🚀 ขั้นตอนการติดตั้ง (Deploy) ทีละขั้น

### ขั้นที่ 1: สร้าง Google Sheets
1. ไปที่ [Google Drive](https://drive.google.com) → คลิก **ใหม่** → **Google ชีต**
2. ตั้งชื่อ เช่น `ระบบบัญชีครุภัณฑ์โรงเรียน`
3. คัดลอก **Spreadsheet ID** จาก URL:
   ```
   https://docs.google.com/spreadsheets/d/[คัดลอกส่วนนี้]/edit
   ```

### ขั้นที่ 2: เปิด Apps Script Editor
1. ใน Google Sheets → เมนู **ส่วนขยาย (Extensions)** → **Apps Script**
2. ตั้งชื่อโครงการ: `ระบบบัญชีครุภัณฑ์โรงเรียน`

### ขั้นที่ 3: วางโค้ด Code.gs
1. ลบโค้ดเดิมใน `Code.gs` ออกทั้งหมด
2. คัดลอกเนื้อหาจากไฟล์ `Code.gs` แล้ววาง
3. **⚠️ สำคัญมาก:** แทนค่า `'YOUR_SPREADSHEET_ID_HERE'` บรรทัดที่ 20 ด้วย ID ที่คัดลอกไว้:
   ```js
   const SPREADSHEET_ID = '1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms'; // ตัวอย่าง
   ```

### ขั้นที่ 4: สร้างไฟล์ Index.html
1. คลิกปุ่ม **+** ด้านซ้าย → เลือก **HTML**
2. ตั้งชื่อ `Index` (ไม่ต้องพิมพ์ .html)
3. ลบโค้ดเดิม แล้วคัดลอกเนื้อหาจากไฟล์ `Index.html` วางแทน

### ขั้นที่ 5: Deploy เป็น Web App
1. คลิก **Deploy** (มุมขวาบน) → **New deployment**
2. คลิกรูปเฟือง ⚙️ → เลือก **Web app**
3. ตั้งค่า:
   - **Execute as:** `Me` (บัญชีของคุณ)
   - **Who has access:** `Anyone` (ทุกคนใน Internet) หรือ `Anyone with Google Account`
4. คลิก **Deploy** → อนุมัติสิทธิ์ → คัดลอก **Web App URL**

> **หมายเหตุ:** ทุกครั้งที่แก้ไขโค้ด ต้อง Deploy ใหม่ (New deployment) หรือ Update deployment เพื่อให้การเปลี่ยนแปลงมีผล

---

## 🔑 บัญชีผู้ใช้เริ่มต้น (Default Accounts)

| บทบาท | Username | Password | สิทธิ์ |
|:---|:---|:---|:---|
| **Admin** | `admin` | `admin123` | เพิ่ม/แก้ไข/ลบ/รายงาน |
| **Teacher** | `teacher` | `123456` | เพิ่ม/แก้ไข/ดูรายงาน |

> บัญชีเหล่านี้ถูกสร้างอัตโนมัติใน Sheet `Users` เมื่อรันครั้งแรก  
> **แนะนำ:** เปลี่ยนรหัสผ่านใน Sheet `Users` ทันทีก่อนใช้งานจริง

---

## 🌟 ฟีเจอร์ทั้งหมด

| ฟีเจอร์ | รายละเอียด |
|:---|:---|
| 📊 **Dashboard** | สรุปสถิติ, มูลค่ารวม, จำนวนตามสถานะและหมวดหมู่ |
| 📋 **ทะเบียนครุภัณฑ์** | เพิ่ม/แก้ไข/ลบ รหัส, ชื่อ, ยี่ห้อ, S/N, ราคา, สถานที่, ผู้รับผิดชอบ |
| 🔍 **ค้นหา & กรอง** | ค้นหาแบบ Real-time ตามรหัส, ชื่อ, ยี่ห้อ, สถานที่, ผู้รับผิดชอบ |
| 🏷️ **QR Code** | สร้าง QR อัตโนมัติ, พิมพ์สติ๊กเกอร์เฉพาะ QR (ไม่พิมพ์ทั้งหน้า) |
| 📷 **สแกน QR** | สแกนด้วยกล้อง เพื่อค้นหาหรือลงทะเบียนใหม่ |
| 🛠️ **ชำรุด/แทงจำหน่าย** | อัปเดตสถานะพร้อมบันทึกอาการชำรุด |
| 🗑️ **ลบรายการ** | Admin เท่านั้น (มี confirmation dialog) |
| 📝 **Activity Logs** | บันทึกการเข้าสู่ระบบและการแก้ไขข้อมูลทุกรายการ |
| 🖨️ **พิมพ์ทะเบียน** | พิมพ์ตารางรายการครุภัณฑ์ (숨기ง header/button อัตโนมัติ) |
| 🔒 **Login / Logout** | Session บน localStorage, ปุ่ม logout พร้อม confirm |

---

## 🗄️ โครงสร้าง Google Sheets (Auto-created)

| Sheet | คอลัมน์หลัก |
|:---|:---|
| **Assets** | AssetID, Code, Name, Category, BrandModel, SerialNumber, Price, AcquisitionDate, BudgetSource, Location, Custodian, Status, ConditionNote, ImageURL, QRCodeURL, CreatedAt, UpdatedAt |
| **Users** | UserID, Username, PasswordHash, FullName, Role, Department, Status, CreatedAt |
| **Logs** | LogID, Timestamp, Username, Action, TargetAssetCode, Details |

---

## ⚠️ ข้อควรระวัง / สำหรับการใช้งานจริง

1. **รหัสผ่าน:** ระบบนี้เก็บรหัสผ่านเป็น plain text ใน Google Sheets — ควรเปลี่ยนรหัสผ่านและจำกัดการเข้าถึง Sheets
2. **สิทธิ์ Sheets:** แนะนำให้ Sheets เป็น Private (Share เฉพาะบัญชีที่จำเป็น)
3. **Quota:** Google Apps Script มี quota: script รันได้ 6 ชั่วโมง/วัน, เขียน Sheets ได้ ~2,000 ครั้ง/วัน — เพียงพอสำหรับโรงเรียน
4. **แก้ไขโค้ดแล้วไม่เห็นผล:** ต้อง **Deploy → Manage deployments → Update** ทุกครั้ง

---

## 🛠️ การจัดการปัญหาที่พบบ่อย

| ปัญหา | วิธีแก้ |
|:---|:---|
| เข้าระบบแล้วขึ้น error | ตรวจสอบ SPREADSHEET_ID ใน Code.gs |
| Sheet ไม่ถูกสร้างอัตโนมัติ | รันฟังก์ชัน `resetInitFlag()` ใน Script Editor แล้ว Deploy ใหม่ |
| สแกน QR ไม่ได้ | ตรวจสอบสิทธิ์กล้องในเบราว์เซอร์ (HTTPS เท่านั้น) |
| ข้อมูลไม่อัปเดต | กด Ctrl+Shift+R เพื่อ Hard Refresh |
