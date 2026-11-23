# IN3062 Group 10 · London Bike Sharing

Can weather improve estimates of recorded hourly London bike hires beyond calendar information? We will compare linear regression, random forest regression and a small dense neural network against two simple baselines. The target, `cnt`, is the recorded number of hires starting in an hour. The weather variables describe conditions during that hour. An advance forecast would need weather information available at the time of prediction.

## Run the baseline notebook

1. If `data/raw/london_merged.csv` is missing, download [Mavrodiev's London Bike Sharing dataset (2019)](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset) and extract the CSV into `data/raw/`. Keep that folder local. Cite the Kaggle dataset and its sources, including the attribution 'Powered by TfL Open Data'.
2. From the repository folder, create an environment with Python 3.12 and start Jupyter using PowerShell. If the environment and dependencies are already installed, run only the last command.

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\python.exe -m pip install -r requirements.txt
   .\.venv\Scripts\python.exe -m notebook
   ```

3. Open [01_data_and_baselines.ipynb](notebooks/01_data_and_baselines.ipynb) and choose **Run All**. The notebook checks the CSV, plots hourly profiles and calculates both baselines on each validation fold.

## Shared evaluation

Fit using earlier records and validate on the next period. Use the same chronological folds for all models.

| Fold | Fit on dates before | Validation dates |
| --- | --- | --- |
| 1 | 1 January 2016 | January to March 2016 |
| 2 | 1 April 2016 | April to June 2016 |
| 3 | 1 July 2016 | July to September 2016 |

Reserve 1 October 2016 onward for the final test. Fit preprocessing and baselines on each fold's training rows. Compare the training mean and the training average for the same weekday and hour. Select model settings using validation RMSE, and record MAE and R² alongside it.

## Next experiments

- Fit linear regression and random forest on the shared folds.
- Add the dense TensorFlow/Keras regressor suggested in the checkpoint feedback. Add its dependency when the network is ready to run.
- For each model, compare calendar inputs with calendar plus weather. Record the feature set, settings, seed where applicable and per-fold scores.
- Once the choices are settled, evaluate on the reserved period and inspect errors by hour and weekday or weekend.

Make small commits as the work progresses. Record data preparation decisions and tested settings in the notebooks so the group can reproduce the report figures.

OpenAI Codex helped prepare the starter files and baseline notebook. For coursework use, follow the School GenAI policy on Moodle and cite reused material in Harvard format.
