# הוראות העלאת נתונים ל-Firebase

## שלב 1: גישה ל-Firebase Console
1. פתח את [Firebase Console](https://console.firebase.google.com)
2. בחר בפרויקט **hours-73365**
3. עבור ל-**Realtime Database** בתפריט הצד

## שלב 2: ניקוי נתונים ישנים (חשוב!)
**לפני** העלאת ה-JSON החדש, צריך למחוק את הנתונים הישנים:

1. ב-Realtime Database, לחץ על **users**
2. לחץ על ה-**X** (מחק) ליד **users**
3. אשר את המחיקה

## שלב 3: העלאת הנתונים החדשים
1. לחץ על **⋮** (שלוש נקודות) בשורש של ה-Database
2. בחר **Import JSON**
3. בחר את הקובץ `firebase-users.json`
4. לחץ **Import**

## שלב 4: אימות הנתונים
אחרי ההעלאה, וודא שהמבנה נראה כך:

```
users/
  ├── papasnir@gmail_com/
  │   ├── name: "שניר דואני"
  │   ├── fullName: "שניר דואני"
  │   ├── role: "instructor"
  │   └── subjects: {...}
  │
  ├── snirdoani@gmail_com/
  │   ├── name: "שניר דואני רכז"
  │   ├── fullName: "שניר דואני רכז"
  │   ├── role: "coordinator"
  │   ├── managedSubjects: [...]
  │   ├── assignedInstructors: [
  │   │     {
  │   │       email: "papasnir@gmail.com",
  │   │       subjects: ["כימיה", "מחשבים"]
  │   │     },
  │   │     {
  │   │       email: "snirdoani2@gmail.com",
  │   │       subjects: ["מחוננים"]
  │   │     }
  │   │   ]
  │   └── subjects: {...}
  │
  ├── snirdoani2@gmail_com/
  │   └── ...
  │
  └── 1technoda1@gmail_com/
      └── ...
```

## שלב 5: בדיקת המערכת
1. **כרכז** (snirdoani@gmail.com):
   - התחבר למערכת
   - וודא שאתה רואה את המדריכים המשויכים
   - נסה לשייך מדריך חדש עם מקצוע ספציפי

2. **כמדריך** (papasnir@gmail.com):
   - התחבר למערכת
   - **רענן את הדף** (F5)
   - פתח את Console (F12)
   - חפש את ההודעות:
     ```
     === INSTRUCTOR SUBJECT LOADING ===
     Instructor email: papasnir@gmail.com
     Checking coordinator: snirdoani@gmail.com
     ```
   - וודא שבטבלת השעות מופיעים **רק** המקצועות שהרכז שייך (כימיה ומחשבים)

3. **כמדריך** (snirdoani2@gmail.com):
   - התחבר למערכת
   - וודא שמופיע **רק** מקצוע "מחוננים"

## פתרון בעיות

### אם המדריך רואה את כל המקצועות:
1. בדוק ב-Firebase Console שהשדה `assignedInstructors` הוא מערך של אובייקטים עם `email` ו-`subjects`
2. וודא שהשדה `subjects` של המדריכים ריק (`morning: []`, `afternoon: []`)
3. רענן את הדף (CTRL+F5 לניקוי cache)
4. בדוק את ה-Console log

### אם השיוך לא עובד דינמית:
- השינויים יופיעו רק אחרי רענון הדף
- המערכת טוענת את הנתונים רק בעת התחברות/רענון

### אם יש שגיאת הרשאה:
- וודא שהאימייל נמצא ב-Firebase עם הפורמט הנכון: `user@domain_com` (עם קו תחתון במקום נקודה)
