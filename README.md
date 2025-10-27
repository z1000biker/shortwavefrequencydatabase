# 📻 Shortwave Frequency Database (A25 · MHz Edition)

A clean, structured, and SDR-friendly version of the **A25 shortwave and broadcast frequency list**, converted entirely to **MHz** with two decimal precision.

This dataset is designed for **Shortwave Listeners (SWL)**, **DXers**, and **SDR enthusiasts** who want a ready-to-use frequency database for logging, scanning, and propagation analysis.

 🐍 Python Script — Fetch and Convert EIBI Shortwave Frequency List (A25)

This script automatically downloads the **EIBI shortwave master frequency list (A25)**  
from [http://www.eibispace.de/dx/freq-a25.txt](http://www.eibispace.de/dx/freq-a25.txt),  
parses the data, and outputs two clean CSV files in **MHz** for SDR, SWL, and DX use.

---

## ⚙️ Requirements

```bash
pip install pandas requests
```

---

## 💻 Script

```python
import pandas as pd
import requests
import re

# URL of EIBI A25 frequency list
URL = "http://www.eibispace.de/dx/freq-a25.txt"

# Download the text file
response = requests.get(URL)
response.raise_for_status()

# Save local copy
with open("freq-a25.txt", "w", encoding="utf-8") as f:
    f.write(response.text)

# Parse lines
lines = response.text.splitlines()

records_unique = []
records_all = []

# Regex: capture frequency (kHz) and station (up to next large space)
pattern_station = re.compile(
    r"^\s*([\d\.]+)\s+\S+\s+([A-Z]{2,3}\s+[A-Z0-9]+\s+[A-Za-z0-9\s\-\(\)\/\.'']+?)\s{2,}"
)
pattern_all = re.compile(r"^\s*([\d\.]+)\s+(.*)")

for line in lines:
    # All entries (for freq_all_converted_MHz.csv)
    match_all = pattern_all.match(line)
    if match_all:
        try:
            freq_khz = float(match_all.group(1))
            freq_mhz = round(freq_khz / 1000, 2)
            full_info = match_all.group(2).strip()
            records_all.append((freq_mhz, full_info))
        except ValueError:
            continue

    # Unique entries (for freq_final_converted_MHz.csv)
    match = pattern_station.match(line)
    if match:
        try:
            freq_khz = float(match.group(1))
            freq_mhz = round(freq_khz / 1000, 2)
            station = match.group(2).strip()
            records_unique.append((freq_mhz, station))
        except ValueError:
            continue

# Create DataFrames
df_unique = pd.DataFrame(records_unique, columns=["Frequency (MHz)", "Station"])
df_all = pd.DataFrame(records_all, columns=["Frequency (MHz)", "Full_Info"])

# Drop duplicate frequencies for unique file
df_unique = df_unique.drop_duplicates(subset=["Frequency (MHz)"])

# Save outputs
df_unique.to_csv("freq_final_converted_MHz.csv", index=False)
df_all.to_csv("freq_all_converted_MHz.csv", index=False)

print("✅ Files created successfully:")
print("- freq_final_converted_MHz.csv (unique stations)")
print("- freq_all_converted_MHz.csv (all entries)")
```

---

## 🛰️ Data Source

All data are provided by **EIBI Shortwave Frequency List**  
📍 URL: [http://www.eibispace.de/dx/freq-a25.txt](http://www.eibispace.de/dx/freq-a25.txt)  
📆 Edition: **A25 (Autumn 2025)**

The data are published by **Eike Bierwirth (EIBI)** for the global shortwave listening community.

---

## 📁 Files Included

| File | Description |
|------|--------------|
| `freq_final_converted_MHz.csv` | One **unique station per frequency** (clean reference list for fast tuning). |
| `freq_all_converted_MHz.csv` | **Full dataset** including all transmissions, languages, schedules, and sites — ideal for analysis or SDR log matching. |

---

## 📊 Data Format

### `freq_final_converted_MHz.csv`
| Column | Description |
|--------|--------------|
| `Frequency (MHz)` | Frequency converted from kHz to MHz (two decimals). |
| `Station` | Primary station name (unique per frequency). |

### `freq_all_converted_MHz.csv`
| Column | Description |
|--------|--------------|
| `Frequency (MHz)` | Frequency converted from kHz to MHz. |
| `Full_Info` | Full line entry from the original A25 schedule (includes station, language, UTC times, transmitter site, etc.). |

---

## 🎧 Use Cases

- 🛰️ **SDR software integration** – import the CSVs into SDR#, HDSDR, SDRUno, or other apps for live scanning.  
- 🌍 **SWL & DXing** – identify international stations, monitor bands, and log receptions.  
- 📊 **Data visualization** – analyze activity by band, region, or broadcaster.  
- 📡 **Propagation studies** – compare seasonal schedules (A25 vs B25, etc.) to detect frequency trends.  

---

## ⚙️ Technical Details

- All frequencies converted from **kHz → MHz** with 2-decimal precision.  
- Parsing and cleaning done with **Python + Regular Expressions**.  
- Dataset based on the **A25 master frequency list (Autumn 2025)**.  

---

## 🧠 Author

Created and compiled by **Nik - sv1eex** — SDR hobbyist, SWL, and DX enthusiast.  
Feel free to contribute updates or suggest improvements through pull requests.

---

## 📜 License

Released under the **MIT License** — free for research, non-commercial, and hobbyist use.

---

## 🛰️ 73’s and Good DX!
