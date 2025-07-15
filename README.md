# nv2cmd - NVUE YAML to NV Commands Converter

**Product:** nv2cmd  
**Author:** Josh Finlay <josh@athenanetworks.com.au>  
**Repository:** https://github.com/AthenaNetworks/cumulus-nv2cmd

A Python script that converts Cumulus Linux NVUE configuration YAML to equivalent `nv` command sets for Cumulus Linux 5+.

## Overview

This script:
1. Executes `nv config show` to get the current NVUE configuration in YAML format
2. Parses the YAML output
3. Converts it into equivalent `nv set` commands that can be used to recreate the configuration

## Requirements

- Cumulus Linux 5+ with NVUE CLI (`nv` command)
- Python 3.6+
- PyYAML library

## Installation

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Make the script executable:
```bash
chmod +x nv2cmd
```

## Usage

Run the script on a Cumulus Linux switch:

```bash
python3 nv2cmd
```

Or directly:
```bash
./nv2cmd
```

The script will:
1. Fetch the current configuration using `nv config show`
2. Convert it to `nv set` commands
3. Output the commands to stdout

## Output

The script generates `nv set` commands that can be used to recreate the current configuration. Example output:

```bash
# Generated NVUE Commands
# Run these commands to recreate the current configuration

nv set interface swp1 ip ipv4 address 192.168.1.1/24
nv set interface swp1 bridge domain br_default
nv set system hostname switch01
nv set service ssh enable on

# Total commands: 4
```

## Features

- Handles nested YAML configurations
- Special processing for interface configurations
- Supports common NVUE configuration sections (system, service, router, vrf, interface)
- Generates clean, executable `nv set` commands

## Limitations

- Complex configurations may require manual review
- Some advanced NVUE features might need custom handling
- Always test generated commands in a lab environment first

## Error Handling

The script includes error handling for:
- Missing `nv` command
- YAML parsing errors
- Command execution failures
