<div id="toc" align="center" style="margin-bottom: 0; padding-bottom: 0;">
  <ul style="list-style: none; margin: 0; padding: 0;">
    <summary>
      <h1 align="center" style="margin: 0; padding: 0;">⋆ palaziks OnePlus Kernel ⋆</h1>
      <p align="center" style="font-size:12px; margin-top: 5px; margin-bottom: 20px;">
        <i>Stability-focused GKI 6.6 kernel for OnePlus 13 (SM8750) with ReSukiSU</i>
      </p>
    </summary>
  </ul>
</div>

<p align="center">
  <a href="#-features"><img src="https://img.shields.io/badge/Features-20+-brightgreen?style=flat-square" /></a>
  <a href="#-build-workflow"><img src="https://img.shields.io/badge/Build-GitHub_Actions-blue?style=flat-square" /></a>
  <a href="#-memory--scheduler-optimizations"><img src="https://img.shields.io/badge/Optimizations-25+_patches-purple?style=flat-square" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/palazik/actions_oplus_sm8750?style=flat-square" /></a>
</p>

---

## ⚙️ Kernel Information

| Property | Value |
|----------|-------|
| **Version** | `6.6.138` (upstreamed from 6.6.89) |
| **Chipset** | `SM8750` \| Snapdragon 8 Elite \| sun |
| **Kernel Version** | `Linux 6.6` (GKI Android 15) |
| **Android Version** | `15 VanillaIceCream` (compatible with later versions) |
| **ROM Compatibility** | OxygenOS / ColorOS (CN & Global) |
| **Root Solution** | SukiSU Ultra / KSU Next (Multi-Manager) |
| **Build System** | GitHub Actions CI/CD (optimized for ~5-6min builds) |

---

## 📝 Features

### 🔁 Kernel Version
- ✅ **Upstream** – Upstreaming the OnePlus's official kernel to the Google's newest A15 6.6 kernel

### 🔐 Security & Hide
- ✅ **SuSFS** – Enhanced environment hiding (path/mount/kstat spoofing)
- ✅ **Baseband Guard** – Anti-brick modem protection
- ✅ **Unicode Bypass Fix** – Path traversal protection

### 🚀 Performance & Scheduler
- ✅ **Fengchi / HMBIRD** – Advanced CPU scheduler optimizations for SM8750
- ✅ **ADIOS IO Scheduler** – Improved read/write performance
- ✅ **SchedUtil Optimizations** – Better CPU governor responsiveness *(optional)*
- ✅ **Oryon CPU Tuning** – `-mcpu=oryon-1` flags for SM8750

### 🌐 Networking
- ✅ **TCP BBR + Brutal** – Modern congestion control algorithms
- ✅ **WireGuard** – Kernel-level VPN support
- ✅ **Full Netfilter** – Conntrack, NAT, hashlimit *(optional)*
- ✅ **IP_SET + IPv6 NAT** – Advanced firewall + IPv6 masquerade *(optional)*
- ✅ **TTL/HL Target** – Hide tethering from carrier detection *(optional)*

### 💾 Storage & Memory
- ✅ **LZ4 1.10.0 + ZSTD 1.5.7** – Faster compression for ZRAM
- ✅ **LZ4KD** – Kernel-level ZRAM optimization *(optional)*
- ✅ **ZRAM Writeback** – Better memory management *(optional)*
- ✅ **F2FS Optimizations** – Enhanced flash storage performance *(optional)*

### 🎮 Gaming & Compatibility
- ✅ **NTSync** – Low-latency NT sync primitives (Wine/Proton gaming) *(optional)*
- ✅ **Droidspaces** – SYSVIPC + PID_NS + POSIX_MQUEUE for proot-distro
- ✅ **LRNG v59** – Better entropy for crypto/gaming *(optional)*

### 🔋 Battery & Power
- ✅ **Wakelock Blocker** – Reduce idle battery drain
- ✅ **Re-Kernel Support** – Enhanced app freezing via NoActive/Freezer *(optional)*

