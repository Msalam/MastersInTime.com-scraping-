# ⌚ MastersInTime.com High-Performance Watch Scraper

<!-- Optional screenshots / diagrams -->
<!-- ![overview](image1.png) -->
<!-- ![schema](image2.png) -->
<!-- ![performance](image3.png) -->

---

## 📌 Project Overview

This project is a **high-performance data engineering solution** designed to extract the entire catalog of **MastersInTime.com**, a premier global platform for luxury wristwatches and timepieces.

The scraper is engineered to navigate deep technical specifications for **thousands of watches**, transforming unstructured HTML into a **structured, research-ready dataset**.  
By implementing advanced concurrency and memory management, this tool achieves **professional-grade extraction speeds** while maintaining a **small resource footprint**.

**Industry:** Horology & Luxury Retail  
**Project Duration:** 1 – 7 days  
**Data Points Extracted:** 50+ per product  

---

## 🚀 Technical Innovations & Speed Optimizations

To outperform standard sequential scrapers, several advanced optimization techniques were implemented:

### 🔹 Persistent Connection Pooling (requests.Session)
Instead of opening a new TCP connection for every product link—which is slow and resource-heavy—the script uses a persistent session with a custom `HTTPAdapter`.

**Benefit:**  
Keeps **50 connections active** at all times, eliminating handshake latency and improving request speed by **up to 400%**.

---

### 🔹 O(1) Attribute Mapping (Single-Pass Parsing)
Most scrapers traverse the DOM **dozens of times** to extract different attributes.

**The Trick:**  
A **dictionary-based attribute map** is built in a single HTML pass.  
All `data-attribute-id` values are stored in memory and accessed instantly.

**Result:**  
Significant reduction in DOM traversal time and CPU overhead.

---

### 🔹 Multi-Threaded Parallelism
Using `ThreadPoolExecutor` with a tuned `MAX_WORKERS` value, the scraper processes **multiple product pages concurrently**.

**Execution Model:**  
Asynchronous-style execution where results are handled **as soon as they are completed**, not sequentially.

---

### 🔹 Buffered Cloud I/O
Writing each record individually to Google Drive introduces heavy network latency.

**The Trick:**  
A **RAM buffer** collects 20 records before performing a single batch write to CSV.

**Result:**  
- Reduced Drive throttling  
- Lower I/O overhead  
- More stable long-running execution  

---

### 🔹 C-Accelerated Parsing
The scraper uses the **lxml parser backend**, leveraging high-speed C libraries instead of pure Python parsing.

**Outcome:**  
The performance bottleneck becomes **network speed**, not CPU.

---

## 📊 Extracted Data Fields

The scraper captures a comprehensive dataset for each timepiece.

### 🧾 General Information
- Title1
- Title2
- Brand
- Name
- Year
- Price Range
- EAN
- Description
- Product URL

### 🕰️ Case Specifications
- Diameter
- Thickness
- Material
- Shape
- Color
- Case Code
- Back Case Material
- Crystal Material

### ⚙️ Movement
- Movement Brand
- Part Number
- Mechanism
- Battery
- Battery Life
- Swiss Movement
- Hackable
- Skeletonized

### 🎽 Strap / Band
- Strap Width
- Material
- Lug Width
- Band Color
- Clasp Type
- Stitching Color
- Wrist Size Suitability

### 🔬 Technical Details
- Water Resistance
- Dial Color
- Hand Colors
- Display Type
- Swiss Made Status
- Mount Type

### 🖼️ Media
- High-Resolution Image Link

---

## 🛠️ Tools & Technologies

- **Requests & Sessions** — High-speed HTTP communication and connection reuse  
- **BeautifulSoup4 (lxml)** — Fast and reliable HTML parsing  
- **Concurrent.Futures** — Multi-threaded execution  
- **tqdm** — Real-time progress and speed tracking  
- **Google Colab & Drive** — Cloud execution and persistent storage  
- **CSV / Excel** — Structured data output  

---

## ⚙️ How It Works

1. **Authentication**  
   Google Drive is mounted to ensure persistent cloud storage.

2. **Initialization**  
   A high-capacity HTTP connection pool (50 connections) is created.

3. **Concurrency**  
   20 parallel worker threads crawl product pages simultaneously.

4. **Parsing**  
   Product attributes are mapped via `data-attribute-id` for instant lookup.

5. **Batching**  
   Results are buffered in memory and written to CSV every 20 records.

---

## 👨‍💻 Author

**Mohamed Sallam**  
Web Scraping & Data Science Enthusiast  

Feel free to fork, optimize, or reach out 🚀
