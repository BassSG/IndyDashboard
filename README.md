# IndyDashboard

แดชบอร์ดเปรียบเทียบผลวิจัย EBW × XAUUSD / Eightcap แบบออฟไลน์

> **CONDITIONAL RESEARCH · NOT CERTIFIED**
> อันดับในเว็บเป็นผลของชุดทดลองจำกัด ไม่ใช่คำแนะนำเทรดจริง ไม่รับรองกำไรในอนาคตหรือความแม่นระยะยาว

## เปิดใช้งาน

ดาวน์โหลด `index.html` แล้วเปิดด้วยเว็บเบราว์เซอร์ได้ทันที ไม่ต้องติดตั้งโปรแกรมหรือเปิดเซิร์ฟเวอร์
ข้อมูลและโค้ดฝังไว้ในไฟล์เดียว ไม่เรียก API, CDN, บริการโมเดล และไม่ส่งคำสั่งซื้อขาย

## ความสามารถ

- คลิกหัวคอลัมน์เพื่อเรียง กดซ้ำกลับทิศ: 29 คอลัมน์ leaderboard และ 17 คอลัมน์ audit
- กรอง TF, Action, TP Fibo, Full / Train / Validation / Holdout, สถานะ, จำนวนไม้ขั้นต่ำ และข้อความ
- การ์ดอันดับเปลี่ยนตามตัวกรอง ไม่จัดอันดับปนเมื่อเลือกทุกช่วง และไม่รวมไม้ซ้ำข้าม configs
- คลิกชุดตั้งค่าเพื่อดู conditional simulation rules และผลแยกทั้งสี่ช่วง
- CSV ดาวน์โหลดเก็บความละเอียดเดิม; audit sample รวม 35 fields ของ 13 ไม้
- N/A อยู่ท้ายทั้งสองทิศทาง ไม่ตีความแถวไม่มีไม้ปิดหรือ BLOCKED เป็นกำไรศูนย์
- แสดงหน่วย Fibo ถูกต้อง เช่น ratio 3.618 = 361.8%
- แยก legacy signal-window boundary ออกจาก nominal close ของข้อมูลแท่งปิด
- รองรับหน้าจอแคบ และโหมดสีตามการตั้งค่าของระบบ

## ข้อมูลและขอบเขต

- 1,794 scored rows / 22 finite profiles / 6 TF
- Snapshot API: 8 ตุลาคม พ.ศ. 2569 เวลา 06.48 น. (Asia/Bangkok)
- ค่าเริ่มต้น: Full, ผลวิจัยที่ยังไม่รับรอง, ≥10 ไม้, กำไรสุทธิมากไปน้อย; 257 แถว
- จำนวน ≥10 ไม้เป็นตัวกรอง ไม่ใช่การทดสอบนัยสำคัญทางสถิติ
- เงินเป็น $ ต่อทอง 1 oz ในงานวิจัย ไม่ใช่ผลตอบแทนพอร์ต %
- DD เป็น bar-close mark-to-market ไม่ใช่ tick-level maximum
- ต้นทุนคงที่ $0.16/oz ต่อไม้เป็นสมมติฐาน ไม่ใช่ spread/bid-ask ย้อนหลังที่ยืนยันแล้ว
- ไม่มี matched TradingView reference, native Action-to-Fibo plan-ID binding, mintick และ Bridge/history ครบ
- Net Profit % / Max DD % ของพอร์ตเป็น N/A เพราะไม่มีทุนและ position sizing
- ไม่รวม raw bars, Pine attachments, ไฟล์ backtest ขนาดใหญ่ หรือการตั้งค่าของเครื่องใน repo นี้

## ผลตรวจ

Automated dashboard tests: 79 ผ่าน ครอบคลุมการเรียงทั้งสองทิศทาง ตัวกรอง หน่วย วันที่ และข้อมูล
ทดสอบ Browser interaction จริง: Win Rate toggle, filters, Holdout cards, N/A, detail dialog และ audit numeric sort
การเผยแพร่เว็บนี้ไม่ได้รัน backtest ใหม่หรือเปลี่ยน P&L เดิม

Dataset SHA256: `e5d911f28bfda3439c8430e2d397c7ad1b343df9d891c681306467f70718651c`

Scored-row JSON SHA256: `5f83dd5d1151f0050447040f50848fc02895fcb96ac32afc221e7e6775992ce8`


## คู่มือวิธีเล่น v2

[เปิดแดชบอร์ดออนไลน์](https://basssg.github.io/IndyDashboard/)

- Popup เริ่มจากคู่มือ A1–A5: เลือกกราฟ/ฝั่ง, ซื้อเมื่อไร, ขายเมื่อไร, เข้าอย่างไร, SL/TP อยู่ตรงไหน
- A4 ใช้ไส้ของแท่งที่ปิดแล้วทะลุ B ตามบริบท TF คุม พร้อมภาพ B/C แบบสเก็ตช์ ไม่ใช่กราฟราคาจริง
- ใช้ชื่อวิธีเล่นที่อ่านง่ายแทน config เป็นข้อความหลัก; รายละเอียด source อยู่ส่วนพับด้านล่าง
- เพิ่ม 611 ตัวอย่างจาก 314 configs ที่มีไม้ปิด: เลือกไม้ชนะ/แพ้แรกจาก Full ไม่ใช่เลือกไม้กำไรสูงสุด
- ตัวอย่างราคาเป็นข้อมูลย้อนหลัง ไม่ใช่ราคาเข้าในปัจจุบัน ไม่ใช่ไม้ของ split ที่เลือก และไม่ใช่ broker fills/tick ที่ยืนยันแล้ว
- สถิติ Full/Train/Validation/Holdout พับไว้หลังคู่มือและตัวอย่าง; ไม้ขั้นต่ำไม่ใช่การยืนยันนัยสำคัญ
- A2 Link ใช้ divergence-pair containment; A3–A5 ใช้ Link codes/parent phase ตาม source ไม่ผสมเป็นกฎเดียว

ตรวจ automated tests 98 ข้อ (79 เดิม +19 คู่มือ) ผ่าน และผู้ตรวจอิสระเทียบตัวอย่างทั้ง611กับ corrected ledger ตรงกันทุก fields ที่ใช้
ไม่รัน backtest ใหม่ ไม่เปลี่ยนคะแนน/P&L และยัง **NOT CERTIFIED** เช่นเดิม
