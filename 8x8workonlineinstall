$ErrorActionPreference="SilentlyContinue"
Stop-Transcript | out-null
$ErrorActionPreference = "Continue"
Start-Transcript -path C:\IntuneLogs\8X8Install.txt -Force
# URL of the file to download
$url = "https://work-desktop-assets.8x8.com/prod-publish/ga/work-64-msi-v8.21.3-1.msi"
# Local path to save the downloaded file
$outputFile = "$env:TEMP\work-64-msi-v8.20.2-12.msi"
# Download the file
try {
    Write-Host "Downloading $url to $outputFile..."
    Invoke-WebRequest -Uri $url -OutFile $outputFile -ErrorAction Stop
    Write-Host "Download complete."
    }
catch {
    Write-Error "Error downloading file: $($_.Exception.Message)"
    exit 1
    }
# Run the downloaded MSI
try {
    Write-Host "Running installer..."
    Start-Process -FilePath "msiexec.exe" -ArgumentList "/i", "`"$outputFile`"", "/qn", "/norestart" -Wait -ErrorAction Stop
    Write-Host "Installation complete."
    }
catch {
    Write-Error "Error running installer: $($_.Exception.Message)"
    exit 1
    }
#Optional: Remove the downloaded file after installation.
try {
    Remove-Item $outputFile -ErrorAction Stop
    Write-Host "Temporary file removed."
    }
catch{
    Write-Warning "Failed to remove temporary file: $($_.Exception.Message)"
    }
exit 0 #Indicate success
Write-Output "work-64-msi-v8.21.3-1.msi successfully installed."
Stop-Transcript
