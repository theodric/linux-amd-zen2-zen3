Kernel config files, tracking Arch packages [linux-amd-znver2](https://aur.archlinux.org/packages/linux-amd-znver2 "linux-amd-znver2") and [linux-amd-znver3](https://aur.archlinux.org/packages/linux-amd-znver3 "linux-amd-znver3"), with modifications to support Fedora 38 (with Zen2) and openSUSE Tumbleweed (with Zen3) - primarily modifications around EFI booting. (Using the Arch config files unmodified on Fedora and openSUSE will result in a kernel that cannot boot.)

You can build with these configs against the kernel source archives available at kernel.org.

**NOTE**

You will also need to obtain and apply the patch to support additional microarchitectures in the Linux kernel from graysky2 *before* building in order to avail of any of the Zen-specific enhancements!

https://github.com/graysky2/kernel_compiler_patch

Per the Arch PKGBUILD, simply download the relevant patch file into the root of your unpacked kernel source and run `git apply nameofpatchfile` to apply the patch, 
 e.g. `git apply more-uarches-for-kernel-6.8-rc4+.patch`

------------

**QnA**


    Q: Why does my Ryzen 7 4700U refuse to clock over 1.4GHz on any kernel 6.7.x, 
       but the same .config used on 6.6.x works fine?

    A: Scaling seems to be fucked up by default for Zen2 on 6.7.x. 
       `cpupower frequency-set -f 2000000` should temporarily resolve this. 
       (You can check `cpupower frequency-info` to confirm.)

       On my system, for some reason, TLP does not work on boot, but requires either the power
       cable to be disconnected and reconnected, or else the service to be restarted to apply
       the configured frequency range and governor settings. Since the latter can be scripted,
       I've simply put this into my /etc/crontab: `@reboot sleep 5; sudo systemctl restart tlp`

       Why the above *isn't* an issue on 6.6.1 through 6.6.21 remains one of life's mysteries.


    Q: Why Zen2 on Fedora 38 and Zen3 on openSUSE?
    A: Because my Zen2 laptop runs Fedora 38, and my Zen3 desktop runs openSUSE Tumbleweed.


    Q: Will you provide other builds to support other combinations of architectures/distributions?
    A: Yes! If you buy me the computer to do it with.


    Q: I don't want to buy you a computer. Why won't you do it anyway?
    A: Pay me.


    Q: Hey you kinda sound like an asshole, man.
    A: You catch on quickly. Your mother would be very proud.

