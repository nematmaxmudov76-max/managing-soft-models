# FOYDALANISHLARNI BOSHQARISH (FOB1506)
## 1-Mavzu: Foydalanishni nazorat qilish asoslari — Xavfsizlik siyosati, Reference Monitor va Ishonchli hisoblash bazasi (TCB)
### 1-Amaliyot: Foydalanish matritsasini qurish va Reference Monitor tamoyilini amaliy tahlil qilish
### Amaliy Keys: 1-Variant — «Elektron Kutubxona Axborot Tizimi»

---

## MUNDARIJA
1. [Mavzuning Maqsadi va Fundamental Ahamiyati](#1-mavzuning-maqsadi-va-fundamental-ahamiyati)
2. [Infratuzilma va Tarmoq Arxitekturasi (Ubuntu Host + VMware + Ubuntu Server + Lokal Wi-Fi)](#2-infratuzilma-va-tarmoq-arxitekturasi)
3. [1-Ma’ruza (.pptx) va Nazariy Tushunchalar (.docx) Bo‘yicha Mukammal Qo‘llanma](#3-1-maruza-va-nazariy-tushunchalar-boyicha-mukammal-qollanma)
   - [3.1. Markaziy Muammo va Kirish (Anderson hisoboti, 1972)](#31-markaziy-muammo-va-kirish-anderson-hisoboti-1972)
   - [3.2. I Bo‘lim: Boshlang‘ich Triada — Subyekt, Obyekt, Operatsiya](#32-i-bolim-boshlangich-triada--subyekt-obyekt-operatsiya)
   - [3.3. II Bo‘lim: Reference Monitor va Ishonchli Hisoblash Bazasi (TCB)](#33-ii-bolim-reference-monitor-va-ishonchli-hisoblash-bazasi-tcb)
   - [3.4. III Bo‘lim: Uch Qatlamli Zanjir — Siyosat, Model, Mexanizm](#34-iii-bolim-uch-qatlamli-zanjir--siyosat-model-mexanizm)
   - [3.5. Foydalanish Matritsasi (ACM), ACL va C-List Nazariyasi (Lampson, 1971)](#35-foydalanish-matritsasi-acm-acl-va-c-list-nazariyasi-lampson-1971)
   - [3.6. Xavfsiz Loyihalash Tamoyillari (Least Privilege, SoD, Default Deny)](#36-xavfsiz-loyihalash-tamoyillari)
4. [Tanlangan Topshiriq: 1-Variant «Elektron Kutubxona» Tahlili va Loyihalash](#4-tanlangan-topshiriq-1-variant-elektron-kutubxona-tahlili-va-loyihalash)
   - [4.1. Tashkilot, Subyektlar va Obyektlar Tavsifi](#41-tashkilot-subyektlar-va-obyektlar-tavsifi)
   - [4.2. 4 × 5 Foydalanish Matritsasi ($M[s, o]$)](#42-4--5-foydalanish-matritsasi-m-s-o)
   - [4.3. Olingan ACL va C-List Tuzilmalari](#43-olingan-acl-va-c-list-tuzilmalari)
   - [4.4. Eng Kam Imtiyoz (Least Privilege) Tahlili (3 ta katak bo‘yicha)](#44-eng-kam-imtiyoz-least-privilege-tahlili-3-ta-katak-boyicha)
   - [4.5. Qo‘shimcha Shartlarning Chuqur Arxitektura Tahlili](#45-qoshimcha-shartlarning-chuqur-arxitektura-tahlili)
5. [Amaliy Mashg‘ulot: Ubuntu Serverda Qadamma-Qadam Bajarish Qo‘llanmasi](#5-amaliy-mashgulot-ubuntu-serverda-qadamma-qadam-bajarish-qollanmasi)
   - [5.1. Tizimni Tayyorlash va POSIX ACL O‘rnatish](#51-tizimni-tayyorlash-va-posix-acl-ornatish)
   - [5.2. «Elektron Kutubxona» Uchun To‘liq Bash Skriptlari To‘plami](#52-elektron-kutubxona-uchun-toliq-bash-skriptlari-toplami)
   - [5.3. Har Bir CLI Buyruqning Mukammal Tahlili](#53-har-bir-cli-buyruqning-mukammal-tahlili)
   - [5.4. 3 Ta Amaliy Tajribani Ubuntu Serverda O‘tkazish](#54-3-ta-amaliy-tajribani-ubuntu-serverda-otkazish)
   - [5.5. Windows (DOCX) va Linux (Ubuntu) Konseptual Qiyosiy Tahlili](#55-windows-docx-va-linux-ubuntu-konseptual-qiyosiy-tahlili)
6. [Murojaat Monitori Shartlari Buzilishi Bo‘yicha Keys-Tahlil (6-bo‘limdagi 5 ta holat)](#6-murojaat-monitori-shartlari-buzilishi-boyicha-keys-tahlil-6-bolimdagi-5-ta-holat)
7. [Boshqa Mustaqil Topshiriq Variantlari Qisqacha Yechimlari (2–5 Variantlar)](#7-boshqa-mustaqil-topshiriq-variantlari-qisqacha-yechimlari-25-variantlar)
8. [Nazorat Savollari va Ilmiy-Amaliy Javoblar (10 ta savol + 7 ta test)](#8-nazorat-savollari-va-ilmiy-amaliy-javoblar-10-ta-savol--7-ta-test)
9. [Yakuniy Xulosalar, Hisobotni Rasmiylashtirish va Baholash Mezonlari](#9-yakuniy-xulosalar-hisobotni-rasmiylashtirish-va-baholash-mezonlari)
10. [Tavsiya Etilgan Ilmiy va Texnik Manbalar](#10-tavsiya-etilgan-ilmiy-va-texnik-manbalar)

---

## 1. MAVZUNING MAQSADI VA FUNDAMENTAL AHAMIYATI

### 1.1. Mavzuning Markaziy Muammosi
Zamonaviy axborot xavfsizligida markaziy savol mavjud:
> **«Kim (qaysi subyekt yoki jarayon), qaysi resursga (obyektga), qanday amalni (operatsiyani) bajarish huquqiga ega va bu huquq operatsion tizim darajasida qanday kafolatlanadi?»**

Agar tizimda ruxsatlarni tekshirish markazlashtirilmagan bo‘lsa, dasturchi har bir kod blokida tekshiruvni o‘zi yozishga majbur bo‘ladi. Natijada xatolar, kesh orqali o‘tib ketish, noqonuniy API chaqiruvlari yoki dasturiy zaifliklar (masalan, IDOR, SQL Injection, Privilege Escalation) orqali tajovuzkor butun tizimni nazorat ostiga oladi.

Ushbu amaliy va nazariy mashg‘ulotning maqsadi — axborot tizimlarida foydalanishni nazorat qilishning **uch fundamental ustuni**ni o‘rganish va ularni mustaqil topshiriqning **1-varianti («Elektron Kutubxona axborot tizimi»)** misolida real **Ubuntu Server** operatsion tizimida amalga oshirishdan iborat:
1. **Reference Monitor (Murojaat monitori):** Har qanday murojaatni qat'iy nazorat qiluvchi, chetlab o‘tib bo‘lmaydigan abstrakt arxitektura.
2. **Trusted Computing Base (TCB — Ishonchli hisoblash bazasi):** Xavfsizlik siyosatini amalga oshiruvchi apparat, mikrodastur va OT yadrosi komponentlari majmui hamda uning daxlsiz perimetri.
3. **Siyosat – Model – Mexanizm zanjiri:** Biznes talablarini texnik dasturiy vositalarga aylantirishning uch bosqichli intellektual zanjiri.

### 1.2. O‘quv va Amaliy Kutiladigan Natijalar
- $\langle 	imes ext{Subyekt}, 	imes ext{Obyekt}, 	imes ext{Operatsiya} 
angle$ triadasini «Elektron kutubxona» tizimi misolida aniq ajrata olish.
- 4 ta subyekt va 5 ta obyektdan iborat $4 	imes imes 5$ o‘lchamli **Foydalanish matritsasini** qurish.
- Matritsani ustunlar bo‘yicha **ACL (Access Control List)** ga va satrlar bo‘yicha **C-list (Capability list)** ga ajratish hamda ularning axborot xavfsizligidagi xususiyatlarini tahlil qilish.
- **Eng kam imtiyoz (*Least Privilege*)** tamoyili asosida matritsadagi ortiqcha huquqlarni topish va xavfsiz holatga keltirish.
- «Elektron kutubxona» siyosatini **Ubuntu Serverda POSIX ACL (`setfacl`, `getfacl`)** vositasida realizatsiya qilish.
- Yozilgan avtomatlashtirilgan Bash skriptlari orqali tizimdan chetlashishlarni (*drift*) fosh etish.
- Reference monitorning 3 ta oltin sharti buzilgan kiberxavfsizlik holatlarini tahlil qilish va yechim berish.

---

## 2. INFRATUZILMA VA TARMOQ ARXITEKTURASI

Ushbu amaliyot **Ubuntu Desktop/Laptop (Host)** operatsion tizimida ishlayotgan **VMware Workstation Pro / Player** virtualizatsiyasi ichidagi **Ubuntu Server VM** muhitida bajariladi. Foydalanuvchi universitet Wi-Fi tarmog‘ida emas, **shaxsiy lokal Wi-Fi** (uy routeri yoki mobil hotspot) tarmog‘ida ishlaydi.

### 2.1. Lokal Wi-Fi Muhitida Nega NAT (`vmnet8`) Rejimi Tanlandi?
Universitet Wi-Fi tarmoqlarida talabalarga xos cheklovlar (Captive portal, 802.1X, portlar blokirovkasi, mijozlar izolatsiyasi) bo‘ladi. Shaxsiy lokal Wi-Fi da esa to‘liq ma’muriy erkinlik mavjud. Lekin Wi-Fi adapterining apparat xususiyati sababli VMware tarmog‘ini to‘g‘ri sozlash muhim:

```
+-------------------------------------------------------------------------+
|                        UBUNTU HOST (Fizik Kompyuter)                    |
|   [Fizik Wi-Fi Chip (wlan0)] <---> Shaxsiy Wi-Fi Router (192.168.1.1)    |
|                |                                                        |
|    +-----------------------+                                            |
|    | VMware NAT Engine     | (vmnet8 virtual switch)                    |
|    | Virtual DHCP & Gateway| (192.168.126.1 / 192.168.126.2)            |
|    +-----------------------+                                            |
|                |                                                        |
|       +--------+-----------------------+                                |
|       |                                |                                |
|   [ens33: 192.168.126.130]         [ens33: 192.168.126.131]             |
|   +-----------------------+        +-----------------------+            |
|   |   UBUNTU SERVER       |        |   QO'SHIMCHA VM       |            |
|   |  (Elektron Kutubxona) |        |      (Node-2)         |            |
|   +-----------------------+        +-----------------------+            |
+-------------------------------------------------------------------------+
```

1. **Wi-Fi protokoli cheklovi (Layer 2 MAC Filtering):** IEEE 802.11 standarti bitta fizik Wi-Fi radiokanalida bitta MAC manzilni bog‘laydi. VMware'da **Bridged (`vmnet0`)** rejimi yoqilsa, virtual mashina routerdan o‘zining virtual MAC manzili bilan alohida IP so‘raydi. Ko‘plab Wi-Fi kartalar (Intel, Realtek) bunga yo‘l qo‘ymaydi, natijada VM internetga chiqa olmaydi yoki IP olmaydi.
2. **NAT (`vmnet8`) rejimining ustunliklari:**
   - VMware virtual drayveri host ichida xavfsiz ichki subnet (masalan, `192.168.126.0/24`) ochadi.
   - Ubuntu Server virtual mashinasi paketlarni tashqi tarmoqqa host orqali NAT (IP Masquerade) qilib uzatadi. Uy routeri faqat host kompyuterni ko‘radi — hech qanday tarmoq konflikti bo‘lmaydi.
   - Virtual mashinada internet kafolatlangan ishlaydi (`sudo apt update` paketlarni o‘rnatadi).
   - Host Ubuntu terminalidan serverga to‘g‘ridan-to‘g‘ri SSH orqali ulanish mumkin.

### 2.2. Ubuntu Serverda Tarmoqni Tekshirish va SSH Ulanish
Virtual server terminalida IP manzilni ko‘rish:
```bash
ip a
```
Host kompyuterdan qulay ishlash uchun SSH orqali ulanish:
```bash
ssh <server_foydalanuvchi>@192.168.126.xxx
```

---

## 3. 1-MA’RUZA VA NAZARIY TUSHUNCHALAR BO‘YICHA MUKAMMAL QO‘LLANMA

Ushbu bo‘lim 1-ma’ruzaning 27 ta slaydi va laboratoriya docx hujjatidagi barcha fundamental nazariy bilimlarni to‘liq birlashtirgan ilmiy qo‘llanmadir.

### 3.1. Markaziy Muammo va Kirish (Anderson hisoboti, 1972)
1972-yilda **James P. Anderson** AQSh Harbiy-havo kuchlari uchun tayyorlagan *«Computer Security Technology Planning Study» (ESD-TR-73-51)* hisobotida ilk bor **Reference Monitor (Murojaat monitori)** tushunchasini fanga kiritdi. U ko‘p foydalanuvchili tizimlarda xavfsizlikni ta’minlashning birdan-bir yo‘li — har bir murojaatni istisnosiz tekshiruvchi markaziy, daxlsiz yadro yaratish ekanligini isbotladi.

---

### 3.2. I Bo‘lim: Boshlang‘ich Triada — Subyekt, Obyekt, Operatsiya

Axborot tizimidagi har qanday xavfsizlik qarori elementar uchlik ustida qabul qilinadi:
$$\langle 	imes ext{Subyekt}, 	imes ext{Obyekt}, 	imes ext{Operatsiya} 
angle$$

```
   +-------------+       Murojaat <s, o, op>       +-------------------+
   |   SUBYEKT   | -----------------------------> | REFERENCE MONITOR |
   |  (Subject)  | <----------------------------- | (Nazorat Nuqtasi) |
   +-------------+       Ruxsat / Rad etish       +-------------------+
                                                            |
                                                   Ruxsat   |
                                                   berilsa  v
                                                   +-------------------+
                                                   |      OBYEKT       |
                                                   |     (Object)      |
                                                   +-------------------+
```

1. **Subyekt (Subject):** Resursga murojaat qiluvchi faol mohiyat (foydalanuvchi, tizim xizmati, fon jarayoni).
   - *Linuxda:* Foydalanuvchi (`UID`), guruh (`GID`), jarayon (`PID`, `Effective UID`).
   - *Windowsda:* Foydalanuvchi/guruhning `SID` identifikatori, `Access Token`.
2. **Obyekt (Object):** Himoyalanadigan passiv resurs (fayl, katalog, ma'lumotlar bazasi, soket).
   - *Linuxda:* Inode, katalog, blok qurilma, quvur (`pipe`).
   - *Windowsda:* NTFS fayllari, kalitlar (`Registry Keys`).
3. **Operatsiya (Operation):** Subyekt obyekt ustida bajaradigan amal (`Read`, `Write`, `Execute`, `Ownership`).

---

### 3.3. II Bo‘lim: Reference Monitor va Ishonchli Hisoblash Bazasi (TCB)

#### 1. Reference Monitor Nima?
Reference Monitor — bu real dastur yoki bitta fayl emas. Bu **abstrakt nazorat mexanizmi** (konseptual model). U har qanday subyektning har qanday obyektga qilayotgan har bir murojaatini xavfsizlik siyosatiga muvofiqligini tekshiradi va qat'iy «RUXSAT» yoki «RAD» qarorini qabul qiladi.

#### 2. Reference Monitorning 3 Ta Oltin Sharti (Anderson Talablari)
Reference Monitor o‘z vazifasini to‘liq bajarishi uchun bir vaqtning o‘zida quyidagi **uchta shart** so‘zsiz bajarilishi shart:

| № | Shart (Inglizcha nomi) | Mazmuni va Talabi | Buzilish Oqibati |
|---|------------------------|-------------------|------------------|
| **1** | **Buzib bo‘lmaslik** (*Tamper-proof*) | Nazorat mexanizmining kodi, xotirasi va xavfsizlik siyosati bazasi ruxsatsiz o‘zgartirilishi mumkin emas. U himoyalangan xotirada (yadro rejimida) yashashi shart. | Agar tajovuzkor nazorat kodini yoki ruxsatlar jadvalini tahrirlay olsa, u o‘ziga cheksiz huquq berib oladi. |
| **2** | **To‘liq vositachilik** (*Always invoked / Complete mediation*) | Har bir murojaat, istisnosiz, monitordan o‘tadi. Hech qanday aylanma yo‘l, kesh orqali o‘tib ketish yoki tekshiruvsiz kirish bo‘lishi mumkin emas. | Agar tizimda «orqa eshik» (backdoor), tekshirilmaydigan to‘g‘ridan-to‘g‘ri API yoki keshdan foydalanish bo‘lsa, nazorat butunlay qadrsizlanadi. |
| **3** | **Tekshirilishi mumkinligi** (*Verifiable / Small & Simple*) | Mexanizm shunchalik ixcham, sodda va biznes-mantiqdan ajratilgan bo‘lishi kerakki, uning to‘g‘riligini to‘liq audit qilish, matematik isbotlash va formal verifikatsiyalash mumkin bo‘lsin. | Agar nazorat kodi 200 000 qatordan iborat bo‘lsa, unda yashirin zaifliklar (0-day) va arxitektura xatolari bo‘lishi muqarrar. |

> **Qoida:** Uchtasidan bittasi buzilsa ham — butun tizim xavfsizligi butunlay qulaydi!

#### 3. Ishonchli Hisoblash Bazasi (TCB — Trusted Computing Base)
TCB — tizimning xavfsizlik siyosatini hayotga tatbiq etish uchun mas'ul bo‘lgan barcha apparat, dasturiy va mikrodasturiy komponentlar majmui.
- **Reference Monitor** — TCB ning mantiqiy yadrosidir.
- **TCB perimetri:** Perimetr ichidagi qismlarga (CPU himoya rejimlari, MMU, Yadro, Reference Monitor) to‘liq ishoniladi. Perimetrdan tashqaridagi hech narsaga (foydalanuvchi dasturlari, tashqi kutubxonalar, brauzerlar) ishonilmaydi!
- **Minimallashtirish tamoyili (*Economy of mechanism*):** Ishonchli kod qancha kam bo‘lsa, xato ehtimoli shuncha past bo‘ladi.

---

### 3.4. III Bo‘lim: Uch Qatlamli Zanjir — Siyosat, Model, Mexanizm

Xavfsizlik tizimini yaratishda to‘g‘ridan-to‘g‘ri kod yozish xatodir. Xavfsizlik fani quyidagi uch qatlamli aniqlashtirish zanjirini talab qiladi:

```
+-------------------------------------------------------------------------+
| 1. XAVFSIZLIK SIYOSATI (Security Policy)                                |
|    - Til: Tabiiy til (inson tili, qoidalar to'plami)                    |
|    - Mazmuni: "NIMA ruxsat etilgan va NIMA taqiqlangan?"                |
|    - Misol: "Kitobxon boshqa kitobxonlarning buyurtmalarini ko'rmasin." |
+-------------------------------------------------------------------------+
                                    |
                                    v  Aniqlashtirish va formallashtirish
+-------------------------------------------------------------------------+
| 2. XAVFSIZLIK MODELI (Security Model)                                   |
|    - Til: Matematika, mantiq, graflar, matritsalar                     |
|    - Mazmuni: "Xavfsizlik holati QANDAY ifodalanadi va isbotlanadi?"    |
|    - Turlari: Lampson Foydalanish Matritsasi, BLP, Biba, RBAC, ABAC     |
|    - Misol: Matritsa M[Kitobxon, Buyurtmalar] = { r, w }, faqat o'ziniki|
+-------------------------------------------------------------------------+
                                    |
                                    v  Dasturiy/apparat darajasida joriy etish
+-------------------------------------------------------------------------+
| 3. XAVFSIZLIK MEXANIZMI (Security Mechanism)                            |
|    - Til: Konkret dasturiy vositalar, fayl tizimi bayroqlari, protokollar|
|    - Mazmuni: "QANDAY vositalar yordamida texnik amalga oshiriladi?"    |
|    - Misol: Linux POSIX ACL (setfacl), Linux VFS, PAM, iptables, Kerberos|
+-------------------------------------------------------------------------+
```

#### Ajratish va Tekshirishning Oltin Qoidasi:
> **Test:** Agar siz xavfsizlik modelini o‘zgartirmagan holda, texnik mexanizmni boshqasiga almashtira olsangiz — siz qatlamlarni to‘g‘ri ajratgansiz!

---

### 3.5. Foydalanish Matritsasi (ACM), ACL va C-List Nazariyasi (Lampson, 1971)

1971-yilda **Butler W. Lampson** universal matematik model — **Foydalanish Matritsasi (Access Control Matrix — ACM)** ni yaratdi.

#### Siyraklik Muammosi (Sparse Matrix)
Haqiqiy tizimlarda millionlab fayllar va minglab foydalanuvchilar bo‘ladi. Ularning 99.9% kataklarida huquq bo‘lmaydi (bo‘sh). To‘liq matritsani xotirada saqlash behuda resurs sarfidir. Shu sababli **matritsa hech qachon yaxlit saqlanmaydi**, balki ikki yo‘nalishda dekompozitsiya qilinadi:

```
                           FOYDALANISH MATRITSASI
                          +-----+-----+-----+-----+-----+
                          | O1  | O2  | O3  | O4  | O5  |
                    +-----+-----+-----+-----+-----+-----+
                    | S1  |  r  |  r  |  -  | r,w |  -  |  =====> C-LIST (Satrlar bo'yicha)
                    | S2  | r,w | r,w | r,w | r,w |  r  |         Subyekt bilan yuradi (Token)
                    | S3  |  r  |  r  |  r  |  r  |  r  |
                    | S4  |r,w,o|r,w,o|  -  |r,w,o|r,w,o|
                    +-----+-----+-----+-----+-----+-----+
                             ||    ||    ||    ||    ||
                             \/    \/    \/    \/    \/
                      ACL (Access Control List - Ustunlar bo'yicha)
                      Obyekt yonida saqlanadi (POSIX ACL, NTFS DACL)
```

| Xususiyati | ACL (Access Control List) | C-list (Capability List) |
|---|---|---|
| **Dekompozitsiya** | Matritsaning **USTUNI** bo‘yicha | Matritsaning **SATRI** bo‘yicha |
| **Saqlanish joyi** | **Obyekt yonida** (fayl metama’lumotlarida / Inode) | **Subyekt bilan birga** (kirish tokeni, kriptografik chipta) |
| **Tez javob beradigan savoli** | *«Ushbu faylga kimlar kira oladi?»* (Fayl auditi oson) | *«Ushbu foydalanuvchi nimalarga kira oladi?»* (Foydalanuvchi profili oson) |
| **Qiyin bo‘lgan amali** | Subyekt ishdan ketganda uning barcha huquqlarini o‘chirish (barcha fayllarni aylanib chiqish kerak) | Bitta fayl o‘chirilganda barcha subyektlardagi tokenni qaytarib olish (*Revocation muammosi*) |
| **Real hayotiy misol** | Linux POSIX ACL (`getfacl`), Windows NTFS DACL, SQL Grants | Kerberos chiptalari (TGT/ST), OAuth 2.0 Access Token (JWT Scope), POSIX File Descriptors |

---

### 3.6. Xavfsiz Loyihalash Tamoyillari

1. **Eng kam imtiyoz tamoyili (*Principle of Least Privilege*):** Har bir subyektga faqat o‘z vazifasini bajarishi uchun zarur bo‘lgan eng minimal huquq beriladi.
2. **Vazifalarni ajratish tamoyili (*Separation of Duties — SoD*):** Tanqidiy jarayonlarni yakka shaxs mustaqil nazorat qila olmaydi.
3. **Standart rad tamoyili (*Default Deny / Fail-Safe Defaults*):** Ruxsatlar ro‘yxatida ochiq yozilmagan har qanday harakat sukut bo‘yicha rad etiladi (*Access Denied*).

---

## 4. TANLANGAN TOPSHIRIQ: 1-VARIANT «ELEKTRON KUTUBXONA» TAHLILI VA LOYIHALASH

Ushbu laboratoriyada docx dagi 7-bo‘limning **1-varianti: «Elektron kutubxona»** to‘liq yechib beriladi.

### 4.1. Tashkilot, Subyektlar va Obyektlar Tavsifi
Elektron kutubxona tizimi talabalar va tadqiqotchilarga kitoblar, jurnallar va elektron resurslardan foydalanish imkonini beruvchi axborot platformasidir.

- **Subyektlar to‘plami ($S$):**
  1. $S_1$ — `lib_kitobxon`: Ro‘yxatdan o‘tgan talaba yoki professor-o‘qituvchi. Resurslarni o‘qiydi va yangi buyurtmalar beradi.
  2. $S_2$ — `lib_kutubxonachi`: Fondni boshqaruvchi, yangi kitoblarni joylovchi, arizalarni qabul qiluvchi xodim.
  3. $S_3$ — `lib_tekshiruvchi`: Fondning to‘g‘riligini, hisobotlarni va faoliyat qonuniyligini tekshiruvchi mustaqil auditor.
  4. $S_4$ — `lib_admin`: Tizimning texnik infratuzilmasi, serverlar va zaxira nusxalar uchun mas'ul ma'mur.
- **Obyektlar to‘plami ($O$):**
  1. $O_1$ — `Katalog`: Barcha kitoblarning bibliografik ma’lumotlari, mualliflar va ISBN ro‘yxati.
  2. $O_2$ — `ElektronNusxalar`: PDF, EPUB va boshqa formatdagi kitoblarning asl fayllari.
  3. $O_3$ — `Kitobxonlar`: Kitobxonlarning shaxsiy pasport, yashash manzili va kontakt ma’lumotlari (PII).
  4. $O_4$ — `Buyurtmalar`: Foydalanuvchilar tomonidan berilgan kitob olish arizalari va navbatlar.
  5. $O_5$ — `Hisobotlar`: Oylik kitob aylanishi, shikastlangan fond va moliyaviy hisobotlar.

---

### 4.2. 4 × 5 Foydalanish Matritsasi ($M[s, o]$)

Quyida «Elektron kutubxona» axborot tizimining xavfsizlik siyosati matritsasi keltirilgan ($r$ — o‘qish, $w$ — yozish/tahrirlash, $own$ — boshqarish va ruxsatlarni belgilash, $—$ — ruxsat yo‘q):

| Subyektlar \ Obyektlar | $O_1$ Katalog | $O_2$ ElektronNusxalar | $O_3$ Kitobxonlar | $O_4$ Buyurtmalar | $O_5$ Hisobotlar |
|:---|:---:|:---:|:---:|:---:|:---:|
| **$S_1$ `lib_kitobxon`** | $r$ | $r$ | — | $r, w$ *(shaxsiy)* | — |
| **$S_2$ `lib_kutubxonachi`** | $r, w$ | $r, w$ | $r, w$ | $r, w$ | $r$ *(tuzatilgan)* |
| **$S_3$ `lib_tekshiruvchi`** | $r$ | $r$ | $r$ | $r$ | $r$ |
| **$S_4$ `lib_admin`** | $r, w, own$ | $r, w, own$ | — *(taqiqlangan!)* | $r, w, own$ | $r, w, own$ |

---

### 4.3. Olingan ACL va C-List Tuzilmalari

#### 1. Tanlangan 3 ta Obyekt uchun ACL (Matritsaning ustunlari):
- $	ext{ACL}(O_1 	imes ext{ Katalog}) = \{ S_1: (r); S_2: (r, w); S_3: (r); S_4: (r, w, own) \}$
- $	ext{ACL}(O_3 	imes ext{ Kitobxonlar}) = \{ S_2: (r, w); S_3: (r) \}$ *(Diqqat: $S_4$ Admin bu ro‘yxatda yo‘q!)*
- $	ext{ACL}(O_5 	imes ext{ Hisobotlar}) = \{ S_2: (r); S_3: (r); S_4: (r, w, own) \}$

#### 2. Tanlangan 2 ta Subyekt uchun C-List (Matritsaning satrlari):
- $	ext{C-list}(S_1 	imes ext{ `lib_kitobxon`}) = \{ O_1: (r); O_2: (r); O_4: (r, w 	imes ext{ - faqat o‘z yozuvi}) \}$
- $	ext{C-list}(S_4 	imes ext{ `lib_admin`}) = \{ O_1: (r, w, own); O_2: (r, w, own); O_4: (r, w, own); O_5: (r, w, own) \}$

---

### 4.4. Eng Kam Imtiyoz (Least Privilege) Tahlili (3 ta katak bo‘yicha)

1. **Katak: $S_2$ (`lib_kutubxonachi`) $
ightarrow$ $O_5$ (`Hisobotlar`):**
   - *Dastlabki noto‘g‘ri huquq:* $r, w$ (O‘qish va Yozish).
   - *Nega ortiqcha:* Kutubxonachi oylik hisobotni dastlab kiritishi mumkin, lekin tasdiqlangan moliyaviy hisobotlarni o‘zgartira olmasligi kerak. Aks holda u kitob yetishmovchiligi yoki jarimalarni yashirish uchun ma'lumotlarni soxtalashtirishi mumkin.
   - *Taklif etilgan to‘g‘ri huquq:* $r$ (Faqat o‘qish) yoki vaqtinchalik kiritish huquqi.
2. **Katak: $S_4$ (`lib_admin`) $
ightarrow$ $O_3$ (`Kitobxonlar`):**
   - *Dastlabki noto‘g‘ri huquq:* Ko‘p tizimlarda adminga barcha joyga $r, w, own$ beriladi.
   - *Nega ortiqcha:* Tizim administratori server dasturlari va drayverlarni sozlaydi. U kitobxonlarning shaxsiy yashash manzillari, telefon raqamlari va pasport ma’lumotlarini o‘qishi shart emas. Bu shaxsiy daxlsizlik (privacy) va qonunchilik talabi.
   - *Taklif etilgan to‘g‘ri huquq:* $—$ (O‘qish mutlaqo taqiqlanadi; faqat disk darajasida zaxira nusxa olish imkoniyati qoladi).
3. **Katak: $S_3$ (`lib_tekshiruvchi`) $
ightarrow$ $O_2$ (`ElektronNusxalar`):**
   - *Dastlabki noto‘g‘ri huquq:* $r, w$ berilishi xavflidir.
   - *Nega ortiqcha:* Auditor faqat tekshiruvchi. Agar unga yozish huquqi berilsa, u tekshiruv davomida fayllarni shikastlashi yoki o‘chirib yuborishi mumkin.
   - *Taklif etilgan to‘g‘ri huquq:* $r$ (Faqat ko‘rish va taqqoslash).

---

### 4.5. Qo‘shimcha Shartlarning Chuqur Arxitektura Tahlili

1-variantda ikkita muhim qo‘shimcha shart qo‘yilgan:

#### 1-Shart: «Kitobxon faqat o‘z buyurtmalarini ko‘rsin»
- **Muammo:** Ushbu shartni bitta umumiy `Buyurtmalar` papkasi darajasida oddiy POSIX ACL yoki NTFS ruxsatlari bilan **ifodalab bo‘lmaydi!** Agar `lib_kitobxon` guruhiga `Buyurtmalar` katalogiga o‘qish ruxsati berilsa, u barcha boshqa kitobxonlarning buyurtma fayllarini ham ko‘ra oladi.
- **Yechim yo‘llari:**
  1. *Fayl tizimi darajasida:* Har bir kitobxon uchun shaxsiy katalog ochiladi: `/Buyurtmalar/user_ali/` va faqat uning egasiga `rwx` beriladi.
  2. *Ilova va DBMS darajasida:* **Row-Level Security (RLS)** yoki **ABAC (Attribute-Based Access Control)** mexanizmi qo‘llaniladi. SQL so‘rovda avtomatik filtr ishlaydi: `SELECT * FROM orders WHERE user_id = CURRENT_USER`.

#### 2-Shart: «Tizim ma’muri tizimni boshqarsin, lekin kitobxonlarning shaxsiy ma’lumotlarini o‘qiy olmasin»
- **Muammo:** Klassik operatsion tizimlarda super-foydalanuvchi (`root` yoki `Administrator`) barcha DAC to‘siqlarini aylanib o‘tish imkoniyatiga ega.
- **Yechim yo‘llari:**
  1. *Kriptografik himoya:* `Kitobxonlar` ma’lumotlari ilova darajasida shifrlanadi (Application-layer Encryption). Shifrlash kaliti faqat kutubxonachida bo‘ladi. Admin faylni ochgan taqdirda ham faqat tushunarsiz shifrlangan matnni ko‘radi.
  2. *Mandatory Access Control (MAC):* Linuxda **SELinux** yoki **AppArmor** profillari orqali hattoki `root` foydalanuvchisi va uning jarayonlari uchun ham ushbu katalogga kirish taqiqlab qo‘yiladi.

---

## 5. AMALIY MASHG‘ULOT: UBUNTU SERVERDA QADAMMA-QADAM BAJARISH QO‘LLANMASI

Endi yuqorida loyihalangan «Elektron kutubxona» tizimini **Ubuntu Server** virtual mashinasida to‘liq amalga oshiramiz.

### 5.1. Tizimni Tayyorlash va POSIX ACL O‘rnatish

Standart Unix huquqlari faqat 3 toifani (Egasi, Guruh, Boshqalar) taniydi. Bizga esa 4 ta mustaqil guruh va 5 ta obyekt kerak. Shuning uchun bizga **POSIX ACL (`setfacl`, `getfacl`)** zarur.

Ubuntu Server terminalida:
```bash
sudo apt update && sudo apt install -y acl
```

Katalogni yaratamiz va unga o‘tamiz:
```bash
sudo mkdir -p /srv/labiam/a1
cd /srv/labiam/a1
```

---

### 5.2. «Elektron Kutubxona» Uchun To‘liq Bash Skriptlari To‘plami

Laboratoriya ishi uchun `/srv/labiam/a1` ichida 5 ta maxsus skript tuzamiz.

---

#### 1. `matritsa.sh` — Elektron Kutubxona Siyosat Manbai
Ushbu skript bizning 1-variantimiz uchun barcha qoidalarni saqlaydi.

Faylni yarating: `sudo nano /srv/labiam/a1/matritsa.sh`
```bash
#!/usr/bin/env bash
# matritsa.sh - 1-Variant: "Elektron Kutubxona" Foydalanish Matritsasi

export LAB_ROOT="/srv/labiam/a1/Obyektlar"

# Subyektlar (Linux guruhlari)
export SUBJECTS=("lib_kitobxon" "lib_kutubxonachi" "lib_tekshiruvchi" "lib_admin")

# Obyektlar (Kataloglar)
export OBJECTS=("Katalog" "ElektronNusxalar" "Kitobxonlar" "Buyurtmalar" "Hisobotlar")

# Matritsa kataklari: s|o -> huquqlar (r, w, own)
# Bo'sh qator - huquq yo'q (Standart rad)
declare -A MATRIX

# 1. lib_kitobxon huquqlari
MATRIX["lib_kitobxon|Katalog"]="r"
MATRIX["lib_kitobxon|ElektronNusxalar"]="r"
MATRIX["lib_kitobxon|Kitobxonlar"]=""     # Boshqalarning ma'lumotlarini ko'rmaydi
MATRIX["lib_kitobxon|Buyurtmalar"]="r,w"  # Shaxsiy buyurtma
MATRIX["lib_kitobxon|Hisobotlar"]=""

# 2. lib_kutubxonachi huquqlari
MATRIX["lib_kutubxonachi|Katalog"]="r,w"
MATRIX["lib_kutubxonachi|ElektronNusxalar"]="r,w"
MATRIX["lib_kutubxonachi|Kitobxonlar"]="r,w"
MATRIX["lib_kutubxonachi|Buyurtmalar"]="r,w"
MATRIX["lib_kutubxonachi|Hisobotlar"]="r"    # Least privilege bo'yicha faqat o'qish!

# 3. lib_tekshiruvchi huquqlari (Auditor - hech qayerga yoza olmaydi)
MATRIX["lib_tekshiruvchi|Katalog"]="r"
MATRIX["lib_tekshiruvchi|ElektronNusxalar"]="r"
MATRIX["lib_tekshiruvchi|Kitobxonlar"]="r"
MATRIX["lib_tekshiruvchi|Buyurtmalar"]="r"
MATRIX["lib_tekshiruvchi|Hisobotlar"]="r"

# 4. lib_admin huquqlari (Tizim ma'muri)
MATRIX["lib_admin|Katalog"]="r,w,own"
MATRIX["lib_admin|ElektronNusxalar"]="r,w,own"
MATRIX["lib_admin|Kitobxonlar"]=""          # Qo'shimcha shart: shaxsiy ma'lumotlarni o'qimasin!
MATRIX["lib_admin|Buyurtmalar"]="r,w,own"
MATRIX["lib_admin|Hisobotlar"]="r,w,own"

# Katak qiymatini olish
get_cell() {
    local s="$1"
    local o="$2"
    local key="${s}|${o}"
    echo "${MATRIX[$key]}"
}

# Matritsani chiroyli jadval ko'rinishida chiqarish
show_matrix() {
    printf "%-18s | %-8s | %-16s | %-12s | %-11s | %-10s
" "Subyekt \ Obyekt" "Katalog" "ElektronNusxalar" "Kitobxonlar" "Buyurtmalar" "Hisobotlar"
    echo "-----------------------------------------------------------------------------------------------------"
    for s in "${SUBJECTS[@]}"; do
        printf "%-18s | " "$s"
        for o in "${OBJECTS[@]}"; do
            local val=$(get_cell "$s" "$o")
            if [ -z "$val" ]; then val="-"; fi
            printf "%-10s | " "$val"
        done
        printf "
"
    done
}

# Katakni POSIX ACL formatiga aylantirish
convert_to_posix_acl() {
    local cell="$1"
    case "$cell" in
        "r,w,own") echo "rwx" ;;
        "r,w")     echo "rwx" ;;
        "r")       echo "rx"  ;;
        "w")       echo "wx"  ;;
        *)         echo ""    ;;
    esac
}
```

---

#### 2. `sozlash.sh` — Matritsani Ubuntu Serverda Realizatsiya Qilish
Ushbu skript Linux guruhlarini yaratadi, kataloglar strukturasini tuzadi va `setfacl` orqali POSIX ACL ruxsatlarini biriktiradi.

Faylni yarating: `sudo nano /srv/labiam/a1/sozlash.sh`
```bash
#!/usr/bin/env bash
# sozlash.sh - Elektron Kutubxona siyosatini Linux POSIX ACL da o'rnatish.

if [ "$EUID" -ne 0 ]; then
    echo "Xato: Skriptni 'sudo' bilan ishga tushiring!" >&2
    exit 1
fi

SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)
source "$SCRIPT_DIR/matritsa.sh"

echo "=== 1. Guruhlarni yaratish ==="
for g in "${SUBJECTS[@]}"; do
    if getent group "$g" >/dev/null 2>&1; then
        echo "Guruh mavjud: $g"
    else
        groupadd "$g"
        echo "Guruh yaratildi: $g"
    fi
done

echo -e "
=== 2. Obyektlar kataloglarini yaratish va ACL o'rnatish ==="
mkdir -p "$LAB_ROOT"
chmod 755 "$LAB_ROOT"

for o in "${OBJECTS[@]}"; do
    dir_path="$LAB_ROOT/$o"
    mkdir -p "$dir_path"
    
    # Namunaviy ma'lumot fayli
    echo "$o obyektining xavfsiz mazmuni" > "$dir_path/namuna.txt"
    
    # Standart himoya: Egasi root, boshqalarga ruxsat mutlaqo yopiq (000)
    chown -R root:root "$dir_path"
    chmod 700 "$dir_path"
    
    # Avvalgi barcha ACL larni tozalash (/reset kabi)
    setfacl -b -R "$dir_path"
    
    # Har bir subyekt huquqini matritsadan olib biriktiramiz
    for s in "${SUBJECTS[@]}"; do
        cell_val=$(get_cell "$s" "$o")
        acl_right=$(convert_to_posix_acl "$cell_val")
        
        if [ -n "$acl_right" ]; then
            setfacl -m "g:${s}:${acl_right}" "$dir_path"
            setfacl -m "g:${s}:${acl_right}" "$dir_path/namuna.txt"
            # Default ACL (yangi fayllarga meros o'tishi uchun)
            setfacl -d -m "g:${s}:${acl_right}" "$dir_path"
            printf "%-18s <- %-18s %s
" "$o" "$s" "$acl_right"
        fi
    done
done

echo -e "
Tayyor: Elektron kutubxona siyosati to'liq o'rnatildi!"
```

---

#### 3. `tekshir.sh` — Tizim Holatini Siyosat Bilan Taqqoslash (Audit)
Ushbu skript real ACL larni o‘qib, C-list va ACL jadvallarini tuzadi hamda `matritsa.sh` dagi siyosatdan har qanday chetlashishni fosh etadi.

Faylni yarating: `sudo nano /srv/labiam/a1/tekshir.sh`
```bash
#!/usr/bin/env bash
# tekshir.sh - Elektron Kutubxona ACL holatini siyosat bilan solishtirish.

SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)
source "$SCRIPT_DIR/matritsa.sh"

echo -e "
[1;36m1) ACL Ko'rinishi (Obyektlar bo'yicha - getfacl orqali o'qildi):[0m"
for o in "${OBJECTS[@]}"; do
    dir_path="$LAB_ROOT/$o"
    printf "ACL(%s) = { " "$o"
    acl_output=$(getfacl -p "$dir_path" 2>/dev/null | grep "^group:lib_" | sed 's/group://g')
    formatted=""
    while read -r line; do
        if [ -n "$line" ]; then
            grp=$(echo "$line" | cut -d':' -f1)
            perm=$(echo "$line" | cut -d':' -f2)
            formatted+="${grp}: (${perm}); "
        fi
    done <<< "$acl_output"
    echo "${formatted% } }"
done

echo -e "
[1;36m2) C-list Ko'rinishi (Buning uchun BARCHA obyektlar aylanib chiqildi):[0m"
for s in "${SUBJECTS[@]}"; do
    printf "C-list(%s) = { " "$s"
    formatted=""
    for o in "${OBJECTS[@]}"; do
        dir_path="$LAB_ROOT/$o"
        perm=$(getfacl -p "$dir_path" 2>/dev/null | grep "^group:${s}:" | cut -d':' -f3)
        if [ -n "$perm" ]; then
            formatted+="${o}: (${perm}); "
        fi
    done
    echo "${formatted% } }"
done

echo -e "
[1;36m3) Siyosat va Haqiqiy Holat Taqqoslanishi (Audit):[0m"
has_discrepancy=0
printf "%-18s | %-16s | %-10s | %-10s | %-20s
" "Subyekt" "Obyekt" "Matritsa" "Haqiqiy" "Xulosa"
echo "--------------------------------------------------------------------------------------------"

for s in "${SUBJECTS[@]}"; do
    for o in "${OBJECTS[@]}"; do
        dir_path="$LAB_ROOT/$o"
        want_raw=$(get_cell "$s" "$o")
        want=$(convert_to_posix_acl "$want_raw")
        have=$(getfacl -p "$dir_path" 2>/dev/null | grep "^group:${s}:" | cut -d':' -f3)
        
        if [ "$want" != "$have" ]; then
            has_discrepancy=1
            verdict=""
            if [ -z "$want" ] && [ -n "$have" ]; then
                verdict="ORTIQCHA HUQUQ (Xavf!)"
            elif [ -n "$want" ] && [ -z "$have" ]; then
                verdict="YETISHMAYDI"
            else
                verdict="FARQ BOR"
            fi
            printf "%-18s | %-16s | %-10s | %-10s | %-20s
" "$s" "$o" "${want:-"-"}" "${have:-"-"}" "$verdict"
        fi
    done
done

if [ "$has_discrepancy" -eq 0 ]; then
    echo -e "[1;32mMos: Tizimdagi ruxsatlar xavfsizlik siyosatiga to'liq mos keladi![0m"
fi
```

---

#### 4. `monitor.sh` — Murojaat Monitorining O‘quv Modeli
Reference Monitor har bir so‘rovni tekshiradi va qaror chiqarib, audit jurnaliga qayd qiladi.

Faylni yarating: `sudo nano /srv/labiam/a1/monitor.sh`
```bash
#!/usr/bin/env bash
# monitor.sh - Elektron Kutubxona Reference Monitor modeli.

SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)
source "$SCRIPT_DIR/matritsa.sh"
LOG_FILE="$SCRIPT_DIR/monitor.log"

invoke_access() {
    local s="$1"
    local o="$2"
    local op="$3"
    local cell=$(get_cell "$s" "$o")
    local allowed=0
    
    if [ -n "$cell" ]; then
        IFS=',' read -ra RIGHTS <<< "$cell"
        for r in "${RIGHTS[@]}"; do
            if [ "$r" == "$op" ]; then
                allowed=1
                break
            fi
        done
    fi
    
    local verdict="RAD"
    if [ "$allowed" -eq 1 ]; then verdict="RUXSAT"; fi
    
    local timestamp=$(date "+%Y-%m-%d %H:%M:%S")
    echo "$timestamp;$s;$o;$op;$verdict" >> "$LOG_FILE"
    
    if [ "$allowed" -eq 1 ]; then return 0; else return 1; fi
}

echo "=== Murojaat Monitori So'rovlarni Tekshirmoqda ==="
printf "%-18s | %-16s | %-6s | %-10s
" "Subyekt" "Obyekt" "Amal" "Qaror"
echo "-----------------------------------------------------------------"

test_requests=(
    "lib_kitobxon:Katalog:r"
    "lib_kitobxon:Kitobxonlar:r"          # Rad: shaxsiy ma'lumot
    "lib_kutubxonachi:ElektronNusxalar:w" # Ruxsat: yangi kitob qo'shish
    "lib_tekshiruvchi:Hisobotlar:w"       # Rad: auditor yoza olmaydi
    "lib_admin:Katalog:own"               # Ruxsat: boshqaruv
    "lib_admin:Kitobxonlar:r"             # Rad: admin shaxsiy ma'lumotni o'qimasin
    "lib_begona:Katalog:r"                # Rad: begona subyekt (Standart rad)
)

for item in "${test_requests[@]}"; do
    IFS=':' read -r sub obj act <<< "$item"
    if invoke_access "$sub" "$obj" "$act"; then
        res="[1;32mRUXSAT[0m"
    else
        res="[1;31mRAD[0m"
    fi
    printf "%-18s | %-16s | %-6s | %b
" "$sub" "$obj" "$act" "$res"
done

echo -e "
Barcha murojaatlar audit jurnaliga yozildi: $LOG_FILE"
```

---

#### 5. `tozalash.sh` — Laboratoriyani Tozalash Skripti
Laboratoriya tugagach tizimni asl holatiga qaytarish uchun.

Faylni yarating: `sudo nano /srv/labiam/a1/tozalash.sh`
```bash
#!/usr/bin/env bash
# tozalash.sh - Elektron Kutubxona laboratoriya obyektlarini tozalash.

if [ "$EUID" -ne 0 ]; then
    echo "Xato: Skriptni 'sudo' bilan ishga tushiring!" >&2
    exit 1
fi

SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)
source "$SCRIPT_DIR/matritsa.sh"

echo "=== Tozalash boshlandi ==="

# Test foydalanuvchisini o'chirish
if id "kitobxon_ali" >/dev/null 2>&1; then
    userdel -r kitobxon_ali 2>/dev/null
    echo "Foydalanuvchi o'chirildi: kitobxon_ali"
fi

# Guruhlarni o'chirish
for g in "${SUBJECTS[@]}"; do
    if getent group "$g" >/dev/null 2>&1; then
        groupdel "$g"
        echo "Guruh o'chirildi: $g"
    fi
done

# Kataloglarni o'chirish
if [ -d "$LAB_ROOT" ]; then
    rm -rf "$LAB_ROOT"
    echo "Papka o'chirildi: $LAB_ROOT"
fi

echo "Elektron kutubxona laboratoriya ob'ektlari tozalandi!"
```

Skriptlarga ruxsat beramiz:
```bash
sudo chmod +x /srv/labiam/a1/*.sh
```

---

### 5.3. Har Bir CLI Buyruqning Mukammal Tahlili

1. `sudo groupadd lib_kitobxon`
   - *Vazifasi:* Yangi xavfsizlik guruhini yaratadi.
   - *Tizimdagi harakat:* `/etc/group` va `/etc/gshadow` fayllariga yangi satr va noyob GID qo‘shiladi.
2. `sudo useradd -m -s /bin/bash kitobxon_ali`
   - *Vazifasi:* Sinov kitobxon foydalanuvchisini ochadi.
   - *Bayroqlar:* `-m` (`--create-home`) foydalanuvchi uchun `/home/kitobxon_ali` katalogini yaratadi; `-s /bin/bash` unga standart buyruqlar interpretatorini belgilaydi.
3. `sudo usermod -aG lib_kitobxon kitobxon_ali`
   - *Vazifasi:* Foydalanuvchini `lib_kitobxon` guruhiga a'zo qiladi.
   - *Bayroqlar:* `-a` (*append*) mavjud guruhlarni saqlab qoladi; `-G` ikkilamchi qo‘shimcha guruhlarni bildiradi.
4. `sudo chmod 700 /srv/labiam/a1/Obyektlar/Katalog`
   - *Vazifasi:* Standart Unix ruxsatlarini qat'iy yopadi.
   - *Raqamli kod:* `7` = egasi (`root`) ga `rwx`; `0` = guruhga hech narsa yo‘q; `0` = boshqalarga umuman ruxsat yo‘q.
5. `sudo setfacl -b -R /srv/labiam/a1/Obyektlar/Katalog`
   - *Vazifasi:* Barcha eski yoki qo‘lda kiritilgan ACL larni butunlay tozalaydi.
   - *Bayroqlar:* `-b` (*remove-all*) barcha ACE yozuvlarini o‘chiradi; `-R` rekursiv ichki fayllarga ham tatbiq etadi.
6. `sudo setfacl -m g:lib_kitobxon:rx /srv/labiam/a1/Obyektlar/Katalog`
   - *Vazifasi:* `Katalog` obyektiga `lib_kitobxon` guruhi uchun o‘qish va kirish ruxsatini beradi.
   - *Bayroqlar:* `-m` (*modify*) ACL yozuvini kiritadi; `g:nomi:rx` guruhga tegishli ruxsat.
7. `sudo setfacl -d -m g:lib_kitobxon:rx /srv/labiam/a1/Obyektlar/Katalog`
   - *Vazifasi:* **Default (Meros) ACL** o‘rnatadi.
   - *Bayroqlar:* `-d` (*default*) ushbu katalog ichida kelajakda yaratiladigan yangi fayllarga ham ushbu huquq avtomatik meros bo‘lib o‘tishini ta'minlaydi (Windowsdagi `(OI)(CI)` merosi bilan bir xil).
8. `getfacl -p /srv/labiam/a1/Obyektlar/Katalog`
   - *Vazifasi:* Obyektning to‘liq ACL ro‘yxatini chiqaradi.
   - *Bayroq:* `-p` yo‘l boshidagi sleshni olib tashlamasdan to‘liq ko‘rsatadi.

---

### 5.4. 3 Ta Amaliy Tajribani Ubuntu Serverda O‘tkazish

Skriptlar yaratilgach, dastlab siyosatni o‘rnatamiz:
```bash
sudo /srv/labiam/a1/sozlash.sh
```

#### 1-Tajriba: Siyosatdan Tashqari Huquq Berish va Audit (Drift Detection)
- **Ssenariy:** Ma’mur yanglishib yoki vaqtincha kitobxonlarga `Hisobotlar` papkasiga ruxsatsiz yozish huquqini berib yubordi:
  ```bash
  sudo setfacl -m g:lib_kitobxon:rwx /srv/labiam/a1/Obyektlar/Hisobotlar
  ```
- **Audit tekshiruvi:**
  ```bash
  /srv/labiam/a1/tekshir.sh
  ```
  *Natija:* Audit qizil rangda ogohlantiradi:
  `lib_kitobxon | Hisobotlar | - | rwx | ORTIQCHA HUQUQ (Xavf!)`
- **Qayta tiklash:** Xavfsizlik siyosati (`matritsa.sh`) yagona haqiqat manbai bo‘lgani uchun, tizimni qayta tiklaymiz:
  ```bash
  sudo /srv/labiam/a1/sozlash.sh
  /srv/labiam/a1/tekshir.sh
  ```
  *Natija:* `Mos: Tizimdagi ruxsatlar xavfsizlik siyosatiga to'liq mos keladi!`

---

#### 2-Tajriba: Haqiqiy Murojaat — Linux Yadrosidagi Reference Monitor
- **Maqsad:** Linux yadrosi VFS qatlamidagi Reference Monitor har bir tizim chaqiruvini qanday tekshirishini ko‘rish.
- **Bajarish tartibi:**
  1. Sinov foydalanuvchisini yaratib, `lib_kitobxon` guruhiga qo‘shamiz:
     ```bash
     sudo useradd -m -s /bin/bash kitobxon_ali
     sudo usermod -aG lib_kitobxon kitobxon_ali
     ```
  2. `kitobxon_ali` nomidan tizimga kiramiz:
     ```bash
     sudo su - kitobxon_ali
     ```
  3. **1-Murojaat (Ruxsat berilgan):** `Katalog` ni o‘qish:
     ```bash
     cat /srv/labiam/a1/Obyektlar/Katalog/namuna.txt
     ```
     *Natija:* `Katalog obyektining xavfsiz mazmuni` (Muvaffaqiyatli o‘qildi!).
  4. **2-Murojaat (Taqiqlangan):** `Kitobxonlar` shaxsiy ma’lumotlarini o‘qish:
     ```bash
     cat /srv/labiam/a1/Obyektlar/Kitobxonlar/namuna.txt
     ```
     *Natija:* `bash: .../Kitobxonlar/namuna.txt: Permission denied`
     *Tushuntirish:* Linux yadrosi VFS Inode dagi ACL ni tekshirdi. `lib_kitobxon` uchun yozuv yo‘q — **Standart rad** ishladi!
  5. **3-Murojaat (Huquqdan tashqari):** `Katalog` ga fayl yozishga urinish:
     ```bash
     echo "Buzg'unchilik" > /srv/labiam/a1/Obyektlar/Katalog/xaker.txt
     ```
     *Natija:* `bash: .../Katalog/xaker.txt: Permission denied`
     *Tushuntirish:* Kitobxonga faqat `rx` berilgan, `w` berilmagan.
  6. Sessiyadan chiqamiz:
     ```bash
     exit
     ```

---

#### 3-Tajriba: Siyosat Faylining O‘zini Himoyalash (Tamper-Proof)
- **Maqsad:** Reference monitorning 1-sharti bo‘lgan «Buzib bo‘lmaslik»ni amalda tekshirish.
- **Tahlil:** Agar `matritsa.sh` faylini oddiy foydalanuvchi o‘zgartira olsa, u o‘ziga hamma huquqlarni yozib oladi.
- **Bajarish tartibi:**
  1. Siyosat faylini faqat `root` ga biriktiramiz:
     ```bash
     sudo chown root:root /srv/labiam/a1/matritsa.sh
     sudo chmod 644 /srv/labiam/a1/matritsa.sh
     ```
  2. Sinov: `kitobxon_ali` nomidan siyosatga ruxsatsiz yozishga urinamiz:
     ```bash
     sudo su - kitobxon_ali -c "echo 'HACK' >> /srv/labiam/a1/matritsa.sh"
     ```
     *Natija:* `bash: /srv/labiam/a1/matritsa.sh: Permission denied`
- **Xulosa:** Siyosat bazasi yozishdan ishonchli himoyalandi. Reference monitorning «Buzib bo‘lmaslik» talabi ta’minlandi!

---

### 5.5. Windows (DOCX) va Linux (Ubuntu) Konseptual Qiyosiy Tahlili

| Tushuncha | Windows Muhitida (.docx) | Linux Ubuntu Muhitida (Biz bajargan) |
|---|---|---|
| **Subyekt** | Mahalliy Guruh (`LAB_Kitobxonlar`), `SID` | Linux Guruhlari (`lib_kitobxon`), `GID` |
| **Obyekt** | NTFS Katalogi (`C:\LabIAM\A1\Obyektlar\Katalog`) | Ext4/XFS Katalogi (`/srv/labiam/a1/Obyektlar/Katalog`) |
| **ACL Boshqaruvi** | `icacls`, PowerShell `Get-Acl` / `Set-Acl` | `setfacl`, `getfacl` (POSIX 1003.1e) |
| **Meros Mexanizmi** | `(OI)(CI)` — Object Inherit, Container Inherit | Default ACL (`setfacl -d -m ...`) |
| **To‘liq Huquq** | Full Control (`F`) | `rwx` va `chown` egaligi |
| **Faqat O‘qish** | Read & Execute (`RX`) | `rx` (o‘qish va ichiga kirish) |
| **Murojaat Monitori**| SRM (Security Reference Monitor, `ntoskrnl.exe`) | Linux Kernel VFS Permission Engine + LSM |
| **Rad Etish Xabari** | `Access is denied` | `Permission denied` |

---

## 6. MUROJAAT MONITORI SHARTLARI BUZILISHI BO‘YICHA KEYS-TAHLIL (6-bo‘limdagi 5 ta holat)

Laboratoriya ishidagi 5 ta tanqidiy kiberxavfsizlik vaziyati tahlili:

1. **1-Holat:** *«Ilovaning administrator huquqlari bilan ishlaydigan moduli ma’lumotlar bazasiga bevosita, ruxsat tekshiruvisiz SQL so‘rov yuboradi.»*
   - **Buzilgan shart:** **To‘liq vositachilik (*Always invoked / Complete mediation*)**.
   - **Yechim:** Administrator moduli ham tekshiruv nuqtasidan (Reference Monitor / API Gateway) o‘tishi, har bir SQL chaqiruv qat'iy tekshirilib, auditga yozilishi shart.
2. **2-Holat:** *«Foydalanuvchi huquqlari saqlanadigan konfiguratsiya fayli oddiy matn ko‘rinishida va barcha foydalanuvchilar uchun yozishga ochiq.»*
   - **Buzilgan shart:** **Buzib bo‘lmaslik (*Tamper-proof*)**.
   - **Yechim:** Konfiguratsiya fayliga faqat tizim egasi (`root`) yozishi kerak (`chmod 600`), fayl yaxlitligi xesh (SHA-256) bilan nazorat qilinishi lozim.
3. **3-Holat:** *«Foydalanishni nazorat qiluvchi modul 150 000 qatorli kodga ega, u biznes-mantiq bilan aralashib ketgan va hech qachon to‘liq audit qilinmagan.»*
   - **Buzilgan shart:** **Tekshirilishi mumkinligi (*Verifiable / Small & Simple*)**.
   - **Yechim:** Xavfsizlik moduli biznes-mantiqdan to‘liq ajratilib, mustaqil ixcham siyosat qaror nuqtasiga (Policy Decision Point) aylantirilishi va kod auditi o‘tkazilishi kerak.
4. **4-Holat:** *«Veb-ilovada huquq faqat brauzer tomonida (JavaScript) tekshiriladi; so‘rovni to‘g‘ridan-to‘g‘ri API ga yuborish orqali tekshiruvni chetlab o‘tish mumkin.»*
   - **Buzilgan shart:** **To‘liq vositachilik (*Always invoked*)**.
   - **Yechim:** Brauzer ishonchsiz muhit. Har bir ruxsat tekshiruvi server tomonida (Backend API) qayta amalga oshirilishi shart.
5. **5-Holat:** *«Tizimda «shoshilinch kirish» (break-glass) hisobi mavjud bo‘lib, u orqali kiritilgan amallar jurnalga yozilmaydi.»*
   - **Buzilgan shart:** **To‘liq vositachilik (*Always invoked*)** va **Hisobdorlik (*Accountability*)**.
   - **Yechim:** Favqulodda hisoblar harakati o‘chirilmasdan, aksincha xavfsizlik xizmatiga real vaqtda signal beruvchi mustaqil SIEM jurnaliga yozilishi shart.

---

## 7. BOSHQARUV TOPSHIRIQ VARIANTLARI QISQACHA YECHIMLARI (2–5 Variantlar)

Boshqa variantlar uchun tayyor qiyosiy ma'lumotlar:

### 2-Variant: Universitet Ombori
- Subyektlar: Omborchi, Hisobchi, Auditor, Bo‘lim boshlig‘i.
- Obyektlar: Kirim, Chiqim, Qoldiqlar, Narxlar, AuditHisobotlari.
- Xususiyat: Auditor hech qayerga yoza olmaydi; Omborchiga Narxlar uchun faqat `r` beriladi (`w` yo‘q).

### 3-Variant: Ilmiy Loyiha
- Subyektlar: Tadqiqotchi, Rahbar, Laborant, Mehmon.
- Obyektlar: XomMalumotlar, TahlilSkriptlari, Maqola, GrantHisoboti, Uskunalar.
- Xususiyat: Mehmon faqat Maqolani o‘qiydi; Vaqtinchalik kirish Linuxda `usermod -e YYYY-MM-DD` yoki cron orqali avtomatik o‘chirish bilan ta'minlanadi.

### 4-Variant: Talabalar Turar Joyi
- Subyektlar: Talaba, Mas’ul, Nazoratchi, Buxgalter.
- Obyektlar: Xonalar, Tolovlar, TashrifJurnali, Shikoyatlar, Talabalar.
- Xususiyat: «Talaba shikoyat yoza olsin, lekin boshqalarnikini o‘qimasin» — Linuxda `Shikoyatlar` papkasiga Write va Execute beriladi, lekin Read olinadi (`chmod 733` yoki `wx`), o‘chirishni bloklash uchun esa **Sticky Bit (`chmod +t`)** qo‘yiladi.

### 5-Variant: Kafedra Hujjatlari
- Subyektlar: O‘qituvchi, Kotib, Mudir, Talaba.
- Obyektlar: OquvReja, Baholar, Bayonnomalar, IshRejalari, Elonlar.
- Xususiyat: Kotib bayonnomani yozadi, mudir tasdiqlagach uni hech kim o‘zgartira olmaydi. Nega DAC yetarli emas? Chunki DAC da egasi ruxsatni yana o‘zgartirishi mumkin. Yechim: **WORM** yoki Linuxda o‘zgarmaslik atributi: `sudo chattr +i bayonnoma.pdf`.

---

## 8. NAZORAT SAVOLLARI VA ILMIY-AMALIY JAVOBLAR

### A) Laboratoriya Ishining 10 Ta Nazorat Savoliga Javoblar:

1. **Subyekt, obyekt va amal tushunchalarini ta’riflang va OT dagi misollarini keltiring.**
   - *Subyekt:* Murojaat qiluvchi faol mohiyat (Linuxda UID/GID va jarayon; Windowsda SID va Token).
   - *Obyekt:* Himoyalanadigan resurs (Linuxda Inode/fayl/katalog; Windowsda NTFS fayl).
   - *Amal:* Harakat turi (`read`, `write`, `execute`, `own`).
2. **Foydalanish matritsasi nega hech qachon butunligicha saqlanmaydi?**
   - Matritsa nihoyatda siyrak (sparse matrix). Kataklarning 99% dan ko‘prog‘i bo‘sh bo‘ladi. To‘liq saqlash xotirani zoe qiladi.
3. **ACL va C-list o‘rtasidagi farq nimada? Qaysi savolga qaysi tuzilma tez javob beradi?**
   - ACL — matritsaning ustuni, obyekt yonida saqlanadi. *«Bu faylga kim kira oladi?»* savoliga tez javob beradi.
   - C-list — matritsaning satri, subyekt olib yuradi. *«Bu foydalanuvchi nimalarga kira oladi?»* savoliga tez javob beradi.
4. **Murojaat monitorining uch xususiyatini sanab bering. 2-tajribada OT ning qaysi mexanizmi murojaatni tekshirdi?**
   - 1) Buzib bo‘lmaslik; 2) To‘liq vositachilik; 3) Tekshirilishi mumkinligi. 2-tajribada murojaatni Linux yadrosining VFS ruxsatlarni tekshirish moduli (`generic_permission`) tekshirdi.
5. **«Standart rad» tamoyili nimani anglatadi va monitor skriptida u qanday amalga oshirilgan?**
   - Ruxsatlar bazasida ochiq ruxsat berilmagan bo‘lsa — har qanday murojaat avtomatik rad etiladi. `monitor.sh` da katak bo‘sh bo‘lsa, natija avtomatik «RAD» bo‘ladi.
6. **Nega egalik (own) huquqi Full Control / root boshqaruviga mos keladi?**
   - Chunki egalik huquqi ruxsatlarni (ACL) o‘zgartirish va egalikni boshqa subyektga berish vakolatini o‘z ichiga oladi.
7. **Eng kam imtiyoz tamoyilini misol bilan tushuntiring.**
   - Subyektga faqat o‘z ishiga kerakli minimal huquq beriladi. Masalan, kutubxonachi hisobotni ko‘radi, lekin tasdiqlangan hisobotni o‘chira olmaydi.
8. **Nega «faqat o‘z yozuvini o‘qish» shartini papka ruxsatlari bilan ifodalab bo‘lmaydi?**
   - Chunki fayl tizimi ruxsatlari butun fayl yoki papka konteyneriga tatbiq etiladi, fayl ichidagi matn qatorlarini ajrata olmaydi. Buning uchun DBMS Row-Level Security (RLS) kerak.
9. **3-tajribada murojaat monitorining qaysi xususiyati xavf ostida edi va u qanday tiklandi?**
   - «Buzib bo‘lmaslik» (*Tamper-proof*) xavf ostida edi. U `matritsa.sh` faylini `root:root` ga o‘tkazib, `chmod 644` qilish orqali tiklandi.
10. **Siyosatdan chetlashishni o‘z vaqtida aniqlash uchun tashkilotda qanday jarayon kerak?**
    - Avtomatlashtirilgan xavfsizlik auditi, muntazam kirish huquqlarini qayta attestatsiyalash (Recertification) va File Integrity Monitoring (FIM — AIDE/Tripwire) tizimlari kerak.

### B) Taqdimotdagi (PPTX) 7 Ta Test Savoli Kaliti:
1. Reference monitor ilk bor: **B) Anderson hisoboti, 1972**
2. Har bir murojaat monitordan o‘tishi: **B) To‘liq vositachilik**
3. TCB nima: **C) Xavfsizlik siyosatini amalga oshiruvchi barcha komponentlar majmui**
4. Faqat brauzerda tekshirilsa: **B) To‘liq vositachilik buziladi**
5. «Faqat rahbar ko‘radi»: **C) Siyosat**
6. RBAC qaysi qatlam: **B) Model**
7. Eng kam imtiyoz: **B) Minimal zarur huquqlar**

---

## 9. YAKUNIY XULOSALAR, HISOBOTNI RASMIYLASHTIRISH VA BAHOLASH MEZONLARI

### 9.1. Laboratoriya Ishi Bo‘yicha Yakuniy Xulosalar
1. **Nazoratning markazlashuvi:** Har qanday tizimda xavfsizlik siyosati bitta markaziy bazada saqlanishi kerak. Tarqoq huquqlar tizimning boshqaruvini yo‘qotishga olib keladi.
2. **Linux VFS va POSIX ACL qudrati:** Ubuntu Serverda POSIX ACL mexanizmi orqali ko‘p foydalanuvchili murakkab tashkilot (Elektron kutubxona) siyosatini to‘liq amalga oshirish mumkin.
3. **Reference Monitor daxlsizligi:** Murojaat monitorining kodi va siyosat bazasi yozishdan qat'iy himoyalangan bo‘lishi (Tamper-proof) va hech qanday chetlab o‘tish yo‘li qolmasligi (Always invoked) axborot xavfsizligining mutlaq qoidasidir.

### 9.2. Hisobotni Rasmiylashtirish Tartibi
Talaba hisobot daftarini yoki PDF hujjatini quyidagi 6 ta bo‘lim bo‘yicha rasmiylashtiradi:
1. **Sarlavha:** F.I.Sh., guruh, sana, 1-variant «Elektron kutubxona».
2. **Maqsad va tashkilot tavsifi:** Kutubxona subyektlari va obyektlari.
3. **Nazariy qism:** 4 × 5 Matritsa, ACL, C-list va 3 ta katak bo‘yicha eng kam imtiyoz tahlili.
4. **Ubuntu Serverdagi natijalar:** `sozlash.sh`, `getfacl`, `tekshir.sh` va `monitor.sh` natijalari skrinshoti/matni.
5. **3 ta tajriba hisoboti:** Kuzatuv, qaysi tamoyil ishladi/buzildi, tuzatish usuli.
6. **Murojaat monitori tahlili (5 ta holat) va 3–5 gapli umumiy xulosa.**

### 9.3. Baholash Mezonlari (10 Ballik Tizim)
| Mezon | Ajratilgan Ball |
|---|:---:|
| Foydalanish matritsasi, ACL va C-list to‘g‘ri tuzilganligi | **2 ball** |
| Eng kam imtiyoz va qo‘shimcha shart tahlili asoslanganligi | **2 ball** |
| Matritsa Ubuntu Serverda (POSIX ACL) amalga oshirilgani va tekshirilgani | **3 ball** |
| 3 ta amaliy tajriba va murojaat monitori keyslari tahlili | **2 ball** |
| Tartibli hisobot va mustaqil xulosa | **1 ball** |
| **JAMI** | **10 BALL** |

---

## 10. TAVSIYA ETILGAN ILMIY VA TEXNIK MANBALAR

1. **Anderson, J. P. (1972).** *Computer Security Technology Planning Study.* ESD-TR-73-51.
2. **Lampson, B. W. (1971/1974).** *Protection.* ACM SIGOPS Operating Systems Review, 8(1), pp. 18-24.
3. **Saltzer, J. H., & Schroeder, M. D. (1975).** *The protection of information in computer systems.* Proceedings of the IEEE, 63(9), 1278-1308.
4. **Mark Stamp (2011).** *Information Security: Principles and Practice (2nd Ed).* John Wiley & Sons.
5. **Messaoud Benantar (2006).** *Access Control Systems: Security, Identity Management and Trust Models.* Springer.
6. **S.K. Ganiyev, M.M. Karimov, K.A. Tashev (2019).** *Axborot xavfsizligi.* Toshkent: «Fan va texnologiya».
7. **S.K. Ganiyev, A.A. Ganiyev, Z.T. Xudoyqulov (2021).** *Kiberxavfsizlik asoslari.* Toshkent: «Iqtisod-moliya».
8. **D.Y. Irgasheva, A.T. Imamaliyev, U. Tojiakbarova, N. Axmedova (2022).** *Foydalanishlarni boshqarish.* Toshkent: «Zebo Print».
9. **Linux Man Pages:** `acl(5)`, `setfacl(1)`, `getfacl(1)`.
10. **NIST SP 800-162:** *Guide to Attribute Based Access Control (ABAC).*
