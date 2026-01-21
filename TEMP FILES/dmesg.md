

```bash

root@mint:~# dmesg
[    0.000000] Linux version 6.14.0-37-generic (buildd@lcy02-amd64-031) (x86_64-linux-gnu-gcc-13 (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0, GNU ld (GNU Binutils for Ubuntu) 2.42) #37~24.04.1-Ubuntu SMP PREEMPT_DYNAMIC Thu Nov 20 10:25:38 UTC 2 (Ubuntu 6.14.0-37.37~24.04.1-generic 6.14.11)
[    0.000000] Command line: BOOT_IMAGE=/casper/vmlinuz boot=casper uuid=6e72f523-dc09-4880-8910-93ffa64401c5 username=mint hostname=mint iso-scan/filename= quiet splash --
[    0.000000] KERNEL supported cpus:
[    0.000000]   Intel GenuineIntel
[    0.000000]   AMD AuthenticAMD
[    0.000000]   Hygon HygonGenuine
[    0.000000]   Centaur CentaurHauls
[    0.000000]   zhaoxin   Shanghai  
[    0.000000] BIOS-provided physical RAM map:
[    0.000000] BIOS-e820: [mem 0x0000000000000000-0x000000000009ffff] usable
[    0.000000] BIOS-e820: [mem 0x0000000000100000-0x000000003901ffff] usable
[    0.000000] BIOS-e820: [mem 0x0000000039020000-0x0000000039d7dfff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000039d7e000-0x0000000039d8dfff] ACPI data
[    0.000000] BIOS-e820: [mem 0x0000000039d8e000-0x000000003abd9fff] ACPI NVS
[    0.000000] BIOS-e820: [mem 0x000000003abda000-0x000000003b5befff] reserved
[    0.000000] BIOS-e820: [mem 0x000000003b5bf000-0x000000003b5bffff] usable
[    0.000000] BIOS-e820: [mem 0x000000003b5c0000-0x000000003b645fff] reserved
[    0.000000] BIOS-e820: [mem 0x000000003b646000-0x000000003bffffff] usable
[    0.000000] BIOS-e820: [mem 0x000000003c000000-0x000000003dffffff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000040000000-0x000000004fffffff] reserved
[    0.000000] BIOS-e820: [mem 0x00000000fed1c000-0x00000000fed44fff] reserved
[    0.000000] BIOS-e820: [mem 0x00000000ff000000-0x00000000ffffffff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000100000000-0x00000004bfffffff] usable
[    0.000000] NX (Execute Disable) protection: active
[    0.000000] APIC: Static calls initialized
[    0.000000] e820: update [mem 0x2a541018-0x2a560a57] usable ==> usable
[    0.000000] e820: update [mem 0x2a534018-0x2a540057] usable ==> usable
[    0.000000] extended physical RAM map:
[    0.000000] reserve setup_data: [mem 0x0000000000000000-0x000000000009ffff] usable
[    0.000000] reserve setup_data: [mem 0x0000000000100000-0x000000002a534017] usable
[    0.000000] reserve setup_data: [mem 0x000000002a534018-0x000000002a540057] usable
[    0.000000] reserve setup_data: [mem 0x000000002a540058-0x000000002a541017] usable
[    0.000000] reserve setup_data: [mem 0x000000002a541018-0x000000002a560a57] usable
[    0.000000] reserve setup_data: [mem 0x000000002a560a58-0x000000003901ffff] usable
[    0.000000] reserve setup_data: [mem 0x0000000039020000-0x0000000039d7dfff] reserved
[    0.000000] reserve setup_data: [mem 0x0000000039d7e000-0x0000000039d8dfff] ACPI data
[    0.000000] reserve setup_data: [mem 0x0000000039d8e000-0x000000003abd9fff] ACPI NVS
[    0.000000] reserve setup_data: [mem 0x000000003abda000-0x000000003b5befff] reserved
[    0.000000] reserve setup_data: [mem 0x000000003b5bf000-0x000000003b5bffff] usable
[    0.000000] reserve setup_data: [mem 0x000000003b5c0000-0x000000003b645fff] reserved
[    0.000000] reserve setup_data: [mem 0x000000003b646000-0x000000003bffffff] usable
[    0.000000] reserve setup_data: [mem 0x000000003c000000-0x000000003dffffff] reserved
[    0.000000] reserve setup_data: [mem 0x0000000040000000-0x000000004fffffff] reserved
[    0.000000] reserve setup_data: [mem 0x00000000fed1c000-0x00000000fed44fff] reserved
[    0.000000] reserve setup_data: [mem 0x00000000ff000000-0x00000000ffffffff] reserved
[    0.000000] reserve setup_data: [mem 0x0000000100000000-0x00000004bfffffff] usable
[    0.000000] efi: EFI v2.4 by American Megatrends
[    0.000000] efi: ESRT=0x3b548218 ACPI=0x3a841000 ACPI 2.0=0x3a841000 SMBIOS=0xf05e0 SMBIOS 3.0=0x3b410000 MOKvar=0x3b40f000 INITRD=0x316a4898 
[    0.000000] efi: Remove mem31: MMIO range=[0x40000000-0x4fffffff] (256MB) from e820 map
[    0.000000] e820: remove [mem 0x40000000-0x4fffffff] reserved
[    0.000000] efi: Not removing mem32: MMIO range=[0xfed1c000-0xfed44fff] (164KB) from e820 map
[    0.000000] efi: Remove mem33: MMIO range=[0xff000000-0xffffffff] (16MB) from e820 map
[    0.000000] e820: remove [mem 0xff000000-0xffffffff] reserved
[    0.000000] SMBIOS 3.0.0 present.
[    0.000000] DMI: MSI MS-7885/X99A GAMING 7 (MS-7885), BIOS H.G0 06/15/2018
[    0.000000] DMI: Memory slots populated: 2/8
[    0.000000] secureboot: Secure boot disabled
[    0.000000] tsc: Fast TSC calibration using PIT
[    0.000000] tsc: Detected 3875.225 MHz processor
[    0.000000] [Firmware Bug]: TSC ADJUST: CPU0: -84577566923754 force to 0
[    0.000562] e820: update [mem 0x00000000-0x00000fff] usable ==> reserved
[    0.000564] e820: remove [mem 0x000a0000-0x000fffff] usable
[    0.000569] last_pfn = 0x4c0000 max_arch_pfn = 0x400000000
[    0.000573] MTRR map: 5 entries (3 fixed + 2 variable; max 23), built from 10 variable MTRRs
[    0.000575] x86/PAT: Configuration [0-7]: WB  WC  UC- UC  WB  WP  UC- WT  
[    0.000991] last_pfn = 0x3c000 max_arch_pfn = 0x400000000
[    0.006422] found SMP MP-table at [mem 0x000fcd10-0x000fcd1f]
[    0.006431] esrt: Reserving ESRT space from 0x000000003b548218 to 0x000000003b548250.
[    0.006437] Using GB pages for direct mapping
[    0.006558] secureboot: Secure boot disabled
[    0.006558] RAMDISK: [mem 0x2a561000-0x2f413fff]
[    0.006886] ACPI: Early table checksum verification disabled
[    0.006889] ACPI: RSDP 0x000000003A841000 000024 (v02 ALASKA)
[    0.006892] ACPI: XSDT 0x000000003A841098 0000AC (v01 ALASKA A M I    01072009 AMI  00010013)
[    0.006896] ACPI: FACP 0x000000003A874F08 00010C (v05 ALASKA A M I    01072009 AMI  00010013)
[    0.006901] ACPI: DSDT 0x000000003A8411D8 033D2E (v02 ALASKA A M I    01072009 INTL 20091013)
[    0.006904] ACPI: FACS 0x000000003ABD8F80 000040
[    0.006906] ACPI: APIC 0x000000003A875018 000100 (v03 ALASKA A M I    01072009 AMI  00010013)
[    0.006909] ACPI: FPDT 0x000000003A875118 000044 (v01 ALASKA A M I    01072009 AMI  00010013)
[    0.006911] ACPI: FIDT 0x000000003A875160 00009C (v01 ALASKA A M I    01072009 AMI  00010013)
[    0.006913] ACPI: MCFG 0x000000003A875200 00003C (v01 ALASKA A M I    01072009 MSFT 00000097)
[    0.006916] ACPI: SSDT 0x000000003A875240 000495 (v01 IdeRef IdeTable 00001000 INTL 20120913)
[    0.006918] ACPI: UEFI 0x000000003A8756D8 000042 (v01 ALASKA A M I    01072009      00000000)
[    0.006921] ACPI: HPET 0x000000003A875720 000038 (v01 ALASKA A M I    00000001 INTL 20091013)
[    0.006923] ACPI: MSCT 0x000000003A875758 000090 (v01 ALASKA A M I    00000001 INTL 20091013)
[    0.006926] ACPI: SLIT 0x000000003A8757E8 00002D (v01 ALASKA A M I    00000001 INTL 20091013)
[    0.006928] ACPI: SRAT 0x000000003A875818 001158 (v03 ALASKA A M I    00000001 INTL 20091013)
[    0.006930] ACPI: WDDT 0x000000003A876970 000040 (v01 ALASKA A M I    00000000 INTL 20091013)
[    0.006933] ACPI: SSDT 0x000000003A8769B0 015307 (v02 ALASKA PmMgt    00000001 INTL 20120913)
[    0.006935] ACPI: NITR 0x000000003A88BCB8 000071 (v02 ALASKA A M I    00000001 INTL 20091013)
[    0.006938] ACPI: BGRT 0x000000003A88BD30 000038 (v01 ALASKA A M I    01072009 AMI  00010013)
[    0.006940] ACPI: DMAR 0x000000003A88BD68 0000DC (v01 ALASKA A M I    00000001 INTL 20091013)
[    0.006942] ACPI: ASF! 0x000000003A88BE48 0000A0 (v32 INTEL   HCG     00000001 TFSM 000F4240)
[    0.006944] ACPI: Reserving FACP table memory at [mem 0x3a874f08-0x3a875013]
[    0.006946] ACPI: Reserving DSDT table memory at [mem 0x3a8411d8-0x3a874f05]
[    0.006946] ACPI: Reserving FACS table memory at [mem 0x3abd8f80-0x3abd8fbf]
[    0.006947] ACPI: Reserving APIC table memory at [mem 0x3a875018-0x3a875117]
[    0.006947] ACPI: Reserving FPDT table memory at [mem 0x3a875118-0x3a87515b]
[    0.006948] ACPI: Reserving FIDT table memory at [mem 0x3a875160-0x3a8751fb]
[    0.006949] ACPI: Reserving MCFG table memory at [mem 0x3a875200-0x3a87523b]
[    0.006949] ACPI: Reserving SSDT table memory at [mem 0x3a875240-0x3a8756d4]
[    0.006950] ACPI: Reserving UEFI table memory at [mem 0x3a8756d8-0x3a875719]
[    0.006951] ACPI: Reserving HPET table memory at [mem 0x3a875720-0x3a875757]
[    0.006951] ACPI: Reserving MSCT table memory at [mem 0x3a875758-0x3a8757e7]
[    0.006952] ACPI: Reserving SLIT table memory at [mem 0x3a8757e8-0x3a875814]
[    0.006953] ACPI: Reserving SRAT table memory at [mem 0x3a875818-0x3a87696f]
[    0.006953] ACPI: Reserving WDDT table memory at [mem 0x3a876970-0x3a8769af]
[    0.006954] ACPI: Reserving SSDT table memory at [mem 0x3a8769b0-0x3a88bcb6]
[    0.006954] ACPI: Reserving NITR table memory at [mem 0x3a88bcb8-0x3a88bd28]
[    0.006955] ACPI: Reserving BGRT table memory at [mem 0x3a88bd30-0x3a88bd67]
[    0.006956] ACPI: Reserving DMAR table memory at [mem 0x3a88bd68-0x3a88be43]
[    0.006956] ACPI: Reserving ASF! table memory at [mem 0x3a88be48-0x3a88bee7]
[    0.006994] ACPI: SRAT: Node 0 PXM 0 [mem 0x00000000-0x3fffffff]
[    0.006995] ACPI: SRAT: Node 0 PXM 0 [mem 0x100000000-0x4bfffffff]
[    0.007000] NUMA: Initialized distance table, cnt=1
[    0.007002] NUMA: Node 0 [mem 0x00001000-0x3fffffff] + [mem 0x100000000-0x4bfffffff] -> [mem 0x00001000-0x4bfffffff]
[    0.007009] NODE_DATA(0) allocated [mem 0x4bffd4540-0x4bfffefff]
[    0.007155] Zone ranges:
[    0.007155]   DMA      [mem 0x0000000000001000-0x0000000000ffffff]
[    0.007157]   DMA32    [mem 0x0000000001000000-0x00000000ffffffff]
[    0.007158]   Normal   [mem 0x0000000100000000-0x00000004bfffffff]
[    0.007159]   Device   empty
[    0.007160] Movable zone start for each node
[    0.007162] Early memory node ranges
[    0.007162]   node   0: [mem 0x0000000000001000-0x000000000009ffff]
[    0.007163]   node   0: [mem 0x0000000000100000-0x000000003901ffff]
[    0.007164]   node   0: [mem 0x000000003b5bf000-0x000000003b5bffff]
[    0.007165]   node   0: [mem 0x000000003b646000-0x000000003bffffff]
[    0.007166]   node   0: [mem 0x0000000100000000-0x00000004bfffffff]
[    0.007167] Initmem setup node 0 [mem 0x0000000000001000-0x00000004bfffffff]
[    0.007172] On node 0, zone DMA: 1 pages in unavailable ranges
[    0.007192] On node 0, zone DMA: 96 pages in unavailable ranges
[    0.008440] On node 0, zone DMA32: 9631 pages in unavailable ranges
[    0.008456] On node 0, zone DMA32: 134 pages in unavailable ranges
[    0.031700] On node 0, zone Normal: 16384 pages in unavailable ranges
[    0.031786] ACPI: PM-Timer IO Port: 0x408
[    0.031795] ACPI: LAPIC_NMI (acpi_id[0x00] high edge lint[0x1])
[    0.031797] ACPI: LAPIC_NMI (acpi_id[0x02] high edge lint[0x1])
[    0.031797] ACPI: LAPIC_NMI (acpi_id[0x04] high edge lint[0x1])
[    0.031798] ACPI: LAPIC_NMI (acpi_id[0x06] high edge lint[0x1])
[    0.031798] ACPI: LAPIC_NMI (acpi_id[0x08] high edge lint[0x1])
[    0.031799] ACPI: LAPIC_NMI (acpi_id[0x0a] high edge lint[0x1])
[    0.031800] ACPI: LAPIC_NMI (acpi_id[0x01] high edge lint[0x1])
[    0.031800] ACPI: LAPIC_NMI (acpi_id[0x03] high edge lint[0x1])
[    0.031801] ACPI: LAPIC_NMI (acpi_id[0x05] high edge lint[0x1])
[    0.031801] ACPI: LAPIC_NMI (acpi_id[0x07] high edge lint[0x1])
[    0.031802] ACPI: LAPIC_NMI (acpi_id[0x09] high edge lint[0x1])
[    0.031802] ACPI: LAPIC_NMI (acpi_id[0x0b] high edge lint[0x1])
[    0.031812] IOAPIC[0]: apic_id 1, version 32, address 0xfec00000, GSI 0-23
[    0.031816] IOAPIC[1]: apic_id 2, version 32, address 0xfec01000, GSI 24-47
[    0.031817] ACPI: INT_SRC_OVR (bus 0 bus_irq 0 global_irq 2 dfl dfl)
[    0.031819] ACPI: INT_SRC_OVR (bus 0 bus_irq 9 global_irq 9 high level)
[    0.031822] ACPI: Using ACPI (MADT) for SMP configuration information
[    0.031823] ACPI: HPET id: 0x8086a701 base: 0xfed00000
[    0.031830] e820: update [mem 0x35232000-0x35472fff] usable ==> reserved
[    0.031840] TSC deadline timer available
[    0.031843] CPU topo: Max. logical packages:   1
[    0.031844] CPU topo: Max. logical dies:       1
[    0.031844] CPU topo: Max. dies per package:   1
[    0.031848] CPU topo: Max. threads per core:   2
[    0.031849] CPU topo: Num. cores per package:     6
[    0.031850] CPU topo: Num. threads per package:  12
[    0.031850] CPU topo: Allowing 12 present CPUs plus 0 hotplug CPUs
[    0.031861] PM: hibernation: Registered nosave memory: [mem 0x00000000-0x00000fff]
[    0.031862] PM: hibernation: Registered nosave memory: [mem 0x000a0000-0x000fffff]
[    0.031863] PM: hibernation: Registered nosave memory: [mem 0x35232000-0x35472fff]
[    0.031865] PM: hibernation: Registered nosave memory: [mem 0x39020000-0x3b5befff]
[    0.031866] PM: hibernation: Registered nosave memory: [mem 0x3b5c0000-0x3b645fff]
[    0.031867] PM: hibernation: Registered nosave memory: [mem 0x3c000000-0xffffffff]
[    0.031868] [mem 0x3e000000-0xfed1bfff] available for PCI devices
[    0.031869] Booting paravirtualized kernel on bare hardware
[    0.031871] clocksource: refined-jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 1910969940391419 ns
[    0.031877] setup_percpu: NR_CPUS:8192 nr_cpumask_bits:12 nr_cpu_ids:12 nr_node_ids:1
[    0.032627] percpu: Embedded 88 pages/cpu s237568 r8192 d114688 u524288
[    0.032633] pcpu-alloc: s237568 r8192 d114688 u524288 alloc=1*2097152
[    0.032635] pcpu-alloc: [0] 00 01 02 03 [0] 04 05 06 07 
[    0.032639] pcpu-alloc: [0] 08 09 10 11 
[    0.032653] Kernel command line: BOOT_IMAGE=/casper/vmlinuz boot=casper uuid=6e72f523-dc09-4880-8910-93ffa64401c5 username=mint hostname=mint iso-scan/filename= quiet splash --
[    0.032761] Unknown kernel command line parameters "splash BOOT_IMAGE=/casper/vmlinuz boot=casper uuid=6e72f523-dc09-4880-8910-93ffa64401c5 username=mint iso-scan/filename=", will be passed to user space.
[    0.032769] random: crng init done
[    0.032770] printk: log buffer data + meta data: 262144 + 917504 = 1179648 bytes
[    0.034295] Dentry cache hash table entries: 2097152 (order: 12, 16777216 bytes, linear)
[    0.035045] Inode-cache hash table entries: 1048576 (order: 11, 8388608 bytes, linear)
[    0.035206] Fallback order for Node 0: 0 
[    0.035210] Built 1 zonelists, mobility grouping on.  Total pages: 4168058
[    0.035211] Policy zone: Normal
[    0.035218] mem auto-init: stack:all(zero), heap alloc:on, heap free:off
[    0.035227] software IO TLB: area num 16.
[    0.083317] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=12, Nodes=1
[    0.083351] Kernel/User page tables isolation: enabled
[    0.083384] ftrace: allocating 60485 entries in 237 pages
[    0.106921] ftrace: allocated 237 pages with 6 groups
[    0.107610] Dynamic Preempt: voluntary
[    0.107690] rcu: Preemptible hierarchical RCU implementation.
[    0.107692] rcu: 	RCU restricting CPUs from NR_CPUS=8192 to nr_cpu_ids=12.
[    0.107693] 	Trampoline variant of Tasks RCU enabled.
[    0.107693] 	Rude variant of Tasks RCU enabled.
[    0.107694] 	Tracing variant of Tasks RCU enabled.
[    0.107694] rcu: RCU calculated value of scheduler-enlistment delay is 100 jiffies.
[    0.107695] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=12
[    0.107706] RCU Tasks: Setting shift to 4 and lim to 1 rcu_task_cb_adjust=1 rcu_task_cpu_ids=12.
[    0.107708] RCU Tasks Rude: Setting shift to 4 and lim to 1 rcu_task_cb_adjust=1 rcu_task_cpu_ids=12.
[    0.107710] RCU Tasks Trace: Setting shift to 4 and lim to 1 rcu_task_cb_adjust=1 rcu_task_cpu_ids=12.
[    0.110523] NR_IRQS: 524544, nr_irqs: 928, preallocated irqs: 16
[    0.110717] rcu: srcu_init: Setting srcu_struct sizes based on contention.
[    0.110798] Console: colour dummy device 80x25
[    0.110800] printk: legacy console [tty0] enabled
[    0.110846] ACPI: Core revision 20240827
[    0.111022] clocksource: hpet: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 133484882848 ns
[    0.111034] APIC: Switch to symmetric I/O mode setup
[    0.111035] DMAR: Host address width 46
[    0.111037] DMAR: DRHD base: 0x000000fbffd000 flags: 0x0
[    0.111047] DMAR: dmar0: reg_base_addr fbffd000 ver 1:0 cap 8d2008c10ef0466 ecap f0205b
[    0.111049] DMAR: DRHD base: 0x000000fbffc000 flags: 0x1
[    0.111052] DMAR: dmar1: reg_base_addr fbffc000 ver 1:0 cap 8d2078c106f0466 ecap f020df
[    0.111054] DMAR: RMRR base: 0x0000003b422000 end: 0x0000003b431fff
[    0.111055] DMAR: ATSR flags: 0x0
[    0.111058] DMAR: RHSA base: 0x000000fbffc000 proximity domain: 0x0
[    0.111060] DMAR-IR: IOAPIC id 1 under DRHD base  0xfbffc000 IOMMU 1
[    0.111061] DMAR-IR: IOAPIC id 2 under DRHD base  0xfbffc000 IOMMU 1
[    0.111062] DMAR-IR: HPET id 0 under DRHD base 0xfbffc000
[    0.111063] DMAR-IR: x2apic is disabled because BIOS sets x2apic opt out bit.
[    0.111064] DMAR-IR: Use 'intremap=no_x2apic_optout' to override the BIOS setting.
[    0.111548] DMAR-IR: Enabled IRQ remapping in xapic mode
[    0.111550] x2apic: IRQ remapping doesn't support X2APIC mode
[    0.112038] ..TIMER: vector=0x30 apic1=0 pin1=2 apic2=-1 pin2=-1
[    0.117033] clocksource: tsc-early: mask: 0xffffffffffffffff max_cycles: 0x6fb7de32a32, max_idle_ns: 881590701073 ns
[    0.117037] Calibrating delay loop (skipped), value calculated using timer frequency.. 7750.45 BogoMIPS (lpj=3875225)
[    0.117060] CPU0: Thermal monitoring enabled (TM1)
[    0.117117] Last level iTLB entries: 4KB 64, 2MB 8, 4MB 8
[    0.117118] Last level dTLB entries: 4KB 64, 2MB 32, 4MB 32, 1GB 4
[    0.117121] process: using mwait in idle threads
[    0.117122] Spectre V1 : Mitigation: usercopy/swapgs barriers and __user pointer sanitization
[    0.117124] Spectre V2 : Mitigation: Retpolines
[    0.117125] Spectre V2 : Spectre v2 / SpectreRSB: Filling RSB on context switch and VMEXIT
[    0.117126] Spectre V2 : Enabling Restricted Speculation for firmware calls
[    0.117128] Spectre V2 : mitigation: Enabling conditional Indirect Branch Prediction Barrier
[    0.117129] Spectre V2 : User space: Mitigation: STIBP via prctl
[    0.117130] Speculative Store Bypass: Mitigation: Speculative Store Bypass disabled via prctl
[    0.117134] MDS: Mitigation: Clear CPU buffers
[    0.117135] TAA: Mitigation: Clear CPU buffers
[    0.117136] MMIO Stale Data: Mitigation: Clear CPU buffers
[    0.117137] VMSCAPE: Mitigation: IBPB before exit to userspace
[    0.117140] x86/fpu: Supporting XSAVE feature 0x001: 'x87 floating point registers'
[    0.117141] x86/fpu: Supporting XSAVE feature 0x002: 'SSE registers'
[    0.117142] x86/fpu: Supporting XSAVE feature 0x004: 'AVX registers'
[    0.117143] x86/fpu: xstate_offset[2]:  576, xstate_sizes[2]:  256
[    0.117145] x86/fpu: Enabled xstate features 0x7, context size is 832 bytes, using 'standard' format.
[    0.136218] Freeing SMP alternatives memory: 48K
[    0.136222] pid_max: default: 32768 minimum: 301
[    0.138909] LSM: initializing lsm=lockdown,capability,landlock,yama,apparmor,ima,evm
[    0.138924] landlock: Up and running.
[    0.138924] Yama: becoming mindful.
[    0.138962] AppArmor: AppArmor initialized
[    0.139020] Mount-cache hash table entries: 32768 (order: 6, 262144 bytes, linear)
[    0.139041] Mountpoint-cache hash table entries: 32768 (order: 6, 262144 bytes, linear)
[    0.140090] smpboot: CPU0: Intel(R) Core(TM) i7-6850K CPU @ 3.60GHz (family: 0x6, model: 0x4f, stepping: 0x1)
[    0.140302] Performance Events: PEBS fmt2+, Broadwell events, 16-deep LBR, full-width counters, Intel PMU driver.
[    0.140319] ... version:                3
[    0.140320] ... bit width:              48
[    0.140321] ... generic registers:      4
[    0.140321] ... value mask:             0000ffffffffffff
[    0.140322] ... max period:             00007fffffffffff
[    0.140323] ... fixed-purpose events:   3
[    0.140324] ... event mask:             000000070000000f
[    0.140413] signal: max sigframe size: 1776
[    0.140425] Estimated ratio of average max frequency by base frequency (times 1024): 1024
[    0.141853] rcu: Hierarchical SRCU implementation.
[    0.141854] rcu: 	Max phase no-delay instances is 400.
[    0.141900] Timer migration: 2 hierarchy levels; 8 children per group; 2 crossnode level
[    0.142648] NMI watchdog: Enabled. Permanently consumes one hw-PMU counter.
[    0.142745] smp: Bringing up secondary CPUs ...
[    0.142834] smpboot: x86: Booting SMP configuration:
[    0.142835] .... node  #0, CPUs:        #1  #2  #3  #4  #5
[    0.002290] [Firmware Bug]: TSC ADJUST differs within socket(s), fixing all errors
[    0.146138]   #6  #7  #8  #9 #10 #11
[    0.148061] MDS CPU bug present and SMT on, data leak possible. See https://www.kernel.org/doc/html/latest/admin-guide/hw-vuln/mds.html for more details.
[    0.148065] TAA CPU bug present and SMT on, data leak possible. See https://www.kernel.org/doc/html/latest/admin-guide/hw-vuln/tsx_async_abort.html for more details.
[    0.148066] MMIO Stale Data CPU bug present and SMT on, data leak possible. See https://www.kernel.org/doc/html/latest/admin-guide/hw-vuln/processor_mmio_stale_data.html for more details.
[    0.148066] VMSCAPE: SMT on, STIBP is required for full protection. See https://www.kernel.org/doc/html/latest/admin-guide/hw-vuln/vmscape.html for more details.
[    0.148101] smp: Brought up 1 node, 12 CPUs
[    0.148101] smpboot: Total of 12 processors activated (93005.40 BogoMIPS)
[    0.149141] Memory: 16153444K/16672232K available (21475K kernel code, 4587K rwdata, 15072K rodata, 5140K init, 4412K bss, 494572K reserved, 0K cma-reserved)
[    0.149548] devtmpfs: initialized
[    0.149548] x86/mm: Memory block size: 128MB
[    0.150934] ACPI: PM: Registering ACPI NVS region [mem 0x39d8e000-0x3abd9fff] (14991360 bytes)
[    0.151120] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 1911260446275000 ns
[    0.151138] futex hash table entries: 4096 (order: 6, 262144 bytes, linear)
[    0.151205] pinctrl core: initialized pinctrl subsystem
[    0.151297] PM: RTC time: 05:19:42, date: 2026-01-21
[    0.151734] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    0.151964] DMA: preallocated 2048 KiB GFP_KERNEL pool for atomic allocations
[    0.152089] DMA: preallocated 2048 KiB GFP_KERNEL|GFP_DMA pool for atomic allocations
[    0.152217] DMA: preallocated 2048 KiB GFP_KERNEL|GFP_DMA32 pool for atomic allocations
[    0.152226] audit: initializing netlink subsys (disabled)
[    0.152233] audit: type=2000 audit(1768972782.040:1): state=initialized audit_enabled=0 res=1
[    0.152233] thermal_sys: Registered thermal governor 'fair_share'
[    0.152233] thermal_sys: Registered thermal governor 'bang_bang'
[    0.152233] thermal_sys: Registered thermal governor 'step_wise'
[    0.152233] thermal_sys: Registered thermal governor 'user_space'
[    0.152233] thermal_sys: Registered thermal governor 'power_allocator'
[    0.152233] cpuidle: using governor ladder
[    0.152233] cpuidle: using governor menu
[    0.152233] ACPI FADT declares the system doesn't support PCIe ASPM, so disable it
[    0.152233] acpiphp: ACPI Hot Plug PCI Controller Driver version: 0.5
[    0.152233] PCI: ECAM [mem 0x40000000-0x4fffffff] (base 0x40000000) for domain 0000 [bus 00-ff]
[    0.152233] PCI: Using configuration type 1 for base access
[    0.152273] kprobes: kprobe jump-optimization is enabled. All kprobes are optimized if possible.
[    0.152281] HugeTLB: registered 1.00 GiB page size, pre-allocated 0 pages
[    0.152281] HugeTLB: 16380 KiB vmemmap can be freed for a 1.00 GiB page
[    0.152281] HugeTLB: registered 2.00 MiB page size, pre-allocated 0 pages
[    0.152281] HugeTLB: 28 KiB vmemmap can be freed for a 2.00 MiB page
[    0.153592] ACPI: Added _OSI(Module Device)
[    0.153594] ACPI: Added _OSI(Processor Device)
[    0.153596] ACPI: Added _OSI(Processor Aggregator Device)
[    0.203098] ACPI: 3 ACPI AML tables successfully acquired and loaded
[    0.207292] ACPI: [Firmware Bug]: BIOS _OSI(Linux) query ignored
[    0.209272] ACPI: Dynamic OEM Table Load:
[    0.232567] ACPI: Interpreter enabled
[    0.232579] ACPI: PM: (supports S0 S3 S4 S5)
[    0.232580] ACPI: Using IOAPIC for interrupt routing
[    0.235117] PCI: Using host bridge windows from ACPI; if necessary, use "pci=nocrs" and report a bug
[    0.235119] PCI: Using E820 reservations for host bridge windows
[    0.235763] ACPI: Enabled 4 GPEs in block 00 to 3F
[    0.269734] ACPI: PCI Root Bridge [UNC0] (domain 0000 [bus ff])
[    0.269739] acpi PNP0A03:03: _OSC: OS supports [ExtendedConfig ASPM ClockPM Segments MSI EDR HPX-Type3]
[    0.271555] acpi PNP0A03:03: _OSC: platform does not support [SHPCHotplug PME AER LTR DPC]
[    0.272572] acpi PNP0A03:03: _OSC: OS now controls [PCIeHotplug PCIeCapability]
[    0.272573] acpi PNP0A03:03: FADT indicates ASPM is unsupported, using BIOS configuration
[    0.272615] PCI host bridge to bus 0000:ff
[    0.272617] pci_bus 0000:ff: root bus resource [bus ff]
[    0.272630] pci 0000:ff:0b.0: [8086:6f81] type 00 class 0x088000 conventional PCI endpoint
[    0.272696] pci 0000:ff:0b.1: [8086:6f36] type 00 class 0x110100 conventional PCI endpoint
[    0.272747] pci 0000:ff:0b.2: [8086:6f37] type 00 class 0x110100 conventional PCI endpoint
[    0.272798] pci 0000:ff:0b.3: [8086:6f76] type 00 class 0x088000 conventional PCI endpoint
[    0.272859] pci 0000:ff:0c.0: [8086:6fe0] type 00 class 0x088000 conventional PCI endpoint
[    0.272909] pci 0000:ff:0c.1: [8086:6fe1] type 00 class 0x088000 conventional PCI endpoint
[    0.272958] pci 0000:ff:0c.2: [8086:6fe2] type 00 class 0x088000 conventional PCI endpoint
[    0.273007] pci 0000:ff:0c.3: [8086:6fe3] type 00 class 0x088000 conventional PCI endpoint
[    0.273061] pci 0000:ff:0c.4: [8086:6fe4] type 00 class 0x088000 conventional PCI endpoint
[    0.273113] pci 0000:ff:0c.5: [8086:6fe5] type 00 class 0x088000 conventional PCI endpoint
[    0.273163] pci 0000:ff:0f.0: [8086:6ff8] type 00 class 0x088000 conventional PCI endpoint
[    0.273212] pci 0000:ff:0f.1: [8086:6ff9] type 00 class 0x088000 conventional PCI endpoint
[    0.273261] pci 0000:ff:0f.4: [8086:6ffc] type 00 class 0x088000 conventional PCI endpoint
[    0.273311] pci 0000:ff:0f.5: [8086:6ffd] type 00 class 0x088000 conventional PCI endpoint
[    0.273361] pci 0000:ff:0f.6: [8086:6ffe] type 00 class 0x088000 conventional PCI endpoint
[    0.273411] pci 0000:ff:10.0: [8086:6f1d] type 00 class 0x088000 conventional PCI endpoint
[    0.273463] pci 0000:ff:10.1: [8086:6f34] type 00 class 0x110100 conventional PCI endpoint
[    0.273514] pci 0000:ff:10.5: [8086:6f1e] type 00 class 0x088000 conventional PCI endpoint
[    0.273562] pci 0000:ff:10.6: [8086:6f7d] type 00 class 0x110100 conventional PCI endpoint
[    0.273611] pci 0000:ff:10.7: [8086:6f1f] type 00 class 0x088000 conventional PCI endpoint
[    0.273660] pci 0000:ff:12.0: [8086:6fa0] type 00 class 0x088000 conventional PCI endpoint
[    0.273685] pci 0000:ff:12.1: [8086:6f30] type 00 class 0x110100 conventional PCI endpoint
[    0.273745] pci 0000:ff:13.0: [8086:6fa8] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.273862] pci 0000:ff:13.1: [8086:6f71] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.273929] pci 0000:ff:13.2: [8086:6faa] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.273992] pci 0000:ff:13.3: [8086:6fab] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274055] pci 0000:ff:13.4: [8086:6fac] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274119] pci 0000:ff:13.5: [8086:6fad] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274183] pci 0000:ff:13.6: [8086:6fae] type 00 class 0x088000 conventional PCI endpoint
[    0.274235] pci 0000:ff:13.7: [8086:6faf] type 00 class 0x088000 conventional PCI endpoint
[    0.274288] pci 0000:ff:14.0: [8086:6fb0] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274350] pci 0000:ff:14.1: [8086:6fb1] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274415] pci 0000:ff:14.2: [8086:6fb2] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274479] pci 0000:ff:14.3: [8086:6fb3] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274540] pci 0000:ff:14.4: [8086:6fbc] type 00 class 0x088000 conventional PCI endpoint
[    0.274592] pci 0000:ff:14.5: [8086:6fbd] type 00 class 0x088000 conventional PCI endpoint
[    0.274643] pci 0000:ff:14.6: [8086:6fbe] type 00 class 0x088000 conventional PCI endpoint
[    0.274694] pci 0000:ff:14.7: [8086:6fbf] type 00 class 0x088000 conventional PCI endpoint
[    0.274747] pci 0000:ff:15.0: [8086:6fb4] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274810] pci 0000:ff:15.1: [8086:6fb5] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274875] pci 0000:ff:15.2: [8086:6fb6] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.274939] pci 0000:ff:15.3: [8086:6fb7] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.275002] pci 0000:ff:16.0: [8086:6f68] type 00 class 0x088000 conventional PCI endpoint
[    0.275058] pci 0000:ff:16.6: [8086:6f6e] type 00 class 0x088000 conventional PCI endpoint
[    0.275113] pci 0000:ff:16.7: [8086:6f6f] type 00 class 0x088000 conventional PCI endpoint
[    0.275165] pci 0000:ff:17.0: [8086:6fd0] type 00 class 0x088000 conventional PCI endpoint
[    0.275219] pci 0000:ff:17.4: [8086:6fb8] type 00 class 0x088000 conventional PCI endpoint
[    0.275271] pci 0000:ff:17.5: [8086:6fb9] type 00 class 0x088000 conventional PCI endpoint
[    0.275324] pci 0000:ff:17.6: [8086:6fba] type 00 class 0x088000 conventional PCI endpoint
[    0.275376] pci 0000:ff:17.7: [8086:6fbb] type 00 class 0x088000 conventional PCI endpoint
[    0.275431] pci 0000:ff:1e.0: [8086:6f98] type 00 class 0x088000 conventional PCI endpoint
[    0.275481] pci 0000:ff:1e.1: [8086:6f99] type 00 class 0x088000 conventional PCI endpoint
[    0.275531] pci 0000:ff:1e.2: [8086:6f9a] type 00 class 0x088000 conventional PCI endpoint
[    0.275583] pci 0000:ff:1e.3: [8086:6fc0] type 00 class 0x088000 conventional PCI endpoint
[    0.275608] pci 0000:ff:1e.4: [8086:6f9c] type 00 class 0x088000 conventional PCI endpoint
[    0.275660] pci 0000:ff:1f.0: [8086:6f88] type 00 class 0x088000 conventional PCI endpoint
[    0.275714] pci 0000:ff:1f.2: [8086:6f8a] type 00 class 0x088000 conventional PCI endpoint
[    0.280049] ACPI: PCI Root Bridge [PCI0] (domain 0000 [bus 00-fe])
[    0.280053] acpi PNP0A08:00: _OSC: OS supports [ExtendedConfig ASPM ClockPM Segments MSI EDR HPX-Type3]
[    0.280273] acpi PNP0A08:00: _OSC: platform does not support [SHPCHotplug PME AER LTR DPC]
[    0.280685] acpi PNP0A08:00: _OSC: OS now controls [PCIeHotplug PCIeCapability]
[    0.280687] acpi PNP0A08:00: FADT indicates ASPM is unsupported, using BIOS configuration
[    0.281195] PCI host bridge to bus 0000:00
[    0.281198] pci_bus 0000:00: root bus resource [io  0x0000-0x0cf7 window]
[    0.281200] pci_bus 0000:00: root bus resource [io  0x1000-0xffff window]
[    0.281202] pci_bus 0000:00: root bus resource [mem 0x000a0000-0x000bffff window]
[    0.281203] pci_bus 0000:00: root bus resource [mem 0x50000000-0xfbffbfff window]
[    0.281204] pci_bus 0000:00: root bus resource [bus 00-fe]
[    0.281225] pci 0000:00:00.0: [8086:6f00] type 00 class 0x060000 PCIe Root Port
[    0.281360] pci 0000:00:01.0: [8086:6f02] type 01 class 0x060400 PCIe Root Port
[    0.281383] pci 0000:00:01.0: PCI bridge to [bus 01]
[    0.281423] pci 0000:00:01.0: PME# supported from D0 D3hot D3cold
[    0.281634] pci 0000:00:03.0: [8086:6f08] type 01 class 0x060400 PCIe Root Port
[    0.281657] pci 0000:00:03.0: PCI bridge to [bus 02]
[    0.281659] pci 0000:00:03.0:   bridge window [io  0xe000-0xefff]
[    0.281661] pci 0000:00:03.0:   bridge window [mem 0xfa000000-0xfb0fffff]
[    0.281668] pci 0000:00:03.0:   bridge window [mem 0xe0000000-0xf1ffffff 64bit pref]
[    0.281700] pci 0000:00:03.0: PME# supported from D0 D3hot D3cold
[    0.281888] pci 0000:00:05.0: [8086:6f28] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.281976] pci 0000:00:05.1: [8086:6f29] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.282088] pci 0000:00:05.2: [8086:6f2a] type 00 class 0x088000 PCIe Root Complex Integrated Endpoint
[    0.282170] pci 0000:00:05.4: [8086:6f2c] type 00 class 0x080020 PCIe Root Complex Integrated Endpoint
[    0.282207] pci 0000:00:05.4: BAR 0 [mem 0xfb41c000-0xfb41cfff]
[    0.282272] pci 0000:00:11.0: [8086:8d7c] type 00 class 0xff0000 PCIe Root Complex Integrated Endpoint
[    0.282449] pci 0000:00:11.4: [8086:8d62] type 00 class 0x010601 conventional PCI endpoint
[    0.282504] pci 0000:00:11.4: BAR 0 [io  0xf0b0-0xf0b7]
[    0.282506] pci 0000:00:11.4: BAR 1 [io  0xf0a0-0xf0a3]
[    0.282508] pci 0000:00:11.4: BAR 2 [io  0xf090-0xf097]
[    0.282510] pci 0000:00:11.4: BAR 3 [io  0xf080-0xf083]
[    0.282512] pci 0000:00:11.4: BAR 4 [io  0xf000-0xf01f]
[    0.282513] pci 0000:00:11.4: BAR 5 [mem 0xfb41b000-0xfb41b7ff]
[    0.282543] pci 0000:00:11.4: PME# supported from D3hot
[    0.282616] pci 0000:00:14.0: [8086:8d31] type 00 class 0x0c0330 conventional PCI endpoint
[    0.282667] pci 0000:00:14.0: BAR 0 [mem 0xfb400000-0xfb40ffff 64bit]
[    0.282694] pci 0000:00:14.0: PME# supported from D3hot D3cold
[    0.282779] pci 0000:00:16.0: [8086:8d3a] type 00 class 0x078000 conventional PCI endpoint
[    0.282832] pci 0000:00:16.0: BAR 0 [mem 0xfb41a000-0xfb41a00f 64bit]
[    0.282860] pci 0000:00:16.0: PME# supported from D0 D3hot D3cold
[    0.282930] pci 0000:00:1a.0: [8086:8d2d] type 00 class 0x0c0320 conventional PCI endpoint
[    0.282988] pci 0000:00:1a.0: BAR 0 [mem 0xfb417000-0xfb4173ff]
[    0.283025] pci 0000:00:1a.0: PME# supported from D0 D3hot D3cold
[    0.283096] pci 0000:00:1b.0: [8086:8d20] type 00 class 0x040300 PCIe Root Complex Integrated Endpoint
[    0.283145] pci 0000:00:1b.0: BAR 0 [mem 0xfb410000-0xfb413fff 64bit]
[    0.283185] pci 0000:00:1b.0: PME# supported from D0 D3hot D3cold
[    0.283260] pci 0000:00:1c.0: [8086:8d10] type 01 class 0x060400 PCIe Root Port
[    0.283291] pci 0000:00:1c.0: PCI bridge to [bus 03]
[    0.283346] pci 0000:00:1c.0: PME# supported from D0 D3hot D3cold
[    0.283366] pci 0000:00:1c.0: Enabling MPC IRBNCE
[    0.283369] pci 0000:00:1c.0: Intel PCH root port ACS workaround enabled
[    0.283442] pci 0000:00:1c.2: [8086:8d14] type 01 class 0x060400 PCIe Root Port
[    0.283473] pci 0000:00:1c.2: PCI bridge to [bus 04]
[    0.283476] pci 0000:00:1c.2:   bridge window [io  0xd000-0xdfff]
[    0.283479] pci 0000:00:1c.2:   bridge window [mem 0xfb300000-0xfb3fffff]
[    0.283532] pci 0000:00:1c.2: PME# supported from D0 D3hot D3cold
[    0.283551] pci 0000:00:1c.2: Enabling MPC IRBNCE
[    0.283554] pci 0000:00:1c.2: Intel PCH root port ACS workaround enabled
[    0.283630] pci 0000:00:1c.3: [8086:8d16] type 01 class 0x060400 PCIe Root Port
[    0.283661] pci 0000:00:1c.3: PCI bridge to [bus 05]
[    0.283666] pci 0000:00:1c.3:   bridge window [mem 0xfb200000-0xfb2fffff]
[    0.283719] pci 0000:00:1c.3: PME# supported from D0 D3hot D3cold
[    0.283739] pci 0000:00:1c.3: Enabling MPC IRBNCE
[    0.283741] pci 0000:00:1c.3: Intel PCH root port ACS workaround enabled
[    0.283814] pci 0000:00:1c.4: [8086:8d18] type 01 class 0x060400 PCIe Root Port
[    0.283845] pci 0000:00:1c.4: PCI bridge to [bus 06]
[    0.283850] pci 0000:00:1c.4:   bridge window [mem 0xfb100000-0xfb1fffff]
[    0.283903] pci 0000:00:1c.4: PME# supported from D0 D3hot D3cold
[    0.283922] pci 0000:00:1c.4: Enabling MPC IRBNCE
[    0.283925] pci 0000:00:1c.4: Intel PCH root port ACS workaround enabled
[    0.283998] pci 0000:00:1d.0: [8086:8d26] type 00 class 0x0c0320 conventional PCI endpoint
[    0.284055] pci 0000:00:1d.0: BAR 0 [mem 0xfb416000-0xfb4163ff]
[    0.284093] pci 0000:00:1d.0: PME# supported from D0 D3hot D3cold
[    0.284170] pci 0000:00:1f.0: [8086:8d47] type 00 class 0x060100 conventional PCI endpoint
[    0.284328] pci 0000:00:1f.3: [8086:8d22] type 00 class 0x0c0500 conventional PCI endpoint
[    0.284379] pci 0000:00:1f.3: BAR 0 [mem 0xfb415000-0xfb4150ff 64bit]
[    0.284382] pci 0000:00:1f.3: BAR 4 [io  0x0580-0x059f]
[    0.284567] pci 0000:00:01.0: PCI bridge to [bus 01]
[    0.284717] pci 0000:02:00.0: [10de:1b80] type 00 class 0x030000 PCIe Legacy Endpoint
[    0.284764] pci 0000:02:00.0: BAR 0 [mem 0xfa000000-0xfaffffff]
[    0.284767] pci 0000:02:00.0: BAR 1 [mem 0xe0000000-0xefffffff 64bit pref]
[    0.284769] pci 0000:02:00.0: BAR 3 [mem 0xf0000000-0xf1ffffff 64bit pref]
[    0.284771] pci 0000:02:00.0: BAR 5 [io  0xe000-0xe07f]
[    0.284773] pci 0000:02:00.0: ROM [mem 0xfb000000-0xfb07ffff pref]
[    0.284778] pci 0000:02:00.0: enabling Extended Tags
[    0.284806] pci 0000:02:00.0: Video device with shadowed ROM at [mem 0x000c0000-0x000dffff]
[    0.284879] pci 0000:02:00.0: 32.000 Gb/s available PCIe bandwidth, limited by 2.5 GT/s PCIe x16 link at 0000:00:03.0 (capable of 126.016 Gb/s with 8.0 GT/s PCIe x16 link)
[    0.284958] pci 0000:02:00.1: [10de:10f0] type 00 class 0x040300 PCIe Endpoint
[    0.285005] pci 0000:02:00.1: BAR 0 [mem 0xfb080000-0xfb083fff]
[    0.285014] pci 0000:02:00.1: enabling Extended Tags
[    0.285117] pci 0000:00:03.0: PCI bridge to [bus 02]
[    0.285158] pci 0000:00:1c.0: PCI bridge to [bus 03]
[    0.285224] pci 0000:04:00.0: [1969:e091] type 00 class 0x020000 PCIe Endpoint
[    0.285302] pci 0000:04:00.0: BAR 0 [mem 0xfb300000-0xfb33ffff 64bit]
[    0.285304] pci 0000:04:00.0: BAR 2 [io  0xd000-0xd07f]
[    0.285327] pci 0000:04:00.0: [Firmware Bug]: disabling VPD access (can't determine size of non-standard VPD format)
[    0.285385] pci 0000:04:00.0: PME# supported from D0 D1 D2 D3hot D3cold
[    0.285495] pci 0000:00:1c.2: PCI bridge to [bus 04]
[    0.285563] pci 0000:05:00.0: [1106:3483] type 00 class 0x0c0330 PCIe Endpoint
[    0.285629] pci 0000:05:00.0: BAR 0 [mem 0xfb200000-0xfb200fff 64bit]
[    0.285684] pci 0000:05:00.0: PME# supported from D0 D1 D2 D3hot D3cold
[    0.285765] pci 0000:00:1c.3: PCI bridge to [bus 05]
[    0.285835] pci 0000:06:00.0: [1b21:1242] type 00 class 0x0c0330 PCIe Endpoint
[    0.285908] pci 0000:06:00.0: BAR 0 [mem 0xfb100000-0xfb107fff 64bit]
[    0.285923] pci 0000:06:00.0: enabling Extended Tags
[    0.286006] pci 0000:06:00.0: PME# supported from D3hot D3cold
[    0.286156] pci 0000:00:1c.4: PCI bridge to [bus 06]
[    0.286207] pci_bus 0000:00: on NUMA node 0
[    0.286811] ACPI: PCI: Interrupt link LNKA configured for IRQ 11
[    0.286855] ACPI: PCI: Interrupt link LNKB configured for IRQ 10
[    0.286897] ACPI: PCI: Interrupt link LNKC configured for IRQ 3
[    0.286938] ACPI: PCI: Interrupt link LNKD configured for IRQ 5
[    0.286980] ACPI: PCI: Interrupt link LNKE configured for IRQ 0
[    0.286981] ACPI: PCI: Interrupt link LNKE disabled
[    0.287022] ACPI: PCI: Interrupt link LNKF configured for IRQ 0
[    0.287023] ACPI: PCI: Interrupt link LNKF disabled
[    0.287065] ACPI: PCI: Interrupt link LNKG configured for IRQ 7
[    0.287110] ACPI: PCI: Interrupt link LNKH configured for IRQ 0
[    0.287111] ACPI: PCI: Interrupt link LNKH disabled
[    0.288047] iommu: Default domain type: Translated
[    0.288047] iommu: DMA domain TLB invalidation policy: lazy mode
[    0.288184] SCSI subsystem initialized
[    0.288191] libata version 3.00 loaded.
[    0.288191] ACPI: bus type USB registered
[    0.288191] usbcore: registered new interface driver usbfs
[    0.288191] usbcore: registered new interface driver hub
[    0.288191] usbcore: registered new device driver usb
[    0.288191] pps_core: LinuxPPS API ver. 1 registered
[    0.288191] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.288191] PTP clock support registered
[    0.288191] EDAC MC: Ver: 3.0.0
[    0.288191] efivars: Registered efivars operations
[    0.288221] NetLabel: Initializing
[    0.288222] NetLabel:  domain hash size = 128
[    0.288223] NetLabel:  protocols = UNLABELED CIPSOv4 CALIPSO
[    0.288234] NetLabel:  unlabeled traffic allowed by default
[    0.288247] mctp: management component transport protocol core
[    0.288247] NET: Registered PF_MCTP protocol family
[    0.288247] PCI: Using ACPI for IRQ routing
[    0.292946] PCI: pci_cache_line_size set to 64 bytes
[    0.293022] e820: reserve RAM buffer [mem 0x2a534018-0x2bffffff]
[    0.293024] e820: reserve RAM buffer [mem 0x2a541018-0x2bffffff]
[    0.293025] e820: reserve RAM buffer [mem 0x35232000-0x37ffffff]
[    0.293025] e820: reserve RAM buffer [mem 0x39020000-0x3bffffff]
[    0.293026] e820: reserve RAM buffer [mem 0x3b5c0000-0x3bffffff]
[    0.293056] pci 0000:02:00.0: vgaarb: setting as boot VGA device
[    0.293056] pci 0000:02:00.0: vgaarb: bridge control possible
[    0.293056] pci 0000:02:00.0: vgaarb: VGA device added: decodes=io+mem,owns=io+mem,locks=none
[    0.293056] vgaarb: loaded
[    0.293083] hpet0: at MMIO 0xfed00000, IRQs 2, 8, 0, 0, 0, 0, 0, 0
[    0.293089] hpet0: 8 comparators, 64-bit 14.318180 MHz counter
[    0.296060] clocksource: Switched to clocksource tsc-early
[    0.296739] VFS: Disk quotas dquot_6.6.0
[    0.296752] VFS: Dquot-cache hash table entries: 512 (order 0, 4096 bytes)
[    0.296882] AppArmor: AppArmor Filesystem Enabled
[    0.296905] pnp: PnP ACPI init
[    0.297251] system 00:01: [io  0x0500-0x057f] has been reserved
[    0.297254] system 00:01: [io  0x0400-0x047f] could not be reserved
[    0.297256] system 00:01: [io  0x0580-0x059f] has been reserved
[    0.297257] system 00:01: [io  0x0600-0x061f] has been reserved
[    0.297258] system 00:01: [io  0x0880-0x0883] has been reserved
[    0.297260] system 00:01: [io  0x0800-0x081f] has been reserved
[    0.297261] system 00:01: [mem 0xfed1c000-0xfed3ffff] has been reserved
[    0.297263] system 00:01: [mem 0xfed45000-0xfed8bfff] has been reserved
[    0.297264] system 00:01: [mem 0xff000000-0xffffffff] has been reserved
[    0.297265] system 00:01: [mem 0xfee00000-0xfeefffff] has been reserved
[    0.297266] system 00:01: [mem 0xfed12000-0xfed1200f] has been reserved
[    0.297267] system 00:01: [mem 0xfed12010-0xfed1201f] has been reserved
[    0.297269] system 00:01: [mem 0xfed1b000-0xfed1bfff] has been reserved
[    0.297440] system 00:02: [io  0x0a00-0x0a0f] has been reserved
[    0.297442] system 00:02: [io  0x0a10-0x0a1f] has been reserved
[    0.297444] system 00:02: [io  0x0a20-0x0a2f] has been reserved
[    0.297445] system 00:02: [io  0x0a30-0x0a3f] has been reserved
[    0.297810] pnp: PnP ACPI: found 3 devices
[    0.303376] clocksource: acpi_pm: mask: 0xffffff max_cycles: 0xffffff, max_idle_ns: 2085701024 ns
[    0.303423] NET: Registered PF_INET protocol family
[    0.303586] IP idents hash table entries: 262144 (order: 9, 2097152 bytes, linear)
[    0.316578] tcp_listen_portaddr_hash hash table entries: 8192 (order: 5, 131072 bytes, linear)
[    0.316598] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)
[    0.316652] TCP established hash table entries: 131072 (order: 8, 1048576 bytes, linear)
[    0.316802] TCP bind hash table entries: 65536 (order: 9, 2097152 bytes, linear)
[    0.316987] TCP: Hash tables configured (established 131072 bind 65536)
[    0.317072] MPTCP token hash table entries: 16384 (order: 6, 393216 bytes, linear)
[    0.317134] UDP hash table entries: 8192 (order: 7, 524288 bytes, linear)
[    0.317220] UDP-Lite hash table entries: 8192 (order: 7, 524288 bytes, linear)
[    0.317318] NET: Registered PF_UNIX/PF_LOCAL protocol family
[    0.317323] NET: Registered PF_XDP protocol family
[    0.317353] pci 0000:00:01.0: PCI bridge to [bus 01]
[    0.317371] pci 0000:00:03.0: PCI bridge to [bus 02]
[    0.317373] pci 0000:00:03.0:   bridge window [io  0xe000-0xefff]
[    0.317379] pci 0000:00:03.0:   bridge window [mem 0xfa000000-0xfb0fffff]
[    0.317383] pci 0000:00:03.0:   bridge window [mem 0xe0000000-0xf1ffffff 64bit pref]
[    0.317391] pci 0000:00:1c.0: PCI bridge to [bus 03]
[    0.317409] pci 0000:00:1c.2: PCI bridge to [bus 04]
[    0.317411] pci 0000:00:1c.2:   bridge window [io  0xd000-0xdfff]
[    0.317418] pci 0000:00:1c.2:   bridge window [mem 0xfb300000-0xfb3fffff]
[    0.317431] pci 0000:00:1c.3: PCI bridge to [bus 05]
[    0.317437] pci 0000:00:1c.3:   bridge window [mem 0xfb200000-0xfb2fffff]
[    0.317450] pci 0000:00:1c.4: PCI bridge to [bus 06]
[    0.317456] pci 0000:00:1c.4:   bridge window [mem 0xfb100000-0xfb1fffff]
[    0.317469] pci_bus 0000:00: resource 4 [io  0x0000-0x0cf7 window]
[    0.317471] pci_bus 0000:00: resource 5 [io  0x1000-0xffff window]
[    0.317472] pci_bus 0000:00: resource 6 [mem 0x000a0000-0x000bffff window]
[    0.317473] pci_bus 0000:00: resource 7 [mem 0x50000000-0xfbffbfff window]
[    0.317475] pci_bus 0000:02: resource 0 [io  0xe000-0xefff]
[    0.317476] pci_bus 0000:02: resource 1 [mem 0xfa000000-0xfb0fffff]
[    0.317477] pci_bus 0000:02: resource 2 [mem 0xe0000000-0xf1ffffff 64bit pref]
[    0.317478] pci_bus 0000:04: resource 0 [io  0xd000-0xdfff]
[    0.317479] pci_bus 0000:04: resource 1 [mem 0xfb300000-0xfb3fffff]
[    0.317480] pci_bus 0000:05: resource 1 [mem 0xfb200000-0xfb2fffff]
[    0.317482] pci_bus 0000:06: resource 1 [mem 0xfb100000-0xfb1fffff]
[    0.317674] pci 0000:00:05.0: disabled boot interrupts on device [8086:6f28]
[    0.318047] pci 0000:02:00.0: CLS mismatch (64 != 32), using 64 bytes
[    0.318050] pci 0000:02:00.1: extending delay after power-on from D3hot to 20 msec
[    0.318080] pci 0000:02:00.1: D0 power state depends on 0000:02:00.0
[    0.318085] pci 0000:04:00.0: set MSI_INTX_DISABLE_BUG flag
[    0.318353] DMAR: [Firmware Bug]: RMRR entry for device 05:00.0 is broken - applying workaround
[    0.318357] DMAR: [Firmware Bug]: RMRR entry for device 06:00.0 is broken - applying workaround
[    0.318359] DMAR: No SATC found
[    0.318361] DMAR: dmar0: Using Queued invalidation
[    0.318364] DMAR: dmar1: Using Queued invalidation
[    0.318387] Trying to unpack rootfs image as initramfs...
[    0.318469] pci 0000:00:1b.0: Adding to iommu group 0
[    0.318655] pci 0000:ff:0b.0: Adding to iommu group 1
[    0.318679] pci 0000:ff:0b.1: Adding to iommu group 1
[    0.318700] pci 0000:ff:0b.2: Adding to iommu group 1
[    0.318721] pci 0000:ff:0b.3: Adding to iommu group 1
[    0.318836] pci 0000:ff:0c.0: Adding to iommu group 2
[    0.318858] pci 0000:ff:0c.1: Adding to iommu group 2
[    0.318880] pci 0000:ff:0c.2: Adding to iommu group 2
[    0.318902] pci 0000:ff:0c.3: Adding to iommu group 2
[    0.318924] pci 0000:ff:0c.4: Adding to iommu group 2
[    0.318946] pci 0000:ff:0c.5: Adding to iommu group 2
[    0.319046] pci 0000:ff:0f.0: Adding to iommu group 3
[    0.319072] pci 0000:ff:0f.1: Adding to iommu group 3
[    0.319096] pci 0000:ff:0f.4: Adding to iommu group 3
[    0.319118] pci 0000:ff:0f.5: Adding to iommu group 3
[    0.319142] pci 0000:ff:0f.6: Adding to iommu group 3
[    0.319242] pci 0000:ff:10.0: Adding to iommu group 4
[    0.319267] pci 0000:ff:10.1: Adding to iommu group 4
[    0.319295] pci 0000:ff:10.5: Adding to iommu group 4
[    0.319319] pci 0000:ff:10.6: Adding to iommu group 4
[    0.319343] pci 0000:ff:10.7: Adding to iommu group 4
[    0.319397] pci 0000:ff:12.0: Adding to iommu group 5
[    0.319422] pci 0000:ff:12.1: Adding to iommu group 5
[    0.319444] pci 0000:ff:13.0: Adding to iommu group 6
[    0.319466] pci 0000:ff:13.1: Adding to iommu group 7
[    0.319490] pci 0000:ff:13.2: Adding to iommu group 8
[    0.319512] pci 0000:ff:13.3: Adding to iommu group 9
[    0.319535] pci 0000:ff:13.4: Adding to iommu group 10
[    0.319557] pci 0000:ff:13.5: Adding to iommu group 11
[    0.319613] pci 0000:ff:13.6: Adding to iommu group 12
[    0.319641] pci 0000:ff:13.7: Adding to iommu group 12
[    0.319663] pci 0000:ff:14.0: Adding to iommu group 13
[    0.319686] pci 0000:ff:14.1: Adding to iommu group 14
[    0.319709] pci 0000:ff:14.2: Adding to iommu group 15
[    0.319732] pci 0000:ff:14.3: Adding to iommu group 16
[    0.319815] pci 0000:ff:14.4: Adding to iommu group 17
[    0.319845] pci 0000:ff:14.5: Adding to iommu group 17
[    0.319873] pci 0000:ff:14.6: Adding to iommu group 17
[    0.319900] pci 0000:ff:14.7: Adding to iommu group 17
[    0.319924] pci 0000:ff:15.0: Adding to iommu group 18
[    0.319947] pci 0000:ff:15.1: Adding to iommu group 19
[    0.319969] pci 0000:ff:15.2: Adding to iommu group 20
[    0.319993] pci 0000:ff:15.3: Adding to iommu group 21
[    0.320062] pci 0000:ff:16.0: Adding to iommu group 22
[    0.320091] pci 0000:ff:16.6: Adding to iommu group 22
[    0.320120] pci 0000:ff:16.7: Adding to iommu group 22
[    0.320220] pci 0000:ff:17.0: Adding to iommu group 23
[    0.320250] pci 0000:ff:17.4: Adding to iommu group 23
[    0.320280] pci 0000:ff:17.5: Adding to iommu group 23
[    0.320312] pci 0000:ff:17.6: Adding to iommu group 23
[    0.320342] pci 0000:ff:17.7: Adding to iommu group 23
[    0.320440] pci 0000:ff:1e.0: Adding to iommu group 24
[    0.320470] pci 0000:ff:1e.1: Adding to iommu group 24
[    0.320500] pci 0000:ff:1e.2: Adding to iommu group 24
[    0.320533] pci 0000:ff:1e.3: Adding to iommu group 24
[    0.320563] pci 0000:ff:1e.4: Adding to iommu group 24
[    0.320615] pci 0000:ff:1f.0: Adding to iommu group 25
[    0.320647] pci 0000:ff:1f.2: Adding to iommu group 25
[    0.320669] pci 0000:00:00.0: Adding to iommu group 26
[    0.320693] pci 0000:00:01.0: Adding to iommu group 27
[    0.320715] pci 0000:00:03.0: Adding to iommu group 28
[    0.320737] pci 0000:00:05.0: Adding to iommu group 29
[    0.320760] pci 0000:00:05.1: Adding to iommu group 30
[    0.320783] pci 0000:00:05.2: Adding to iommu group 31
[    0.320806] pci 0000:00:05.4: Adding to iommu group 32
[    0.320828] pci 0000:00:11.0: Adding to iommu group 33
[    0.320866] pci 0000:00:11.4: Adding to iommu group 34
[    0.320890] pci 0000:00:14.0: Adding to iommu group 35
[    0.320931] pci 0000:00:16.0: Adding to iommu group 36
[    0.320953] pci 0000:00:1a.0: Adding to iommu group 37
[    0.320977] pci 0000:00:1c.0: Adding to iommu group 38
[    0.321000] pci 0000:00:1c.2: Adding to iommu group 39
[    0.321022] pci 0000:00:1c.3: Adding to iommu group 40
[    0.321045] pci 0000:00:1c.4: Adding to iommu group 41
[    0.321068] pci 0000:00:1d.0: Adding to iommu group 42
[    0.321121] pci 0000:00:1f.0: Adding to iommu group 43
[    0.321155] pci 0000:00:1f.3: Adding to iommu group 43
[    0.321210] pci 0000:02:00.0: Adding to iommu group 44
[    0.321246] pci 0000:02:00.1: Adding to iommu group 44
[    0.321270] pci 0000:04:00.0: Adding to iommu group 45
[    0.321295] pci 0000:05:00.0: Adding to iommu group 46
[    0.321318] pci 0000:06:00.0: Adding to iommu group 47
[    0.325643] DMAR: Intel(R) Virtualization Technology for Directed I/O
[    0.325648] PCI-DMA: Using software bounce buffering for IO (SWIOTLB)
[    0.325649] software IO TLB: mapped [mem 0x0000000026534000-0x000000002a534000] (64MB)
[    0.342381] Initialise system trusted keyrings
[    0.342394] Key type blacklist registered
[    0.342438] workingset: timestamp_bits=36 max_order=22 bucket_order=0
[    0.342449] zbud: loaded
[    0.342650] squashfs: version 4.0 (2009/01/31) Phillip Lougher
[    0.342726] fuse: init (API version 7.42)
[    0.342847] integrity: Platform Keyring initialized
[    0.342851] integrity: Machine keyring initialized
[    0.352418] Key type asymmetric registered
[    0.352422] Asymmetric key parser 'x509' registered
[    0.352446] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 243)
[    0.352496] io scheduler mq-deadline registered
[    0.352797] ledtrig-cpu: registered to indicate activity on CPUs
[    0.354183] shpchp: Standard Hot Plug PCI Controller Driver version: 0.4
[    0.354313] Monitor-Mwait will be used to enter C-1 state
[    0.354323] Monitor-Mwait will be used to enter C-2 state
[    0.354982] input: Power Button as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0C0C:00/input/input0
[    0.355006] ACPI: button: Power Button [PWRB]
[    0.355029] input: Power Button as /devices/LNXSYSTM:00/LNXPWRBN:00/input/input1
[    0.355064] ACPI: button: Power Button [PWRF]
[    0.356909] Serial: 8250/16550 driver, 32 ports, IRQ sharing enabled
[    0.377556] serial8250: ttyS0 at I/O 0x3f8 (irq = 4, base_baud = 115200) is a 16550A
[    0.398228] serial8250: ttyS1 at I/O 0x2f8 (irq = 3, base_baud = 115200) is a 16550A
[    0.399825] Linux agpgart interface v0.103
[    0.401587] loop: module loaded
[    0.401784] ACPI: bus type drm_connector registered
[    0.402444] tun: Universal TUN/TAP device driver, 1.6
[    0.402477] PPP generic driver version 2.4.2
[    0.402703] ehci-pci 0000:00:1a.0: EHCI Host Controller
[    0.402711] ehci-pci 0000:00:1a.0: new USB bus registered, assigned bus number 1
[    0.402723] ehci-pci 0000:00:1a.0: debug port 2
[    0.406660] ehci-pci 0000:00:1a.0: irq 18, io mem 0xfb417000
[    0.412302] ehci-pci 0000:00:1a.0: USB 2.0 started, EHCI 1.00
[    0.412370] usb usb1: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 6.14
[    0.412374] usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.412376] usb usb1: Product: EHCI Host Controller
[    0.412378] usb usb1: Manufacturer: Linux 6.14.0-37-generic ehci_hcd
[    0.412380] usb usb1: SerialNumber: 0000:00:1a.0
[    0.412514] hub 1-0:1.0: USB hub found
[    0.412529] hub 1-0:1.0: 2 ports detected
[    0.412746] xhci_hcd 0000:00:14.0: xHCI Host Controller
[    0.412752] xhci_hcd 0000:00:14.0: new USB bus registered, assigned bus number 2
[    0.413851] xhci_hcd 0000:00:14.0: hcc params 0x200077c1 hci version 0x100 quirks 0x0000000000009810
[    0.414140] xhci_hcd 0000:00:14.0: xHCI Host Controller
[    0.414145] xhci_hcd 0000:00:14.0: new USB bus registered, assigned bus number 3
[    0.414149] xhci_hcd 0000:00:14.0: Host supports USB 3.0 SuperSpeed
[    0.414185] ehci-pci 0000:00:1d.0: EHCI Host Controller
[    0.414217] usb usb2: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 6.14
[    0.414220] usb usb2: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.414222] usb usb2: Product: xHCI Host Controller
[    0.414224] usb usb2: Manufacturer: Linux 6.14.0-37-generic xhci-hcd
[    0.414226] usb usb2: SerialNumber: 0000:00:14.0
[    0.414387] hub 2-0:1.0: USB hub found
[    0.414408] hub 2-0:1.0: 15 ports detected
[    0.420878] ehci-pci 0000:00:1d.0: new USB bus registered, assigned bus number 4
[    0.420890] ehci-pci 0000:00:1d.0: debug port 2
[    0.424836] usb usb3: New USB device found, idVendor=1d6b, idProduct=0003, bcdDevice= 6.14
[    0.424839] usb usb3: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.424840] usb usb3: Product: xHCI Host Controller
[    0.424841] usb usb3: Manufacturer: Linux 6.14.0-37-generic xhci-hcd
[    0.424842] usb usb3: SerialNumber: 0000:00:14.0
[    0.424875] ehci-pci 0000:00:1d.0: irq 18, io mem 0xfb416000
[    0.424928] hub 3-0:1.0: USB hub found
[    0.424941] hub 3-0:1.0: 6 ports detected
[    0.430313] ehci-pci 0000:00:1d.0: USB 2.0 started, EHCI 1.00
[    0.430344] usb usb4: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 6.14
[    0.430346] usb usb4: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.430347] usb usb4: Product: EHCI Host Controller
[    0.430348] usb usb4: Manufacturer: Linux 6.14.0-37-generic ehci_hcd
[    0.430349] usb usb4: SerialNumber: 0000:00:1d.0
[    0.430430] hub 4-0:1.0: USB hub found
[    0.430435] hub 4-0:1.0: 2 ports detected
[    0.430561] xhci_hcd 0000:05:00.0: xHCI Host Controller
[    0.430565] xhci_hcd 0000:05:00.0: new USB bus registered, assigned bus number 5
[    0.430679] xhci_hcd 0000:05:00.0: hcc params 0x002841eb hci version 0x100 quirks 0x0000200000000890
[    0.430845] xhci_hcd 0000:05:00.0: xHCI Host Controller
[    0.430847] xhci_hcd 0000:05:00.0: new USB bus registered, assigned bus number 6
[    0.430849] xhci_hcd 0000:05:00.0: Host supports USB 3.0 SuperSpeed
[    0.430876] usb usb5: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 6.14
[    0.430878] usb usb5: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.430879] usb usb5: Product: xHCI Host Controller
[    0.430880] usb usb5: Manufacturer: Linux 6.14.0-37-generic xhci-hcd
[    0.430881] usb usb5: SerialNumber: 0000:05:00.0
[    0.430948] hub 5-0:1.0: USB hub found
[    0.430954] hub 5-0:1.0: 1 port detected
[    0.431018] usb usb6: New USB device found, idVendor=1d6b, idProduct=0003, bcdDevice= 6.14
[    0.431021] usb usb6: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.431022] usb usb6: Product: xHCI Host Controller
[    0.431023] usb usb6: Manufacturer: Linux 6.14.0-37-generic xhci-hcd
[    0.431024] usb usb6: SerialNumber: 0000:05:00.0
[    0.431088] hub 6-0:1.0: USB hub found
[    0.431096] hub 6-0:1.0: 4 ports detected
[    0.431238] xhci_hcd 0000:06:00.0: xHCI Host Controller
[    0.431243] xhci_hcd 0000:06:00.0: new USB bus registered, assigned bus number 7
[    0.450603] Freeing initrd memory: 80588K
[    0.490193] xhci_hcd 0000:06:00.0: hcc params 0x0200eec0 hci version 0x110 quirks 0x0000000000800010
[    0.490473] xhci_hcd 0000:06:00.0: xHCI Host Controller
[    0.490476] xhci_hcd 0000:06:00.0: new USB bus registered, assigned bus number 8
[    0.490479] xhci_hcd 0000:06:00.0: Host supports USB 3.1 Enhanced SuperSpeed
[    0.490520] usb usb7: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 6.14
[    0.490522] usb usb7: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.490523] usb usb7: Product: xHCI Host Controller
[    0.490524] usb usb7: Manufacturer: Linux 6.14.0-37-generic xhci-hcd
[    0.490526] usb usb7: SerialNumber: 0000:06:00.0
[    0.490614] hub 7-0:1.0: USB hub found
[    0.490622] hub 7-0:1.0: 2 ports detected
[    0.490695] usb usb8: We don't know the algorithms for LPM for this host, disabling LPM.
[    0.490718] usb usb8: New USB device found, idVendor=1d6b, idProduct=0003, bcdDevice= 6.14
[    0.490720] usb usb8: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.490721] usb usb8: Product: xHCI Host Controller
[    0.490722] usb usb8: Manufacturer: Linux 6.14.0-37-generic xhci-hcd
[    0.490723] usb usb8: SerialNumber: 0000:06:00.0
[    0.490784] hub 8-0:1.0: USB hub found
[    0.490791] hub 8-0:1.0: 2 ports detected
[    0.490903] i8042: PNP: No PS/2 controller found.
[    0.490949] mousedev: PS/2 mouse device common for all mice
[    0.491026] rtc_cmos 00:00: RTC can wake from S4
[    0.491225] rtc_cmos 00:00: registered as rtc0
[    0.491256] rtc_cmos 00:00: setting system clock to 2026-01-21T05:19:43 UTC (1768972783)
[    0.491280] rtc_cmos 00:00: alarms up to one month, y3k, 114 bytes nvram
[    0.491286] i2c_dev: i2c /dev entries driver
[    0.491453] device-mapper: core: CONFIG_IMA_DISABLE_HTABLE is disabled. Duplicate IMA measurements will not be recorded in the IMA log.
[    0.491471] device-mapper: uevent: version 1.0.3
[    0.491504] device-mapper: ioctl: 4.49.0-ioctl (2025-01-17) initialised: dm-devel@lists.linux.dev
[    0.491530] intel_pstate: Intel P-state driver initializing
[    0.492124] Relocating firmware framebuffer to offset 0x0000000001000000[d] within [mem 0xf0000000-0xf1ffffff flags 0x14220c]
[    0.492338] simple-framebuffer simple-framebuffer.0: [drm] Registered 1 planes with drm panic
[    0.492343] [drm] Initialized simpledrm 1.0.0 for simple-framebuffer.0 on minor 0
[    0.493780] fbcon: Deferring console take-over
[    0.493785] simple-framebuffer simple-framebuffer.0: [drm] fb0: simpledrmdrmfb frame buffer device
[    0.493936] drop_monitor: Initializing network drop monitor service
[    0.494049] NET: Registered PF_INET6 protocol family
[    0.501296] Segment Routing with IPv6
[    0.501306] In-situ OAM (IOAM) with IPv6
[    0.501324] NET: Registered PF_PACKET protocol family
[    0.501356] Key type dns_resolver registered
[    0.502305] microcode: Current revision: 0x0b000040
[    0.502306] microcode: Updated early from: 0x0b00002e
[    0.502527] resctrl: L3 allocation detected
[    0.502528] resctrl: L3 monitoring detected
[    0.502545] IPI shorthand broadcast: enabled
[    0.503826] sched_clock: Marking stable (502001385, 1290727)->(517713037, -14420925)
[    0.503966] registered taskstats version 1
[    0.504325] Loading compiled-in X.509 certificates
[    0.504774] Loaded X.509 cert 'Build time autogenerated kernel key: b878835a90265075bf75bb69cfcef4210fdf14ae'
[    0.505159] Loaded X.509 cert 'Canonical Ltd. Live Patch Signing 2025 Kmod: d541cef61dc7e793b7eb7e899970a2eef0b5dc8c'
[    0.505553] Loaded X.509 cert 'Canonical Ltd. Live Patch Signing: 14df34d1a87cf37625abec039ef2bf521249b969'
[    0.505939] Loaded X.509 cert 'Canonical Ltd. Kernel Module Signing: 88f752e560a1e0737e31163a466ad7b70a850c19'
[    0.505941] blacklist: Loading compiled-in revocation X.509 certificates
[    0.505956] Loaded X.509 cert 'Canonical Ltd. Secure Boot Signing: 61482aa2830d0ab2ad5af10b7250da9033ddcef0'
[    0.505967] Loaded X.509 cert 'Canonical Ltd. Secure Boot Signing (2017): 242ade75ac4a15e50d50c84b0d45ff3eae707a03'
[    0.505978] Loaded X.509 cert 'Canonical Ltd. Secure Boot Signing (ESM 2018): 365188c1d374d6b07c3c8f240f8ef722433d6a8b'
[    0.505988] Loaded X.509 cert 'Canonical Ltd. Secure Boot Signing (2019): c0746fd6c5da3ae827864651ad66ae47fe24b3e8'
[    0.505998] Loaded X.509 cert 'Canonical Ltd. Secure Boot Signing (2021 v1): a8d54bbb3825cfb94fa13c9f8a594a195c107b8d'
[    0.506008] Loaded X.509 cert 'Canonical Ltd. Secure Boot Signing (2021 v2): 4cf046892d6fd3c9a5b03f98d845f90851dc6a8c'
[    0.506018] Loaded X.509 cert 'Canonical Ltd. Secure Boot Signing (2021 v3): 100437bb6de6e469b581e61cd66bce3ef4ed53af'
[    0.506029] Loaded X.509 cert 'Canonical Ltd. Secure Boot Signing (Ubuntu Core 2019): c1d57b8f6b743f23ee41f4f7ee292f06eecadfb9'
[    0.508983] Demotion targets for Node 0: null
[    0.509060] Key type .fscrypt registered
[    0.509061] Key type fscrypt-provisioning registered
[    0.515246] cryptd: max_cpu_qlen set to 1000
[    0.517524] AES CTR mode by8 optimization enabled
[    0.532061] Key type encrypted registered
[    0.532064] AppArmor: AppArmor sha256 policy hashing enabled
[    0.532340] ima: No TPM chip found, activating TPM-bypass!
[    0.532343] Loading compiled-in module X.509 certificates
[    0.532738] Loaded X.509 cert 'Build time autogenerated kernel key: b878835a90265075bf75bb69cfcef4210fdf14ae'
[    0.532740] ima: Allocated hash algorithm: sha256
[    0.532747] ima: No architecture policies found
[    0.532758] evm: Initialising EVM extended attributes:
[    0.532759] evm: security.selinux
[    0.532760] evm: security.SMACK64
[    0.532761] evm: security.SMACK64EXEC
[    0.532762] evm: security.SMACK64TRANSMUTE
[    0.532762] evm: security.SMACK64MMAP
[    0.532763] evm: security.apparmor
[    0.532764] evm: security.ima
[    0.532764] evm: security.capability
[    0.532765] evm: HMAC attrs: 0x1
[    0.532999] PM:   Magic number: 10:346:315
[    0.533032] tty tty40: hash matches
[    0.533056] acpi device:200: hash matches
[    0.535305] RAS: Correctable Errors collector initialized.
[    0.542428] clk: Disabling unused clocks
[    0.542431] PM: genpd: Disabling unused power domains
[    0.543455] Freeing unused decrypted memory: 2028K
[    0.544192] Freeing unused kernel image (initmem) memory: 5140K
[    0.544261] Write protecting the kernel read-only data: 38912k
[    0.544660] Freeing unused kernel image (text/rodata gap) memory: 1052K
[    0.544959] Freeing unused kernel image (rodata/data gap) memory: 1312K
[    0.586537] x86/mm: Checked W+X mappings: passed, no W+X pages found.
[    0.586539] x86/mm: Checking user space page tables
[    0.624625] x86/mm: Checked W+X mappings: passed, no W+X pages found.
[    0.624629] Run /init as init process
[    0.624630]   with arguments:
[    0.624632]     /init
[    0.624633]     splash
[    0.624634]   with environment:
[    0.624634]     HOME=/
[    0.624635]     TERM=linux
[    0.624636]     BOOT_IMAGE=/casper/vmlinuz
[    0.624636]     boot=casper
[    0.624637]     uuid=6e72f523-dc09-4880-8910-93ffa64401c5
[    0.624638]     username=mint
[    0.624639]     iso-scan/filename=
[    0.648324] usb 1-1: new high-speed USB device number 2 using ehci-pci
[    0.655327] usb 2-1: new full-speed USB device number 2 using xhci_hcd
[    0.671312] usb 4-1: new high-speed USB device number 2 using ehci-pci
[    0.671326] usb 5-1: new high-speed USB device number 2 using xhci_hcd
[    0.773684] usb 1-1: New USB device found, idVendor=8087, idProduct=800a, bcdDevice= 0.05
[    0.773692] usb 1-1: New USB device strings: Mfr=0, Product=0, SerialNumber=0
[    0.774192] hub 1-1:1.0: USB hub found
[    0.774319] hub 1-1:1.0: 6 ports detected
[    0.778562] usb 2-1: not running at top speed; connect to a high speed hub
[    0.779298] usb 2-1: New USB device found, idVendor=046d, idProduct=c08b, bcdDevice=69.00
[    0.779303] usb 2-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[    0.779306] usb 2-1: Product: G502 HERO Gaming Mouse
[    0.779309] usb 2-1: Manufacturer: Logitech
[    0.779311] usb 2-1: SerialNumber: 2080397E5241
[    0.787492] hid: raw HID events driver (C) Jiri Kosina
[    0.790897] usbcore: registered new interface driver usbhid
[    0.790900] usbhid: USB HID core driver
[    0.792663] input: Logitech G502 HERO Gaming Mouse as /devices/pci0000:00/0000:00:14.0/usb2/2-1/2-1:1.0/0003:046D:C08B.0001/input/input2
[    0.792739] hid-generic 0003:046D:C08B.0001: input,hidraw0: USB HID v1.11 Mouse [Logitech G502 HERO Gaming Mouse] on usb-0000:00:14.0-1/input0
[    0.792958] input: Logitech G502 HERO Gaming Mouse Keyboard as /devices/pci0000:00/0000:00:14.0/usb2/2-1/2-1:1.1/0003:046D:C08B.0002/input/input3
[    0.796681] usb 4-1: New USB device found, idVendor=8087, idProduct=8002, bcdDevice= 0.05
[    0.796688] usb 4-1: New USB device strings: Mfr=0, Product=0, SerialNumber=0
[    0.797054] hub 4-1:1.0: USB hub found
[    0.797194] hub 4-1:1.0: 8 ports detected
[    0.798813] usb 5-1: New USB device found, idVendor=2109, idProduct=3431, bcdDevice= 4.20
[    0.798817] usb 5-1: New USB device strings: Mfr=0, Product=1, SerialNumber=0
[    0.798818] usb 5-1: Product: USB2.0 Hub
[    0.799606] hub 5-1:1.0: USB hub found
[    0.799758] hub 5-1:1.0: 4 ports detected
[    0.844473] hid-generic 0003:046D:C08B.0002: input,hiddev0,hidraw1: USB HID v1.11 Keyboard [Logitech G502 HERO Gaming Mouse] on usb-0000:00:14.0-1/input1
[    0.846729] alx 0000:04:00.0 eth0: Qualcomm Atheros AR816x/AR817x Ethernet [d8:cb:8a:cd:4e:7e]
[    0.846736] ahci 0000:00:11.4: version 3.0
[    0.846947] ahci 0000:00:11.4: AHCI vers 0001.0300, 32 command slots, 6 Gbps, SATA mode
[    0.846952] ahci 0000:00:11.4: 1/4 ports implemented (port mask 0x2)
[    0.846954] ahci 0000:00:11.4: flags: 64bit ncq led clo pio ems apst 
[    0.847388] scsi host0: ahci
[    0.847585] scsi host1: ahci
[    0.847742] scsi host2: ahci
[    0.847878] scsi host3: ahci
[    0.847930] ata1: DUMMY
[    0.847933] ata2: SATA max UDMA/133 abar m2048@0xfb41b000 port 0xfb41b180 irq 54 lpm-pol 0
[    0.847935] ata3: DUMMY
[    0.847936] ata4: DUMMY
[    0.849981] alx 0000:04:00.0 enp4s0: renamed from eth0
[    0.892336] usb 2-2: new full-speed USB device number 3 using xhci_hcd
[    1.016459] usb 2-2: New USB device found, idVendor=1b1c, idProduct=1ba4, bcdDevice= 1.03
[    1.016466] usb 2-2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[    1.016469] usb 2-2: Product: CORSAIR K55 RGB PRO Gaming Keyboard
[    1.016472] usb 2-2: Manufacturer: Corsair
[    1.016475] usb 2-2: SerialNumber: F5001BC06724BB02AE062C810100B026
[    1.019545] input: Corsair CORSAIR K55 RGB PRO Gaming Keyboard as /devices/pci0000:00/0000:00:14.0/usb2/2-2/2-2:1.0/0003:1B1C:1BA4.0003/input/input6
[    1.070491] hid-generic 0003:1B1C:1BA4.0003: input,hidraw2: USB HID v1.00 Keyboard [Corsair CORSAIR K55 RGB PRO Gaming Keyboard] on usb-0000:00:14.0-2/input0
[    1.071942] hid-generic 0003:1B1C:1BA4.0004: hiddev1,hidraw3: USB HID v1.00 Device [Corsair CORSAIR K55 RGB PRO Gaming Keyboard] on usb-0000:00:14.0-2/input1
[    1.073320] hid-generic 0003:1B1C:1BA4.0005: hiddev2,hidraw4: USB HID v1.00 Device [Corsair CORSAIR K55 RGB PRO Gaming Keyboard] on usb-0000:00:14.0-2/input2
[    1.156805] ata2: SATA link up 6.0 Gbps (SStatus 133 SControl 300)
[    1.157139] ata2.00: Model 'Crucial_CT1050MX300SSD1', rev ' M0CR040', applying quirks: zeroaftertrim
[    1.157145] ata2.00: supports DRM functions and may not be fully accessible
[    1.157147] ata2.00: ATA-10: Crucial_CT1050MX300SSD1,  M0CR040, max UDMA/133
[    1.159281] ata2.00: 2051200368 sectors, multi 16: LBA48 NCQ (depth 32), AA
[    1.162037] ata2.00: Features: Trust Dev-Sleep NCQ-sndrcv NCQ-prio
[    1.162274] ata2.00: supports DRM functions and may not be fully accessible
[    1.167160] ata2.00: configured for UDMA/133
[    1.167369] scsi 1:0:0:0: Direct-Access     ATA      Crucial_CT1050MX R040 PQ: 0 ANSI: 5
[    1.167754] sd 1:0:0:0: Attached scsi generic sg0 type 0
[    1.167768] ata2.00: Enabling discard_zeroes_data
[    1.167785] sd 1:0:0:0: [sda] 2051200368 512-byte logical blocks: (1.05 TB/978 GiB)
[    1.167797] sd 1:0:0:0: [sda] Write Protect is off
[    1.167801] sd 1:0:0:0: [sda] Mode Sense: 00 3a 00 00
[    1.167815] sd 1:0:0:0: [sda] Write cache: enabled, read cache: enabled, doesn't support DPO or FUA
[    1.167854] sd 1:0:0:0: [sda] Preferred minimum I/O size 512 bytes
[    1.168243] ata2.00: Enabling discard_zeroes_data
[    1.186332] usb 2-4: new high-speed USB device number 4 using xhci_hcd
[    1.188479]  sda: sda1 sda2 sda3
[    1.188753] sd 1:0:0:0: [sda] supports TCG Opal
[    1.188756] sd 1:0:0:0: [sda] Attached SCSI disk
[    1.313286] usb 2-4: New USB device found, idVendor=0930, idProduct=6545, bcdDevice= 1.00
[    1.313300] usb 2-4: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[    1.313304] usb 2-4: Product: TransMemory
[    1.313307] usb 2-4: Manufacturer: TOSHIBA
[    1.313309] usb 2-4: SerialNumber: 0391E57111D3A93F
[    1.323395] usb-storage 2-4:1.0: USB Mass Storage device detected
[    1.323618] scsi host4: usb-storage 2-4:1.0
[    1.323764] usbcore: registered new interface driver usb-storage
[    1.326223] usbcore: registered new interface driver uas
[    1.360298] tsc: Refined TSC clocksource calibration: 3874.996 MHz
[    1.360307] clocksource: tsc: mask: 0xffffffffffffffff max_cycles: 0x6fb62d88a0f, max_idle_ns: 881590767011 ns
[    1.360330] clocksource: Switched to clocksource tsc
[    1.418305] raid6: avx2x4   gen() 31608 MB/s
[    1.435306] raid6: avx2x2   gen() 37876 MB/s
[    1.452308] raid6: avx2x1   gen() 34312 MB/s
[    1.452309] raid6: using algorithm avx2x2 gen() 37876 MB/s
[    1.469306] raid6: .... xor() 22223 MB/s, rmw enabled
[    1.469307] raid6: using avx2x2 recovery algorithm
[    1.470202] xor: automatically using best checksumming function   avx       
[    1.471005] async_tx: api initialized (async)
[    1.633177] EXT4-fs (sda2): INFO: recovery required on readonly filesystem
[    1.633185] EXT4-fs (sda2): write access will be enabled during recovery
[    1.638384] EXT4-fs (sda2): recovery complete
[    1.639874] EXT4-fs (sda2): mounted filesystem 4588079c-fc78-42a7-bf9a-86c700b12ca5 ro with ordered data mode. Quota mode: none.
[    1.640439] EXT4-fs (sda2): unmounting filesystem 4588079c-fc78-42a7-bf9a-86c700b12ca5.
[    2.383692] scsi 4:0:0:0: Direct-Access     TOSHIBA  TransMemory      5.00 PQ: 0 ANSI: 0 CCS
[    2.383987] sd 4:0:0:0: Attached scsi generic sg1 type 0
[    2.387725] sd 4:0:0:0: [sdb] 8058880 512-byte logical blocks: (4.13 GB/3.84 GiB)
[    2.387872] sd 4:0:0:0: [sdb] Write Protect is off
[    2.387876] sd 4:0:0:0: [sdb] Mode Sense: 23 00 00 00
[    2.388010] sd 4:0:0:0: [sdb] No Caching mode page found
[    2.388013] sd 4:0:0:0: [sdb] Assuming drive cache: write through
[    2.404018]  sdb: sdb1
[    2.404071] sd 4:0:0:0: [sdb] Attached SCSI removable disk
[    3.281558] loop0: detected capacity change from 0 to 5142688
[    3.382468] overlayfs: null uuid detected in lower fs '/', falling back to xino=off,index=off,nfs_export=off.
[    4.226871] evm: overlay not supported
[   13.451366] systemd[1]: Inserted module 'autofs4'
[   13.601619] systemd[1]: systemd 255.4-1ubuntu8.12 running in system mode (+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified)
[   13.601631] systemd[1]: Detected architecture x86-64.
[   13.627422] systemd[1]: Initializing machine ID from random generator.
[   13.919970] systemd[1]: Queued start job for default target graphical.target.
[   13.954245] systemd[1]: Created slice system-modprobe.slice - Slice /system/modprobe.
[   13.954856] systemd[1]: Created slice user.slice - User and Session Slice.
[   13.955007] systemd[1]: Started systemd-ask-password-wall.path - Forward Password Requests to Wall Directory Watch.
[   13.955360] systemd[1]: Set up automount proc-sys-fs-binfmt_misc.automount - Arbitrary Executable File Formats File System Automount Point.
[   13.955389] systemd[1]: Reached target integritysetup.target - Local Integrity Protected Volumes.
[   13.955419] systemd[1]: Reached target nss-user-lookup.target - User and Group Name Lookups.
[   13.955428] systemd[1]: Reached target remote-fs.target - Remote File Systems.
[   13.955439] systemd[1]: Reached target slices.target - Slice Units.
[   13.955456] systemd[1]: Reached target swap.target - Swaps.
[   13.955476] systemd[1]: Reached target veritysetup.target - Local Verity Protected Volumes.
[   13.955566] systemd[1]: Listening on dm-event.socket - Device-mapper event daemon FIFOs.
[   13.956974] systemd[1]: Listening on lvm2-lvmpolld.socket - LVM2 poll daemon socket.
[   13.957115] systemd[1]: Listening on syslog.socket - Syslog Socket.
[   13.958742] systemd[1]: Listening on systemd-coredump.socket - Process Core Dump Socket.
[   13.958808] systemd[1]: Listening on systemd-initctl.socket - initctl Compatibility Named Pipe.
[   13.958915] systemd[1]: Listening on systemd-journald-dev-log.socket - Journal Socket (/dev/log).
[   13.959025] systemd[1]: Listening on systemd-journald.socket - Journal Socket.
[   13.959061] systemd[1]: systemd-pcrextend.socket - TPM2 PCR Extension (Varlink) was skipped because of an unmet condition check (ConditionSecurity=measured-uki).
[   13.960474] systemd[1]: Listening on systemd-udevd-control.socket - udev Control Socket.
[   13.960565] systemd[1]: Listening on systemd-udevd-kernel.socket - udev Kernel Socket.
[   13.981422] systemd[1]: Mounting dev-hugepages.mount - Huge Pages File System...
[   13.982299] systemd[1]: Mounting dev-mqueue.mount - POSIX Message Queue File System...
[   13.983098] systemd[1]: Mounting sys-kernel-debug.mount - Kernel Debug File System...
[   13.983712] systemd[1]: Mounting sys-kernel-tracing.mount - Kernel Trace File System...
[   13.984936] systemd[1]: Starting systemd-journald.service - Journal Service...
[   13.985013] systemd[1]: Finished blk-availability.service - Availability of block devices.
[   13.985744] systemd[1]: Starting keyboard-setup.service - Set the console keyboard layout...
[   13.994811] systemd[1]: Starting kmod-static-nodes.service - Create List of Static Device Nodes...
[   13.995479] systemd[1]: Starting lvm2-monitor.service - Monitoring of LVM2 mirrors, snapshots etc. using dmeventd or progress polling...
[   13.996289] systemd[1]: Starting modprobe@configfs.service - Load Kernel Module configfs...
[   13.996925] systemd[1]: Starting modprobe@dm_mod.service - Load Kernel Module dm_mod...
[   13.997568] systemd[1]: Starting modprobe@drm.service - Load Kernel Module drm...
[   13.998289] systemd[1]: Starting modprobe@efi_pstore.service - Load Kernel Module efi_pstore...
[   13.999130] systemd[1]: Starting modprobe@fuse.service - Load Kernel Module fuse...
[   13.999996] systemd[1]: Starting modprobe@loop.service - Load Kernel Module loop...
[   14.046369] pstore: Using crash dump compression: deflate
[   14.051389] systemd[1]: Starting systemd-modules-load.service - Load Kernel Modules...
[   14.051406] systemd[1]: systemd-pcrmachine.service - TPM2 PCR Machine ID Measurement was skipped because of an unmet condition check (ConditionSecurity=measured-uki).
[   14.051672] pstore: Registered efi_pstore as persistent store backend
[   14.052118] systemd[1]: Starting systemd-remount-fs.service - Remount Root and Kernel File Systems...
[   14.052162] systemd[1]: systemd-tpm2-setup-early.service - TPM2 SRK Setup (Early) was skipped because of an unmet condition check (ConditionSecurity=measured-uki).
[   14.052801] systemd[1]: Starting systemd-udev-trigger.service - Coldplug All udev Devices...
[   14.054108] systemd[1]: Mounted dev-hugepages.mount - Huge Pages File System.
[   14.054198] systemd[1]: Mounted dev-mqueue.mount - POSIX Message Queue File System.
[   14.054279] systemd[1]: Mounted sys-kernel-debug.mount - Kernel Debug File System.
[   14.054373] systemd[1]: Mounted sys-kernel-tracing.mount - Kernel Trace File System.
[   14.054531] systemd[1]: Finished kmod-static-nodes.service - Create List of Static Device Nodes.
[   14.054729] systemd[1]: modprobe@configfs.service: Deactivated successfully.
[   14.054831] systemd[1]: Finished modprobe@configfs.service - Load Kernel Module configfs.
[   14.055022] systemd[1]: modprobe@dm_mod.service: Deactivated successfully.
[   14.055125] systemd[1]: Finished modprobe@dm_mod.service - Load Kernel Module dm_mod.
[   14.055373] systemd[1]: modprobe@drm.service: Deactivated successfully.
[   14.055484] systemd[1]: Finished modprobe@drm.service - Load Kernel Module drm.
[   14.055679] systemd[1]: modprobe@efi_pstore.service: Deactivated successfully.
[   14.055783] systemd[1]: Finished modprobe@efi_pstore.service - Load Kernel Module efi_pstore.
[   14.055973] systemd[1]: modprobe@fuse.service: Deactivated successfully.
[   14.056077] systemd[1]: Finished modprobe@fuse.service - Load Kernel Module fuse.
[   14.056269] systemd[1]: modprobe@loop.service: Deactivated successfully.
[   14.056396] systemd[1]: Finished modprobe@loop.service - Load Kernel Module loop.
[   14.057164] systemd[1]: Mounting sys-fs-fuse-connections.mount - FUSE Control File System...
[   14.057718] systemd[1]: Mounting sys-kernel-config.mount - Kernel Configuration File System...
[   14.059507] systemd-journald[900]: Collecting audit messages is disabled.
[   14.068518] systemd[1]: systemd-repart.service - Repartition Root Disk was skipped because no trigger condition checks were met.
[   14.069426] systemd[1]: Starting systemd-tmpfiles-setup-dev-early.service - Create Static Device Nodes in /dev gracefully...
[   14.070321] systemd[1]: Mounted sys-fs-fuse-connections.mount - FUSE Control File System.
[   14.070444] systemd[1]: Mounted sys-kernel-config.mount - Kernel Configuration File System.
[   14.090484] systemd[1]: Finished systemd-remount-fs.service - Remount Root and Kernel File Systems.
[   14.140343] systemd[1]: systemd-hwdb-update.service - Rebuild Hardware Database was skipped because no trigger condition checks were met.
[   14.155420] systemd[1]: Starting systemd-pstore.service - Platform Persistent Storage Archival...
[   14.156116] systemd[1]: Starting systemd-random-seed.service - Load/Save OS Random Seed...
[   14.156134] systemd[1]: systemd-tpm2-setup.service - TPM2 SRK Setup was skipped because of an unmet condition check (ConditionSecurity=measured-uki).
[   14.156205] systemd[1]: Started systemd-journald.service - Journal Service.
[   14.250977] systemd-journald[900]: Received client request to flush runtime journal.
[   14.362159] lp: driver loaded but no devices found
[   14.425331] ppdev: user-space parallel port driver
[   14.449261] parport0: PC-style at 0x378 (0x778) [PCSPP,TRISTATE,EPP]
[   14.670519] lp0: using parport0 (polling).
[   15.944350] RAPL PMU: API unit is 2^-32 Joules, 1 fixed counters, 655360 ms ovfl timer
[   15.944359] RAPL PMU: hw unit of domain package 2^-14 Joules
[   15.967090] i801_smbus 0000:00:1f.3: enabling device (0001 -> 0003)
[   15.967268] i801_smbus 0000:00:1f.3: SMBus using PCI interrupt
[   16.521000] EDAC sbridge: Seeking for: PCI ID 8086:6fa0
[   16.521011] EDAC sbridge: Seeking for: PCI ID 8086:6fa0
[   16.521017] EDAC sbridge: Seeking for: PCI ID 8086:6f60
[   16.521021] EDAC sbridge: Seeking for: PCI ID 8086:6fa8
[   16.521023] EDAC sbridge: Seeking for: PCI ID 8086:6fa8
[   16.521026] EDAC sbridge: Seeking for: PCI ID 8086:6f71
[   16.521028] EDAC sbridge: Seeking for: PCI ID 8086:6f71
[   16.521031] EDAC sbridge: Seeking for: PCI ID 8086:6faa
[   16.521034] EDAC sbridge: Seeking for: PCI ID 8086:6faa
[   16.521036] EDAC sbridge: Seeking for: PCI ID 8086:6fab
[   16.521039] EDAC sbridge: Seeking for: PCI ID 8086:6fab
[   16.521042] EDAC sbridge: Seeking for: PCI ID 8086:6fac
[   16.521044] EDAC sbridge: Seeking for: PCI ID 8086:6fac
[   16.521047] EDAC sbridge: Seeking for: PCI ID 8086:6fad
[   16.521049] EDAC sbridge: Seeking for: PCI ID 8086:6fad
[   16.521052] EDAC sbridge: Seeking for: PCI ID 8086:6f68
[   16.521054] EDAC sbridge: Seeking for: PCI ID 8086:6f79
[   16.521058] EDAC sbridge: Seeking for: PCI ID 8086:6f6a
[   16.521061] EDAC sbridge: Seeking for: PCI ID 8086:6f6b
[   16.521065] EDAC sbridge: Seeking for: PCI ID 8086:6f6c
[   16.521069] EDAC sbridge: Seeking for: PCI ID 8086:6f6d
[   16.521072] EDAC sbridge: Seeking for: PCI ID 8086:6ffc
[   16.521074] EDAC sbridge: Seeking for: PCI ID 8086:6ffc
[   16.521077] EDAC sbridge: Seeking for: PCI ID 8086:6ffd
[   16.521079] EDAC sbridge: Seeking for: PCI ID 8086:6ffd
[   16.521083] EDAC sbridge: Seeking for: PCI ID 8086:6faf
[   16.521085] EDAC sbridge: Seeking for: PCI ID 8086:6faf
[   16.521105] EDAC sbridge: CPU SrcID #0, Ha #0, Channel #1 has DIMMs, but ECC is disabled
[   16.521109] EDAC sbridge: Couldn't find mci handler
[   16.521110] EDAC sbridge: Failed to register device with error -19.
[   16.976148] MXM: GUID detected in BIOS
[   16.976278] nouveau 0000:02:00.0: NVIDIA GP104 (134000a1)
[   17.005447] intel_rapl_common: Found RAPL domain package
[   17.084749] nouveau 0000:02:00.0: bios: version 86.04.60.00.60
[   17.094229] snd_hda_intel 0000:00:1b.0: enabling device (0000 -> 0002)
[   17.094461] snd_hda_intel 0000:02:00.1: Disabling MSI
[   17.094479] snd_hda_intel 0000:02:00.1: Handle vga_switcheroo audio client
[   17.134915] nouveau 0000:02:00.0: pmu: firmware unavailable
[   17.157208] input: HDA NVidia HDMI/DP,pcm=3 as /devices/pci0000:00/0000:00:03.0/0000:02:00.1/sound/card1/input7
[   17.157269] input: HDA NVidia HDMI/DP,pcm=7 as /devices/pci0000:00/0000:00:03.0/0000:02:00.1/sound/card1/input8
[   17.157332] input: HDA NVidia HDMI/DP,pcm=8 as /devices/pci0000:00/0000:00:03.0/0000:02:00.1/sound/card1/input9
[   17.157419] input: HDA NVidia HDMI/DP,pcm=9 as /devices/pci0000:00/0000:00:03.0/0000:02:00.1/sound/card1/input10
[   17.191624] snd_hda_codec_realtek hdaudioC0D0: ALC1150: picked fixup  for PCI SSID 1462:0000
[   17.191635] snd_hda_codec_realtek hdaudioC0D0: ALC1150: SKU not ready 0x00000000
[   17.192107] snd_hda_codec_realtek hdaudioC0D0: autoconfig for ALC1150: line_outs=3 (0x14/0x15/0x16/0x0/0x0) type:line
[   17.192112] snd_hda_codec_realtek hdaudioC0D0:    speaker_outs=0 (0x0/0x0/0x0/0x0/0x0)
[   17.192115] snd_hda_codec_realtek hdaudioC0D0:    hp_outs=1 (0x1b/0x0/0x0/0x0/0x0)
[   17.192117] snd_hda_codec_realtek hdaudioC0D0:    mono: mono_out=0x0
[   17.192119] snd_hda_codec_realtek hdaudioC0D0:    dig-out=0x1e/0x0
[   17.192121] snd_hda_codec_realtek hdaudioC0D0:    inputs:
[   17.192124] snd_hda_codec_realtek hdaudioC0D0:      Rear Mic=0x18
[   17.192127] snd_hda_codec_realtek hdaudioC0D0:      Front Mic=0x19
[   17.192129] snd_hda_codec_realtek hdaudioC0D0:      Line=0x1a
[   17.210395] input: HDA Intel PCH Rear Mic as /devices/pci0000:00/0000:00:1b.0/sound/card0/input11
[   17.210543] input: HDA Intel PCH Front Mic as /devices/pci0000:00/0000:00:1b.0/sound/card0/input12
[   17.210669] input: HDA Intel PCH Line as /devices/pci0000:00/0000:00:1b.0/sound/card0/input13
[   17.211146] input: HDA Intel PCH Line Out Front as /devices/pci0000:00/0000:00:1b.0/sound/card0/input14
[   17.211768] input: HDA Intel PCH Line Out Surround as /devices/pci0000:00/0000:00:1b.0/sound/card0/input15
[   17.212213] input: HDA Intel PCH Line Out CLFE as /devices/pci0000:00/0000:00:1b.0/sound/card0/input16
[   17.212998] input: HDA Intel PCH Front Headphone as /devices/pci0000:00/0000:00:1b.0/sound/card0/input17
[   17.294061] nouveau 0000:02:00.0: vgaarb: deactivate vga console
[   17.294170] nouveau 0000:02:00.0: fb: 8192 MiB GDDR5X
[   17.315074] nouveau 0000:02:00.0: drm: VRAM: 8192 MiB
[   17.315077] nouveau 0000:02:00.0: drm: GART: 536870912 MiB
[   17.315078] nouveau 0000:02:00.0: drm: BIT table 'A' not found
[   17.315080] nouveau 0000:02:00.0: drm: BIT table 'L' not found
[   17.315081] nouveau 0000:02:00.0: drm: TMDS table version 2.0
[   17.316356] nouveau 0000:02:00.0: drm: MM: using COPY for buffer copies
[   17.317392] snd_hda_intel 0000:02:00.1: bound 0000:02:00.0 (ops nv50_audio_component_bind_ops [nouveau])
[   17.570081] nouveau 0000:02:00.0: [drm] Registered 4 planes with drm panic
[   17.570088] [drm] Initialized nouveau 1.4.0 for 0000:02:00.0 on minor 1
[   17.618311] nouveau 0000:02:00.0: drm: DDC responded, but no EDID for DP-1
[   17.686194] fbcon: nouveaudrmfb (fb0) is primary device
[   17.686197] fbcon: Deferring console take-over
[   17.686199] nouveau 0000:02:00.0: [drm] fb0: nouveaudrmfb frame buffer device
[   17.750313] nouveau 0000:02:00.0: drm: DDC responded, but no EDID for DP-1
[   17.911313] nouveau 0000:02:00.0: drm: DDC responded, but no EDID for DP-1
[   28.104994] audit: type=1400 audit(1768972811.112:2): apparmor="STATUS" operation="profile_load" profile="unconfined" name="rsyslogd" pid=1509 comm="apparmor_parser"
[   29.221846] NET: Registered PF_QIPCRTR protocol family
[   31.055774] alx 0000:04:00.0 enp4s0: NIC Up: 1 Gbps Full
[   47.089318] nouveau 0000:02:00.0: drm: DDC responded, but no EDID for DP-1
[   47.204315] nouveau 0000:02:00.0: drm: DDC responded, but no EDID for DP-1
[   77.980337] nouveau 0000:02:00.0: drm: DDC responded, but no EDID for DP-1
[   81.997426] nouveau 0000:02:00.0: drm: DDC responded, but no EDID for DP-1
[   93.071583] nouveau 0000:02:00.0: drm: DDC responded, but no EDID for DP-1
[  286.328839] usb 3-5: new SuperSpeed USB device number 2 using xhci_hcd
[  286.349257] usb 3-5: New USB device found, idVendor=04e8, idProduct=61f5, bcdDevice= 1.00
[  286.349264] usb 3-5: New USB device strings: Mfr=2, Product=3, SerialNumber=1
[  286.349268] usb 3-5: Product: Portable SSD T5
[  286.349271] usb 3-5: Manufacturer: Samsung
[  286.349274] usb 3-5: SerialNumber: 123456824EB0
[  286.352787] scsi host5: uas
[  286.353283] scsi 5:0:0:0: Direct-Access     Samsung  Portable SSD T5  0    PQ: 0 ANSI: 6
[  286.354986] sd 5:0:0:0: Attached scsi generic sg2 type 0
[  286.357044] sd 5:0:0:0: [sdc] 1953525168 512-byte logical blocks: (1.00 TB/932 GiB)
[  286.357165] sd 5:0:0:0: [sdc] Write Protect is off
[  286.357171] sd 5:0:0:0: [sdc] Mode Sense: 43 00 00 00
[  286.357327] sd 5:0:0:0: [sdc] Write cache: enabled, read cache: enabled, doesn't support DPO or FUA
[  286.380959] sd 5:0:0:0: [sdc] Preferred minimum I/O size 512 bytes
[  286.380966] sd 5:0:0:0: [sdc] Optimal transfer size 33553920 bytes
[  286.400188]  sdc: sdc1
[  286.400281] sd 5:0:0:0: [sdc] Attached SCSI disk
[  286.577762] exFAT-fs (sdc1): Volume was not properly unmounted. Some data may be corrupt. Please run fsck.
root@mint:~# 

```

