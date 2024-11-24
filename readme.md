# manual
manual from page https://www.willhaley.com/blog/debian-arm-qemu/  \

links http://ftp.us.debian.org/debian/dists/stable/main/installer-arm64/current/images/cdrom/
```
curl -O http://ftp.us.debian.org/debian/dists/stable/main/installer-arm64/current/images/cdrom/initrd.gz
curl -O http://ftp.us.debian.org/debian/dists/stable/main/installer-arm64/current/images/cdrom/vmlinuz
```
iso https://cdimage.debian.org/debian-cd/current/arm64/iso-dvd/

```
qemu-system-aarch64   -m 4G   -machine type=virt   -cpu max   -m 8g   -smp 4 \
  -initrd "./initrd.gz"   -kernel "./vmlinuz"   -append "console=ttyAMA0" \
  -drive file=./debian-12.5.0-arm64-DVD-1.iso,id=cdrom,if=none,media=cdrom \
  -device virtio-scsi-device     -device scsi-cd,drive=cdrom \
  -drive file="./debian-arm.sda.qcow2",id=hd,if=none,media=disk  \
  -device virtio-scsi-device     -device scsi-hd,drive=hd \
  -netdev user,id=net0,hostfwd=tcp::5555-:22  \
  -device virtio-net-device,netdev=net0 \
  -nographic

```

