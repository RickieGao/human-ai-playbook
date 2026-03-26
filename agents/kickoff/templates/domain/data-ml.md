## Domain: Data / ML

### Data Handling
- Never modify raw/source data — treat it as immutable, write outputs to separate directories
- Large data files (datasets, models) must not be committed to git — use `.gitignore` and document where data lives
- Document data sources, formats, and any preprocessing steps in the project README or a dedicated `data/README.md`

### Notebooks & Scripts
- Notebooks are for exploration and visualization — production logic belongs in `.py` modules
- If a notebook produces a reusable result, extract the logic into a function with tests
- Clear all notebook outputs before committing (use pre-commit hook or `nbstripout`)

### Reproducibility
- Pin all dependency versions (exact versions in requirements.txt or lock file)
- Set random seeds explicitly when results must be reproducible
- Log experiment parameters and results — don't rely on memory or notebook state

### Model Management
- Save model artifacts with version identifiers, not overwriting a single file
- Document model inputs, outputs, and expected performance metrics
- Never deploy a model without evaluation on a held-out test set

### Environment
- Use virtual environments — never install into system Python
- Document the full setup process (Python version, GPU requirements, env vars)
- Keep training scripts and inference scripts separate — different concerns, different entry points