### 🧩 KernelSU Enhancements
- ✅ **KPM Support** – Kernel Patch Module for SukiSU Ultra / ReSukiSU *(optional)*
- ✅ **Multi-Manager** – Compatible with multiple KSU variants

---

## 🧠 Memory & Scheduler Optimizations (WildKernels)

> 25 low-level patches for reduced latency, better cache usage, and improved responsiveness.

| Patch | Purpose |
|-------|---------|
| `optimized_mem_operations.patch` | Optimized memcpy/memset for ARM64 |
| `file_struct_8bytes_align.patch` | Align file structures for better cache locality |
| `reduce_cache_pressure.patch` | Lower memory pressure during heavy workloads |
| `mem_opt_prefetch.patch` | Smart prefetching for sequential access patterns |
| `optimise_memcmp.patch` | Faster memory comparison routines |
| `minimise_wakeup_time.patch` | Reduce CPU wake latency for interactive tasks |
| `int_sqrt.patch` | Optimized integer square root for scheduler math |
| `force_tcp_nodelay.patch` | Reduce TCP latency for gaming/streaming |
| `reduce_gc_thread_sleep_time.patch` | Shorter GC thread sleeps for smoother UI |
| `add_timeout_wakelocks_globally.patch` | Prevent aggressive wakelock timeouts |
| `f2fs_reduce_congestion.patch` | Lower F2FS write contention |
| `reduce_freeze_timeout.patch` | Faster app freeze/unfreeze transitions |
| `clear_page_16bytes_align.patch` | 16-byte aligned page clearing for NEON efficiency |
| `add_limitation_scaling_min_freq.patch` | Smarter min-frequency scaling limits |
| `re_write_limitation_scaling_min_freq.patch` | Refined frequency scaling behavior |
| `adjust_cpu_scan_order.patch` | Optimized CPU selection order for task placement |
| `avoid_extra_s2idle_wake_attempts.patch` | Reduce unnecessary suspend-to-idle wakes |
| `disable_cache_hot_buddy.patch` | Prevent cache thrashing in buddy allocator |
| `f2fs_enlarge_min_fsync_blocks.patch` | Larger fsync batches for F2FS efficiency |
| `increase_ext4_default_commit_age.patch` | Less frequent EXT4 journal commits |
| `increase_sk_mem_packets.patch` | Larger socket buffer for high-throughput networking |
| `reduce_pci_pme_wakeups.patch` | Fewer PCIe power management wakeups |
| `silence_irq_cpu_logspam.patch` | Reduce IRQ-related kernel log noise |
| `silence_system_logspam.patch` | Cleaner dmesg output |
| `use_unlikely_wrap_cpufreq.patch` | Branch prediction hints for cpufreq paths |

---

## 🤖 Compiler & Build Configuration

### Toolchain
- **Clang**: ZyCromerZ Clang 19.0.0git (Oryon-optimized)
- **Linker**: LLD 19 with ThinLTO cache in RAM (`/dev/shm`)
- **CCache**: ECS-enhanced ccache with 10GB cache + aggressive sloppiness

### Compiler Flags
```bash
-O2                          # Balanced optimization level
-mcpu=oryon-1               # Target Snapdragon 8 Elite cores
-fno-strict-aliasing        # Safer pointer aliasing
-fno-delete-null-pointer-checks  # Extra null safety
-flto=thin                  # ThinLTO for link-time optimization (optional)
-ffile-prefix-map=...       # Reproducible builds
```

---

## 🛠️ Build Workflow (GitHub Actions)

### Quick Start
1. **Fork** this repository (ensure all branches are copied)
2. Go to **Actions** → Enable workflows
3. Click **"SukiSU Ultra OP13 Build"** → **"Run workflow"**
4. Configure options:
   - ✅ SuSFS (recommended for hiding)
   - ✅ Fengchi (performance scheduler)
   - ✅ Memory Opt Patches (25 optimizations)
   - 🔘 LTO Type: `thin` (balanced) / `none` (fastest compile) / `full` (max optimization)
   - 🔘 Optional features: KPM, LZ4KD, NTSync, IPv6 NAT, etc.
