# iPhone 15 → Windows PC Backup (Safe Method)

This guide safely copies all photos and videos from your iPhone DCIM folder to:

C:\iPhone_Backup

using PowerShell with verification.

---

## STEP 0 – Prepare iPhone

1. Unlock iPhone
2. Connect with USB cable
3. Tap "Trust This Computer"
4. Enter passcode
5. Settings → Display & Brightness → Auto Lock → Set to Never (temporarily)
6. Keep screen ON during transfer

If phone locks, transfer may stop.

---

## STEP 1 – Confirm iPhone Is Visible

Open File Explorer and confirm:

This PC  
└── Apple iPhone  
  └── Internal Storage  
    └── DCIM  

If DCIM opens, continue.

---

## STEP 2 – Create Backup Folder

Open PowerShell as Administrator and run:

```powershell
mkdir C:\iPhone_Backup
```

---

## STEP 3 – Copy All Files Safely

Run:

```powershell
robocopy "This PC\Apple iPhone\Internal Storage\DCIM" "C:\iPhone_Backup" /E /Z /R:3 /W:5 /V /TEE /LOG:C:\iphone_copy_log.txt
```

Explanation:

/E  → Copy all subfolders  
/Z  → Restartable mode  
/R:3 → Retry 3 times  
/W:5 → Wait 5 seconds  
/V  → Verbose output  
/TEE → Show progress  
/LOG → Save transfer log  

Do not disconnect cable during transfer.

---

## STEP 4 – Verify File Count

Count files on iPhone:

```powershell
(Get-ChildItem "This PC\Apple iPhone\Internal Storage\DCIM" -Recurse -File).Count
```

Count files in backup:

```powershell
(Get-ChildItem "C:\iPhone_Backup" -Recurse -File).Count
```

If both numbers match, backup is successful.

---

## STEP 5 – Check Backup Size (Optional)

```powershell
(Get-ChildItem "C:\iPhone_Backup" -Recurse | Measure-Object -Property Length -Sum).Sum / 1GB
```

This shows total backup size in GB.

---

## Log File Location

C:\iphone_copy_log.txt

---

## Final Result

All photos and videos from:

This PC\Apple iPhone\Internal Storage\DCIM

are copied to:

C:\iPhone_Backup
