# Arch Linux CPU Performance Mode

## Check Current CPU Governor
To check the current CPU frequency scaling governor, run:

```sh
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
```

## Install cpupower
Install `cpupower` using pacman:

```sh
sudo pacman -S cpupower
```

## Enable Performance Mode
To set the CPU to performance mode, use the following command:

```sh
sudo cpupower frequency-set -g performance
```

## Verify the Mode
Check again to confirm that the governor is set to `performance`:

```sh
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
```

Now your CPU should be running at maximum clock speeds. 🚀

## Persistence After Reboot
By default, this setting **does not persist** after a reboot. You may need to reapply it manually when needed, such as when gaming.

### Optional: Make It Persistent
To apply this setting automatically at boot, you can create a systemd service:

1. Create a new systemd service file:
   
   ```sh
   sudo nano /etc/systemd/system/cpupower.service
   ```

2. Add the following content:
   
   ```ini
   [Unit]
   Description=Set CPU Governor to Performance
   After=multi-user.target

   [Service]
   Type=oneshot
   ExecStart=/usr/bin/cpupower frequency-set -g performance
   RemainAfterExit=yes

   [Install]
   WantedBy=multi-user.target
   ```

3. Save the file and enable the service:
   
   ```sh
   sudo systemctl enable cpupower.service
   ```

4. Start the service immediately:
   
   ```sh
   sudo systemctl start cpupower.service
   ```

Now, the performance mode should persist across reboots. 🎯
