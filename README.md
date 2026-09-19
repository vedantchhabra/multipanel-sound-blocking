# Multipanel Sound Blocking

A Dataiku DSS project for analyzing and modeling sound insulation in multilayer panels. The project combines simulated acoustic and material-property data with exploratory analysis and regression models to study transmission loss and predict sound-blocking performance.

## Project goals

- Explore transmission-loss behavior across multilayer panel configurations.
- Prepare simulation data with derived material and construction features.
- Compare machine-learning models for acoustic-performance prediction.
- Analyze targets including transmission loss, OITC rating, and related sound-blocking metrics.
- Provide reusable Dataiku datasets, recipes, analyses, and dashboards.

## Repository structure

| Path | Description |
| --- | --- |
| [`datasets/`](datasets/) | Input and prepared simulation datasets, including transmission-loss, STL, and OITC data. |
| [`recipes/`](recipes/) | Dataiku recipe exports. The OITC preparation recipe derives `Total_Thickness_mm` and `Average_Density`. |
| [`analysis/`](analysis/) | Dataiku analyses and machine-learning configurations for regression and feature-processing experiments. |
| [`model_comparisons/`](model_comparisons/) | Exported model-comparison configurations and results. |
| [`explore/`](explore/) | Exploration and visualization configurations for transmission loss and OITC simulation data. |
| [`dashboards/`](dashboards/) | Exported dashboard definitions. |
| [`lib/`](lib/) | Project library and external-library configuration. |
| `params.json` | Dataiku project metadata and project settings. |
| `tags.json` | Dataiku project tags. |
| `apikeys.json` | Local/API-key configuration; treat this file as sensitive and do not publish credentials. |

## Data and modeling workflow

1. Load the simulation datasets from [`datasets/`](datasets/).
2. Use the recipes in [`recipes/`](recipes/) to prepare modeling features. The OITC preparation flow creates:
   - `Total_Thickness_mm`: the sum of the three panel and three absorber thicknesses.
   - `Average_Density`: total basis weight normalized by total thickness.
3. Explore relationships among panel properties, absorber properties, frequency, transmission loss, and OITC ratings using the configurations in [`explore/`](explore/).
4. Run the regression analyses in [`analysis/`](analysis/) to predict acoustic targets such as `Transmission_Loss` and `Sp_OITC_Rating`.
5. Review model comparisons and visual summaries in [`model_comparisons/`](model_comparisons/) and [`dashboards/`](dashboards/).

## Requirements

- A Dataiku DSS instance compatible with the exported project configuration.
- Access to the project’s configured data connections or local dataset files.
- A configured Python environment if Python-based analysis or recipes are enabled.
- Spark/Hive/Impala access only if the corresponding distributed execution settings are used.

The repository is primarily a versioned export of a Dataiku DSS project rather than a standalone Python package, so there is no single `pip install` or application start command.

## Getting started with Dataiku DSS

1. Clone or download this repository.
2. In Dataiku DSS, create a new project or open an existing project intended for import.
3. Import the project configuration and associated objects from the repository, or use the repository as the project’s Git-backed source where appropriate.
4. Configure the required connections, code environments, and dataset locations for your DSS installation.
5. Review and update dataset inputs in the Flow before running recipes.
6. Run the preparation recipe, then rebuild the analyses and dashboards.
7. Validate generated metrics and model outputs against your data source and execution environment.

The exact import steps depend on your Dataiku DSS version and deployment configuration. Do not assume that repository paths alone provide access to the original DSS connections or managed datasets.

## Important security note

Review [`apikeys.json`](apikeys.json) before sharing or publishing this repository. API keys, tokens, passwords, and connection secrets should never be committed. Rotate any credential that may have been exposed and replace secrets with environment variables or DSS-managed credentials.

## Reproducibility notes

- The project metadata records the project name as **STL simulation**.
- Model configurations include regression experiments with acoustic targets and material/property features.
- Some analyses and recipes depend on Dataiku-managed datasets, connections, engines, and code environments that are not fully represented by the files in this repository.
- Re-run preparation and modeling steps after changing input datasets or DSS configuration.

## License

No license is currently specified. Until a license is added, all rights remain with the repository owner and reuse should be treated as unauthorized unless permission is granted.

## Contributing

For changes:

1. Create a branch for the update.
2. Keep Dataiku exports and documentation synchronized.
3. Remove credentials and other sensitive values before committing.
4. Describe any changes to datasets, recipes, model settings, or required DSS configuration in the pull request.
