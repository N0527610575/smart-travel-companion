# ✈️ Smart Travel Companion

> **העוזר האוטונומי החכם לטיסות ונסיעות הפועל בגישת Offline-First מוחלטת עם היתוך חיישנים (Sensor Fusion).**

[![GitHub Pages](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-0ea5e9?style=for-the-badge&logo=github&logoColor=white)](https://n0527610575.github.io/apptravelorgenize/)
[![Offline First](https://img.shields.io/badge/Architecture-100%25%20Offline--First-10b981?style=for-the-badge&logo=pwa&logoColor=white)](#-offline-first-architecture)
[![Sensor Fusion](https://img.shields.io/badge/Core-Sensor%20Fusion%20Engine-38bdf8?style=for-the-badge&logo=android&logoColor=white)](#-חיישנים-ו-sensor-fusion)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

---

## 🌐 אתר האפליקציה ודף הנחיתה החי
דף הנחיתה הרשמי והסימולטור האינטראקטיבי זמינים באוויר בכתובת:  
👉 **[https://n0527610575.github.io/apptravelorgenize/](https://n0527610575.github.io/apptravelorgenize/)**

---

## 📖 אודות הפרויקט (Overview)

**Smart Travel Companion** היא אפליקציית סמארטפון חדשנית שנבנתה מתוך ההבנה ששדות תעופה, מטוסים ומעברי גבול הם המקומות שבהם חיבור האינטרנט הוא הכי פחות אמין ויקר ביותר. 

במקום לחפש צילומי מסך בגלריה, לחטט בקבצי PDF בתיקיות או להיאבק עם Wi-Fi מקרטע בשדה התעופה – האפליקציה **מזהה בעצמה את שלב המסע** שבו אתה נמצא באמצעות היתוך חיישנים מתקדם ומקפיצה את המסמך המדויק אל מסך הנעילה.

---

## 🚀 פיצ'רים עיקריים (Core Features)

### 1. 🎛️ היתוך חיישנים חכם (Sensor Fusion)
* **חיישן ברומטר (מד לחץ אוויר):** מזהה שינויים בדיחוס תא הנוסעים (Cabin Depressurization). ירידה לרמת ~780 hPa מעידה על המראה ושיוט, ועלייה חזרה ל-~1013 hPa מעידה על נחיתה ביעד.
* **גידור גיאוגרפי (Geofencing & Beacons):** זיהוי קרבה לשערי עלייה למטוס (Boarding Gates) ולנמלי תעופה ללא תלות ב-GPS לווייני רציף.
* **מד תאוצה (Accelerometer):** אימות רגעי האטה פתאומית (Touchdown) של גלגלי המטוס על המסלול להפעלת פרוטוקול הגעה.

### 2. 📴 ארכיטקטורת Offline-First מוחלטת
* **אפס תלות בענן:** כל הפעולות, החישובים, האלגוריתמים והמסמכים מנוהלים מקומית בלבד.
* **פרטיות ברמת חומרה:** דרכונים, מספרי הזמנה וכרטיסים אינם נשלחים לעולם לשרתים חיצוניים.
* **חיסכון קיצוני בסוללה:** אלגוריתם דגימה אדפטיבי מבוסס שינויי מומנטום שאינו מרוקן את הסוללה.

### 3. 🔍 סריקה ופענוח מקומיים (Auto-Scan & Local OCR)
* סריקת קובצי PDF ותמונות ישירות מתיקיית ה-Downloads במכשיר.
* פענוח מהיר של ברקודים תקניים: **PDF417** (כרטיסי עלייה למטוס IATA), **Aztec**, ו-**QR Codes**.
* חילוץ מועדי טיסות, מספרי הזמנת מלון, וכרטיסי נסיעה ללא חיבור רשת.

### 4. 🗺️ ציר זמן ומסלול דינמי (Dynamic Itinerary)
* בנייה אוטומטית של רצף הנסיעה: משדה המוצא, שער העלייה, שעות הטיסה, ועד ההסעה והמלון ביעד.
* עדכון דינמי של שלבי המסלול גם אם יש עיכובים במהלך הטיסה.

---

## 🛠️ ארכיטקטורת המערכת (System Architecture)

```
┌─────────────────────────────────────────────────────────────┐
│                    On-Device Sensors                        │
│   [ Barometer ]       [ Accelerometer ]     [ Geofence ]    │
└───────────┬───────────────────┬─────────────────────┬───────┘
            │                   │                     │
            ▼                   ▼                     ▼
┌─────────────────────────────────────────────────────────────┐
│                 Sensor Fusion Logic Engine                  │
│       Detects: Ground ➔ Gate ➔ Takeoff ➔ Cruise ➔ Landing   │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                 Local Storage & OCR Engine                  │
│        (PDF417, QR, Aztec, Boarding Passes, Vouchers)       │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                   Autonomous Trigger UI                     │
│         Pop-up Right Document at the Exact Second           │
└─────────────────────────────────────────────────────────────┘
```

---

## 💻 מבנה הקבצים (Repository Structure)

```bash
apptravelorgenize/
├── docs/                 # קבצי דף הנחיתה עבור GitHub Pages
│   └── index.html        # דף הנחיתה הרספונסיבי עם הסימולטור
├── src/                  # קוד המקור של אפליקציית המובייל
├── assets/               # נכסים גרפיים ואייקונים
├── README.md             # תיעוד הפרויקט
└── LICENSE               # רישיון קוד פתוח (MIT)
```

---

## 🏃‍♂️ הרצה וצפייה מקומית בדף הנחיתה

לצפייה מקומית בדף הנחיתה ללא שרת חיצוני:
```bash
# נווט לתיקיית הדוקומנטציה
cd docs

# פתח ישירות בדפדפן (macOS)
open index.html

# או הרץ שרת מקומי קל
npx serve .
# או
python3 -m http.server 8000
```

---

## 🤝 תרומה לפרויקט (Contributing)

הצעות לשיפור, דיווחי באגים ו-Pull Requests יתקבלו בברכה!
1. צור Fork למאגר.
2. צור ענף חדש (`git checkout -b feature/amazing-feature`).
3. בצע Commit לשינויים (`git commit -m 'Add amazing feature'`).
4. בצע Push לענף (`git push origin feature/amazing-feature`).
5. פתח Pull Request מסודר.

---

## 📄 רישיון (License)

פרויקט זה מופץ תחת רישיון MIT. לפרטים נוספים ראה קובץ [LICENSE](LICENSE).

---

<p align="center">
  פותח בגאווה ע"י <strong><a href="https://github.com/N0527610575">N0527610575</a></strong> 🛫
</p>

