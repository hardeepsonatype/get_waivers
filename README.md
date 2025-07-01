# Sonatype IQ Policy Waiver Extractor

This Python script connects to a Sonatype IQ Server instance using its REST API to extract all policy waivers. It systematically fetches waivers applied at both the **organization** and **application** levels and consolidates them into a single JSON file.

## Description

The script is designed to provide a complete audit of all policy waivers within a Sonatype IQ Server. It performs the following actions:

1. Authenticates to the Sonatype IQ Server using the provided credentials.
2. Fetches a list of all configured organizations.
3. Iterates through each organization (including the `ROOT_ORGANIZATION_ID`) and requests any associated policy waivers.
4. Fetches a list of all configured applications.
5. Iterates through each application and requests its associated policy waivers.
6. Aggregates all collected waivers into a single list.
7. Saves the complete list of waivers to a JSON file named `all_policy_waivers.json`.

## Prerequisites

* Python 3.x
* The `requests` library for Python.

You can install the necessary library using pip:
```bash
pip install requests
```

## Usage

The script is executed from the command line and requires the Sonatype IQ Server URL and user credentials to be passed as arguments.

### Command-Line Arguments

* `-u` or `--url`: **(Required)** The full base URL of your Sonatype IQ Server (e.g., `http://localhost:8070`).
* `-a` or `--user`: **(Required)** The username for a user with sufficient permissions to access the API endpoints.
* `-p` or `--password`: **(Required)** The password for the specified user.

### Example

```bash
python get_waivers.py --url http://your-sonatype-server:8070 --user your_username --password your_password
```

Replace the placeholder values with your actual server URL and credentials.

## Output

The script will generate a file named `all_policy_waivers.json` in the same directory where the script is run. This file contains a JSON array of all the policy waiver objects found on the server.

### Example JSON Output Structure

```json
[
    {
        "policyWaiverId": "c4fd6c26cbf754873c2536ff6fd1e6bf",
        "comment": "",
        "createTime": "2025-06-30T15:03:27.756+0000",
        "scopeOwnerType": "root_organization",
        "scopeOwnerId": "ROOT_ORGANIZATION_ID",
        "scopeOwnerName": "Root Organization",
        "hash": "40f8048097cceacdb11d",
        "policyId": "6f7980f861194016a6de7e5a0d526d0e",
        "vulnerabilityId": "sonatype-2015-0002",
        "creatorId": "admin",
        "creatorName": "Admin Builtin",
        "matcherStrategy": "EXACT_COMPONENT",
        "associatedPackageUrl": "pkg:maven/commons-collections/commons-collections@3.1?type=jar",
        "componentIdentifier": {
            "format": "maven",
            "coordinates": {
                "artifactId": "commons-collections",
                "extension": "jar",
                "groupId": "commons-collections",
                "version": "3.1"
            }
        },
        "reasonText": null,
        "expireWhenRemediationAvailable": false,
        "policyWaiverReasonId": null,
        "displayName": {
            "parts": [
                { "field": "Group", "value": "commons-collections" },
                { "field": "Artifact", "value": "commons-collections" },
                { "field": "Version", "value": "3.1" }
            ]
        },
        "name": "commons-collections"
    },
    {
        "policyWaiverId": "bf52bf375b4063d1bb0b77b2a766",
        "comment": "",
        "createTime": "2025-06-27T13:38:47.972+0000",
        "scopeOwnerType": "application",
        "scopeOwnerId": "d692a13a11964d3795ed76491e9ea312",
        "scopeOwnerName": "java_webgoat2",
        "hash": "feb109788d196a304583",
        "policyId": "6f7980f861194016a6de7e5a0d526d0e",
        "vulnerabilityId": "CVE-2022-23221",
        "creatorId": "admin",
        "creatorName": "Admin Builtin",
        "matcherStrategy": "EXACT_COMPONENT",
        "associatedPackageUrl": "pkg:maven/com.h2database/h2@1.4.187?type=jar",
        "componentIdentifier": {
            "format": "maven",
            "coordinates": {
                "artifactId": "h2",
                "extension": "jar",
                "groupId": "com.h2database",
                "version": "1.4.187"
            }
        },
        "reasonText": null,
        "expireWhenRemediationAvailable": false,
        "policyWaiverReasonId": null,
        "displayName": {
            "parts": [
                { "field": "Group", "value": "com.h2database" },
                { "field": "Artifact", "value": "h2" },
                { "field": "Version", "value": "1.4.187" }
            ]
        },
        "name": "h2"
    }
]
