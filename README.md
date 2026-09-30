# LMU Telemetry Analytics

Local-first analytics project based on Le Mans Ultimate (LMU) telemetry. The goal is
to turn real sessions into reproducible analyses that help drivers understand where
they gain or lose time.

## Initial stack

- Python 3.12 with `venv`, `pip`, and `requirements.txt`.
- LMU's native DuckDB session files as the provisional source data.
- DuckDB and SQL for local analytical processing.
- dbt-duckdb for analytical models.
- pytest and Ruff for tests and Python code quality.

The future user interface is intentionally undecided. Airflow, Spark, Databricks,
cloud infrastructure, and CI/CD will be introduced only when the project or a
specific learning activity justifies them.

## Repository layout

```text
ai_context/       Project decisions, discovery, technical debt, and handoff notes
data/
  raw/            Local, unmodified source sessions (not tracked by Git)
  processed/      Local generated analytical data (not tracked by Git)
dbt_project.yml   dbt project configuration at repository root
models/
  staging/
  intermediate/
  marts/
src/lmu_telemetry/
tests/
  unit/
  integration/
  dbt/            dbt singular data tests
```

The native session files are read-only inputs. Do not commit telemetry or generated
local databases. Run dbt commands from the repository root. dbt's local profile
belongs in the user's `~/.dbt/profiles.yml`, not in this repository.

## Local setup

On Debian/Ubuntu, install the Python virtual-environment package if `python3 -m venv`
is unavailable:

```bash
sudo apt install python3.12-venv
```

Create and activate the local environment, then install the pinned dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Create `~/.dbt/profiles.yml` outside the repository and point it to a local ignored
DuckDB file:

```yaml
lmu_telemetry_analytics:
  target: dev
  outputs:
    dev:
      type: duckdb
      path: /absolute/path/to/lmu-telemetry-analytics/data/local/lmu_telemetry.duckdb
      threads: 4
```

Validate the project and local database connection:

```bash
dbt debug
dbt parse
```
