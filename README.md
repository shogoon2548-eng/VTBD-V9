# VTBD Tower – ตั้งค่าเล่นออนไลน์ (GitHub Pages + Firebase)

ไฟล์ในโฟลเดอร์นี้
- `index.html` — ตัวเกม (ไม่ต้องแก้)
- `firebase-config.js` — **ไฟล์เดียวที่ต้องแก้** ใส่ค่า Firebase ของคุณ
- `database.rules.json` — กฎของ Realtime Database (วางใน Firebase Console)

## 1) สร้าง Firebase
1. เข้า https://console.firebase.google.com → **Add project** (ปิด Google Analytics ได้)
2. เมนู **Build → Realtime Database → Create Database**
   - Location: **Singapore (asia-southeast1)** (ใกล้ไทยที่สุด)
   - เลือก **Start in locked mode**
3. แท็บ **Rules** → ลบของเดิม → วางเนื้อหาจาก `database.rules.json` → **Publish**
4. ไอคอนเฟือง **Project settings → General → Your apps → Web (</>)** → ตั้งชื่อ → Register
   แล้วคัดลอก `firebaseConfig` มาใส่ใน `firebase-config.js`
   - `databaseURL` ดูได้ที่หน้า Realtime Database (ด้านบนของตารางข้อมูล)

## 2) ขึ้น GitHub Pages
1. สร้าง repository ใหม่บน GitHub (Public)
2. อัปโหลดไฟล์ `index.html`, `firebase-config.js` (ที่แก้แล้ว), `database.rules.json`, `README.md` ไว้ที่ราก (root)
3. **Settings → Pages → Build and deployment** → Source: *Deploy from a branch* → Branch: `main` / `(root)` → Save
4. รอ 1-2 นาที จะได้ลิงก์ `https://<ชื่อผู้ใช้>.github.io/<ชื่อ repo>/`

## 3) ทดสอบ
เปิดลิงก์บน 2 เครื่อง เลือกตำแหน่งต่างกัน แก้ไขสตริปหรือกด Reset Strip อีกเครื่องต้องเปลี่ยนตามทันที
ป้ายมุมจอจะขึ้น **● LIVE · ออนไลน์ N** ถ้าไม่ออนไลน์ให้เปิด DevTools → Console ดูข้อความ `[VTBD]`

## ข้อควรรู้
- `apiKey` ของ Firebase เป็นค่าสาธารณะโดยออกแบบ ความปลอดภัยอยู่ที่ Rules
- Rules ชุดนี้เปิดให้ทุกคนที่มีลิงก์อ่าน/เขียนได้ (เหมาะกับเล่นกันเป็นกลุ่ม) อย่าแชร์ลิงก์สาธารณะ
  ถ้าต้องการจำกัดเพิ่ม: Google Cloud Console → APIs & Services → Credentials → จำกัด API key ให้ใช้ได้เฉพาะ `https://<ชื่อผู้ใช้>.github.io/*`
- ล้างข้อมูลทั้งหมด: Firebase Console → Realtime Database → เลือกโหนด `strips` → ลบ
  (ครั้งถัดไปที่เปิดเกมจะสร้างสตริปเริ่มต้นให้ใหม่)
- ข้อมูลออนไลน์เก็บในโหนด `strips`, `metar`, `meta`, `presence` เท่านั้น
