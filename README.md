# Flashing UHD Blu‑ray Drives on macOS

## 1. Confirm Drive Compatibility
Consult the MakeMKV forum list of “UHD‑friendly” models. Example reference: [**LG BP60NB10**](https://amzn.to/4gZl18F).

## 2. Install MakeMKV
Download and install from <https://www.makemkv.com/>.

## 3. Identify the Drive
Connect the drive. In Terminal:
```bash
makemkvcon f -l
```
If you get a "command not found" error, you may need to update your shell path. Google how to add MakeMKV binaries to your system $PATH.

Once the command works, your output should look something like this:
```
Found 1 drives(s)
00: /IOBDServices/7296B36D, /dev/rdisk20, /dev/rdisk20
  HL-DT-ST_BD-RE_BP60NB10_1.02_212107081556_SIM04OBLC3053
```
Note the identifier returned (e.g., `/IOBDServices/7296B36D`) and current firmware version.

## 4. Obtain Correct Firmware
Find the exact patched firmware for your model and version on the [MakeMKV forum](https://forum.makemkv.com/forum/viewtopic.php?f=16&t=19634). Flashing the wrong file can brick the drive.

## 5. Prepare Files
Download `sdf.bin` from the [MakeMKV site](https://makemkv.com/sdf.bin).  
Place `sdf.bin` and the firmware file in the same directory.

## 6. Flash
```bash
sudo makemkvcon f -d '/IOBDServices/<ID>' -f /path/to/sdf.bin rawflash enc -i /path/to/<firmware>.bin
```
Replace `<ID>` and `<firmware>.bin`. Do not interrupt the process.

## 7. Verify
Run `makemkvcon f -l` again or open MakeMKV.  
`Firmware Type` should display **Patched** and **LibreDrive Enabled**.

## 8. Test
Insert a UHD disc and attempt a rip. If the drive fails to read, power‑cycle the drive or flash a downgrade firmware first, then upgrade.
