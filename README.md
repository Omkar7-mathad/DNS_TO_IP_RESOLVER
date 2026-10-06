# DNS to IP Resolver

A Python & Flask web application that demonstrates **Domain Name System (DNS) resolution** and **in-memory DNS caching**.

## 📌 Features

- **Domain to IP Resolution**: Converts hostnames/domains (e.g., `google.com`) into IPv4 addresses using socket lookups.
- **DNS Caching Mechanism**:
  - **DNS LOOKUP**: Performs actual lookup on initial query and records response latency.
  - **CACHE HIT**: Serves subsequent queries for cached domains instantly (~0ms response time).
- **Search History**: Maintains a reverse-chronological record of previous lookups.
- **Cache & History Management**: Easily clear cached IP mappings or resolution history with single-click actions.
- **Smart URL Sanitation**: Automatically cleans inputs containing `http://`, `https://`, or subpaths (e.g., `https://example.com/path` -> `example.com`).

---

## 🛠️ Technology Stack

- **Backend**: Python 3, Flask framework
- **Networking**: `socket` standard library
- **Frontend**: HTML5, CSS3 (Rendered via Flask `render_template_string`)

---

## 🚀 Quick Start

### Prerequisites

- Python 3.x installed on your system.

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Omkar7-mathad/DNS_TO_IP_RESOLVER.git
   cd DNS_TO_IP_RESOLVER
   ```

2. **Install dependencies**:
   ```bash
   pip install flask
   ```

### Running the Application

Execute the main script:
```bash
python app.py
```

Open your browser and navigate to:
```
http://127.0.0.1:5000
```

---

## 📖 How It Works

1. **User Request**: The user submits a domain name via the web interface.
2. **Input Normalization**: `clean_domain()` removes scheme prefixes (`http://`, `https://`) and URL paths.
3. **Cache Evaluation**:
   - If domain exists in `dns_cache`: Returns IP immediately with status `CACHE HIT` (0 ms latency).
   - If not found in cache: Calls `socket.gethostbyname()`, calculates latency in milliseconds, saves to `dns_cache`, and marks as `DNS LOOKUP`.
4. **History Update**: The result is prepended to the search history table.