5. Click **"Run workflow"** → Wait ~4-5 minutes
6. Download `AnyKernel3_*.zip` from artifacts or Telegram

### Workflow Optimizations
This CI pipeline includes:
- 🚀 **Parallel patch application** for 20+ WildKernels patches
- 💾 **RAM-based LTO cache** (`/dev/shm`) to avoid disk I/O bottlenecks
- ⚡ **ThinLTO job limiting** (`--thinlto-jobs=$(nproc/2)`) to prevent CPU thrashing
- 🔄 **Aggressive ccache** with kernel-specific sloppiness for maximal cache hits
- 📦 **Pre-downloaded toolchain** via aria2c with 16 connections
- 🗑️ **Background cleanup** of unused GitHub runner packages

### Build Time Expectations with CCache
| Configuration | Estimated Time |
|--------------|----------------|
| `lto_type: none` + minimal patches | ~3:20-3:50 |
| `lto_type: thin` + all patches (default) | ~4:50-5:50 |
| `lto_type: full` + all patches | ~7:00-9:00 |

> 💡 **Tip**: Use `lto_type: none` for rapid testing, `thin` for release builds.

---

## 📱 Supported Devices

| Device | Codename | Status |
|--------|----------|--------|
| **OnePlus 13** | `PJZ110` (CN) / `OP13` (Global) | ✅ Fully Supported |
| **OnePlus 13T** | `OP13T` | ⚠️ Untested (may work) |

> Requires unlocked bootloader + custom recovery (TWRP / KernelFlasher)

---

## 📦 Installation

1. Download the latest `AnyKernel3_*.zip` from [Releases](../../releases) or Actions artifacts
2. Boot to custom recovery (TWRP / OrangeFox / KernelFlasher)
3. Flash the ZIP file
4. **(Required)** Install a metamodule for KSU:
   - [mountify](https://github.com/SukiSU-Ultra/mountify)
   - [meta-overlayfs](https://github.com/SukiSU-Ultra/meta-overlayfs)
   - [meta-magicmount](https://github.com/SukiSU-Ultra/meta-magicmount)
5. Reboot and enjoy! 🎉

> ⚠️ **Disclaimer**: I am not responsible for bricked devices, data loss, or other issues. Flash at your own risk.

---

## 🤝 Credits & Acknowledgements

| Contributor | Contribution |
|-------------|-------------|
| [mrcxlinux](https://github.com/mrcxlinux) | The base workflow
| [xiaomichael](https://github.com/xiaomichael) | Some help & GKI infrastructure |
| [cctv18](https://github.com/cctv18) | SuSFS, ccache-ECS, Baseband Guard, public ccache |
| [vc-teahouse](https://github.com/vc-teahouse) | SukiSU Ultra core & KPM framework |
| [Numbersf](https://github.com/Numbersf) | Fengchi / HMBIRD scheduler patches |
| [WildKernels](https://github.com/WildKernels) | 25 memory/scheduler optimization patches & workflow optimization |
| [ShirkNeko](https://github.com/ShirkNeko) | LZ4KD & ZRAM patches |
| [ZyCromerZ](https://github.com/ZyCromerZ) | Oryon-optimized Clang 19 toolchain |
| [TheWildJames](https://github.com/TheWildJames) | Unicode fix & additional kernel patches |

---

## 🌟 Support the Project

<p align="center">
  If this kernel improves your daily driver, please consider:
</p>

<p align="center">
  ⭐ <b>Starring this repository</b> – helps others discover it!<br>
  🐛 <b>Reporting issues</b> – helps me fix bugs faster<br>
  💡 <b>Suggesting features</b> – I read every issue!<br>
  🔁 <b>Sharing your builds</b> – tag me in your Telegram/Discord posts
</p>

<p align="center">
  <sub>Built with ❤️ by palaziks • Kernel version: <code>6.6.138-palaziks-ShiftPorts</code></sub>
</p>
```
