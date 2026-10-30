# 📥 Anthem EOB Bulk Downloader

> A lightweight, 100% private browser console script to bulk-download all your Anthem Blue Cross Explanation of Benefits (EOB) statements in one go — before Anthem purges your 24-month claims history.

No extension. No dependencies. No install. Just paste it into your browser's developer console and run it.

🎥 **Watch the 2-Minute Walkthrough:** [YouTube Video Link]

---

## Table of Contents
- [Why This Matters (The 24-Month Cutoff)](#why-this-matters-the-24-month-cutoff)
- [What It Does](#what-it-does)
- [Step-by-Step Instructions](#step-by-step-instructions)
- [Configuration Options](#configuration-options)
- [Security & Privacy Guarantee](#security--privacy-guarantee)
- [How to Generate Scripts for Other Insurers (Gemini Prompt)](#how-to-generate-scripts-for-other-insurers-gemini-prompt)
- [Disclaimer](#disclaimer)
- [License](#license)

---

## Why This Matters (The 24-Month Cutoff)

If you use a **Health Savings Account (HSA)** for long-term triple-tax-advantaged growth, you need both your payment receipts and official insurance **Explanation of Benefits (EOB)** statements as IRS audit proof when you reimburse yourself years down the road.

**The Problem:** Anthem Blue Cross automatically purges claims history after **24 months**, and their member portal offers **no bulk download button**. Downloading 50+ claims manually requires clicking every single link one by one.

**The Solution:** This lightweight script automates the tedious clicking directly inside your browser console in safe, rate-limited batches.

---

## What It Does

- Automatically identifies all **"Download EOB"** buttons on the Anthem page using Anthem's official table test ID (`data-testid="claims.eobSummaryTable.table-download-button"`).
- Clicks through them in paced batches (default: 20 files at a time).
- Waits **2 seconds** between clicks and takes a **10-second pause** between batches so the Anthem server does not rate-limit or block you.
- Logs live progress to the console (`[1/23] Clicked: Download EOB...`) so you can track download progress in real time.
- Runs 100% locally in your browser tab — zero external network requests, zero tracking, nothing sent to third-party servers.

---

## Step-by-Step Instructions

1. **Log in to Anthem:** Open [member.anthem.com](https://member.anthem.com) in Chrome, Edge, or Firefox.
2. **Open EOB Center:** Go to **Claims & Payments** > **Explanation of Benefits Center**.
3. **Select Date Range:** Choose **24 Months** to grab everything Anthem still retains (or **12 Months** for annual backups) and click **Apply Filters**.
4. **Open Developer Tools Console:**
   - **Mac:** Press `Cmd + Option + J` (or go to **View** > **Developer** > **JavaScript Console**)
   - **Windows:** Press `Ctrl + Shift + J` (or `F12`)
   *(If Chrome blocks pasting, type `allow pasting` and press Enter).*
5. **Paste and Run:** Copy the code from [`code`](code) into the console and hit **Enter**.
6. **Allow Multiple Downloads:** When your browser prompts:
   > *"This site attempted to download multiple files automatically"*  
   Select **Always allow** and click **Done**.

Downloads will stream directly into your default `Downloads` folder!

---

## Configuration Options

You can easily adjust the timing variables at the bottom of the script if you have a faster or slower connection:

```javascript
// Every 20 downloads, pause for 10 seconds; otherwise, wait 2 seconds
if ((i + 1) % 20 === 0) {
  console.log(`Processed ${i + 1} items. Pausing for 10 seconds to avoid rate limiting...`);
  await delay(10000); // Pause duration between batches (in ms)
} else {
  await delay(2000);  // Delay between individual clicks (in ms)
}
```

---

## Security & Privacy Guarantee

- **Zero Tracking:** The script contains no external URLs, API calls, or analytics scripts.
- **Client-Side Only:** Runs entirely inside your browser's local sandbox.
- **No PHI Read:** The code only simulates mouse clicks on download buttons; it does not read, store, or transmit your protected health information (PHI) or personal claim details.

---

## How to Generate Scripts for Other Insurers (Gemini Prompt)

If your insurance provider is **Aetna, UnitedHealthcare, Cigna, or Blue Shield**, you can use Google Gemini to write a custom script in under 1 minute:

1. Right-click any "Download" button on your insurance portal and choose **Inspect**.
2. Right-click the highlighted `<button>` element > **Copy** > **Copy element**. *(Only copy the button element to protect your personal privacy!)*
3. Go to [gemini.google.com](https://gemini.google.com) and paste this prompt:

```text
Write a vanilla JavaScript console script that finds all download buttons matching this element:
[PASTE COPIED BUTTON ELEMENT]

Add a 2-second delay between each click, and a 10-second pause after every 20 downloads to avoid server rate limits. Do not use external libraries or send data anywhere.
```

If your portal splits claims across multiple pages, inspect the "Next Page" button as well, and prompt Gemini to click "Next Page" and repeat the process.

---

## Disclaimer

This project is an independent open-source automation utility for personal recordkeeping. It is not affiliated with, authorized, maintained, or endorsed by Anthem Blue Cross, Elevance Health, or any of their affiliates. Use responsibly and in accordance with your portal's terms of service.

---

## License

MIT License © 2026 KrishG28