# Intune Documentation

<img align="right" src="https://github.com/ThomasKur/IntuneDocumentation/raw/master/Logo/IntuneDocumentationLogo.png" width="300px" alt="Automatic Intune Documentation Logo">Automatic Intune Documentation to simplify the life of admins and consultants.

This Script will document:

- Configuration Policies
- Compliance Policies
- Device Enrollment Restrictions
- Terms and Conditions
- Applications (Only Assigned)
- Application Protection Policies
- AutoPilot Configuration
- Enrollment Page Configuration
- Apple Push Certificate
- Apple VPP
- Device Categories
- Exchange Connector
- Application Configuration
- PowerShell Scripts
- ADMX backed Configuration Profiles
- Security Baseline
- Custom Roles

## Usage

Since version 2.0.0 the Automatic Intune Documentation script is available in th PowerShell Gallery and therefore its much simpler to install and use it. You can just use these two commands:

```powershell

Install-Module IntuneDocumentation
Invoke-IntuneDocumentation -FullDocumentationPath c:\temp\IntuneDoc.docx

```

**Important:** Before using the Script the first time, you have to ensure, that you have installed the Microsoft.Graph.Intune and PSWord Module. To do that, you have to start PowerShell as an Adminstrator and install them:

```powershell

Install-Module Microsoft.Graph.Intune
Install-Module PSWord

```

## Additional Options

### UseTranslationBeta

When using this parameter the API names will be translated to the labels used in the Intune Portal.
Note:
These Translations need to be created manually, only a few are translated yet. If you are willing
to support this project. You can do this by [translating the json files](https://github.com/ThomasKur/IntuneDocumentation/blob/master/AddTranslation.md) which are mentioned to you when you generate the documentation in your tenant.

```powershell

Invoke-IntuneDocumentation -FullDocumentationPath c:\temp\IntuneDoc.docx -UseTranslationBeta

```

### Use script silently

In the past I got requests that users would like to execute the Intune Documentation script silently. I have now extended the script by two new option and a new functions which can automatically create the App Registration in Azure AD for you. 

#### Automatically Create App Registration

Your account requires Global Admin privileges to execute these commands and you need to have the AzureAD Module installed.

```powershell

$p = New-IntuneDocumentationAppRegistration
$p | fl

```

The following result will be displayed and can then be used. Safe the ClientSecret in your password vault.

```powershell

ClientID               : d5cf6364-82f7-4024-9ac1-73a9fd2a6ec3
ClientSecret           : S03AESdMlhLQIPYYw/cYtLkGkQS0H49jXh02AS6Ek0U=
ClientSecretExpiration : 21.07.2025 21:39:02
TenantId               : d873f16a-73a2-4ccf-9d36-67b8243ab99a

```

#### Manually Create App Registration

You can follow the manual of Michael Niehaus https://oofhours.com/2019/11/29/app-based-authentication-with-intune/

But select also the following permission scopes:

- 'Policy.Read.All'
- 'Directory.Read.All'
- 'DeviceManagementServiceConfig.Read.All'
- 'DeviceManagementRBAC.Read.All'
- 'DeviceManagementManagedDevices.Read.All'
- 'DeviceManagementConfiguration.Read.All'
- 'DeviceManagementApps.Read.All'
- 'Device.Read.All'

#### Generate Documentation without user interaction

You can now call the Intune Documentation with the new parameters:

```powershell

Invoke-IntuneDocumentation `
    -FullDocumentationPath c:\temp\IntuneDoc.docx `
    -ClientId d5cf6364-82f7-4024-9ac1-73a9fd2a6ec3 `
    -ClientSecret S03AESdMlhLQIPYYw/cYtLkGkQS0H49jXh02AS6Ek0U= `
    -Tenant d873f16a-73a2-4ccf-9d36-67b8243ab99a

```

## Issues / Feedback

For any issues or feedback related to this module, please register for GitHub, and post your inquiry to this project's issue tracker.

## Thanks to

@Microsoftgraph for the PowerShell Examples: <https://github.com/microsoftgraph/powershell-intune-samples>

@guidooliveira for the PSWord Module, which enables the creation of the Word file. <https://github.com/guidooliveira/PSWord>

@joslieben for extending and improving the script

@dads07a for adding Application protection Policies to the documentation

@mirkocolemberg for the help and testing of the script.

![Created by baseVISION](https://www.basevision.ch/wp-content/uploads/2015/12/baseVISION-Logo_RGB.png)
