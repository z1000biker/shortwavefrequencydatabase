# 📻 Shortwave Frequency Database (A25 · MHz Edition)

A clean, structured, and SDR-friendly version of the **A25 shortwave and broadcast frequency list**, converted entirely to **MHz** with two decimal precision.

This dataset is designed for **Shortwave Listeners (SWL)**, **DXers**, and **SDR enthusiasts** who want a ready-to-use frequency database for logging, scanning, and propagation analysis.

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
