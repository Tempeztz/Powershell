# README

## Overview
This repository contains two PowerShell scripts designed to automate Excel file processing:

1. **Unmerge.ps1** - Cleans and formats Excel files by unmerging cells, removing unnecessary rows, and handling empty columns.
2. **Dataretrieve.ps1** - Retrieves specific publisher-related data from multiple Excel files and consolidates it into a single output file.

Both scripts leverage the `ImportExcel` module for Excel manipulations.

## Prerequisites
- Windows OS with PowerShell installed.
- Microsoft Excel installed.
- [`ImportExcel`](https://www.powershellgallery.com/packages/ImportExcel) PowerShell module.

### Install `ImportExcel`:
```powershell
Install-Module -Name ImportExcel -Force -Scope CurrentUser
```

## Script Details

### 1. Unmerge.ps1
#### Description
`Unmerge.ps1` processes Excel files by:
- Detecting and unmerging merged cells.
- Removing unnecessary rows above a specified header row.
- Identifying and removing empty columns.
- Saving the cleaned files in a specified output directory.

#### Setup
- **Source Directory:** Define the path containing the Excel files to clean:
  ```powershell
  $sourceDir = "C:\Path\To\Your\Excel\Files\*.xlsx"
  ```
- **Output Directory:** Define where cleaned files will be saved:
  ```powershell
  $outputDir = "C:\Path\To\Save\Cleaned\Files"
  ```

#### Usage
1. Open PowerShell as Administrator.

2. Navigate to the script’s directory:
   ```powershell
   cd "C:\Path\To\Script"
   ```
3. Run the script:
   ```powershell
   .\Unmerge.ps1
   ```

#### Output
- Cleaned Excel files saved in the specified output directory.

### 2. Dataretrieve.ps1
#### Description
`dataretrieve.ps1` extracts publisher-specific data from Excel files by:
- Reading publisher names from `publisher.xlsx`.
- Searching for matches in other Excel files within a specified directory.
- Extracting related product and OS details.
- Saving results into `outputfile.xlsx`.

#### Setup
- **Publisher File:** Path to the Excel file containing a list of publishers:
  ```powershell
  $publisherFile = "C:\Path\To\publisher.xlsx"
  ```
- **Source Directory:** Directory containing Excel files to search:
  ```powershell
  $sourceDirectory = "C:\Path\To\Source\Files"
  ```
- **Output File:** Path for the result file:
  ```powershell
  $outputFile = "C:\Path\To\outputfile.xlsx"
  ```

#### Usage
1. Ensure `publisher.xlsx` contains a `"publisher"` column with names.
2. Place Excel files in the source directory.
3. Open PowerShell as Administrator.
4. Navigate to the script’s directory:
   ```powershell
   cd "C:\Path\To\Script"
   ```
5. Run the script:
   ```powershell
   .\dataretrieve.ps1
   ```

#### Output
- Extracted data saved into `outputfile.xlsx`.

## Troubleshooting
- For script execution issues, temporarily bypass execution policy:
  ```powershell
  Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
  ```
- Ensure all Excel files are closed before running the scripts.
- Verify that Excel and the `ImportExcel` module are installed.

## Conclusion
These PowerShell scripts simplify the process of cleaning and extracting data from Excel files, making data preparation and analysis more efficient. For any issues or further customization, review the script comments or modify paths as needed.
