---
plugin: add-to-gallery-preparation
---

# Get list of available content types on library in SharePoint Online

> [!Note]
> This is a submission helper template please find the [contributor guidance](/docfx/contribute.md) to help you write this scenario.

## Summary

This script connects to the SharePoint Online admin center, retrieves all site collections in the tenant (excluding OneDrive sites), and for each site, it lists all document libraries and the content types associated with them. The collected data is exported to a CSV file for reporting or auditing purposes.

This is especially useful when your organization has implemented a strong content type structure for document management. Knowing which content types are available on each document library helps you:

✅ Validate governance and compliance by ensuring that only the intended content types are being used across libraries.

✅ Support automation and metadata consistency by confirming the presence of expected columns and content types that automated flows and policies rely on.

✅ Identify and clean up legacy or orphaned content types, which can reduce confusion and improve maintainability.

✅ Enhance the user experience by limiting content types to what’s relevant, helping users apply the right metadata quickly.

✅ Prepare for broader solutions like metadata-driven navigation, Viva Topics, Syntex models, or Power BI reporting across multiple sites or hub sites.

In short, this script helps ensure that your SharePoint content architecture stays clean, consistent, and aligned with your organization's information management goals.

# [PnP PowerShell](#tab/pnpps)

```powershell

# Ensure you have the PnP PowerShell module installed and imported
# Install-Module -Name "PnP.PowerShell" -Force

# Connect to the SharePoint tenant
$AdminSiteUrl = "https://YOURDOMAIN-admin.sharepoint.com"
Connect-PnPOnline -Url $AdminSiteUrl -ClientId "" -Interactive

# Output file to store the results
$OutputFile = "C:\Temp\LibrariesAndContentTypes.csv"
$Results = @()

# Get all site collections
$SiteCollections = Get-PnPTenantSite -IncludeOneDriveSites:$false 
foreach ($Site in $SiteCollections) {
    Write-Host "Processing site: $($Site.Url)" -ForegroundColor Cyan

    # Connect to the site
    Connect-PnPOnline -Url $Site.Url -ClientId "" -Interactive

    # Get all document libraries in the site
    $Libraries = Get-PnPList | Where-Object { $_.BaseTemplate -eq 101 }

    foreach ($Library in $Libraries) {
        Write-Host "Processing library: $($Library.Title)" -ForegroundColor Yellow

        # Get all content types associated with the library
        $ContentTypes = Get-PnPContentType -List $Library

        foreach ($ContentType in $ContentTypes) {
            $Results += [PSCustomObject]@{
                SiteName       = $Site.Url
                LibraryName    = $Library.Title
                ContentType    = $ContentType.Name
            }
        }
    }
}

# Export results to CSV
$Results | Export-Csv -Path $OutputFile -NoTypeInformation -Encoding UTF8
Write-Host "Results exported to $OutputFile" -ForegroundColor Green

```
[!INCLUDE [More about PnP PowerShell](../../docfx/includes/MORE-PNPPS.md)]

## Contributors

| Author(s) |
|-----------|
| [Anouck Fierens](https://github.com/anouckf) |

[!INCLUDE [DISCLAIMER](../../docfx/includes/DISCLAIMER.md)]
<img src="https://m365-visitor-stats.azurewebsites.net/spo-export-checked-out-files-in-all-sites-associated-with-a-hub-site-to-csv" aria-hidden="true" />