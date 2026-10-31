# 📋 Rivo Mobile App: Today's Sprint API Testing Checklist (Figma Gap Completion)

> **তারিখ:** ৩১ অক্টোবর, ২০২৬  
> **গিট ব্রাঞ্চ (Backend):** `feature/figma-gap-completion`  
> **ব্রুনো কালেকশন (Bruno):** `main` ব্রাঞ্চ (`D:\Docker\GitHub\rivo\bruno-rivo-api\Rivo-api`)  
> **ব্যবহার নির্দেশিকা:** ব্রুনোতে প্রতিটি এপিআই টেস্ট করার সময় এই চেকলিস্টটি ব্যবহার করুন। টেস্ট সফল হলে চেকবক্স টিক `[x]` করুন।

---

## 🔑 গ্লোবাল ব্রুনো ভ্যারিয়েবলস ও হেডারস (Global Variables & Headers)

| হেডার / ভ্যারিয়েবল | মান (Value) | বিবরণ |
| :--- | :--- | :--- |
| `base_url` | `http://10.10.28.53:80/api` (বা `http://localhost:81/api`) | ব্যাকএন্ড এপিআই বেস ইউআরএল |
| `Accept` | `application/json` | JSON রেসপন্স নিশ্চিত করার জন্য |
| `Authorization` | `Bearer {{userSarah}}` (বা `{{userToken}}`) | টেস্ট ইউজার সারা'র Sanctum অথ টোকেন |
| `petId` | `1` | পেড্রো'র (Pedro) আইডি |

---

## 🐾 PART 1: Pet Training & Guided Tutorials (প্রশিক্ষণ মডিউল — ৭টি API)

Figma স্ক্রিন: `train_tutorial_screens.png` (Training Academy, ক্যাটালগ ও স্টেপ-বাই-স্টেপ গাইডেন্স)

- [ ] **01. GET** `/api/v1/training/home/:pet`
  - **ব্রুনো ফাইল:** `Pet Training/Get Training Home.yml`
  - **কাজ:** পেটের বর্তমান ট্রেইনিং লেভেল, স্ট্রিক, Gold III র‍্যাঙ্ক, TP প্রগ্রেস এবং প্রস্তাবিত লেসন দেখা।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **02. GET** `/api/v1/training/categories`
  - **ব্রুনো ফাইল:** `Pet Training/Get Categories.yml`
  - **কাজ:** ট্রেইনিং ক্যাটালগ ক্যাটাগরি তালিকা (Basic Commands, Leash Walking, Fun Tricks, Behavior & Barking) এবং সক্রিয় লেসন কাউন্ট দেখা।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **03. GET** `/api/v1/training/lessons`
  - **ব্রুনো ফাইল:** `Pet Training/List Lessons.yml`
  - **প্যারামিটার (ঐচ্ছিক):** `filter[category_id]`, `filter[difficulty]` (`beginner`, `intermediate`, `advanced`), `filter[is_plus_only]`, `sort=order_column`
  - **কাজ:** লেসন ফিল্টারিং ও ব্রাউজিং।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **04. GET** `/api/v1/training/lessons/:lesson`
  - **ব্রুনো ফাইল:** `Pet Training/Get Lesson Step-by-Step.yml`
  - **কাজ:** লেসনের ধাপে ধাপে নির্দেশিকা, টেক্সট নির্দেশনা, স্টেপ ইমেজ ও অডিও কিউ (যেমন: ক্লিকার বা কমান্ড প্রম্পট)।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **05. POST** `/api/v1/training/pets/:pet/lessons/:lesson/complete`
  - **ব্রুনো ফাইল:** `Pet Training/Complete Lesson.yml`
  - **বডি (JSON):**
    ```json
    {
      "rating": 5,
      "notes": "Pedro learned sit command in 10 minutes!"
    }
    ```
  - **কাজ:** লেসন সম্পন্ন করা, পেটের ট্রেনিং স্ট্যাটাস আপডেট, TP/XP রিওয়ার্ড যোগ এবং দৈনিক ট্রেনিং স্ট্রিক বৃদ্ধি করা।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **06. POST** `/api/v1/training/pets/:pet/lessons/:lesson/bookmark`
  - **ব্রুনো ফাইল:** `Pet Training/Toggle Lesson Bookmark.yml`
  - **কাজ:** পছন্দের লেসন বুকমার্ক করা বা বুকমার্ক তুলে নেওয়া (টগল)।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **07. GET** `/api/v1/training/pets/:pet/bookmarks`
  - **ব্রুনো ফাইল:** `Pet Training/Get Bookmarked Lessons.yml`
  - **কাজ:** বুকমার্ক করা সকল লেসনের তালিকা দেখা।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

