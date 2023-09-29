# Community Finding between Streamer in Twitch Data

## Introduction

This Jupyter Notebook is designed to transform raw data of Twitch user/streamer connections from May '23, graciously provided by GitHub user "snoww" of the "stats.roki.sh" stat, into a weighted connection graph. The purpose of this notebook is to extract meaningful insights from the data and create a visual representation of the connections between various elements, primiarily for community finding.

## Code Overview

The code provided in this notebook performs the following steps:

### Loading Data and adding nodes

The `load_data` function loads data from a JSON file and applies a chatter threshold. The `add_nodes_to_graph` function adds nodes and edges to the graph based on the input data. It constructs an initial graph representation with all users documented (~7.5-8mil)

### Calculating Thresholds

The `calculate_thresholds` function calculates streamer thresholds based on the minimum degree required. Users without atleast these many unique 'chatters' will be removed from consideration as nodes on the graph. 

### Calculating Overlap and Weighted Graph

The `calc_overlap_and_weighted` function combines the calculation of viewer overlap and the construction of the weighted graph (and much faster). It sets edge weights based on common viewers, and it also sets the 'viewer_count' attribute for each node in the weighted graph. Yet to decide if a simple addition is enough or if we need some form of 'authority' metric. Seeing as it's community finding, IDTS, its just '\<streamer> viewers also watch \<streamer>'

### Analyzing Files

The `analyze_file` function orchestrates the entire process for a specific file and chatter threshold, creating weighted graphs for different chatter thresholds. Inappropriately named as no analysis is done, just refining and .gml generation. 

### Configuration and Execution

The code is pre-configured with the following parameters:

- `data_folder`: Path to the folder containing the raw data files.
  (note: data folder has been .gitignored )
- `chatter_thresholds`: A list of chatter thresholds to analyze.
- `edge_weight_threshold`: The threshold for edge weights (fraction). Only when the number of common viewers between two users is greater than this threshold times the total unique 'chatters' of the user with lower 'chatters', would an edge be added

You can customize these parameters to tailor the analysis to your specific requirements.

## Results

The notebook will generate weighted graph files for different chatter thresholds, which you can use for further analysis and visualization.

## Acknowledgments

We would like to express our gratitude to GitHub user "snoww" for graciously providing the May '23 data from "stats.roki.sh."
