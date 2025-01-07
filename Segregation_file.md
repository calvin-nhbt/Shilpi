# How to create segfile in shilpi system

# Index

1. [Prerequisites](#prerequisites)
2. [Info 1](#info_1)
3. [Info 2](#info-2)

## Prerequisites (This needs to be done first)
- Import files and do bill posting of CM and FO segments.

## Download Files required for Segfile
### Files needed for segfile generation
We mainly need these files to be imported
1) CC01 file
  - This gives us information about
      - Globe fund allocation
      - securities pledged and their EOD values.
  - Files to import are
```
      - F_CC01_<member_code._<date>.csv
      - C_CC01_<member_code._<date>.csv
```
2) Haircut info files (Only if securities are pledged)
  - If the client or we have pledged securites with Globe for margin, we'll need to calculate the haircut applicable.
  - Available margin from pledged securities = Actual value of securities - haircut %
  - The files required here are
    ```
      - Haircut File for Stocks       (APPSEC_COLLVAL_<date>.csv)
      - Haircut File for Mutual Funds (MF_VAR_<date>.csv)
    ```
3) Price files (Only if securities are pledged)
  - To calculate the value of these securities, we need their closing prices.
  - The files needed here are
```
  - Price file for stocks  (Bhavcopy_CM_...)
  - Price for mutual funds (NAVDWLD_<date>.txt)
```

### How to download the files
Note: most of these files would be sent via email already.
1) CC01 files are member files (These are available on the NSE's member portal)
2) Haircut files (search for "NSE all reports". These files are available on the public website of nse report downloads)
3) price files
  - Stocks -> "NSE All reports"
  - Mutual Funds ->
```
  - Google "BSE Star MF"
  - Visit this link "https://bsestarmf.in/index.aspx"
  - Click "NAV Master" at the bottom of the page.
  - In the dialog box that opens, select the date.
  - click "Export to Text"
  - It will download this file -> NAVDWLD_<date>.txt
```