---

## ⚡ PART 2: Pet Activity Dashboard & Multi-Streak Engine (অ্যাক্টিভিটি ও স্ট্রিক — ৩টি API)

Figma স্ক্রিন: `activity_dashboard_screen.png` ও `streaks_modals_detail.png`

- [ ] **08. GET** `/api/v1/pets/:pet/activity-dashboard`
  - **ব্রুনো ফাইল:** `Pet Activity/Get Pet Activity Dashboard.yml`
  - **কাজ:** 
    - লেভেল কার্ড: `Level 3` (XP প্রগ্রেস বার ও "70 XP to Level 4")
    - র‍্যাঙ্ক কার্ড: `Gold III` (৭০০/৭৭০ TP ও "70 to Gold II")
    - ৩টি মেট্রিক কার্ড: Walk Activity (`12.4 km`), Training (`3 sessions`), Care (`32 tasks`)
    - আজকের টাইমলাইন: কেয়ার টাস্ক, ওয়াক ও ট্রেনিং সেশনের ক্রোনোলজিক্যাল ইউনিফাইড ফিড ("Just now", "2 hours ago")
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **09. GET** `/api/v1/pets/:pet/streaks`
  - **ব্রুনো ফাইল:** `Pet Activity/Get Pet Streaks.yml`
  - **কাজ:** ৩টি ভিন্ন স্ট্রিক (Walk Streak, Training Streak, Care Streak) এবং প্রতিটি স্ট্রিকের জন্য রবিবার-শনিবার ৭ দিনের ডট ইন্ডিকেটর (`[S, M, T, W, T, F, S]`)।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **10. GET** `/api/v1/pets/:pet/streaks/:type`
  - **ব্রুনো ফাইল:** `Pet Activity/Get Single Streak.yml`
  - **পাথ ভ্যালু:** `walk`, `training`, অথবা `care`
  - **কাজ:** নির্দিষ্ট একটি স্ট্রিকের বিস্তারিত মডাল পপআপ ডেটা।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

---

## 🚨 PART 3: 24/7 Emergency Locator & SOS Mode (জরুরি সেবা ও ক্লিনিক লোকেটর — ৩টি API)

Figma স্ক্রিন: `emergency_mode_screen.png`, `emergency_contacts_screen.png`, `emergency_main_screen.png`

- [ ] **11. GET** `/api/v1/emergency/mode`
  - **ব্রুনো ফাইল:** `Emergency Vet/Get Emergency Mode Guidance.yml`
  - **কাজ:** 
    - রেড অ্যালার্ট ৫টি লাইফ-সেভিং ফার্স্ট-এইড স্টেপ (Stay calm, No human meds, Clear airway, Pressure on wounds, Careful transport)
    - ইউজারের প্রাইমারি ও সেকেন্ডারি বিশ্বস্ত ভেট ডাক্তারের কুইক-ডায়াল ফোন নম্বর
    - মেডিক্যাল ডিসক্লেইমার ব্যানার
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **12. GET** `/api/v1/emergency/clinics`
  - **ব্রুনো ফাইল:** `Emergency Vet/Locate Nearby 24-7 Clinics.yml`
  - **কুয়েরি প্যারামিটার:**
    - `latitude=37.7749&longitude=-122.4194&radius_km=30`
    - `filter[is_open_24_7]=1`
    - `filter[search]=Metropolitan` (ঐচ্ছিক সার্চ)
  - **কাজ:** Haversine স্পেয়ারিকাল জিও-ক্যালকুলেশন দিয়ে সবচেয়ে কাছের ২৪/৭ জরুরি পশু হাসপাতালগুলো ক্রমানুসারে দেখা, গুগল ম্যাপস ডিরেকশন লিংক ও স্পেশালাইজড সার্ভিসেস (`ICU`, `Emergency Surgery`, `Blood Bank`, `CT Scan`)।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **13. GET** `/api/v1/emergency/clinics/:clinic`
  - **ব্রুনো ফাইল:** `Emergency Vet/Get Clinic Details.yml`
  - **কাজ:** ক্লিনিকের ফুল প্রোফাইল, ডাক্তারদের টিম, হটলাইন এবং জরুরি সেবা সংক্রান্ত বিস্তারিত।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

