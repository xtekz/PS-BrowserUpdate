# PS-Scripts
#General PowerShell Scripts

#Google Chrome uses the Google Update service (also known as Omaha) to manage updates. We can use the Google Update's command line tool to force an update check.

#Here's a simple PowerShell script to force Google Chrome to check for updates:

# Check if Google Update is installed
if (Test-Path "HKLM:\SOFTWARE\WOW6432Node\Google\Update") {
    # Get the Google Update installation path
    $googleUpdatePath = Get-ItemPropertyValue -Path "HKLM:\SOFTWARE\WOW6432Node\Google\Update" -Name "UpdateDefault"
    
    #Check if the Google Update executable exists
    if (Test-Path "$googleUpdatePath\GoogleUpdate.exe") {
        # Run Google Update with the "/ua" flag to force update check
        & "$googleUpdatePath\GoogleUpdate.exe" /ua /tag
        Write-Host "Google Chrome update check initiated."
    } else {
        Write-Host "Google Update executable not found. Please ensure Google Chrome is installed correctly."
    }
} else {
    Write-Host "Google Update not found. Please ensure Google Chrome is installed on this machine."
}


#Microsoft Edge is updated through Windows Update, so to force Microsoft Edge to check for updates, you'll need to trigger a check for Windows updates. Here's a #PowerShell script to do that:

# Check if the Windows Update Agent is available on the system

if (Get-Command -Name "Get-WindowsUpdate" -ErrorAction SilentlyContinue) {
    # Run the Windows Update Agent with the EdgeUpdate parameter to check for updates
    Get-WindowsUpdate -MicrosoftProductName "EdgeUpdate" -Install
    Write-Host "Microsoft Edge update check initiated."
} else {
    Write-Host "The Windows Update Agent is not available on this system. Please ensure you have the required module installed."
}
Before you run this script, you need to install the PSWindowsUpdate module, which provides the Get-WindowsUpdate command. You can install it by running the following command in an elevated PowerShell session:

powershell
Copy code
Install-Module -Name PSWindowsUpdate
