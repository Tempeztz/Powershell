# Excel Data Updater Script

This PowerShell script processes and updates Excel files by combining data from two source files. It updates resource group information and disk size values (OS disk and data disk) in a target Excel file based on matching records from a source file.

## Overview

- **Source Excel File (`Azuredisks_prod.xlsx`)**:  
  Contains original data with details like **ServerName**, **Resource Group**, and disk sizes (Measured in GiB). This file is used to extract resource group and disk size information.

- **Target Excel File (`CombinedResult1.xlsx`)**:  
  Contains records that need to be updated with resource group and disk size information. If the necessary columns (`Resource Group`, `osdisk`, and `datadisk`) are missing, the script adds them.

- **Output Excel File (`CombinedResult2.xlsx`)**:  
  The final updated Excel file, saved with a new worksheet named **UpdatedData**.

## Prerequisites  

- **PowerShell (v5 or higher)**  
  Ensure you have an appropriate version of PowerShell installed on your machine.

- **ImportExcel Module**  
  This script uses the [ImportExcel](https://github.com/dfinke/ImportExcel) module to handle Excel file operations.  
  Install the module by running the following command in PowerShell (if not already installed):

  ```powershell
  Install-Module ImportExcel -Scope CurrentUser
  ```

## How It Works

1. **Importing Excel Files**  
   The script imports two Excel files:  
   - *Book1:* Contains the source data (example: resource group and disk size details)  
   - *Book2:* Contains the data to be updated  

2. **Column Verification and Addition**  
   The script checks whether the target file (*Book2*) has the following columns:  
   - `Resource Group`  
   - `osdisk`  
   - `datadisk`  
   If any of these columns are missing, they are added with default values (empty string for Resource Group, `0` for disk sizes).  

3. **Updating Records**  
   The script updates *Book2* based on matching values from *Book1* using the `ServerName` column as a reference.  

4. **Output Excel File (`CombinedResult2.xlsx`)**  
   The final updated Excel file, saved with a new worksheet named **UpdatedData**.  

## Usage

### Run the Script

Save the PowerShell script in the same directory as the Excel files and run:

```powershell
.\Update-Excel.ps1
```

### Example PowerShell Code

```powershell
# Import Required Module
Import-Module ImportExcel

# Load Source and Target Excel Files
$SourceFile = "Azuredisks_prod.xlsx"
$TargetFile = "CombinedResult1.xlsx"
$OutputFile = "CombinedResult2.xlsx"

# Read Excel Data
$SourceData = Import-Excel -Path $SourceFile
$TargetData = Import-Excel -Path $TargetFile

# Ensure Required Columns Exist in Target File
if (-not ($TargetData | Get-Member -Name 'Resource Group')) {
    $TargetData | Add-Member -MemberType NoteProperty -Name 'Resource Group' -Value ''
}

if (-not ($TargetData | Get-Member -Name 'osdisk')) {
    $TargetData | Add-Member -MemberType NoteProperty -Name 'osdisk' -Value 0
}

if (-not ($TargetData | Get-Member -Name 'datadisk')) {
    $TargetData | Add-Member -MemberType NoteProperty -Name 'datadisk' -Value 0
}

# Update Data Based on Matching ServerName
foreach ($row in $TargetData) {
    $match = $SourceData | Where-Object { $_.ServerName -eq $row.ServerName }
    if ($match) {
        $row."Resource Group" = $match."Resource Group"
        $row.osdisk = $match.osdisk
        $row.datadisk = $match.datadisk
    }
}

# Export Updated Data to New Excel File
$TargetData | Export-Excel -Path $OutputFile -WorksheetName "UpdatedData" -AutoSize

Write-Output "Excel file updated successfully: $OutputFile"
```

## Notes

- Ensure that the **source** and **target** Excel files are in the same directory as the script.  
- This script modifies an Excel file. Always keep a backup before running.  
- If PowerShell execution policies block running the script, you may need to enable script execution:

  ```powershell
  Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
  ```

---

**Author:** Your Name  
**Date:** Current Date  
**Version:** 1.0  