---

## 💉 PART 4: Dedicated Pet Vaccination Records (ভ্যাক্সিনেশন ট্র্যাকিং — ৬টি API)

Figma স্ক্রিন: `health_care_screens.png` (ভ্যাকসিনেশন রেকর্ড, স্ট্যাটাস ব্যাজ ও সার্টিফিকেট)

- [ ] **14. GET** `/api/v1/pets/:pet/vaccinations`
  - **ব্রুনো ফাইল:** `Pet Vaccinations/Get Pet Vaccinations.yml`
  - **কুয়েরি প্যারামিটার (ঐচ্ছিক):**
    - `filter[status]=up_to_date` (বা `due_soon`, `overdue`)
    - `filter[vaccine_type]=core` (বা `non_core`, `lifestyle`)
    - `sort=due_at`
  - **কাজ:** পেটের সব টিকার তালিকা, রিয়েল-টাইম গণনা করা ব্যাজ (`Up to Date` Green, `Due Soon` Orange, `Overdue` Red) এবং সার্টিফিকেট ফাইল ইউআরএল।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **15. GET** `/api/v1/pets/:pet/vaccinations/summary`
  - **ব্রুনো ফাইল:** `Pet Vaccinations/Get Vaccination Summary.yml`
  - **কাজ:** 
    - টপ ড্যাশবোর্ড কার্ড: মোট ভ্যাকসিন সংখ্যা, আপ-টু-ডেট সংখ্যা, ডিউ সুন সংখ্যা, ওভারডিউ সংখ্যা
    - ওভারঅল ব্যাজ (`1 Vaccine Overdue` বা `All Up to Date`)
    - পরবর্তী ডিউ ভ্যাকসিনের কাউন্টডাউন ("Due in 18 days")
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **16. POST** `/api/v1/pets/:pet/vaccinations`
  - **ব্রুনো ফাইল:** `Pet Vaccinations/Record Pet Vaccination.yml`
  - **বডি (Multipart Form-Data):**
    - `name`: `Canine Influenza (H3N2/H3N8)`
    - `vaccine_type`: `non_core`
    - `administered_at`: `2026-10-31`
    - `due_at`: `2027-10-31`
    - `clinic_name`: `Downtown Animal Medical Center`
    - `veterinarian_name`: `Dr. Sarah Chen, DACVIM`
    - `batch_number`: `FLU-8820-K`
    - `notes`: `Bivalent canine influenza vaccine administered.`
    - `certificate`: *(ঐচ্ছিক ফাইল: PDF, JPG, PNG)*
  - **কাজ:** নতুন ভ্যাক্সিন রেকর্ড সেভ করা, SmartUpload দিয়ে ফাইল সংরক্ষণ এবং পেটের `is_vaccinated` স্ট্যাটাস অটো-সিঙ্ক।
  - **প্রত্যাশিত স্ট্যাটাস:** `201 Created`

