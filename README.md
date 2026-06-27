# Kind Studio — LIFF Booking Demo

A single-file demo of the **LINE LIFF booking experience** for Kind Studio
(DIY hair-accessory workshop, Bangkok). Thai-first UI.

The core promise: **double-booking is structurally impossible.** Each class is
a fixed, non-overlapping 90-minute block — there's no way to create a 30-minute
overlap like the incident that started this project. Once a slot is booked it's
locked for everyone.

## Flow

1. **เลือกเวลา** — pick a date (next 14 days) and an available time block. Full
   slots are shown as `เต็ม` and can't be selected.
2. **ยืนยัน** — booking summary + PromptPay payment prompt.
3. **เสร็จสิ้น** — confirmation with a booking reference.

The customer's name and photo are pulled from their LINE profile via the LIFF
SDK — no manual form needed.

## Run it

Just open `index.html` in a browser. Outside the LINE app it runs in **DEMO
mode** (badge shown top-right, sample name used). Availability data is mocked.

## Make it live in LINE

1. In the [LINE Developers console](https://developers.line.biz/console/),
   create a LIFF app under Kind Studio's existing LINE OA channel.
2. Set the LIFF endpoint URL to wherever this is hosted (any static host —
   GitHub Pages, Netlify, Vercel, Firebase Hosting all work).
3. Copy the **LIFF ID** and paste it into `index.html`:

   ```js
   const LIFF_ID = "0000000000-XXXXXXXX"; // ← real LIFF ID here
   ```

4. Open the LIFF URL from inside LINE — it will use the real profile and the
   "ปิดหน้าต่าง" button will close the LIFF window.

## What's mocked vs. real (for the production build)

| Piece | Demo | Production |
|---|---|---|
| Availability | Hard-coded in `seedAvailability()` | Google Workspace (Sheet/Calendar) as the source of truth |
| Booking commit | Locks slot in-memory | POST to backend → write to Workspace |
| Confirmation | On-screen only | Gmail auto-confirmation email |
| Payment | PromptPay placeholder QR | Real PromptPay QR / amount |

These hooks are marked with comments in `index.html` (search for `production`).
