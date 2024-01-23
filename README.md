# CloudNativeQuickStart

**Intended Use Case:** Baseline configuration policy for an AADJ/Entra ID-Joined (Cloud Native) workstations: https://aka.ms/CloudNativeDevices

**Included Policy:**
- Autopilot Profile
- Compliance Policies
- Device Configuration
- Driver Update Profiles
- Endpoint Security
- Enrollment Status Page
- Settings Catalog
- Update Policies

_**Note: All Policies should show up in Devices > Configuration Profiles, except for:**_
  - Autopilot ESP / Deployment Profiles
  -	AV, Firewall, ASR Rules, Bitlocker Encryption
  - Windows Hello for Business (Config & Settings)
  - Windows LAPS
  - Driver Policies

**Policy Notes**
| Policy      | Definition |
| ----------- | ----------- |
| Device Security - D - Login and Lock Screen      | Note: Set your own Preferred AAD Tenant Domain Name       |
| Device Security - U - Device Guard, Credential Guard and HVCI   | NOTE: Applying this policy to Devices will cause a reboot between Device and User ESP phases.        |
| Windows Hello for Business - U - WHfB Configuration_Settings | This will set Global Windows  Hello For Business Configuration Settings as described [here](https://learn.microsoft.com/en-us/mem/intune/protect/windows-hello) |
| Google Chrome - U - Profiles, Sign-In and Sync | Note: Set your own browser primary account Domain Name |
| Microsoft OneDrive - D - Configuration | Note: Set your own Tenant ID for syncing AND silent move (should happen automatically) |
| Microsoft OneDrive - U - Configuration | Note: Set your own Tenant ID for OD location setting (should happen automatically) |
| Windows Hello for Business - D - Cloud Kerberos Trust | Note: Requres [Cloud Kerberos Trust](https://learn.microsoft.com/en-us/windows/security/identity-protection/hello-for-business/deploy/hybrid-cloud-kerberos-trust) be deployed |
| WUfB - D - Delivery Optimization | Note: If you will not be using Microsoft Connected Cache(s) you can delete the Cache Server Fallback Foreground and Background settings |
| WUfB - D - Temporary Enterprise Feature Control | Note: Optional policy. Read [here](https://learn.microsoft.com/en-us/windows/whats-new/temporary-enterprise-feature-control). |
| WUfB - D - Updates - Ring 0.1 - Dev | Note: Use for testing purposes |
| WUfB - D - Updates - Ring 0.2 - Beta | Note: Use for testing purposes |
| WUfB - D - Updates - Ring 0.3 - Insider Preview | Note: Use for testing purposes (recommended) |
| Attack Surface Reduction - D - ASR Rules (Audit Mode) | Recommended ASR rules set to Audit by default. Enable to your preference.  |

**Importing:**
- The baseline was exported using the tool developed by Mikael Karlsson (GitHub and Twitter), and can be imported in the same way.
- Should just be able to run start.cmd in the IntuneManagement-master folder

**Assignment:**


**Limitations:** 
-	AppLocker configuration was excluded due to wide variance between environments. Apps that do not require elevation or install to a user's AppData folder may not be blocked.

**Post Import Actions:**
-	Importing Tool should replace your Tenant ID in all applicable policies. However, you will need to set your own preferred AAD tenant domain name in _Device Security - D - Login and Lock Screen_
-	Assign Policies
    -	D: Recommended to assign to Devices
    - U: Recommended to assign to users
-	[Set enrollment restrictions to allow Intune enrollment](https://learn.microsoft.com/en-us/mem/intune/enrollment/enrollment-restrictions-set)
-	[Import Autopilot Devices](https://learn.microsoft.com/en-us/autopilot/add-devices)
-	[Deploy a Target Feature Update for Windows 10 and Later policy](https://learn.microsoft.com/en-us/mem/intune/protect/windows-10-feature-updates)
    -	_Note: without targetting an Feature Update, devices will go straight to their Latest Supported Feature Update according to the configured Feature Update deferral in their Update Rings for Windows 10 and later policy_ 

**Supporting Configurations:**
- [Configure WHFB Cloud Kerberos Trust](https://learn.microsoft.com/en-us/windows/security/identity-protection/hello-for-business/deploy/hybrid-cloud-kerberos-trust)
- [Enable WUFB Reports](https://learn.microsoft.com/en-us/windows/deployment/update/wufb-reports-enable)
- [Configure M365 Servicing Profiles / M365 Cloud Policy](https://learn.microsoft.com/en-gb/deployoffice/admincenter/servicing-profile)
- [Configure MDE Onboarding in Intune](https://learn.microsoft.com/en-us/mem/intune/protect/advanced-threat-protection-configure)
- [Enable Windows LAPS in Entra Device Settings](https://learn.microsoft.com/en-us/windows-server/identity/laps/laps-scenarios-azure-active-directory)

**Credit**
- Credit to [SkipToTheEndpoint](https://github.com/SkipToTheEndpoint), who's [OpenIntuneBaseline](https://github.com/SkipToTheEndpoint/OpenIntuneBaseline?tab=readme-ov-file) project was the jumping off point and is used as reference for a majority of the security policies.