- [ ] **17. GET** `/api/v1/pets/:pet/vaccinations/:vaccination`
  - **ব্রুনো ফাইল:** `Pet Vaccinations/Get Vaccination Details.yml`
  - **কাজ:** নির্দিষ্ট একটি ভ্যাকসিনের ফুল ডিটেইলস, লট নাম্বার ও সার্টিফিকেট ডাউনলোড লিংক দেখা।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **18. POST (or PUT)** `/api/v1/pets/:pet/vaccinations/:vaccination`
  - **ব্রুনো ফাইল:** `Pet Vaccinations/Update Pet Vaccination.yml`
  - **বডি (Multipart Form-Data):** নাম, নোটস বা রিপ্লেসমেন্ট সার্টিফিকেট ফাইল
  - **কাজ:** ভ্যাকসিনের তথ্য আপডেট করা। নতুন সার্টিফিকেট দিলে পুরনো ফাইলটি ডিস্ক থেকে স্বয়ংক্রিয়ভাবে মুছে যাবে (`HasUploadPurge`)।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

- [ ] **19. DELETE** `/api/v1/pets/:pet/vaccinations/:vaccination`
  - **ব্রুনো ফাইল:** `Pet Vaccinations/Delete Pet Vaccination.yml`
  - **কাজ:** ভ্যাক্সিনেশন রেকর্ড মুছে ফেলা এবং স্টোরেজ ডিস্ক থেকে সার্টিফিকেট পার্জ করা।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

---

## 🏥 PART 5: Health Vault Dashboard Integration (ইন্টিগ্রেশন চেক — ১টি API)

- [ ] **20. GET** `/api/v1/pets/:pet/health-vault/dashboard`
  - **ব্রুনো ফাইল:** `Health Vault/Get Dashboard.yml`
  - **কাজ:** হেলথ ভল্ট ড্যাশবোর্ডে নতুন ভ্যাক্সিনেশন সিস্টেম ইন্টিগ্রেট হয়েছে কি না যাচাই করা।
    - ১০০-পয়েন্টের হেলথ স্কোর ক্যালকুলেশনে ভ্যাক্সিনের ২০ পয়েন্ট সক্রিয় কি না দেখা (কোন ভ্যাকসিন ওভারডিউ থাকলে স্কোর কমবে)।
    - `vaccinations.upcoming_list` এবং `overall_badge` সঠিকভাবে আসছে কি না দেখা।
  - **প্রত্যাশিত স্ট্যাটাস:** `200 OK`

---

## 🧪 টেস্ট কভারেজ ও সিস্টেম স্ট্যাটাস

| ফিচার টেস্ট ফাইল | টেস্ট সংখ্যা | Assertions | স্ট্যাটাস |
| :--- | :--- | :--- | :--- |
| `tests/Feature/PetTrainingTest.php` | ৬টি টেস্ট | ৪৬টি | 🟢 **PASS (100%)** |
| `tests/Feature/PetActivityTest.php` | ৫টি টেস্ট | ১৪টি | 🟢 **PASS (100%)** |
| `tests/Feature/EmergencyClinicTest.php` | ৫টি টেস্ট | ৪৬টি | 🟢 **PASS (100%)** |
| `tests/Feature/PetVaccinationTest.php` | ৮টি টেস্ট | ৯০টি | 🟢 **PASS (100%)** |
| **সর্বমোট আজকের টেস্ট** | **২৪টি টেস্ট** | **১৯৬টি assertions** | 🟢 **সবগুলো সফল** |

---

### 💡 টেস্টিং টিপস:
1. টেস্ট ডাটা হিসেবে ডাটাবেজে **Pedro** (`pet_id = 1`) এবং ইউজার হিসেবে **Sarah** (`Bearer {{userSarah}}`) সিড করা আছে।
2. যদি ডাটা রিসেট বা রিসিড করতে চান, ডকারে রান করুন:
   ```bash
   docker exec rivo-app php artisan db:seed --class=TrainingSeeder
   docker exec rivo-app php artisan db:seed --class=ActivityAndStreakSeeder
   docker exec rivo-app php artisan db:seed --class=EmergencyClinicSeeder
   docker exec rivo-app php artisan db:seed --class=VaccinationSeeder
   ```
3. ব্রুনোর প্রতিটি রিকোয়েস্টে অলরেডি প্রয়োজনীয় প্যারামিটার ও ডকুমেন্টেশন যুক্ত করা আছে।
