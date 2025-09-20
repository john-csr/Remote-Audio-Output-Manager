# Remote-Audio-Output-Manager


Audio Output Manager is a lightweight HTA (HTML Application) tool designed to remotely manage audio playback devices on Windows machines using PowerShell and the `AudioDeviceCmdlets` module.

## Features

- Install the `AudioDeviceCmdlets` module remotely
- Verify module installation on a target machine
- List available playback devices
- Set a specific playback device as the default

## Requirements

- Windows operating system with HTA support
- PowerShell remoting enabled (`Enable-PSRemoting`)
- Administrator privileges on the target machine
- Network access to the remote machine

## Usage

1. **Launch the HTA file**  
   Double-click the `.hta` file to open the Audio Output Manager interface.

2. **Enter the remote computer name**  
   Fill in the `Computer Name` field with the target machine's name.

3. **Install Module**  
   Click `Install Module` to install `AudioDeviceCmdlets` remotely.

4. **Verify Module**  
   Click `Verify Module` to check if the module is installed.

5. **List Playback Devices**  
   Click `List Playback Devices` to retrieve all playback devices from the remote system.

6. **Set Default Device**  
   Enter the desired device name in the `Device Name` field and click `Set Default Device`.

## PowerShell Commands Used

- **Install Module**
  ```powershell
  Install-PackageProvider -Name NuGet -Force
  Install-Module -Name AudioDeviceCmdlets -Force -Scope AllUsers
  ```

- **Verify Module**
  ```powershell
  Get-Module -ListAvailable | Where-Object { $_.Name -eq 'AudioDeviceCmdlets' }
  ```

- **List Playback Devices**
  ```powershell
  Get-AudioDevice -List | Where-Object { $_.Type -eq 'Playback' }
  ```

- **Set Default Device**
  ```powershell
  Import-Module AudioDeviceCmdlets
  $device = Get-AudioDevice -List | Where-Object { $_.Name -eq '<DeviceName>' -and $_.Type -eq 'Playback' }
  Set-AudioDevice -Index $device.Index
  ```

## Notes

- The tool uses VBScript to execute PowerShell commands via `WScript.Shell`.
- Output from each operation is displayed in the `Output` text area.
- Ensure firewall rules and network permissions allow remote PowerShell execution.

## Author

John C.

