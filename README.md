# outlier data

## requirements

- [Homebrew](https://brew.sh/)
- [Git LFS](https://git-lfs.github.com/)
- [Python 3.5+](https://www.python.org/downloads/) (tested on Python 3.9.1)
- [pipenv](https://pipenv.pypa.io/en/latest/) (we'll install this with homebrew)
- [Node.js 14+](https://nodejs.org/en/) (tested on Node.js 17.7.2)
- 16+ GB RAM (although I did it on an 8 GB RAM M1 Macbook)
- Roughly 6GB of disk space

## installation

```bash
# install git-lfs
brew install git-lfs
git lfs install
# install geo build deps
brew install gdal proj spatialindex
# install pipenv
brew install pipenv
# install python dependencies
pipenv install
# install node.js dependencies
npm install
```

## quickstart

You'll first need to pull the reference shapefile data via `git lfs`:

```bash
git lfs pull
```

Then, you can generate the test data from this project by running:

```bash
pipenv run generate
```

`generate` is [custom pipenv script](https://pipenv.pypa.io/en/latest/advanced/#custom-script-shortcuts) that uses [papermill](https://papermill.readthedocs.io/en/latest/index.html) to run the jupyter notebook from the command line.

See `output files` for more details on the generated data.

---

You can also start the jupyter notebook to read how the generation script works:

Start notebook

```bash
pipenv run jupyter notebook
```

## output files

### development

The dev files include the following fields:

```
'GEOID10': state + county + tract string. unique
'state': 2 digit state code
'county': 3 digit county code
'tract': 6 digit census tract code
'kir_white_pooled_p75': mean predicted individual income for *Black* kids w/ parental income in 75th percentile
'kir_black_pooled_p75': mean predicted individual income for *White* kids w/ parental income in 75th percentile
'geometry': geometry data
```

This is a large dataset so these files only include one outcome along two racial variables (Black and white) and include pooled gender data. This data will increase substantially but this should be enough to start the bones of the work.

Refer to the jupyter notebook to augmenting/adjusting the provided fields.

The dev data includes:

- `data/processed/dev-tracts-simplified-geo.json`: geojson file for all matched census tracts with the above fields
- `data/processed/dev-tracts-simplified-topo.json`: same as the geojson but formatted as topojson. The topojson file is much smaller but requires topojson as a dependency.

### production

TK
