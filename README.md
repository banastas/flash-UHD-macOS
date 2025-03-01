# 📀 Flashing a UHD Drive on macOS
**Last Updated: 2025-03-01**

I spent **3+ hours** trying to get this to work, so I wanted to make a **quick guide** for anyone flashing a **UHD Blu-ray drive on macOS**.

There are **GUI tools for Windows**, but they **did not work for me** — even with **Parallels**.

The **steps below did work for me**, and I hope they **save you frustration**.

---

## 🛠 **1️⃣ Acquire a UHD Drive**
Your best bet is to check the **MakeMKV forums** to find a **compatible drive**:  
🔗 [Ultimate UHD Drives Flashing Guide Updated 2025](https://forum.makemkv.com/forum/viewtopic.php?f=16&t=19634)

I chose the **LG BP60NB10 External Drive**:  
👉 [Amazon Link](https://amzn.to/4gZl18F)

---

## 🖥 **2️⃣ Install MakeMKV**
Download and install **MakeMKV** from the official site:  
🔗 [https://www.makemkv.com/](https://www.makemkv.com/)

---

## 🔍 **3️⃣ Identify Your UHD Drive**
With your UHD drive **connected**, open **Terminal** and run:

```
makemkvcon f -l
```

If you get a "command not found" error, you may need to update your shell path. Google how to add MakeMKV binaries to your system $PATH.

Once the command works, your output should look something like this:
```
Found 1 drives(s)
00: /IOBDServices/7296B36D, /dev/rdisk20, /dev/rdisk20
  HL-DT-ST_BD-RE_BP60NB10_1.02_212107081556_SIM04OBLC3053
```

---


## 🔽 **4️⃣ Get the Correct Firmware**
	
1.	Open MakeMKV and select your drive from the dropdown.
2.	Check the firmware version and product ID (write these down).
3.	Find the right firmware:
 - Use the MakeMKV forums to locate the UHD-friendly firmware for your exact drive model.
 - [This guide](https://forum.makemkv.com/forum/viewtopic.php?f=16&t=19634) is a great place to start.

⚠️ WARNING:
 - ❌ Flashing the wrong firmware can brick your drive!
 - ✅ Double-check before proceeding.

---

## 🔗 **5️⃣ Download sdf.bin**

MakeMKV requires an additional file to flash your drive.

Download sdf.bin from the official MakeMKV site:
🔗 https://makemkv.com/sdf.bin

📂 Move sdf.bin and your firmware into the same folder.
When I did this, I created a folder called **MKV** on my Desktop.

---

## 🚀 **6️⃣ Flash the Firmware**

This step was where I got stuck for hours - the original command I was running looked like it worked, but the firmware never updated.

Here's the correct command that worked for me on the first try:

```
sudo makemkvcon f -d '/IOBDServices/F7A19655' -f ~/Desktop/MKV/sdf.bin rawflash enc -i ~/Desktop/MKV/DE_LG_BP60NB10_1.02-MK.bin
```
#### 🚀 Important Notes:
 - Replace F7A19655 with your own drive identifier from Step 3.
 - The *rawflash enc* flag ensures the flash actually applies.
 - DO NOT interrupt the flashing process!

---

## ✅ **7️⃣ Verify the Firmware Update**

After flashing, check if it worked by running:
```
makemkvcon f -l
```

Then, open MakeMKV and check the info tab when the drive is selected from the dropdown.
 - ✅ "Firmware Type" should say "Patched"
 - ✅ LibreDrive Status should say "Enabled"

---

## 📀 **8️⃣ Test UHD Playback**

Pop in a UHD Blu-ray and test ripping. 🎉
If your drive does not read UHD discs, try:
 - Unplugging & replugging the drive.
 - Restarting MakeMKV.
 - Flashing 1.00-MK before 1.02-MK (some drives need a downgrade first).

---

## 🔥 **Final Thoughts**

This method worked flawlessly on macOS, and I hope it helps others avoid the same headaches I had.

Feel free to submit a pull request if you find improvements!
