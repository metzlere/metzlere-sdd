# Context

Data scientist specializing in cybersecurity analytics. Intermediate Python with OOP understanding, not a software engineer. Writing code for data scientists and analysts - no external users, focused on building analytics and internal tools.

# Core Principles

- **Simplicity First**: Intuitive code over clever solutions
- **Readability**: Colleagues should understand the implementation, not just the interface
- **Modular & Extensible**: Design for adaptation without over-engineering
- **Minimal Testing**: Integration tests on pipelines to catch breakage; nothing more

# Project Organization

- `src/` — Source code (subdirectories only when complexity warrants it)
- `scripts/` — Entry points and orchestration (imports from `src/`)
- `config/config.yaml` — Parameters, thresholds, paths
- `.env` — Secrets (never committed)
- `src/config.py` — Loads config and environment variables

```python
"""Configuration management."""
import os
from pathlib import Path
import yaml
from dotenv import load_dotenv

load_dotenv()

PROJECT_ROOT = Path(__file__).parent.parent

def load_config() -> dict:
    """Load configuration from YAML file."""
    with open(PROJECT_ROOT / "config" / "config.yaml") as f:
        return yaml.safe_load(f)

API_KEY = os.getenv("API_KEY")
```

# Code Standards

NumPy-style docstrings with type hints on public functions:

```python
def process_events(events: pd.DataFrame, threshold: float = 0.8) -> pd.DataFrame:
    """
    Filter security events by threat score.
    
    Parameters
    ----------
    events : pd.DataFrame
        Raw events with columns: timestamp, ip, threat_score
    threshold : float, default=0.8
        Minimum threat score
        
    Returns
    -------
    pd.DataFrame
        Filtered events exceeding threshold
    """
```

Naming: `snake_case` for files/functions/variables, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants.

# Testing

Integration tests only. One test per major pipeline: feed sample input, assert output has expected shape and type. Add regression tests when something breaks. Use pytest.

# Dependencies

`requirements.txt` with pinned major versions:

```
pandas>=2.0.0,<3.0.0
scikit-learn>=1.3.0,<2.0.0
pytest>=7.4.0,<8.0.0
```
```