# dns-suffix-retierve-script
PowerShell Script to retierive DNS suffixes list from the host regisetery and ask the users if they want to delete them.

$registryPath = "HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters"
$registryKey = Get-Item -Path $registryPath

$registryValue = Get-ItemProperty -Path $registryKey.PSPath

Write-Output $registryValue

# Check if user wants to delete Domain key value
$deleteDomain = Read-Host -Prompt "Do you want to delete the Domain key value? (Y/N)"
if ($deleteDomain -eq "Y") {
    Remove-ItemProperty -Path $registryKey.PSPath -Name "Domain"
}

# Check if user wants to delete NV Domain key value
$deleteNVDomain = Read-Host -Prompt "Do you want to delete the NV Domain key value? (Y/N)"
if ($deleteNVDomain -eq "Y") {
    Remove-ItemProperty -Path $registryKey.PSPath -Name "NV Domain"
}

# Check if user wants to delete SearchList key value
$deleteSearchList = Read-Host -Prompt "Do you want to delete the SearchList key value? (Y/N)"
if ($deleteSearchList -eq "Y") {
    Remove-ItemProperty -Path $registryKey.PSPath -Name "SearchList"
}
