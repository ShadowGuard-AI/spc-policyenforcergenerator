# spc-PolicyEnforcerGenerator
A script to generate basic enforcement scripts (bash or Python) from a high-level policy document. It parses the policy document using PyYAML or the JSON standard library, identifies key rules, and translates them into commands to verify configurations and enforce compliance. Scripts are built by string construction in the code; no templating library is used.

Each rule value must be a mapping whose values are strings, with at least one `check` or `enforce` value. A policy with no rules, a rule with no check or enforce value, or a rule that is not a mapping is a validation error: the tool exits non-zero and writes no script.

In generated Python, check and enforce values and rule names are emitted with repr quoting, so operator text stays inside one string literal and cannot become extra statements. In comments in both output types, descriptions and rule names are labels: newlines in them are flattened so they stay on their comment line. The check and enforce values copied into bash are the commands the operator wrote, which is the documented purpose of a bash enforcement script. Generated scripts are written with mode 644 by default, not executable.

## Install
`git clone https://github.com/ShadowGuard-AI/spc-policyenforcergenerator`

## Usage
`python3 main.py POLICY_FILE [-o OUTPUT_FILE] [-s bash|python] [-l LEVEL] [-v SCHEMA_FILE]`

## Parameters
- `policy_file`: Path to the policy file (YAML or JSON).
- `-h`: Show help message and exit
- `--output_file`: Path to the output enforcement script.
- `--script_type`: Type of script to generate.
- `--log_level`: Set the logging level.
- `--validate_schema`: Path to JSON schema file for policy validation.

## License
MIT License. See LICENSE.
