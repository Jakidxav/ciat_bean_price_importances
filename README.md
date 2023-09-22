## Description:
This is the repository that holds my Jupyter Notebooks containing my analysis of bean price feature importances within the [PABRA](http://www.pabra-africa.org/) program at the International Center for Tropical Agriculture or [CIAT](https://ciat.cgiar.org/). Information about the data used in this study can be found at the following links:
- [WorldClim](https://www.worldclim.org/data/monthlywth.html) global monthly temperature and precipitation data
- [FAO GIEWS](https://fpma.apps.fao.org/giews/food-prices/tool/public/#/dataset/domestic) domestic food prices for beans
- [FAOSTAT](http://www.fao.org/faostat/en/#data) population, land use/change, and food security indicators
- [AfricaFertilizer](https://africafertilizer.org/national/#tab-id-3) national fertlizer prices

## Conda Environment:
I have set up an `environment.yml` file that will install all of the packages you need for this project using Anaconda. To preserve the conda environment across sessions, please add this line of code into your `~/.condarc` file, or create that file if it does not currently exist:
```bash
envs_dirs:
 - /home/user/conda-envs/
```

Once you are in the project directory, run:
```bash
conda env create -f environment.yml -n ciat
```

And to activate the environment:
```bash
conda activate ciat
```

And then you should be up and running!

## Data Processing
The general flow of this repository goes something like this:
- Data for a given topic, say bean prices, is kept in one of three directories: `raw/`, `processed/`, or `full/`. Data in the `raw/` folder is just that: it is unprocessed, and if you wanted you could load in the raw data yourself or recreate my processing steps. The `processed/` folder contains data that has gone through exploratory data analysis (EDA) and is at the very least formatted correctly and interpolated. Then, in the `full/` directory, there is a dataframe combining all of the different types of data into one file (bean prices, fertilizer prices, demographic data, etc.). I chose to process the data this way because I thought that it would be easier to separate out different files at the start, and then combine them at the end for the ML part of the analysis. This makes the data processing a bit tedious, but the ML part much easier.

## Jupyter Notebooks
The Jupyter Notebooks are numbered with an order that I suggest you run them in. However, you will need to run the Notebook `0_install_geospatial_data.ipynb` first before you do anything else. This downloads all of the `.tif` files for the historical weather data that we care about, and without running it some of the later Jupyter Notebooks will not run. I have saved all of the data at each stage, so after running the setup Notebook it is possible to skip to the last Notebook `7_feature_importances.ipynb` if you wanted to. If you want to look through the Notebooks without running them, make sure you go through all of the Notebooks with `_eda.ipynb` at the end first, in no particular order, but then continue with Notebooks 5, 6 and 7.

- Jupyter Notebooks with `_eda.ipynb` appended at the end of their names are meant to be for general data exploration and plotting. These Notebooks take data from the `raw/` folder for a *single* topic, process it, and save it to its corresponding `processed/` folder.

- The Notebook `merge_data.ipynb` takes all of these disparate data sources and merges them into one dataframe per country in the analysis and puts the four resulting datasets in the `full/` folder.

- Lastly, `feature_importances.ipynb` uses the four final datasets for Kenya, Rwanda, Tanzania, and Uganda and trains two tree-based machine learning models on each country's data to determine the importance of individual variables on bean prices.
