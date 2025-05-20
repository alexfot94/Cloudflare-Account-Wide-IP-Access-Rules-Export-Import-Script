Cloudflare Account-Wide IP Access Rules Export & Import Scripts
Overview

This repository provides two PowerShell scripts for managing Cloudflare account-level IP Access Rules (firewall rules):

    Export Script: Retrieves and saves existing IP Access Rules to a JSON file.

    Import Script: Reads a JSON file of IP Access Rules and applies them to your Cloudflare account.

These tools are useful for backup, audit, replication, or migration of security rules between Cloudflare accounts or environments.
Technologies Used

    PowerShell: Scripting language for automation (compatible with Windows PowerShell 5.1+ and PowerShell Core).

    Cloudflare API v4: REST API to manage firewall access rules at the account level.

    JSON Processing: PowerShell’s ConvertTo-Json and ConvertFrom-Json cmdlets are used for data formatting.

Scripts Included
1. Export-Cloudflare-IP-Rules.ps1

This script exports all account-level IP Access Rules to a JSON file.

Key Features:

    Handles paginated results from the Cloudflare API.

    Retries on API rate limits (HTTP 429).

    Logs successful IPs and failed page requests.

    Outputs:

        account_ip_access_rules.json: The complete set of exported rules.

        account_export_success_summary.txt: Successfully retrieved IPs.

        account_export_failed_summary.txt: List of failed pages with error details.

2. Import-Cloudflare-IP-Rules.ps1

This script imports IP Access Rules from a previously exported JSON file back into a Cloudflare account.

Key Features:

    Avoids re-importing IPs that are already applied (tracked via a local log).

    Retries on API rate limits.

    Logs successful and failed imports.

    Outputs:

        imported_ips.log: Tracks which IPs have already been imported.

        import_success_summary.txt: Successfully imported IPs.

        import_failed_summary.txt: Failed imports with error messages.

Setup Instructions
Prerequisites

    PowerShell 5.1+ on Windows or PowerShell Core on macOS/Linux.

    Active Cloudflare account.

    Cloudflare Global API Key and associated email address.

Configuration

Both scripts require the following header configuration to authenticate with the Cloudflare API:

$headers = @{
    "X-Auth-Email" = "your-email@example.com"
    "X-Auth-Key"   = "your-global-api-key"
    "Content-Type" = "application/json"
}

Replace the placeholders with your actual Cloudflare credentials.
Usage
Exporting Rules

    Open PowerShell.

    Run Export-Cloudflare-IP-Rules.ps1.

    The following files will be created on your Desktop:

        account_ip_access_rules.json

        account_export_success_summary.txt

        account_export_failed_summary.txt

Importing Rules

    Ensure zone_ip_access_rules.json is present on your Desktop. This can be renamed from the export output if needed.

    Run Import-Cloudflare-IP-Rules.ps1.

    The following files will be updated/created:

        imported_ips.log

        import_success_summary.txt

        import_failed_summary.txt

Security Notice

    Do not hardcode or commit your API credentials in version-controlled files.

    Consider using environment variables or a secure secrets manager for production environments.

    Your Global API Key has full access to your Cloudflare account and must be protected accordingly.

License

This project is released under the MIT License. You are free to use, modify, and distribute it with attribution.
