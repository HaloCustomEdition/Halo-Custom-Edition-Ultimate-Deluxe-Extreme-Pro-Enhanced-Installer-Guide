# Halo Custom Edition Ultimate Deluxe Extreme Pro Enhanced Installer Guide

A short and concise guide for installing Halo Custom Edition with the latest and greatest features.

## Download

Download and unzip the file bundles:

* [Hakunamakuba's Halo CE Installer Bundle](https://1drv.ms/u/s!AlL62iEz1c7E2IdqJMiWvElrJZsWGQ)
* [Hakunamakuba's Halo CE Custom Map Bundle](https://1drv.ms/u/s!AlL62iEz1c7E2Id_QX_N8atkTYvabw)

## Installation

* Open the `halo ce installer bundle` folder.

* Install `7z1805-x64.exe`.

7zip is required to unzip compressed files.

* Install `vcredist_x86.exe`.

Contains the latest C++ distributables.

* Install `dxwebsetup.exe`.

Contains the latest DirectX graphics software.

* Install `halocesetup_en_1.00.exe`.

The actual Halo CE game installer.

Use one of the following keys:

```
WWCXQ-QKQ4V-QRWKQ-YDVGJ-FCRYJ
G9QK2-22KV6-TFXCR-V3Y9M-2CCBJ
PGQTG-4X4J3-68M87-B28TR-J2CBJ
M4GHF-MMRWK-MW9BD-B76JK-6P8MJ
W4WMQ-BP7J4-YPV8D-9HYK3-KQTVW
RGGD9-BYCC4-6J6FV-VPJJQ-HCXHW
G9Qk2-22KV6-TFXCR-V3Y9M-2CCBJ
V84H7-J62Y4-HTMHK-RKH6T-BHXHW
T39RX-JH7Y2-XWTJD-VJX8X-G7MD8
FCM2T-3Q7FG-TXKGQ-KR4CD-FCGV3
PP6D8-F4MF3-3YTCQ-X8CKH-2FVQ8
QQ4MC-T48BC-CD69T-QKF9M-W3TVW
QMWM6-WVDMK-86Q86-BFC8X-JHCBJ
TRF2B-Y67K2-GV7RR-H4DCB-QDC7W
VHVG2-6DGXG-GCKHQ-VX2YH-4Q4YQ
W7VY8-86HKG-6MWFX-7PPH8-733KT
XBQDX-GRKCB-KQVMV-WRR9P-F2CBJ
41248-79455-34565-87945-68742
FRFW7-HH4B7-C9444-TR94F-QHXHY
G3T32-2HMJJ-7GTGX-VTRBX-GT27Y
J34HV-YYPM6-M3BH6-46037-VV338
KMCT7-2QKVF-4KV27-6P83J-THCBJ
K9TGM-K337P-JW24T-B9V73-C3TVW
8D69D-8BFB8-93949-5845F-FH686
KYKMH-JWWXQ-XG2HH-CPDFC-KX2BJ
```

* Install `haloce-patch-1.0.10.exe`.

Official Microsoft patch for Halo CE.

* Copy the `haloceded.exe` file to `C:\Program Files (x86)\Microsoft Games\Halo Custom Edition\`.

Patch for the dedicated server.

* Copy `haloce.exe` to `C:\Program Files (x86)\Microsoft Games\Halo Custom Edition\`.

This will disable cd key check in multiplayer games.

* Install `C:\Program Files (x86)\Microsoft Games\Halo Custom Edition\redist\msxmlenu.msi`.

Enables in-game chat.

* Unzip the `Universal_UI_Version_1.1.zip` and copy the `UI.map` file to `C:\Program Files (x86)\Microsoft Games\Halo Custom Edition\maps\`.

Fixes game ui problems.

* Unzip `release.zip` and copy the `loader.dll` file to `C:\Program Files (x86)\Microsoft Games\Halo Custom Edition\controls\`.

Plugin that enables field of view (fov) configuration and other useful enhancements.

* Unzip the `haloce_mp_semirefined_r8.7z` and copy the `*.map` file to `C:\Program Files (x86)\Microsoft Games\Halo Custom Edition\maps\`.

Enhanced version of the default halo maps.

* Copy the `haloce.exe - Shortcut` to `C:\Program Files (x86)\Microsoft Games\Halo Custom Edition`.

The shortcut starts halo in full hd, enables the developer console and disables intro videos.

* Run the game by clicking on the shortcut, create a profile, see if you can list online servers and close the game afterwards.

This obviously requires internet connection.

* Copy the `halo4.zip` to `Documents\My Games\Halo CE\hac\packs\`.

Create the subfolders if necessary.

## Offline test

* Disconnect your computer from the internet.

* Start the game by clicking on the `haloce.exe - Shortcut`.

* Press `§` on your keyboard.

This command starts the developer console.

* Enter `optic load halo4`

Loads the halo4 medal pack.

## Custom maps

* Open the `halo ce custom maps bundle` folder.

* Copy alls `*.map` files to `C:\Program Files (x86)\Microsoft Games\Halo Custom Edition\maps`.

## Keyboard shortcuts

A list of important keyboard shortcuts.

    F6 - Change the fov.

## Troubleshooting

**Problem**

You receive an error warning about missing DLL followed by "Unable to load HAC! Error 126".

**Solution**

Your operating system likely needs to be updated. Download the Microsoft Visual C++ 2010 Runtime from here as well as the most up-to-date version of DirectX9 from here.

**Problem**

You receive an error that states, "Unable to load HAC! Error 126".

**Problem**

Your anti-virus software is likely preventing HAC from loading. Add loader.dll to your white list or temporarily disable your anti-virus protection before you load Halo. If required, please consult the manual for your anti-virus software for the specifics on how to do this.

## Maintain files

Use the following PowerShell functions to validate hash values for the installer bundle files.

**Create-Hash.ps1**

```powershell
$files = @(
    "7z1805-x64.exe",
    "haloce_mp_semirefined_r8.7z",
    "Universal_UI_Version_1.1.zip",
    "vcredist_x86.exe",
    "dxwebsetup.exe",
    "halo4.zip",
    "release.zip",
    "halocesetup_en_1.00.exe",
    "haloceded.exe",
    "haloce-patch-1.0.10.exe",
    "haloce.exe - Shortcut.lnk",
    "haloce.exe"
)

$hashes = @()

Get-ChildItem | Where-Object { $files -contains $_.Name } | ForEach-Object {
    $hashes += @{
        Name = $_.Name
        Hash = (Get-FileHash -Path $_).Hash
    }
}

$hashes | ConvertTo-Json | Set-Content "hahses.json"
```

**Validate-Hash.ps1**

```powershell
$files = @(
    "7z1805-x64.exe",
    "haloce_mp_semirefined_r8.7z",
    "Universal_UI_Version_1.1.zip",
    "vcredist_x86.exe",
    "dxwebsetup.exe",
    "halo4.zip",
    "release.zip",
    "halocesetup_en_1.00.exe",
    "haloceded.exe",
    "haloce-patch-1.0.10.exe",
    "haloce.exe - Shortcut.lnk",
    "haloce.exe"
)

$hashes = (Get-Content "hahses.json" | ConvertFrom-Json)

Get-ChildItem | Where-Object { $files -contains $_.Name } | ForEach-Object {

    $file = $_

    if (-not ($hashes | Where-Object { $_.Name -eq $file.Name })) {
        Write-Error "File $($file.Name) does not exist."

    } elseif (-not ($hashes | Where-Object { $_.Hash -eq (Get-FileHash $file).Hash })) {
        Write-Error "Hash did not match for $($file.Name)."

    } else {
        Write-Host "File $($file.Name) has a valid hash."
    }
}
```

## Source

[The Halo CE Ultimate Enhancement Guide. Updated 14/11/18](https://opencarnage.net/index.php?/topic/7383-the-halo-ce-ultimate-enhancement-guide-updated-141118/)
