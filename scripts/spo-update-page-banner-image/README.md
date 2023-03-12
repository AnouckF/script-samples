---
plugin: add-to-gallery
---

# Update SharePoint Page Banner Image

## Summary

This sample script shows how to update the banner image at the top of the SharePoint online modern page using PnP PowerShell.

![Outupt Screenshot](assets/output.png)

# [PnP PowerShell](#tab/pnpps)

```powershell

# SharePoint online site url
$siteUrl = "https://contoso.sharepoint.com/sites/wlive"	

# Connect to SharePoint Online site  
Connect-PnPOnline -Url $siteUrl -Interactive

# Update site page banner image
Set-PnPPage -Identity "Open-Door-Policy" -HeaderType Custom -ServerRelativeImageUrl "/sites/wlive/SiteAssets/work-remotely.jpeg"

```

[!INCLUDE [More about PnP PowerShell](../../docfx/includes/MORE-PNPPS.md)]

***

## Contributors

| Author(s) |
|-----------|
| [Ganesh Sanap](https://ganeshsanapblogs.wordpress.com/about) |


<img src="https://m365-visitor-stats.azurewebsites.net/script-samples/scripts/spo-update-page-banner-image?labelText=Visitors" class="img-visitor" aria-hidden="true" />


[!INCLUDE [DISCLAIMER](../../docfx/includes/DISCLAIMER.md)]
