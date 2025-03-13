# Install Home Assistant on a Device Without an Ethernet Port (Surface Pro 4 Example)

This guide details how to install Home Assistant OS on a device without an Ethernet port, specifically using a Surface Pro 4 with a corrupted SSD. We'll use a Windows 11 PC to prepare the necessary files and an external NVMe enclosure to run Home Assistant.
---

> [!IMPORTANT]
> ### Equipment List
> - **Windows 11 PC**
> - **Surface Pro 4** (or similar device)
> - **External NVMe enclosure** (e.g., [SSK Aluminum Enclosure](https://www.amazon.com/SSK-Aluminum-Enclosure-Adapter-External/dp/B07MNFH1PX))
> - **USB 3.0 powered hub**
> - **Keyboard and mouse with Logitech Unifying dongle**
> - **7-Zip** (for extracting files)
> - **Balena Etcher** (for flashing the image to the drive)
---

1. **Download Home Assistant OS Image**
    - On your Windows 11 PC, download the latest dev version of Home Assistant from [Home Assistant OS Artifacts](https://os-artifacts.home-assistant.io/index.html).
      > For this example, the chosen file is `haos_generic-x86-64-13.0.dev20240708.img.xz`.

2. **Extract the Image File**
    - Use 7-Zip to extract the `.xz` file to get the `.img` file.
      > Right-click the .xz file > 7-Zip > Extract Here

3. **Flash the Image to the External Drive**
    - Connect your external NVMe enclosure to the Windows PC.
    - Open Balena Etcher and select the extracted `.img` file.
    - Choose the external NVMe enclosure as the target.
    - Click "Flash!" to start the process.

4. **Setup Surface Pro 4**
    - Connect the external NVMe enclosure to your Surface Pro 4 via the USB 3.0 powered hub.
    - Also, plug in the Logitech Unifying dongle for your keyboard and mouse.

5. **Initial Setup of Home Assistant OS**
    - Power on the Surface Pro 4 and boot from the external drive.
      > Home Assistant OS will run through its initial setup.
      > When the system fails to connect to the Internet and drops to the recovery prompt `#`, type the following commands:
        ```sh
        nmcli device
        ```

6. **Scan for Wi-Fi Networks**
    ```sh
    nmcli device wifi rescan # you may not see anything
    nmcli device wifi list # find the network you want to connect to
    ```

7. **Connect to Wi-Fi**
    > Replace `SSID` with your Wi-Fi network name and `PASS` with your Wi-Fi password.
      ```sh
      nmcli device wifi connect "SSID" password "PASS"
      ```

8. **Verify the Connection**
    ```sh
    ping google.com
    ***google.com is alive***
    ```

9. **Restart Home Assistant CLI**
    - If the Wi-Fi connection is successful and you can ping external websites, restart the Home Assistant CLI via:
      ```sh
      hassos-cli
      ```

10. **Access Home Assistant Web Interface**
    - After connecting to Wi-Fi, open Home Assistant by navigating to one of the following URLs in your web browser:
      > [http://homeassistant.local:8123](http://homeassistant.local:8123)
      > [http://homeassistant:8123](http://homeassistant:8123)
