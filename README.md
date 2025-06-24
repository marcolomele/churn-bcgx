# Churn Prediction – BCG X Data Science Competition

This repository contains the solution developed for a Data Science competition judged by BCG X. The objective was to isolate key drivers of churn and build a predictive model to identify customers at risk of churn.

## Repository Structure
```
churn_bcgx/
├── data/             # Raw and processed datasets
├── inference/        # Scripts for model inference
├── main/             # Main execution scripts
├── modelling/        # Model training, evaluation, and prediction code
├── supplementary/    # Additional resources and documentation
├── .gitignore        # Git ignore file
└── LICENSE           # Project license (Apache 2.0)
```

- **data/**: Contains raw and processed datasets used for training and evaluation.
- **inference/**: Scripts and utilities for running model inference on new data.
- **main/**: Main scripts to execute the pipeline or key project steps.
- **modelling/**: Code for model training, validation, and prediction.
- **supplementary/**: Additional resources, documentation, or supporting materials.

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/marcolomele/churn_bcgx.git
   cd churn_bcgx
   ```
2. Set up a virtual environment and install dependencies using `requirements.txt`.

3. Explore the `main/` directory for entry-point scripts to reproduce results or run the pipeline.

## Data

- The `data/` directory contains all datasets used in the project.

## Modeling

- All model development, training, and evaluation scripts are located in the `modelling/` directory.

## Inference

- The `inference/` directory contains notebooks on inferring churn drivers via data analysis.

## Supplementary Materials

- Additional work using Small Language Model to generate emotional involvement of customers is in the `supplementary/` directory.

## Results

- Identified multiple churn drivers that align with business intuition. The final model achieved strong performance in predicting customer churn.
- See [Churn Modelling Presentation.pdf](churn-modelling-presentation.pdf) for an overview of our methods and the results.
- See [Churn Modelling Report.pdf](churn-modelling-report.pdf) for an in-depth explanation of our methods and the results.

## Contributors

- [@sluque1](https://github.com/sluque1)
- [@marcolomele](https://github.com/marcolomele)
- [@Coldilger](https://github.com/Coldilger)
- [@GioviManto](https://github.com/GioviManto)
- [@javirubio4](https://github.com/javirubio4)

## License

This project is licensed under the Apache-2.0 License. See the [LICENSE](LICENSE) file for details.
