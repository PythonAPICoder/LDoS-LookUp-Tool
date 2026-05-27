# LDoS Lookup Snippet Tool

The **LDoS Lookup Snippet Tool** is a Python automation tool for Cisco lifecycle and migration analysis using authorized public-facing support APIs that help teams review Cisco product lifecycle data by querying Cisco Support Tools APIs and generating a structured migration report.

This tool is designed to reduce manual effort when reviewing large Product ID lists for lifecycle status, Last Date of Support information, documentation links, and recommended migration products.

See https://developer.cisco.com/docs/support-apis/ for more info on Cisco Support Tools APIs

---

## Disclaimer

The LDoS Lookup Tool is an independent automation solution and is not an officially supported Cisco product.

Users are responsible for:

* API credential management
* Compliance with Cisco API policies
* Responsible rate limit usage
* Internal governance
* Operational validation

---

## Overview

Managing product lifecycle migrations can be time-consuming, especially when working with large inventories approaching **Last Date of Support (LDoS)**.

Manually reviewing each Product ID, checking lifecycle notices, following documentation links, and identifying migration products can be inefficient and error-prone.

The LDoS Lookup Snippet automates this process by using Cisco Support Tools APIs and a Python script to:

- Ingest a list of Cisco Product IDs
- Query official lifecycle / EoX data by Product ID
- Return key lifecycle dates
- Provide documentation links
- Identify migration product information when available
- Generate a structured CSV report

The final output is a clear and actionable report that can support account teams, partner teams, customer success teams, and leadership planning.

---

## Benefits

- Automates lifecycle and migration lookups
- Reduces manual research time
- Improves accuracy by using authoritative Cisco API data
- Supports inclusion and exclusion filters
- Enables repeatable reporting
- Produces a structured CSV output
- Helps prioritize lifecycle migration planning

---

## Requirements

### API Access

Cisco Support Tools API access with permission to use the following endpoint:

```text
EoXByProductID
````

### Python

Python 3.x is required.

### Python Libraries

Install the required Python libraries:

```bash
pip install pandas requests
```

### Source Data

The tool can use an Excel source file named:

```text
pid_source.xlsx
```

The file should contain a single column named:

```text
Product
```

The Product ID list can be:

* Manually created in Excel
* Exported from internal systems
* Derived from Cisco’s Global Price List
* Omitted entirely if using `include_patterns` and `exclude_patterns` from `config.ini`

---

## Setup

Place the script in its own folder.

Optional source file:

```text
pid_source.xlsx
```

Expected folder example:

```text
LDoS-Lookup/
├── ldos_lookup.py
├── pid_source.xlsx
└── config.ini
```

On the first run, the script will automatically create a default `config.ini` file and then exit.

Open `config.ini`, update the required settings, and then run the script again.

---

## Configuration

Edit the generated `config.ini` file.

### Secrets

```ini
[secrets]
client_id = <your_client_id>
client_secret = <your_client_secret>
```

### API Settings

```ini
[api]
token_url = https://id.cisco.com/oauth2/default/v1/token
endpoint_url = https://apix.cisco.com/supporttools/eox/rest/5/EOXByProductID/1/
```

### Filters

Use include and exclude patterns to control which Product IDs are processed.

```ini
include_patterns = C92*, C93*
exclude_patterns =
```

Rules:

* `include_patterns` is applied first
* `exclude_patterns` is applied after include filtering
* Wildcard prefixes are supported
* If no `pid_source.xlsx` file is supplied, the tool can use `include_patterns` and `exclude_patterns` as the source list

---

## Usage

### First Run

```bash
python ldos_lookup.py
```

The first run creates:

```text
config.ini
```

Update the configuration file with your API credentials and desired filters.

### Run Lookup

```bash
python ldos_lookup.py
```

The script will:

1. Authenticate to the Cisco API
2. Read Product IDs from `pid_source.xlsx` or configured patterns
3. Query lifecycle data using the EoXByProductID endpoint
4. Apply include and exclude filters
5. Generate the output report

---

## Output

The tool generates:

```text
Product_Migration.csv
```

This report includes lifecycle and migration information for the processed Product IDs.

---

## Example Workflow

1. Create or export a Product ID list
2. Save it as `pid_source.xlsx`
3. Ensure the column name is `Product`
4. Run the script once to generate `config.ini`
5. Update API credentials and filters
6. Run the script again
7. Review `Product_Migration.csv`

---

## Use Cases

* Product lifecycle reviews
* LDoS migration planning
* Partner enablement
* Customer success reporting
* Account team planning
* Large inventory lifecycle analysis
* Cisco product migration research

---


## Author

**Steve Hartman**

Python Automation Developer
Enterprise Workflow Automation
Cisco API Automation

GitHub: [https://github.com/PythonAPICoder](https://github.com/PythonAPICoder)

---

## Disclaimer

This is not an officially supported Cisco product.
