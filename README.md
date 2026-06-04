# Extraction Workflow

Automated workflow flowchart for extracting FIFA World Cup finals data from Wikipedia and appending it to Google Sheets via the Sheets API.

## 📋 Assignment Overview

**Objective:** Automate the extraction of information from the first 10 rows of the ["List of FIFA World Cup finals"](https://en.wikipedia.org/wiki/List_of_FIFA_World_Cup_finals) table on Wikipedia.

**Extracted columns:** `Year`, `Winner`, `Score`, `Runners-up`

**Target:** Append extracted data to a Google Sheet using the Google Sheets API (configured as a Postman-style POST request).

## 🔄 Workflow Summary

```
1. OPEN PAGE      →  Navigate to the Wikipedia page
2. LOOP (10×)     →  For each of the first 10 table rows:
   ├── 2.1  EXTRACT HTML  →  Year
   ├── 2.2  EXTRACT HTML  →  Winner
   ├── 2.3  EXTRACT HTML  →  Score
   ├── 2.4  EXTRACT HTML  →  Runners-up
   └── 2.5  CALL API      →  POST row to Google Sheets
3. END
```

## 🧩 Steps Used (from Step Library)

| Step | Type | Purpose |
|------|------|---------|
| 1 | **Open Page** | Load the Wikipedia FIFA World Cup finals page |
| 2 | **Loop** | Iterate 10 times (index `i` = 1 → 10) |
| 2.1 | **ExtractHTML** | Extract **Year** via DOM path |
| 2.2 | **ExtractHTML** | Extract **Winner** via DOM path |
| 2.3 | **ExtractHTML** | Extract **Score** via DOM path |
| 2.4 | **ExtractHTML** | Extract **Runners-up** via DOM path |
| 2.5 | **Call API** | Append row to Google Sheets |

## 🌐 API Details

| Field | Value |
|-------|-------|
| **Method** | `POST` |
| **URL** | `https://sheets.googleapis.com/v4/spreadsheets/{SPREADSHEET_ID}/values/Sheet1!A:D:append` |
| **Params** | `valueInputOption=USER_ENTERED`, `insertDataOption=INSERT_ROWS` |
| **Headers** | `Authorization: Bearer {ACCESS_TOKEN}`, `Content-Type: application/json` |

**Request Body:**
```json
{
  "range": "Sheet1!A:D",
  "majorDimension": "ROWS",
  "values": [
    ["{year}", "{winner}", "{score}", "{runner_up}"]
  ]
}
```

## 📊 Extracted Data (First 10 Rows)

| # | Year | Winner | Score | Runners-up |
|---|------|--------|-------|------------|
| 1 | 1930 | Uruguay | 4–2 | Argentina |
| 2 | 1934 | Italy | 2–1 (a.e.t.) | Czechoslovakia |
| 3 | 1938 | Italy | 4–2 | Hungary |
| 4 | 1950 | Uruguay | 2–1 | Brazil |
| 5 | 1954 | West Germany | 3–2 | Hungary |
| 6 | 1958 | Brazil | 5–2 | Sweden |
| 7 | 1962 | Brazil | 3–1 | Czechoslovakia |
| 8 | 1966 | England | 4–2 (a.e.t.) | West Germany |
| 9 | 1970 | Brazil | 4–1 | Italy |
| 10 | 1974 | West Germany | 2–1 | Netherlands |

## 📂 How to View

Open **`flowchart.html`** in any browser to view the detailed, interactive flowchart with all inputs, outputs, DOM paths, and API configuration for each step.
