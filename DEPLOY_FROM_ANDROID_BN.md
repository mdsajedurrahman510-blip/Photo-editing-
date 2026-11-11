# Android মোবাইল থেকে ওয়েবসাইট অনলাইনে প্রকাশ

এই নির্দেশিকা ধরে নেওয়া হয়েছে তোমার কাছে `ai-photo-studio-pro-upgraded.zip` ফাইলটি আছে এবং তুমি Android Chrome ব্যবহার করছ। কোডিং না জানলেও ধাপে ধাপে করা যাবে, তবে একবারে সব কাজ না করে প্রতিটি ধাপ শেষ করে পরের ধাপে যাবে।

## ১. ZIP ফাইল Extract করো

1. Android-এর Files / My Files অ্যাপ খুলে ZIP ফাইলটি খুঁজে বের করো।
2. Extract / Unzip চাপো।
3. `ai-photo-studio-pro` নামের ফোল্ডারটি তৈরি হবে।
4. ভেতরে `package.json`, `src`, `public`, `engine` এবং README ফাইল আছে কি না দেখো।

## ২. GitHub Repository তৈরি করো

1. Chrome-এ `https://github.com` খোলো এবং সাইন ইন করো।
2. `+` → `New repository` চাপো।
3. নাম দাও `ai-photo-studio-pro`।
4. Repository private রাখাই ভালো, কারণ প্রজেক্টে ব্যক্তিগত কনফিগারেশন থাকতে পারে। `.env.local` কখনো আপলোড করবে না।
5. Create repository চাপো।

## ৩. সোর্স ফাইল GitHub-এ আপলোড

GitHub-এর মোবাইল ওয়েবসাইটে repository খুলে `Add file` → `Upload files` ব্যবহার করো। ZIP ফাইলটি নিজে নিজে extract হবে না—প্রজেক্টের ভেতরের ফাইলগুলো তাদের ফোল্ডার-স্ট্রাকচার ঠিক রেখে আপলোড করতে হবে। Android-এর file picker-এ ফোল্ডার একসঙ্গে আপলোড করা না গেলে এই ধাপটি মোবাইলে ঝামেলাপূর্ণ হতে পারে; তখন GitHub Codespaces বা কম্পিউটার ব্যবহার করে repository-তে extracted project push করা সহজ হবে।

গুরুত্বপূর্ণ: repository root-এ সরাসরি `package.json`, `src/`, `public/`, `engine/` থাকতে হবে। `ai-photo-studio-pro/ai-photo-studio-pro/package.json` এমন nested folder যেন না হয়।

## ৪. Vercel-এ Frontend Deploy

1. `https://vercel.com` খোলো।
2. GitHub দিয়ে সাইন ইন করো।
3. `Add New` → `Project` চাপো।
4. `ai-photo-studio-pro` repository Import করো।
5. Framework হিসেবে Next.js শনাক্ত হলে ডিফল্ট Build Settings রাখো।
6. Deploy চাপো।
7. সফল হলে Vercel একটি `*.vercel.app` ঠিকানা দেবে।

এই ধাপে Browser Photo Editor, basic enhancement, passport print sheet, paired canvas এবং batch ZIP export ব্যবহার করা যাবে।

## ৫. ঐচ্ছিক Python Engine

Background removal এবং OpenCV server-side processing চালাতে আলাদা Python Engine host দরকার। শুধু Vercel Frontend deploy করলেই Python Engine চলবে না। `engine/` ফোল্ডারের Dockerfile বা `engine/main.py` ব্যবহার করে Python host-এ চালাতে হবে। তারপর Vercel-এর Environment Variables-এ `PHOTO_ENGINE_URL` দিতে হবে এবং redeploy করতে হবে।

ফ্রি প্ল্যাটফর্মে GPU বা সবসময় চালু থাকা সার্ভার নিশ্চিত নয়। কোনো পাবলিক Python engine deploy করলে authentication, rate limiting এবং HTTPS যোগ না করে ব্যক্তিগত ছবি আপলোড করো না।

## ৬. মোবাইলে অ্যাপের মতো ব্যবহার

Vercel URL Chrome-এ খুলে `⋮` → `Add to Home screen` চাপো। এতে ফোনের হোম স্ক্রিনে শর্টকাট আসবে। একই URL কম্পিউটারের Chrome/Edge-এ খুললেও ব্যবহার করতে পারবে।

## সতর্কতা

- Browser-side file data reload করলে হারিয়ে যায়; আবার আপলোড করতে হবে।
- বড় ছবি বা অনেক ছবি মোবাইলে একসঙ্গে প্রসেস না করে sequential batch চালাও।
- Browser fallback AI generative restoration নয়; এটি classical photo finishing।
- Paired canvas-এর মাপ হলো দুজনকে একসঙ্গে রাখা সম্পূর্ণ ছবির মাপ, প্রত্যেক ব্যক্তির আলাদা passport crop নয়।
