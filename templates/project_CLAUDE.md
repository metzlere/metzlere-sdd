# Project: [PROJECT_NAME]

## Overview

[2-3 sentences: What problem does this solve? What's the analytical goal?]

## Data

### Sources
| Name | Location | Format | Update Frequency |
|------|----------|--------|------------------|
| [source_name] | [path/connection] | [csv/parquet/API/etc] | [daily/static/etc] |

### Key Fields
- `[field_name]`: [description, any quirks]
- `[field_name]`: [description, any quirks]

### Known Issues
- [Data quality issues, missing values patterns, gotchas]

## Architecture
```
scripts/
    run_pipeline.py      # [what it does]
src/
    ingest.py            # [what it does]
    features.py          # [what it does]
    model.py             # [what it does]
config/
    config.yaml
```

## Pipeline Flow
```
[source] → ingest → [intermediate] → features → [final] → model → [output]
```

## Configuration

Key parameters in `config/config.yaml`:
- `[param]`: [what it controls, valid range]
- `[param]`: [what it controls, valid range]

## Usage
```bash
# [Primary use case]
python scripts/run_pipeline.py

# [Other common commands]
python scripts/[other_script].py --arg value
```

## Current State

- [ ] [Major task/milestone]
- [ ] [Major task/milestone]
- [x] [Completed item]

## Decisions & Context

### [Date or Topic]
[Why we chose X over Y. Context that would be lost otherwise.]

## Domain Notes

[Cybersecurity-specific context: threat models, detection logic rationale, threshold justifications, relevant standards/frameworks]