# RAID
## What is RAID?
RAID stands for Redundant Array of Inexpensive Disks. The idea is to create a large storage system using a pool of cheap disks. System capacity and cost depend on the number of disks in the pool.
### Advantages
Fault tolerance, improved system performance because of concurrency (you can read multiple parts of the file at the same time pretty fast)
## **RAID 0 (Striping)**
- **Purpose**: Performance
- **How it works**: Data is split into "stripes" and distributed across all disks in the array.
- **Advantages**:
  - High read/write speeds as data is accessed from multiple disks simultaneously.
  - Maximum storage utilization (no overhead).
- **Disadvantages**:
  - No redundancy: If one disk fails, all data is lost.
- **Use cases**: Non-critical applications where speed is essential, such as gaming.

---

## **RAID 1 (Mirroring)**
- **Purpose**: Redundancy
- **How it works**: Data is duplicated (mirrored) across two disks.
- **Advantages**:
  - High redundancy: If one disk fails, the other contains a complete copy of the data.
  - Improved read performance (data can be read from either disk).
- **Disadvantages**:
  - Storage efficiency is 50% (half of the total capacity is used for mirroring).
  - No improvement in write performance.
- **Use cases**: Critical data storage, such as operating systems or databases.

---

## **RAID 2 (Bit-Level Striping with Hamming Code)**
- **Purpose**: Redundancy
- **How it works**: Data is striped at the bit level, with error correction using Hamming codes.
- **Advantages**:
  - Theoretical data correction capabilities.
- **Disadvantages**:
  - Rarely used due to inefficiency and high complexity.
  - Requires a significant number of disks.
- **Use cases**: Practically obsolete.

---

## **RAID 3 (Byte-Level Striping with Parity Disk)**
- **Purpose**: Redundancy and performance
- **How it works**: Data is striped at the byte level, with parity stored on a dedicated disk.
- **Advantages**:
  - Improved performance for large sequential data transfers.
  - Fault tolerance for a single disk failure.
- **Disadvantages**:
  - Poor performance for small, random I/O operations.
  - The dedicated parity disk can become a bottleneck.
- **Use cases**: Media streaming or similar workloads.

---

## **RAID 4 (Block-Level Striping with Parity Disk)**
- **Purpose**: Redundancy and performance
- **How it works**: Data is striped at the block level, with parity stored on a dedicated disk.
- **Advantages**:
  - Better performance than RAID 3 for block-level operations.
  - Single-disk fault tolerance.
- **Disadvantages**:
  - The dedicated parity disk can still become a bottleneck.
- **Use cases**: Applications needing both performance and redundancy.

---

## **RAID 5 (Block-Level Striping with Distributed Parity)**
- **Purpose**: Redundancy and performance
- **How it works**: Data and parity are striped across all disks. Parity is distributed, avoiding a single point of failure.
- **Advantages**:
  - Balanced performance and fault tolerance.
  - Storage efficiency (total capacity = (n-1) * size of the smallest disk, where n is the number of disks).
- **Disadvantages**:
  - Write performance is slower due to parity calculations.
  - Can only tolerate the failure of one disk.
- **Use cases**: General-purpose storage, such as file servers.

---

## **RAID 6 (Block-Level Striping with Dual Distributed Parity)**
- **Purpose**: High redundancy
- **How it works**: Similar to RAID 5, but with two parity blocks per stripe, distributed across all disks.
- **Advantages**:
  - Can tolerate the failure of two disks simultaneously.
  - Better redundancy than RAID 5.
- **Disadvantages**:
  - More storage overhead (total capacity = (n-2) * size of the smallest disk).
  - Slower write performance due to dual parity calculations.
- **Use cases**: Critical data storage with high fault tolerance requirements, such as enterprise environments.

---

Each RAID level has its trade-offs, and the choice depends on your specific needs for performance, redundancy, and storage efficiency.
