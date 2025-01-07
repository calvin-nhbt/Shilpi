# How to create segfile in shilpi system

# Index

- [Prerequisites](#prerequisites-this-needs-to-be-done-first)
- [Download Files required for Segfile](#download-files-required-for-segfile)
  - [Files needed for segfile generation](#files-needed-for-segfile-generation)
  - [How to download the files](#how-to-download-the-files)
- [Upload files on Shilpi Software](#upload-files-and-generate-the-segfile-on-shilpi-software)
- [Check for Errors in Segfile](#check-for-errors-in-segfile)
- [Future Ideas](#future-ideas)

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


## Upload files and generate the Segfile on Shilpi Software
- Click [IMP].
  - Click "Closing Rate"
    - *_Price for Stocks_*
      - Not explaining here. Is is assumed to be uploaded already.
    - *_Price for Mutual Funds_*
      - Exchange = [NATIONAL STOCK EXCHANGE]
      - File Type = [NAV-BSEMF]
      - Uncheck "uDiff Formatted"
      - Trade Date = <date>
      - File Name = [ Select the "NAVDWLD_<date>.csv file] 
      - Click Import

- Click [i](Inspection Reports)
  - Click [Segragations and Monitoring of Collateral + Allocations]
    - Click [CC/Enmass/RTRMS File] (Upload CC01 for CM and FO here)
      - Uploading for CM now
        - Segment = CM
        - Check the CC01 box
        - Select the <date>.
        - select the proper file for the <date> -> "C_CC01_<member-code>_<date>.csv
      - Uploading for FO now
        - Segment = FO
        - Check the CC01 box
        - Select the <date>.
        - select the proper file for the <date> -> "F_CC01_<member-code>_<date>.csv
    - Close this dialog box for [CC/Enmass/RTRMS File]

    - Click [BGR/FDR Details]  (We'll add the details of the cash available on the ledger in here.)
      - Add cash details for FO
      - Add cash details for CM
    - Close this dialog box for [BGR/FDR Details]

    - Calculating Segregation
      - At the top right corner, under "Calculation Parameters",
        - update "Report Date".
        - keep pressing tab so it updates all the dates.
      - Click "Segregation Report".
      - Click "Calculate"

    - Generating the Segfile
      - At the top, under "File Export For Clearing"
        - select "Member"
      - Clg. Member = GLOBE
      - Check the <date> under "Deposit Export For Trading Day"
      - Under "Segregation Export"
        - Click "Client Monitoring Report"

    - The segfile will be generated under 
```
Windows(C:) > Shilpi > output > AAACG..._COMB_<date>_01.csv
```



## Check for Errors in Segfile
1) "Cash Retained by TM"
  - This value should be 0 for all.
  - File cannot be uploaded without this.


2) "Approved Securities Cash Component Retained by TM" / "Approved Securities Non-cash Component Retained by TM"
  - This should ideally be 0.
  - Even if it is not, file can still be uploaded.

3) "Other Collaterals placed with CM"
  - This is the last column we are allowed to edit.
  - All values after this should be 0.
  - If not, you cannot upload the file.
  - There is some calculation issue, or some file hasn't been uploaded, or some issue with shilpi software.

        
## Future Ideas
1) "Cash Retained by TM"
- This can happen.
- Ideally for this we need to upload a file with the details about retention.
Tip: Unexplored option. "Retention_Code_Reporting.. "
- Check if this file can be generated for this.