# Streetwise Score

This is an open data science project compatible with the [Renku platform](https://renkulab.io).

Data sources are required in the following folders:

- **enhanced_preproc** - a set of preprocessed images
- **models** - trained model in `.h5` format
- **data** - a `scoring.csv` with corresponding `images/*.jpg`

This collection of images of Switzerland sourced from Mapillary have been pre-processed for training the Streetwise algorithm, are available from our team for R&D and training purposes only. Licensed CC BY-SA - for further details see https://www.mapillary.com/terms

In additional to the `data` folder, you may wish [to download](https://streetwise.eu-central-1.linodeobjects.com/models.zip) an extract a `models` folder into the root in order to start with pre-trained networks. Alternatively, the code used to train the networks can be found in ```scripts/NN-training.py```.

## Background

This is a script using a pre-trained neural network (see [1]) to predict the perceived safety score of a certain place in a city.

The NN model compares pairs of images and estimates which one is taken in the safest place. This information is then used to compute the TrueSkill score [2] using the TrueSkill package [3]. The results are then exported in the GeoJSON format [4].

The safety scores are on a scale 0-50, where 0 represents a very unsafe place and 50  a very safe place.

Another script allows to aggregate the data using rectangular tesselation, which gives a lower granularity, but also less noisy, visualization. Some sample tesselated data can be found in the ```tesselated_scores```folder. When visualized, these look for example as follows:

[<img src="https://github.com/Streetwise/streetwise-score/blob/master/wiki_images/zurich_tessel.jpg" alt="Zurich tesselated" width="500px"/>](https://api.mapbox.com/styles/v1/colombmo/ckg0t167k2it219nyvvws0dov/draft.html?fresh=true&title=view&access_token=pk.eyJ1IjoiY29sb21ibW8iLCJhIjoiY2tlYTE5MmpvMTB6cTJxcm41Ynl1OTNxYSJ9.6SsIy1FTpxao9Sv-hvRDSg)

### Results

Sample results can be found in the ```safety_scores``` folder. These can be easily visualized, for example using mapbox:

[<img src="https://github.com/Streetwise/streetwise-score/blob/master/wiki_images/romanshorn.png" alt="Romanshorn" width="500px"/>](https://api.mapbox.com/styles/v1/colombmo/ckesny6m30o9019p97rv594qx.html?fresh=true&title=view&access_token=pk.eyJ1IjoiY29sb21ibW8iLCJhIjoiY2tlYTE5MmpvMTB6cTJxcm41Ynl1OTNxYSJ9.6SsIy1FTpxao9Sv-hvRDSg)

[<img src="https://github.com/Streetwise/streetwise-score/blob/master/wiki_images/luzern.png" alt="Luzern" width="500px"/>](https://api.mapbox.com/styles/v1/colombmo/ckeskgshq764k19o21zu3l7fw.html?fresh=true&title=view&access_token=pk.eyJ1IjoiY29sb21ibW8iLCJhIjoiY2tlYTE5MmpvMTB6cTJxcm41Ynl1OTNxYSJ9.6SsIy1FTpxao9Sv-hvRDSg)

[<img src="https://github.com/Streetwise/streetwise-score/blob/master/wiki_images/stgallen.png" alt="St. Gallen" width="500px"/>](https://api.mapbox.com/styles/v1/colombmo/ckesiukh124lb19mt27xeg56r.html?fresh=true&title=view&access_token=pk.eyJ1IjoiY29sb21ibW8iLCJhIjoiY2tlYTE5MmpvMTB6cTJxcm41Ynl1OTNxYSJ9.6SsIy1FTpxao9Sv-hvRDSg)

[<img src="https://github.com/Streetwise/streetwise-score/blob/master/wiki_images/schaffhausen.png" alt="Schaffhausen" width="500px"/>](https://api.mapbox.com/styles/v1/colombmo/cketssk0r91th19qq2l9jcd3h/draft.html?fresh=true&title=view&access_token=pk.eyJ1IjoiY29sb21ibW8iLCJhIjoiY2tlYTE5MmpvMTB6cTJxcm41Ynl1OTNxYSJ9.6SsIy1FTpxao9Sv-hvRDSg)

## Renku configuration

Project options can be found in `.renku/renku.ini`. In this project there is currently only one option, which specifies the default type of environment to open, in this case `/lab` for JupyterLab. You may also choose `/tree` to get to the "classic" Jupyter interface.

### References

[1] https://github.com/Streetwise/streetwise-data/wiki/MachineLearning

[2] Herbrich, R., Minka, T. and Graepel, T., 2007. TrueSkill™: a Bayesian skill rating system. In _Advances in neural information processing systems_ (pp. 569-576).

[3] https://trueskill.org/

[4] https://geojson.org/