```
rustam@rustam-zenbook:~/qemu-journal/debian$ qemu-system-aarch64   -m 4G   -machine type=virt   -cpu max   -m 8g   -smp 4   -initrd "./initrd.gz"   -kernel "./vmlinuz"   -append "console=ttyAMA0"   -drive file=./debian-12.5.0-arm64-DVD-1.iso,id=cdrom,if=none,media=cdrom     -device virtio-scsi-device     -device scsi-cd,drive=cdrom   -drive file="./debian-arm.sda.qcow2",id=hd,if=none,media=disk     -device virtio-scsi-device     -device scsi-hd,drive=hd   -netdev user,id=net0,hostfwd=tcp::5555-:22     -device virtio-net-device,netdev=net0   -nographic
[    0.000000] Booting Linux on physical CPU 0x0000000000 [0x000f0510]
[    0.000000] Linux version 6.1.0-27-arm64 (debian-kernel@lists.debian.org) (gcc-12 (Debian 12.2.0-14) 12.2.0, GNU ld (GNU Binutils for Debian) 2.40) #1 SMP Debian 6.1.115-1 (2024-11-01)
[    0.000000] random: crng init done
[    0.000000] Machine model: linux,dummy-virt
[    0.000000] efi: UEFI not found.
[    0.000000] NUMA: No NUMA configuration found
[    0.000000] NUMA: Faking a node at [mem 0x0000000040000000-0x000000023fffffff]
[    0.000000] NUMA: NODE_DATA [mem 0x23efe8380-0x23efeafff]
[    0.000000] Zone ranges:
[    0.000000]   DMA      [mem 0x0000000040000000-0x00000000ffffffff]
[    0.000000]   DMA32    empty
[    0.000000]   Normal   [mem 0x0000000100000000-0x000000023fffffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000040000000-0x000000023fffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000040000000-0x000000023fffffff]
[    0.000000] cma: Reserved 64 MiB at 0x00000000fc000000
[    0.000000] psci: probing for conduit method from DT.
[    0.000000] psci: PSCIv1.1 detected in firmware.
[    0.000000] psci: Using standard PSCI v0.2 function IDs
[    0.000000] psci: Trusted OS migration not required
[    0.000000] psci: SMC Calling Convention v1.0
[    0.000000] percpu: Embedded 31 pages/cpu s86632 r8192 d32152 u126976
[    0.000000] Detected PIPT I-cache on CPU0
[    0.000000] CPU features: detected: Address authentication (architected QARMA5 algorithm)
[    0.000000] CPU features: detected: Hardware dirty bit management
[    0.000000] CPU features: detected: Spectre-v4
[    0.000000] alternatives: applying boot alternatives
[    0.000000] Fallback order for Node 0: 0 
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 2064384
[    0.000000] Policy zone: Normal
[    0.000000] Kernel command line: console=ttyAMA0
[    0.000000] Dentry cache hash table entries: 1048576 (order: 11, 8388608 bytes, linear)
[    0.000000] Inode-cache hash table entries: 524288 (order: 10, 4194304 bytes, linear)
[    0.000000] mem auto-init: stack:all(zero), heap alloc:on, heap free:off
[    0.000000] software IO TLB: area num 4.
[    0.000000] software IO TLB: mapped [mem 0x00000000f8000000-0x00000000fc000000] (64MB)
[    0.000000] Memory: 3090876K/8388608K available (13056K kernel code, 2804K rwdata, 9464K rodata, 6464K init, 626K bss, 281640K reserved, 65536K cma-reserved)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1
[    0.000000] ftrace: allocating 44010 entries in 172 pages
[    0.000000] ftrace: allocated 172 pages with 4 groups
[    0.000000] trace event string verifier disabled
[    0.000000] rcu: Hierarchical RCU implementation.
[    0.000000] rcu: 	RCU restricting CPUs from NR_CPUS=256 to nr_cpu_ids=4.
[    0.000000] 	Rude variant of Tasks RCU enabled.
[    0.000000] 	Tracing variant of Tasks RCU enabled.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 25 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=4
[    0.000000] NR_IRQS: 64, nr_irqs: 64, preallocated irqs: 0
[    0.000000] Root IRQ handler: gic_handle_irq
[    0.000000] GICv2m: range[mem 0x08020000-0x08020fff], SPI[80:143]
[    0.000000] rcu: srcu_init: Setting srcu_struct sizes based on contention.
[    0.000000] arch_timer: cp15 timer(s) running at 62.50MHz (virt).
[    0.000000] clocksource: arch_sys_counter: mask: 0x1ffffffffffffff max_cycles: 0x1cd42e208c, max_idle_ns: 881590405314 ns
[    0.000159] sched_clock: 57 bits at 63MHz, resolution 16ns, wraps every 4398046511096ns
[    0.032951] Console: colour dummy device 80x25
[    0.042716] Calibrating delay loop (skipped), value calculated using timer frequency.. 125.00 BogoMIPS (lpj=250000)
[    0.043936] pid_max: default: 32768 minimum: 301
[    0.047952] LSM: Security Framework initializing
[    0.050617] landlock: Up and running.
[    0.050730] Yama: disabled by default; enable with sysctl kernel.yama.*
[    0.056463] AppArmor: AppArmor initialized
[    0.056647] TOMOYO Linux initialized
[    0.057795] LSM support for eBPF active
[    0.062649] Mount-cache hash table entries: 16384 (order: 5, 131072 bytes, linear)
[    0.063048] Mountpoint-cache hash table entries: 16384 (order: 5, 131072 bytes, linear)
[    0.126965] cacheinfo: Unable to detect cache hierarchy for CPU 0
[    0.146341] cblist_init_generic: Setting adjustable number of callback queues.
[    0.146432] cblist_init_generic: Setting shift to 2 and lim to 1.
[    0.148242] cblist_init_generic: Setting adjustable number of callback queues.
[    0.148307] cblist_init_generic: Setting shift to 2 and lim to 1.
[    0.153212] rcu: Hierarchical SRCU implementation.
[    0.153306] rcu: 	Max phase no-delay instances is 1000.
[    0.187994] EFI services will not be available.
[    0.197486] smp: Bringing up secondary CPUs ...
[    0.223214] Detected PIPT I-cache on CPU1
[    0.242557] cacheinfo: Unable to detect cache hierarchy for CPU 1
[    0.252515] CPU1: Booted secondary processor 0x0000000001 [0x000f0510]
[    0.298110] Detected PIPT I-cache on CPU2
[    0.299775] cacheinfo: Unable to detect cache hierarchy for CPU 2
[    0.300413] CPU2: Booted secondary processor 0x0000000002 [0x000f0510]
[    0.313690] Detected PIPT I-cache on CPU3
[    0.316065] cacheinfo: Unable to detect cache hierarchy for CPU 3
[    0.317334] CPU3: Booted secondary processor 0x0000000003 [0x000f0510]
[    0.320829] smp: Brought up 1 node, 4 CPUs
[    0.320960] SMP: Total of 4 processors activated.
[    0.321228] CPU features: detected: Branch Target Identification
[    0.321344] CPU features: detected: 32-bit EL0 Support
[    0.321416] CPU features: detected: 32-bit EL1 Support
[    0.321486] CPU features: detected: ARMv8.4 Translation Table Level
[    0.321579] CPU features: detected: Data cache clean to the PoU not required for I/D coherence
[    0.322029] CPU features: detected: Common not Private translations
[    0.322109] CPU features: detected: CRC32 instructions
[    0.322197] CPU features: detected: Data cache clean to Point of Deep Persistence
[    0.322268] CPU features: detected: Data cache clean to Point of Persistence
[    0.322337] CPU features: detected: E0PD
[    0.322417] CPU features: detected: Enhanced Privileged Access Never
[    0.322584] CPU features: detected: Generic authentication (architected QARMA5 algorithm)
[    0.322666] CPU features: detected: RCpc load-acquire (LDAPR)
[    0.322734] CPU features: detected: LSE atomic instructions
[    0.322805] CPU features: detected: Privileged Access Never
[    0.322874] CPU features: detected: RAS Extension Support
[    0.322943] CPU features: detected: Random Number Generator
[    0.323013] CPU features: detected: Speculation barrier (SB)
[    0.323082] CPU features: detected: Stage-2 Force Write-Back
[    0.323165] CPU features: detected: Trap EL0 IMPLEMENTATION DEFINED functionality
[    0.323233] CPU features: detected: TLB range maintenance instructions
[    0.323395] CPU features: detected: Scalable Matrix Extension
[    0.323466] CPU features: detected: FA64
[    0.323535] CPU features: detected: Speculative Store Bypassing Safe (SSBS)
[    0.323609] CPU features: detected: Scalable Vector Extension
[    0.351262] SVE: maximum available vector length 256 bytes per vector
[    0.356375] SVE: default vector length 64 bytes per vector
[    0.360836] SME: minimum available vector length 16 bytes per vector
[    0.360934] SME: maximum available vector length 256 bytes per vector
[    0.361002] SME: default vector length 32 bytes per vector
[    0.361506] CPU: All CPU(s) started at EL1
[    0.362702] alternatives: applying system-wide alternatives
[    2.205672] node 0 deferred pages initialised in 1464ms
[    2.329792] devtmpfs: initialized
[    2.502354] Registered cp15_barrier emulation handler
[    2.502716] Registered setend emulation handler
[    2.510168] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    2.511416] futex hash table entries: 1024 (order: 4, 65536 bytes, linear)
[    2.542562] pinctrl core: initialized pinctrl subsystem
[    2.576448] DMI not present or invalid.
[    2.594104] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    2.647805] DMA: preallocated 1024 KiB GFP_KERNEL pool for atomic allocations
[    2.657902] DMA: preallocated 1024 KiB GFP_KERNEL|GFP_DMA pool for atomic allocations
[    2.667197] DMA: preallocated 1024 KiB GFP_KERNEL|GFP_DMA32 pool for atomic allocations
[    2.668043] audit: initializing netlink subsys (disabled)
[    2.675439] audit: type=2000 audit(2.232:1): state=initialized audit_enabled=0 res=1
[    2.696407] thermal_sys: Registered thermal governor 'fair_share'
[    2.696574] thermal_sys: Registered thermal governor 'bang_bang'
[    2.696668] thermal_sys: Registered thermal governor 'step_wise'
[    2.696741] thermal_sys: Registered thermal governor 'user_space'
[    2.696814] thermal_sys: Registered thermal governor 'power_allocator'
[    2.697829] cpuidle: using governor ladder
[    2.698379] cpuidle: using governor menu
[    2.700781] hw-breakpoint: found 6 breakpoint and 4 watchpoint registers.
[    2.704488] ASID allocator initialised with 65536 entries
[    2.713774] Serial: AMBA PL011 UART driver
[    2.893386] 9000000.pl011: ttyAMA0 at MMIO 0x9000000 (irq = 13, base_baud = 0) is a PL011 rev1
[    2.974657] printk: console [ttyAMA0] enabled
[    3.028453] KASLR enabled
[    3.201537] HugeTLB: registered 1.00 GiB page size, pre-allocated 0 pages
[    3.204425] HugeTLB: 0 KiB vmemmap can be freed for a 1.00 GiB page
[    3.208214] HugeTLB: registered 32.0 MiB page size, pre-allocated 0 pages
[    3.210558] HugeTLB: 0 KiB vmemmap can be freed for a 32.0 MiB page
[    3.213175] HugeTLB: registered 2.00 MiB page size, pre-allocated 0 pages
[    3.215247] HugeTLB: 0 KiB vmemmap can be freed for a 2.00 MiB page
[    3.217518] HugeTLB: registered 64.0 KiB page size, pre-allocated 0 pages
[    3.219934] HugeTLB: 0 KiB vmemmap can be freed for a 64.0 KiB page
[    3.271911] ACPI: Interpreter disabled.
[    3.288457] iommu: Default domain type: Translated 
[    3.289547] iommu: DMA domain TLB invalidation policy: strict mode 
[    3.296114] pps_core: LinuxPPS API ver. 1 registered
[    3.296734] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    3.297790] PTP clock support registered
[    3.298864] EDAC MC: Ver: 3.0.0
[    3.365215] NetLabel: Initializing
[    3.365770] NetLabel:  domain hash size = 128
[    3.366522] NetLabel:  protocols = UNLABELED CIPSOv4 CALIPSO
[    3.372183] NetLabel:  unlabeled traffic allowed by default
[    3.379080] vgaarb: loaded
[    3.393806] clocksource: Switched to clocksource arch_sys_counter
[    3.411487] VFS: Disk quotas dquot_6.6.0
[    3.413108] VFS: Dquot-cache hash table entries: 512 (order 0, 4096 bytes)
[    3.437392] AppArmor: AppArmor Filesystem Enabled
[    3.439171] pnp: PnP ACPI: disabled
[    3.755591] NET: Registered PF_INET protocol family
[    3.761400] IP idents hash table entries: 131072 (order: 8, 1048576 bytes, linear)
[    3.808959] tcp_listen_portaddr_hash hash table entries: 4096 (order: 4, 65536 bytes, linear)
[    3.811419] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)
[    3.816055] TCP established hash table entries: 65536 (order: 7, 524288 bytes, linear)
[    3.827027] TCP bind hash table entries: 65536 (order: 9, 2097152 bytes, linear)
[    3.833681] TCP: Hash tables configured (established 65536 bind 65536)
[    3.850733] MPTCP token hash table entries: 8192 (order: 5, 196608 bytes, linear)
[    3.855173] UDP hash table entries: 4096 (order: 5, 131072 bytes, linear)
[    3.858583] UDP-Lite hash table entries: 4096 (order: 5, 131072 bytes, linear)
[    3.865911] NET: Registered PF_UNIX/PF_LOCAL protocol family
[    3.868244] NET: Registered PF_XDP protocol family
[    3.870192] PCI: CLS 0 bytes, default 64
[    3.893645] Trying to unpack rootfs image as initramfs...
[    3.913868] hw perfevents: enabled with armv8_pmuv3 PMU driver, 7 counters available
[    3.919054] kvm [1]: HYP mode not available
[    4.547065] Initialise system trusted keyrings
[    4.557574] Key type blacklist registered
[    4.570113] workingset: timestamp_bits=42 max_order=21 bucket_order=0
[    4.759228] zbud: loaded
[    4.791937] integrity: Platform Keyring initialized
[    4.793796] integrity: Machine keyring initialized
[    4.794668] Key type asymmetric registered
[    4.795717] Asymmetric key parser 'x509' registered
[   10.384259] Freeing initrd memory: 21332K
[   10.904268] alg: self-tests for CTR-KDF (hmac(sha256)) passed
[   10.907849] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)
[   10.918714] io scheduler mq-deadline registered
[   11.101971] pl061_gpio 9030000.pl061: PL061 GPIO chip registered
[   11.123657] shpchp: Standard Hot Plug PCI Controller Driver version: 0.4
[   11.138687] pci-host-generic 4010000000.pcie: host bridge /pcie@10000000 ranges:
[   11.141195] pci-host-generic 4010000000.pcie:       IO 0x003eff0000..0x003effffff -> 0x0000000000
[   11.143115] pci-host-generic 4010000000.pcie:      MEM 0x0010000000..0x003efeffff -> 0x0010000000
[   11.144340] pci-host-generic 4010000000.pcie:      MEM 0x8000000000..0xffffffffff -> 0x8000000000
[   11.146565] pci-host-generic 4010000000.pcie: Memory resource size exceeds max for 32 bits
[   11.148804] pci-host-generic 4010000000.pcie: ECAM at [mem 0x4010000000-0x401fffffff] for [bus 00-ff]
[   11.154032] pci-host-generic 4010000000.pcie: PCI host bridge to bus 0000:00
[   11.155323] pci_bus 0000:00: root bus resource [bus 00-ff]
[   11.156233] pci_bus 0000:00: root bus resource [io  0x0000-0xffff]
[   11.157534] pci_bus 0000:00: root bus resource [mem 0x10000000-0x3efeffff]
[   11.158540] pci_bus 0000:00: root bus resource [mem 0x8000000000-0xffffffffff]
[   11.163649] pci 0000:00:00.0: [1b36:0008] type 00 class 0x060000
[   11.367029] Serial: 8250/16550 driver, 4 ports, IRQ sharing enabled
[   11.426519] Serial: AMBA driver
[   11.427947] SuperH (H)SCI(F) driver initialized
[   11.447363] msm_serial: driver initialized
[   11.478661] cacheinfo: Unable to detect cache hierarchy for CPU 0


[            (1*installer)  2 shell  3 shell  4- log           ][ Nov 24 16:32 ]
                                                                                
                                                                                
                                                                                
                                                                                
                                                                                
                                                                                
                                                                                
                                                                                 

BusyBox v1.35.0 (Debian 1:1.35.0-4+b3) built-in shell (ash)
Enter 'help' for a list of built-in commands.

~ # uname -a
Linux (none) 6.1.0-27-arm64 #1 SMP Debian 6.1.115-1 (2024-11-01) aarch64 GNU/Linux
~ # poweroff
The system is going down NOW!
Sent SIGTERM to all processes
Sent SIGKILL to all processes
Requesting system poweroff
[   83.628554] reboot: Power down

```
