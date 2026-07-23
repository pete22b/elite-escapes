# Elite Escapes Website

Multi-page static website for **Elite Escapes Co., Ltd.** — a private members vacation club in Patong, Phuket (part of PSN/Pisona Group properties). Target domain: **www.elite-escapes.club**.

Content source of truth: `Update_2026_-Club_Unique_Website_01_07_2026.xlsx` (client spec — sitemap, page copy, footer/contact info). All page copy in the HTML files was extracted from that spec; do not rewrite the client's copy unless asked.

## Structure

Plain HTML + one shared CSS file. No build step, no framework. Deploy target: GitHub Pages (later pointed to elite-escapes.club via CNAME).

- `index.html` — HOME: hero + "Plan My Escape" search card, stat cards, category tiles, lifestyle cards (beach clubs / nightlife / culture), member quotes, CTA band
- `about.html` — story, management, core values (Quality / Flexibility / Service)
- `member-services.html` — team intro (9 languages) + enquiry form
- `home-resort.html` — Patong Bay Hill Resort: amenities (#amenities), One-Bedroom Suite (#suite)
- `interval.html` — Interval International partner page
- `benefits.html` — 4 benefit cards with anchors: #b-interval, #b-discount, #b-referral, #b-lounge
- `join.html` — **Membership Enquiry** (prospective members): Q&A (FAQ) + enquiry form (First/Last/Email/Phone/"What interests you?"/Message, NO dates). "Our team will contact you to arrange a personal presentation." Submit = alert() placeholder.
- `booking.html` — **Book Your Stay** (existing members): concierge booking form (Member Name/Membership No./Email/Check-in/Check-out/Guests/Special Requests). "Send to Concierge" button opens a `mailto:memberservice@elite-escapes.club` prefilled with the request. Linked from every footer Site Map as "Book a Stay". Two forms are intentionally separate: join = sign-up interest (sales talks first), booking = members reserve stays.
- `style.css` — shared design system (all visual tokens in `:root`)
- `img/` — two beach photos extracted from the client's xlsx

## Design system (current: v4)

- Layout language modeled on plus.co.th (corporate, clean): white sticky nav, rounded 16px cards, soft shadows, pill buttons, floating search card over hero, stat cards overlapping hero bottom.
- Nav modeled on the Patong Bay Hill hotel site: uppercase letter-spaced menu, CSS hover dropdowns (Home Resort ▾, Club Benefits ▾), orange pill "Book Now" button right.
- Tokens in `:root`: `--brand:#16405A` (navy), `--cta:#F08033` (PBH orange, Book Now + accents), `--accent:#C9A45C` (gold, sparing), bg `#F6F7F9`.
- Fonts: Marcellus (display) + Nunito Sans (body), Google Fonts.
- `.reveal` fade-in via IntersectionObserver (index only); reduced-motion respected.

## Images

**All images are now hosted locally in `img/` (53 files) — no more remote hotlinks (done 05 Jul 2026, TODO #3).** Downloaded from PBH CDN / Paradise / KUDO / PBR / Illuzion / Unsplash; all `background-image:url(...)` now point to `img/...`. Naming: `pbh-*`, `paradise-*`, `kudo-*`, `pbr-*`, `illuzion-*`, and `unsplash-<photoid>.jpg` (reused Unsplash photos share one file).

Still open (content, not hosting): **replace stock/placeholder shots (~23 spots: Culture cards, Welcome family/couple slides, Hollywood, benefits tiles) with real hotel photography** when the marketing team provides them — just swap the file in `img/`, filenames can stay.

## Known TODO (from chat with Pete)

1. Replace stock photos with real hotel photography.
2. Wire the two forms (member-services enquiry, join booking) to a real backend (Formspree/EmailJS or company mail) — currently `alert()` placeholders.
3. Member testimonials on index are **fabricated placeholders** (marked in-page) — must be replaced with real reviews before launch.
4. Q&A content on join.html is placeholder — awaiting real FAQ from the team.
5. Client theme color was "On Process" in the spec — current palette is a proposal; confirm with the team.
6. Deploy: git init → GitHub (private repo ok for source, Pages needs public on free plan) → Settings → Pages → branch main → add CNAME for elite-escapes.club.

## Contact block (footer, all pages — from client spec)

Elite Escapes Co., Ltd. · 79/6 Hasib Pee Road, Patong, Kathu, Phuket 83150 · Tel +66 76 683 083 · memberservice@elite-escapes.club · IG @eliteescapes.official · Map: 7.877686, 98.298915

## Conventions

- Keep all pages' nav/footer identical — when editing one, propagate to all 7 files.
- English site copy; talk to Pete in Thai, concise, direct.
- Prefer editing `style.css` tokens over per-page inline styles.
- **CSS cache-busting:** all pages link `style.css?v=N`. Browsers here cache `style.css` hard (CSS edits don't show even on hard-refresh while HTML edits do). **After ANY `style.css` change, bump `N` in the `<link>` of all 7 files** (currently `v=4`) — this is what reliably forces the new CSS to load.
- **Logo assets** (all transparent PNG, from client's `img/LOGO.png`): `logo-full.png` = full logo, navy text (nav, light bg, 56px) · `logo-palm.png` = gold palm only · `logo-light.png` = full logo w/ cream text (footer + home hero, dark bg). Nav = single `logo-full.png` image; footer + home hero = `logo-light.png`.


---

## Session update (05 Jul 2026) — สถานะล่าสุดก่อนย้ายเข้า Codex

### สิ่งที่เปลี่ยนจากด้านบน (ยึดตามนี้)
- **เมนู: ปุ่ม Book Now ถูกถอดออกแล้วทุกหน้า** (Pete สั่ง) — ทางเข้าจอง = search card หน้า Home, ลิงก์ Join the Club ใน footer, ปุ่ม WhatsApp ลอย
- **ปุ่มติดต่อลอยทุกหน้า** `.float-contact`: WhatsApp (wa.me/6676683080) + โทร — ⚠️ ยังไม่ยืนยันว่าเบอร์นี้เปิด WhatsApp Business แล้ว
- **โทนภาพทั้งเว็บ (สำคัญ — ห้ามแก้ทิ้ง):** เกรดเป็น "ฟิล์มนุ่มฟุ้ง พาสเทล คอนทราสต์ต่ำ อุ่นจางๆ" ตามที่ Pete เลือกจาก hero หน้า benefits
  - `.bg,.slide,.panel{filter:saturate(.8) contrast(.9) brightness(1.06) sepia(.16)}`
  - `.hero::before` = ม่านครีมฟุ้งบน + กรมท่าอ่อนล่าง (ดู style.css ส่วน SALES POLISH)
- **สไลด์โชว์ = 6 วิ/ภาพ** (slidefade 18s / slidefade5 30s) — Pete ต้องการช้าเพื่อให้เซลส์ชี้อธิบายทัน ห้ามเร่งกลับ
- **Booking form (join.html) เวอร์ชันกระชับ**: grid 2 คอลัมน์, Membership No. ซ่อนหลัง checkbox, date min=วันนี้ + checkout≥checkin (JS ท้าย body), ปุ่ม WhatsApp ข้างปุ่มส่ง
- **member-services.html มี section ใหม่ #privileges**: การ์ด 6 ใบ (Baytara Spa / SITA / Full-Board / In-Suite Kitchen / Private Members Lounge / In-Room Dining) ภาพจริงจากเว็บ PBH
- **หน้า About**: hero ภาพเดียว (main-slide-3) — แถบ showcase 3 การ์ดถูกลบแล้ว (Pete ไม่ชอบ) อย่าเพิ่มกลับ
- **meta description ครบทั้ง 7 หน้าแล้ว**
- `img/pbh-rooftop-pool.jpg` = ภาพตัดจากแคป IG @patongbayhill (718px) ใช้เป็นสไลด์แรก "The Resort" หน้า home-resort — รอไฟล์ต้นฉบับคมกว่าจากทีมการตลาดมาแทน

### กติกาเลือกภาพ (บทเรียนจริง)
- CDN PBH: `https://cdn-65d07681c1ac18be64b9e983.closte.com/wp-content/uploads`
- ❌ `PBH-Welcome-Lounge-1200x800.jpg` = โซฟาลายสับปะรด **ห้ามใช้เด็ดขาด** / ✅ `PBH-Welcome-Lounge-1-1200x800.jpg` = ตัวหรูมีแชนเดอเลียร์
- การเลือกภาพจากชื่อไฟล์โดยไม่เห็นภาพเคยพลาดมาแล้ว 2 ครั้ง — ถ้าไม่แน่ใจให้ Pete แคปยืนยันก่อน
- ภาพสต็อกที่เหลือ (~23 จุด: การ์ด Culture, Welcome สไลด์ครอบครัว/คู่รัก, Hollywood, tiles หน้า benefits) = ตั้งใจใช้ชั่วคราว รอภาพจริงจากทีม

### TODO ก่อน Go-Live (เรียงความสำคัญ)
1. ต่อฟอร์มเข้า Formspree/อีเมลจริง:
   - ✅ **booking.html** — Formspree `xvzjyenp` (AJAX, name: member_name/membership_number/email/checkin/checkout/guests/special_requests, `_subject`="Booking Request - Elite Escapes")
   - ✅ **join.html** — Formspree `xvzjyenp` (AJAX, name: first_name/last_name/email/phone/interest/message, `_subject`="Membership Enquiry - Elite Escapes")
   - ⚠️ ทั้งคู่ใช้ **endpoint เดียวกันชั่วคราวสำหรับเทส** (`xvzjyenp`) — แยกด้วย `_subject` · production ควรแยก endpoint (booking → memberservice@ / join → sales) · ครั้งแรกที่ส่ง Formspree ส่งเมลยืนยัน endpoint ให้กดก่อน
   - ✅ **member-services.html** — ฟอร์ม Enquiry เดิมถูกแทนด้วย **ฟอร์ม Booking** (เหมือน booking.html: "Book Your Stay" / Send to Concierge / member_name..special_requests / `_subject`="Booking Request - Elite Escapes"). ส่วนทีม 9 ภาษา + Member Privileges 6 การ์ด คงไว้ (Pete สั่ง 07 Jul — member-services = จองสำหรับสมาชิก ไม่ใช่ enquiry)
   - **ฟอร์มที่ต่อแล้ว:** booking.html + member-services.html (ทั้งคู่ = Booking Request) · join.html (Membership Enquiry, **ห้ามแตะ/เปลี่ยนเป็น booking เด็ดขาด — Pete กำชับ**) · ทุกตัว AJAX + thank-you ในหน้า + WhatsApp
   - เหลือ (ก) ยืนยัน endpoint ครั้งแรกทางอีเมล (ข) แยก endpoint ตอน production (booking/member-services → memberservice@ / join → sales)
2. ยืนยันเบอร์ 076 683 080 เปิด WhatsApp Business
3. ~~ดาวน์โหลดภาพ hotlink ทั้งหมด (PBH CDN / Paradise / KUDO / PBR / Illuzion / Unsplash) มาไว้ img/ แล้วแก้ URL~~ ✅ **เสร็จ 05 Jul 2026** — ภาพทั้งหมด local ใน img/ (53 ไฟล์) ไม่เหลือ hotlink ภายนอก (ยกเว้น href เว็บโรงแรม/Google Fonts/Maps ที่ตั้งใจเก็บ)
4. รีวิวสมาชิก 3 อันหน้า index = ตัวอย่างแต่ง ต้องแทนของจริงที่ได้ความยินยอม
5. รายละเอียด Full-Board package จากทีม F&B → อัปเดตการ์ดใน #privileges
6. Deploy GitHub Pages — ✅ **push แล้ว** repo `github.com/pete22b/elite-escapes` (branch main, ผ่าน Git for Windows ที่ `C:\Program Files\Git\cmd\git.exe`; `.gitignore` กัน xlsx/AGENTS.md/.Codex ไม่ให้ขึ้น repo สาธารณะ) · ⏳ เหลือ: Pete เปิด **Settings → Pages** (branch main) + ตั้ง CNAME elite-escapes.club + บังคับ HTTPS
7. เดโม่ all-in-one (ไฟล์เดียว hash router) เป็นของนอกโปรเจกต์นี้ — แก้อะไรในโปรเจกต์ไม่ต้อง sync ไปหามัน
8. **โลโก้ footer + hero(Home) = `img/logo-light.png`** (โลโก้เต็ม ตัวอักษร**ครีม** พื้นโปร่ง) — ✅ ไฟล์มีจริง (73 KB) · ⚠️ ต้องเช็กด้วยตาว่าตัวอักษรครีมอ่านชัด/คมพอบนพื้น footer เข้ม (`--brand-2` #0F2B3D) ไหม — ถ้าจางหรือไม่คม ให้ทำเวอร์ชันตัวอักษร**ขาวล้วน**แยกสำหรับ footer (nav ใช้ `logo-full.png` ตัวอักษรกรมท่า พื้นขาว — คนละไฟล์ ไม่เกี่ยว)
