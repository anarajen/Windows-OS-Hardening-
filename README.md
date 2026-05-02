.DESCRIPTION
    This script aims to harden Windows Server 2019 VM baseline policies using Desired State Configurations (DSC) for CIS Benchmark Windows Server 2019 Version 1.0.0 supported by ZCSPM.
.NOTE
    Copyright (c) ZCSPM. All rights reserved.
    Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is  furnished to do so, subject to the following conditions:
    The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
    # PREREQUISITE
    * Windows PowerShell version 5 and above
        1. To check PowerShell version type "$PSVersionTable.PSVersion" in PowerShell and you will find PowerShell version,
        2. To Install powershell follow link https://docs.microsoft.com/en-us/powershell/scripting/install/installing-windows-powershell?view=powershell-6
    * DSC modules should be installed
        1. AuditPolicyDsc
        2. SecurityPolicyDsc
        3. NetworkingDsc
        4. PSDesiredStateConfiguration
        
        To check Azure AD version type "Get-InstalledModule -Name <ModuleName>" in PowerShell window
        You can Install the required modules by executing below command.
            Install-Module -Name <ModuleName> -MinimumVersion <Version>
.EXAMPLE
    
    .\CIS_Benchmark_WindowsServer2019_v100.ps1 [Script will generate MOF files in directory]
    Start-DscConfiguration -Path .\CIS_Benchmark_WindowsServer2019_v100  -Force -Verbose -Wait
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
# Windows Server 2019 CIS Hardening – Prerequisites and Execution

This document describes the prerequisites and execution steps for applying **CIS Benchmark Windows Server 2019 v1.0.0** hardening using **Desired State Configuration (DSC)**.

## Description

The hardening script applies baseline security policies aligned with the CIS benchmark for Windows Server 2019. It uses PowerShell DSC to generate and apply configuration files (MOF files) to the target virtual machine.

## Prerequisites

### Requirements

- Windows Server 2019
- Windows PowerShell 5.0 or later
- Administrator privileges
- Internet access to install required PowerShell modules from PSGallery

### Verify PowerShell Version

Open **Windows PowerShell as Administrator** and run:


# Verify PowerShell version
$PSVersionTable.PSVersion

# Configure PowerShell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
Set-PSRepository -Name PSGallery -InstallationPolicy Trusted

# Install required modules
Install-Module -Name AuditPolicyDsc -Force
Install-Module -Name SecurityPolicyDsc -Force
Install-Module -Name NetworkingDsc -Force
Install-Module -Name PSDesiredStateConfiguration -Force

# Verify installed modules
Get-InstalledModule AuditPolicyDsc
Get-InstalledModule SecurityPolicyDsc
Get-InstalledModule NetworkingDsc
Get-InstalledModule PSDesiredStateConfiguration

# Navigate to script location
cd C:\Hardening

# Generate MOF files
.\CIS_Benchmark_WindowsServer2019_v100.ps1

# Apply DSC configuration
Start-DscConfiguration -Path .\CIS_Benchmark_WindowsServer2019_v100 -Force -Verbose -Wait

# Verify status
Get-DscConfigurationStatus

# View applied configuration
Get-DscConfiguration


