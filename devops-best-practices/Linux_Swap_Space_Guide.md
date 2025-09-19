# ⚡ Linux Swap Space Guide

Swap space is one of the most **overlooked performance factors** in Linux systems.  
Configured poorly, it can **slow your system to a crawl**. Configured well, it acts as a **stability booster** and prevents crashes under memory pressure.  

This guide covers everything you need to know about **Swap Space configuration, best practices, tips, and tricks**.  

---

## 🔹 What is Swap Space?

- **Swap** is a portion of disk storage used as **virtual memory** when physical RAM is full.  
- When memory runs out, **inactive pages** are moved to swap, freeing RAM for active tasks.  
- **Downside:** Disk (even SSD) is much slower than RAM, so excessive swapping reduces performance.  

Think of swap as a **safety net**, not a performance booster.

---

## 🔹 How Much Swap Do You Need?

| System RAM       | Recommended Swap Size |
|------------------|------------------------|
| ≤ 2 GB           | 2 × RAM                |
| 2–8 GB           | Equal to RAM           |
| 8–64 GB          | 0.5 × RAM              |
| ≥ 64 GB          | 4–8 GB (safety net)    |

👉 If you use **hibernate**, allocate at least as much swap as RAM.

---

## 🔹 Swap Partition vs. Swap File

- **Swap Partition**
  - Slightly faster, avoids filesystem overhead.
  - Good for dedicated servers.
- **Swap File**
  - Flexible (easy to create, resize, delete).
  - Ideal for VMs and cloud environments.

✅ **Recommendation:** Use **swap files** for most modern setups.

---

## 🔹 Tuning `swappiness`

`swappiness` determines how aggressively Linux swaps memory pages.

- Range: `0` (least aggressive) → `100` (most aggressive).
- Default: `60` (often too aggressive).
- Best Practice:
  - `10–20` for production servers (databases, web apps).
  - `30–40` for desktops.

Check current value:
```bash
cat /proc/sys/vm/swappiness

Set temporarily:
sudo sysctl vm.swappiness=20
Make permanent:
echo "vm.swappiness=20" | sudo tee -a /etc/sysctl.conf

🔹 Tips & Tricks for Swap Optimization

⚡ Use SSD/NVMe for Swap
Placing swap on fast storage drastically reduces latency compared to HDD.

⚡ Enable zswap or zram

zram: Creates a compressed block device in RAM.
zswap: Compresses pages before swapping to disk.
Both reduce disk I/O and improve performance.

⚡ Monitor Swap Usage
free -h
vmstat 5
htop
If swap is consistently high → Add more RAM, not just more swap.

⚡ Multiple Swap Devices
On NUMA or multi-disk servers, spread swap across devices for better throughput.

🔹 Step-by-Step: Create a Swap File

Create a swap file (example: 4 GB):
sudo fallocate -l 4G /swapfile

Secure permissions:
sudo chmod 600 /swapfile

Format as swap:
sudo mkswap /swapfile

Enable it:
sudo swapon /swapfile

Verify:
swapon --show
free -h

Make it permanent (add to /etc/fstab):
/swapfile none swap sw 0 0

🔹 Common Mistakes to Avoid
❌ Allocating too much swap (wasted disk, slow performance).
❌ Leaving swappiness at default (60) on production servers.
❌ Treating swap as a RAM replacement.
❌ Using slow HDDs for swap on high-load systems.

🎯 Final Thoughts
Swap space is not a replacement for RAM.
It’s a safety net that provides stability during peak loads and prevents OOM (Out of Memory) errors.

By following these best practices—right sizing, using swap files, tuning swappiness, leveraging SSDs/zram, and monitoring—you’ll achieve a stable, efficient, and production-ready swap configuration.

📌 References
Linux Kernel Documentation: Swappiness : https://www.kernel.org/doc/Documentation/sysctl/vm.txt

Red Hat Performance Tuning Guide : https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/

💡 Pro Tip: If swap usage is constantly high → don’t just tweak swap. Upgrade your RAM!
