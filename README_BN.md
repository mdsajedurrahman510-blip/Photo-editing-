# AI Photo Studio Pro — বাংলা সেটআপ গাইড

এই প্রজেক্টটি মোবাইল ও কম্পিউটারের ব্রাউজারে ব্যবহারযোগ্য Photo-only ওয়েব অ্যাপ। ভিডিও ফিচার বাদ দেওয়া হয়েছে।

## অ্যাপটি কী করতে পারে

1. JPG, PNG ও WebP ছবি আপলোড।
2. মোবাইল/ব্রাউজারেই বাস্তব Basic Photo Enhancement: Adaptive Exposure, Brightness, Contrast, মৃদু Noise Softening ও Conservative Sharpening।
3. একসঙ্গে একাধিক ছবি ধারাবাহিকভাবে প্রসেস করে ZIP ডাউনলোড।
4. একজনের পাসপোর্ট সাইজের প্রিন্ট শিট তৈরি।
5. দুইজন একসঙ্গে থাকা ছবিকে নির্দিষ্ট mm ও DPI-র Paired Photo Canvas-এ সাজানো।
6. ঐচ্ছিক Python/OpenCV সার্ভার যুক্ত করা।

**সীমাবদ্ধতা:** built-in browser processing হলো classical/non-generative processing; এটি Remini-এর AI face restoration নয়। Background removal চালাতে Python engine এবং `rembg` মডেল ইনস্টল থাকতে হবে। Free hosting-এ স্থায়ী GPU বা শক্তিশালী AI সার্ভার নিশ্চিত নয়।

## মোবাইল দিয়ে ব্যবহার

ওয়েবসাইট Deploy হলে Android Chrome-এ লিংক খুলবে। তারপর Chrome-এর `⋮` মেনু থেকে `Add to Home screen` বা `Install app` চাপবে। এতে হোম স্ক্রিনে অ্যাপের মতো শর্টকাট হবে।

## Developer সেটআপ

প্রজেক্টে Node.js 20.9+ এবং npm দরকার।

```bash
npm install
npm run dev
```

তারপর `http://localhost:3000` খুলবে।

Python engine আলাদাভাবে চালাতে:

```bash
pip install -r engine/requirements.txt
uvicorn engine.main:app --host 0.0.0.0 --port 8000
```

`.env.local`-এ লিখবে:

```env
PHOTO_ENGINE_URL=http://127.0.0.1:8000
```

এরপর Next.js সার্ভার রিস্টার্ট করতে হবে।

## গুরুত্বপূর্ণ

- ছবি ব্রাউজার সেশনের মেমোরিতে থাকে; রিফ্রেশের পর আবার আপলোড করতে হবে।
- একাধিক বড় ছবি একসঙ্গে না চালিয়ে sequential batch ব্যবহার করো।
- Paired canvas-এ দেওয়া মাপ সম্পূর্ণ দুইজনের ছবির মাপ; প্রত্যেক ব্যক্তির আলাদা passport size নয়।
- সরকারি পাসপোর্টের নিয়ম দেশভেদে ভিন্ন। নির্দিষ্ট কর্তৃপক্ষের মাপ যাচাই করে প্রিন্ট করবে।
- জনসমক্ষে Python engine চালু করার আগে authentication, rate limiting ও HTTPS যোগ করতে হবে।
