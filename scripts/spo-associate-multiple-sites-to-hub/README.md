---
plugin: add-to-gallery
---

# Associate Multiple Site Collections to Hub Site

## Summary

This PowerShell script can be used to  associate mutilple site collections to HUB site. you can provide list of site collection urls in the array.

## Implementation

- Open Windows PowerShell ISE
- Create a new file
- Update the parameters with site collection urls and hub site url
- Save the file and run it
 
# [PnP PowerShell](#tab/pnpps)
```powershell

	#Parameters

     #Provide Hub Site URL
	$HubSiteURL = "https://******.sharepoint.com/sites/**********"

	#Array of site collections to associate site with
    $arrSCs = @("https://******.sharepoint.com/sites/**********", "https://******.sharepoint.com/sites/**********", "https://******.sharepoint.com/sites/**********")

	#get admin user credentials
	$creds = (Get-Credential)

	function AssociateHubSite{
		try{
			foreach ($SC in $arrSCs){ 
				Write-Host "Connecting site collection " $SC 
				Connect-PnPOnline -Url $SC -Credentials $creds
				Add-PnPHubSiteAssociation -Site $SC -HubSite $HubSiteURL -ErrorAction Stop
				Write-Host "Hub site associated with site collection:" $SC -ForegroundColor Green            
			}
		}
		catch {
			Write-Host "Error in associating hub site $($SC) :" $_.Exception.Message -ForegroundColor Red
		}   
		
		#Disconnect sharepoint connection
		Disconnect-PnPOnline
	}

	AssociateHubSite
```
[!INCLUDE [More about PnP PowerShell](../../docfx/includes/MORE-PNPPS.md)]
***

## Contributors

| Author(s) |
|-----------|
| [Siddharth Vaghasia](https://github.com/siddharth-vaghasia)


<img src="https://m365-visitor-stats.azurewebsites.net/script-samples/scripts/spo-associate-multiple-sites-to-hub?labelText=Visitors" class="img-visitor" aria-hidden="true" />

[!INCLUDE [DISCLAIMER](../../docfx/includes/DISCLAIMER.md)]
