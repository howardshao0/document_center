# Upgrade AI Device to KDP2 Firmware

**Note**: KneronDFUT supports 3 platforms - Windows 10 (x86_64 64-bit), Ubuntu 18.04 (x86_64 64-bit), and Raspberry Pi OS - Buster (armv7l 32-bit)

**Note**: If you are not using the 3 platforms, you may use the DFUT_console provided in Kneron PLUS. Please refer [Build with DFUT_console](../../plus_c/introduction/build_plus.md#23-build-with-dfutconsole)

**Note**: Please use the latest version of KneronDFUT to avoid problems caused by incompatibility.

**Note**: Downgrading Kneron AI device to previous KDP firmware is not allowed.

**Note**: If the Kneron AI device you wish to upgrade is running HICO firmware, please manually reset the device first before the update process.

---

## 1. Introduction

**KDP2 Firmware** is the firmware designed for KP APIs in PLUS. Using KDP2 Firmware allows Kneron AI device performing corresponding operation requested by PLUS.

There are two modes to activate KDP2 firmware in Kneron AI device:

- **Runtime Upload Firmware (USB Boot)**

    - USB boot mode is only available on **KL520**.

    - USB boot mode is using usb to upload KDP2 firmware before the inference process.

    - Uploading firmware requires the assistance from the loader firmware("**KDP2 loader**") in flash memory.

    - The GUI or command line of **KneronDFUT** can be used for writing the loader firmware to flash memory and switch AI devices to USB boot mode.

    - After writing the loader firmware and switching device to USB boot mode. The KDP2 firmware can be uploaded via following KP API, before inference:

        * C user: `kp_load_firmware_from_file()`
        * Python user: `kp.core.load_firmware_from_file()`

- **Firmware in Flash Memory (Flash Boot)**

    - This mode is using the **KDP2 firmware** stored in the flash memory of AI devices.

    - Once the AI device is electrified, the firmware will be automatically activated.

    - The GUI or command line of **KneronDFUT** can be used for writing KDP2 firmware to flash memory and switch AI devices to Flash boot mode.

Note: Some 96 boards may run a customized firmware which does not accept commands from the usb interface. Therefore, these 96 boards are not able to be upgraded to kdp2 firmware through Kneron DFUT. For the demands of upgrading these 96 boards, please refer [Program Flash via JTAG/SWD Interface for KDP2](../../520_1.7.0/flash_management/flash_management.md#5-program-flash-via-jtagswd-interface-for-kdp2) for more information.

---

## 2. Download Kneron DFUT

Download the KneronDFUT_ubuntu.zip into Ubuntu from  https://www.kneron.com/tw/support/developers/. It is located at **Kneron PLUS** section.

```bash
$ unzip KneronDFUT_ubuntu.zip
$ cd Kneron_DFUT/
$ chmod +x bin/KneronDFUT # optional
```

Command line usage
```bash
$ sudo sh KneronDFUT.sh --help
```

```bash
[Display help message]
    --help                : [no argument]         help message

[Scan and list all information]
    --list                : [no argument]         list all dongles information

[Update dongles to usb boot] (Only works for KL520)
    --kl520-usb-boot      : [no argument]         choose update to Usb Boot
    --port                : [argument required]   port id set ("all" or specified multiple port ids "13,537")

[Update dongles to flash boot] (Only works for KL520)
    --kl520-flash-boot    : [no argument]         choose update to Flash Boot
    --port                : [argument required]   port id set ("all" or specified multiple port ids "13,537")
    --scpu                : [argument required]   self pointed scpu firmware file path (.bin)
    --ncpu                : [argument required]   self pointed ncpu firmware file path (.bin)

[Update dongles to usb boot] (Only works for KL630)
    --kl630-usb-boot      : [no argument]         choose update to Usb Boot
    --port                : [argument required]   port id set ("all" or specified multiple port ids "13,537")

[Update dongles to usb boot] (Only works for KL630)
    --kl630-flash-boot    : [no argument]         choose update to Flash Boot
    --port                : [argument required]   port id set ("all" or specified multiple port ids "13,537")
    --scpu                : [argument required]   self pointed firmware file path (.tar)

[Update dongles to usb boot] (Only works for KL730)
    --kl730-usb-boot      : [no argument]         choose update to Usb Boot
    --port                : [argument required]   port id set ("all" or specified multiple port ids "13,537")

[Update dongles to usb boot] (Only works for KL730)
    --kl730-flash-boot    : [no argument]         choose update to Flash Boot
    --port                : [argument required]   port id set ("all" or specified multiple port ids "13,537")
    --scpu                : [argument required]   self pointed firmware file path (.tar)

[Update firmware file to flash memory in dongles] (Only works for KL720)
    --kl720-update        : [no argument]         choose write firmware to flash memory
    --port                : [argument required]   port id set ("all" or specified multiple port ids "13,537")
    --scpu                : [argument required]   self pointed scpu firmware file path (.bin)
    --ncpu                : [argument required]   self pointed ncpu firmware file path (.bin)

[Update model file to flash memory in dongles]
    --model-to-flash      : [argument required]   self pointed model file path (.nef)
    --type                : [argument required]   type of device ("KL520", "KL630", "KL720", or "KL730")
    --port                : [argument required]   port id set ("all" or specified multiple port ids "13,537")

[Enable Graphic User Interface]
    --gui                 : [no argument]         display GUI

[Get Current Kneron DFUT Version]
    --version             : [no argument]         display the version of Kneron DFUT
```

---

## 3. Install Driver for Windows

When you execute any kind of update on Kneron DFUT, it will check whether the driver of KL520, KL630, KL720, or KL730 has been installed on Windows. If the driver has not been installed, Kneron DFUT will install the driver before any update.

Note: Kneron DFUT only check and install driver when it was executed on Windows.

Note: In order to install driver, Kneron DFUT must be run as Administrator.

Note: This feature and example are only provided in Kneron DFUT v1.3.0 and above.

1. Use Command line

    ```bash
    $ KneronDFUT.exe --kl520-usb-boot --port all
    ```

    ```bash
    Installing driver for KL520 ... Success(0)

    Start Update Device with Port Id 389 to USB Boot

    ==== Update of Device with Port Id: 389 Succeeded ====
    ```

2. Use GUI

    ![](../imgs/dfut_install_driver.png)

---

## 4. [KL520] Update to USB Boot Mode

### 4.1 Use GUI to Update AI Device

```bash
$ sudo sh KneronDFUT.sh
```

1. Select **KL520** Tab.

2. Select the KL520 devices to be update to USB Boot Mode.

3. Select **Update to USB Boot**

4. Push **Run** button.

    ![](../imgs/dfut_kl520_usb_boot.png)


### 4.2 Use Command Line to Update AI Device

1. List all devices

    ```bash
    $ sudo sh KneronDFUT.sh --list
    ```

    ```bash
    ===========================================
    Index:          1
    Port Id:        133
    Kn Number:      0x270A265C
    Device Type:    KL520
    FW Type:        KDP
    Usb Speed:      High-Speed
    Connectable:    true
    ===========================================
    ```

2. Upgrade the selected KL520 devices using the port id

    ```bash
    $ sudo sh KneronDFUT.sh --kl520-usb-boot --port 133
    ```

    ```bash
    Start Update Device with Port Id 133 to USB Boot

    ==== Update of Device with Port Id: 133 Succeeded ====

    ```


---

## 5. [KL520] Update to Flash Boot Mode

### 5.1 Use GUI to Update AI Device
```bash
$ sudo sh KneronDFUT.sh
```

1. Select **KL520** Tab.

2. Select the KL520 devices to be **Update to Flash Boot** Mode.

3. Select **Update to Flash Boot**

4. Manually choose **SCPU firmware file** and **NCPU firmware file**.

    SCPU and NCPU firmware file for KL520 can be found in **${PLUS_FOLDER}/res/firmware/KL520/**

5. Push **Run** button.

    ![](../imgs/dfut_kl520_flash_boot.png)

### 5.2 Use Command Line to Update AI Device

1. List all devices

    ```bash
    $ sudo sh KneronDFUT.sh --list
    ```

    ```bash
    ===========================================
    Index:          1
    Port Id:        133
    Kn Number:      0x270A265C
    Device Type:    KL520
    FW Type:        KDP
    Usb Speed:      High-Speed
    Connectable:    true
    ===========================================
    ```

2. Upgrade the selected KL520 devices using the port id

    ```bash
    $ sudo sh KneronDFUT.sh --kl520-flash-boot --port 133 --scpu ${SCPU_FILE_PATH} --ncpu ${NCPU_FILE_PATH}
    ```

    ```bash
    Start Update Device with Port Id 133 to Flash Boot

    ==== Update of Device with Port Id: 133 Succeeded ====
    ```

    SCPU and NCPU firmware file for KL520 can be found in **${PLUS_FOLDER}/res/firmware/KL520/**

---

## 6. [KL630] Update to USB Boot Mode

### 6.1 Use GUI to Update AI Device

```bash
$ sudo sh KneronDFUT.sh
```

1. Select **KL630** Tab.

2. Select the KL630 devices to be update to USB Boot Mode.

3. Select **Update to USB Boot**

4. Push **Run** button.

    ![](../imgs/dfut_kl630_usb_boot.png)


### 6.2 Use Command Line to Update AI Device

1. List all devices

    ```bash
    $ sudo sh KneronDFUT.sh --list
    ```

    ```bash
    ===========================================
    Index:          1
    Port Id:        133
    Kn Number:      0x270A265C
    Device Type:    KL630
    FW Type:        KDP2
    Usb Speed:      High-Speed
    Connectable:    true
    ===========================================
    ```

2. Upgrade the selected KL630 devices using the port id

    ```bash
    $ sudo sh KneronDFUT.sh --kl630-usb-boot --port 133
    ```

    ```bash
    Start Update Device with Port Id 133 to USB Boot

    ==== Update of Device with Port Id: 133 Succeeded ====

    ```


---

## 7. [KL630] Update to Flash Boot Mode

### 7.1 Use GUI to Update AI Device
```bash
$ sudo sh KneronDFUT.sh
```

1. Select **KL630** Tab.

2. Select the KL630 devices to be **Update to Flash Boot** Mode.

3. Select **Update to Flash Boot**

4. Manually choose **SCPU firmware file**.

    SCPU firmware file for KL630 can be found in **${PLUS_FOLDER}/res/firmware/KL630/**

5. Push **Run** button.

    ![](../imgs/dfut_kl630_flash_boot.png)

### 7.2 Use Command Line to Update AI Device

1. List all devices

    ```bash
    $ sudo sh KneronDFUT.sh --list
    ```

    ```bash
    ===========================================
    Index:          1
    Port Id:        13
    Kn Number:      0x09011004
    Device Type:    KL630
    FW Type:        KDP2
    Usb Speed:      High-Speed
    Connectable:    true
    ===========================================
    ```

2. Upgrade the selected KL630 devices using the port id

    ```bash
    $ sudo sh KneronDFUT.sh --kl630-flash-boot --port 13 --scpu ${SCPU_FILE_PATH}
    ```

    ```bash
    Start Update Device with Port Id 13 to Flash Boot

    ==== Update of Device with Port Id: 13 Succeeded ====
    ```

    SCPU firmware file for KL630 can be found in **${PLUS_FOLDER}/res/firmware/KL630/**

---

## 8. [KL720] Update Firmware to Flash Memory


**Note**: Update flash for KL720 is required under USB3.0\(Super-Speed) model

### 8.1 Use GUI to Update AI Device

```bash
$ sudo sh KneronDFUT.sh
```

1. Select **KL720** Tab.

2. Select the KL720 devices to be update to KDP2 firmware.

3. Select **Update Firmware to Flash**

4. Manually choose **SCPU firmware file** and **NCPU firmware file**.

    The firmware files can be found in **${PLUS_FOLDER}/res/firmware/KL720/**

5. Push **Run** button.

    ![](../imgs/dfut_kl720_firmware.png)

### 8.2 Use Command Line to Update AI Device

1. List all devices

    ```bash
    $ sudo sh KneronDFUT.sh --list
    ```

    ```bash
    ===========================================
    Index:          1
    Port Id:        262
    Kn Number:      0x2004142C
    Device Type:    KL720
    FW Type:        KDP
    Usb Speed:      Super-Speed
    Connectable:    true
    ===========================================
    ```

2. Upgrade the selected KL720 devices using the port id

    ```bash
    $ sudo sh KneronDFUT.sh --kl720-update --port 262 --scpu ${SCPU_FILE_PATH} --ncpu ${NCPU_FILE_PATH}
    ```

    ```bash
    Start Update Firmware to Device with Port Id 262

    ==== Update Firmware to Device with Port Id: 262 Succeeded ====
    ```

    SCPU and NCPU firmware file for KL720 can be found in **${PLUS_FOLDER}/res/firmware/KL720/**

---

## 9. [KL730] Update to USB Boot Mode

### 9.1 Use GUI to Update AI Device

```bash
$ sudo sh KneronDFUT.sh
```

1. Select **KL730** Tab.

2. Select the KL730 devices to be update to USB Boot Mode.

3. Select **Update to USB Boot**

4. Push **Run** button.

    ![](../imgs/dfut_kl730_usb_boot.png)


### 9.2 Use Command Line to Update AI Device

1. List all devices

    ```bash
    $ sudo sh KneronDFUT.sh --list
    ```

    ```bash
    ===========================================
    Index:          1
    Port Id:        133
    Kn Number:      0x270A265C
    Device Type:    KL730
    FW Type:        KDP2
    Usb Speed:      High-Speed
    Connectable:    true
    ===========================================
    ```

2. Upgrade the selected KL730 devices using the port id

    ```bash
    $ sudo sh KneronDFUT.sh --kl730-usb-boot --port 133
    ```

    ```bash
    Start Update Device with Port Id 133 to USB Boot

    ==== Update of Device with Port Id: 133 Succeeded ====

    ```


---

## 10. [KL730] Update to Flash Boot Mode

### 10.1 Use GUI to Update AI Device
```bash
$ sudo sh KneronDFUT.sh
```

1. Select **KL730** Tab.

2. Select the KL730 devices to be **Update to Flash Boot** Mode.

3. Select **Update to Flash Boot**

4. Manually choose **SCPU firmware file**.

    SCPU firmware file for KL730 can be found in **${PLUS_FOLDER}/res/firmware/KL730/**

5. Push **Run** button.

    ![](../imgs/dfut_kl730_flash_boot.png)

### 10.2 Use Command Line to Update AI Device

1. List all devices

    ```bash
    $ sudo sh KneronDFUT.sh --list
    ```

    ```bash
    ===========================================
    Index:          1
    Port Id:        13
    Kn Number:      0x09011004
    Device Type:    KL730
    FW Type:        KDP2
    Usb Speed:      High-Speed
    Connectable:    true
    ===========================================
    ```

2. Upgrade the selected KL730 devices using the port id

    ```bash
    $ sudo sh KneronDFUT.sh --kl730-flash-boot --port 13 --scpu ${SCPU_FILE_PATH}
    ```

    ```bash
    Start Update Device with Port Id 13 to Flash Boot

    ==== Update of Device with Port Id: 13 Succeeded ====
    ```

    SCPU firmware file for KL730 can be found in **${PLUS_FOLDER}/res/firmware/KL730/**
