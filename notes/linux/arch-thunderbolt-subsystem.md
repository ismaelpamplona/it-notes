Make sure your kernel has Thunderbolt support. Most recent kernels include Thunderbolt drivers, but it's a good idea to keep your system up to date. You can check the support with:

```bash
lsmod | grep thunderbolt
```

If the Thunderbolt module is not loaded, you may need to load it with:

```bash
sudo modprobe thunderbolt
```

Bolt is a daemon for managing Thunderbolt 3 devices. It allows you to securely authorize and manage Thunderbolt devices. You can install Bolt from the Arch User Repository (AUR) using an AUR helper like paru:

```bash
paru -S bolt
```

Once Bolt is installed, enable and start the service:

```bash
sudo systemctl enable bolt
sudo systemctl start bolt

```

Use the `boltctl` command-line tool to manage Thunderbolt devices and grant or deny access to them. List the Thunderbolt devices connected to your system:

```bash
boltctl list
```

To authorize a device, you can use:

```bash
boltctl enroll <device-uuid>
```

Reboot your system to ensure everything takes effect.

--

Start the service immediately and enable it to start at boot. This command will enable the bolt service to start at boot and also start it immediately without needing a reboot.

```sh
sudo systemctl enable --now bolt
```
