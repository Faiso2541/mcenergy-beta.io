# McEnergy — Service & Maintenance Report

แบบฟอร์มรายงานตรวจสอบและบำรุงรักษาอุปกรณ์ (เว็บล้วน ไม่ต้องมีเซิร์ฟเวอร์ ไม่ต้องมีฐานข้อมูล)
ข้อมูลทั้งหมดอยู่ในเครื่องของผู้ใช้เท่านั้น

## ไฟล์ในโฟลเดอร์นี้

| ไฟล์ | หน้าที่ |
|---|---|
| `index.html` | ตัวฟอร์มทั้งหมด (HTML + CSS + JS ในไฟล์เดียว) |
| `manifest.webmanifest` | ข้อมูลแอปสำหรับติดตั้งลงหน้าจอโฮม |
| `sw.js` | Service worker — ทำให้เปิดใช้งานได้แม้ไม่มีเน็ต |
| `icon-*.png`, `apple-touch-icon.png` | ไอคอนแอป |
| `.nojekyll` | บอก GitHub Pages ไม่ต้องประมวลผลไฟล์ซ้ำ |

## วิธีนำขึ้น GitHub Pages

### แบบไม่ต้องใช้คำสั่ง (แนะนำ)

1. เข้า https://github.com/new สร้าง repository เช่นชื่อ `mcenergy-report`
   เลือก **Public** แล้วกด **Create repository**
2. ในหน้า repo กด **Add file → Upload files**
   แล้วลาก **ไฟล์ทั้งหมดในโฟลเดอร์ `web` นี้** (ไม่ใช่ตัวโฟลเดอร์) ลงไป
   *ไฟล์ `.nojekyll` ขึ้นต้นด้วยจุด ถ้า Windows ซ่อนไว้ ให้เปิด View → Hidden items*
3. กด **Commit changes**
4. ไปที่ **Settings → Pages**
   - Source: **Deploy from a branch**
   - Branch: **main** / โฟลเดอร์ **/ (root)** → **Save**
5. รอ 1–2 นาที จะได้ลิงก์
   `https://<ชื่อบัญชี>.github.io/mcenergy-report/`

### แบบใช้ Git

```bash
cd web
git init
git add .
git commit -m "McEnergy service & maintenance report"
git branch -M main
git remote add origin https://github.com/<ชื่อบัญชี>/mcenergy-report.git
git push -u origin main
```
แล้วเปิด Settings → Pages ตามข้อ 4 ด้านบน

## เวลาแก้ไขฟอร์มแล้วอัปโหลดใหม่

เปิด `sw.js` แก้บรรทัด

```js
var CACHE_VERSION = 'mce-report-v1';
```

เป็น `v2`, `v3` ... ทุกครั้งที่แก้ `index.html`
ถ้าไม่แก้เลข เครื่องที่เคยเปิดไว้จะยังเห็นฟอร์มเวอร์ชันเก่าจากแคช

## การใช้งานบนมือถือ

- **Android / Chrome** — เปิดลิงก์ จะมีปุ่ม "ติดตั้งแอป" สีเขียวขึ้นบนแถบด้านบน
- **iPhone / iPad** — เปิดด้วย **Safari** แล้วใช้ปุ่ม **แชร์ → Print** เพื่อบันทึกหรือส่ง PDF
  (อย่าเพิ่มลง Home Screen เพราะ iOS จะซ่อนแถบแชร์ ทำให้สั่งพิมพ์ไม่ได้)

## ข้อควรทราบ

- ฟอร์มเก็บฉบับร่างไว้ใน localStorage ของเบราว์เซอร์เครื่องนั้น **ไม่ได้ส่งขึ้นเซิร์ฟเวอร์**
  ถ้าเปลี่ยนเครื่องหรือล้างข้อมูลเบราว์เซอร์ ข้อมูลจะหาย
- ใช้ปุ่ม **"บันทึกสถานะล่าสุด"** (สีเขียว) เป็นจุดกู้คืนกันเผลอกดล้างฟอร์ม
- ใช้ปุ่ม **"เก็บงานไว้ทำต่อ"** เพื่อบันทึกเป็นไฟล์ `.json` ไว้ย้ายเครื่องหรือสำรองจริงจัง
- repository เป็น Public หมายถึงใครก็เปิดฟอร์มเปล่าได้ แต่ **ไม่มีใครเห็นข้อมูลที่กรอก**
  เพราะข้อมูลไม่เคยออกจากเครื่องผู้กรอก

---
McEnergy Evolution Co., Ltd.
