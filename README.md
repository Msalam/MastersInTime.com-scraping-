
⌚ MastersInTime.com High-Performance Watch Scraper

![alt text](https://img.shields.io/badge/python-3.9%2B-blue)


![alt text](https://img.shields.io/badge/Engine-BeautifulSoup4%20%2F%20Requests-green)


![alt text](https://img.shields.io/badge/Optimized-Multi--Threaded-orange)

📌 Project Overview

This project is a high-performance data engineering solution designed to extract the entire catalog of MastersInTime.com, a premier global platform for luxury wristwatches and timepieces.

The scraper is engineered to navigate deep technical specifications for thousands of watches, transforming unstructured HTML into a structured, research-ready dataset. By implementing advanced concurrency and memory management, this tool achieves professional-grade extraction speeds while maintaining a small resource footprint.

Industry: Horology & Luxury Retail

Project Duration: 1 – 7 days

Data Points Extracted: 50+ per product

🚀 Technical Innovations & "Speed Tricks"

To outperform standard sequential scrapers, I implemented several advanced optimization techniques:

1. Persistent Connection Pooling (requests.Session)

Instead of opening a new TCP connection for every product link—which is slow and resource-heavy—the script uses a persistent session with a custom HTTPAdapter.

The Benefit: It keeps 50 connections active at all times, eliminating the "handshake" lag and increasing request speed by up to 400%.

2. O(1) Attribute Mapping (Single-Pass Parsing)

Most scrapers search the entire page 50 times to find 50 different labels.

The Trick: I built a Dictionary Map of the product table in a single pass. The script reads the HTML once, stores all data-attribute-id values in memory, and then instantly retrieves them. This reduces DOM traversal time significantly.

3. Multi-Threaded Parallelism

Using ThreadPoolExecutor with a tuned MAX_WORKERS setting, the scraper processes dozens of URLs simultaneously. It uses an asynchronous-style workflow where data is processed as soon as it arrives, rather than waiting in a queue.

4. Buffered Cloud I/O

Writing to a CSV on Google Drive after every row is slow due to network latency.

The Trick: I implemented a List Buffer. The script collects 20 records in RAM before performing a single "Batch Append" operation. This protects the hardware from excessive I/O and prevents Google Drive from throttling the connection.

5. C-Accelerated Parsing

By utilizing the lxml parser backend, the script processes the HTML structure using high-speed C libraries rather than native Python code, ensuring that the bottleneck is always the internet speed, not the CPU.

📊 Extracted Data Fields

The scraper captures an exhaustive dataset for every timepiece:

Category	Fields
General Info	Title1, Title2, Brand, Name, Year, Price Range, EAN, Description, URL
Case Specs	Diameter, Thickness, Material, Shape, Color, Case Code, Back Case Material, Crystal Material
Movement	Movement Brand, Part Number, Mechanism, Battery, Battery Life, Swiss Movement, Hackable, Skeletonized
Strap/Band	Strap Width, Material, Lug Width, Band Color, Clasp Type, Stitching Color, Wrist Size Suitability
Technical	Water Resistance, Dial Color, Hand Colors, Display Type, Swiss Made Status, Mount Type
Media	High-Resolution Image Link
🛠️ Tools & Technologies

Requests & Sessions: For high-speed HTTP communication and connection reuse.

BeautifulSoup4 (lxml): For rapid structural analysis of web documents.

Concurrent.Futures: For multi-threaded parallel execution.

tqdm: For real-time progress monitoring and velocity tracking (it/s).

Google Colab & Drive Integration: For cloud-based execution and persistent storage.

CSV/Excel: For final data structuring and delivery.

⚙️ How It Works

Authentication: Mounts Google Drive to ensure the data is saved securely in the cloud.

Initialization: Sets up a high-capacity connection pool (50 connections).

Concurrency: Launches 20 simultaneous worker threads to crawl product pages.

Parsing: Maps data attributes via IDs for instantaneous lookups.

Batching: Collects results in a memory buffer and flushes to the CSV every 20 items to optimize storage performance.

👨‍💻 Author

[Mohamed Sallam]
Web Scraping & Data Science Enthusiast

Disclaimer: This project was created for educational and research purposes. Please ensure compliance with the target website's Terms of Service and robots.txt before use.