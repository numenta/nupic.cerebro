# Cerebro

A tool for [NuPIC](http://github.com/numenta/nupic) to run CLA models and visually examine the output of the Spatial Pooler. [Click here for a video introduction and tutorial](http://youtu.be/WQWU1K5tE5o).

## What is Cerebro?

- A DVR for the CLA algorithm
- A visual debugging tool for the CLA
- A dataset generator
- A local web app
- Another client of the OPF
- A tool for finding mutants

## How do I use it?

To install (with [Homebrew for Mac OS X](http://brew.sh/)):

    brew install libevent
    brew install mongodb
    pip install -r requirements.txt

To launch:

    mongod &
    python cerebro.py <portnum>

In a browser, navigate to:

    http://localhost:<portnum>

## Datasets

### File based
- Need a description.py file as input
- Can load a base and sub description.py file
- Path to data file should be in the description.py file

### Function based
- Write a function to procedurally generate datasets
- Python
- Provides a number of useful utilities for generating datasets
- Can save to CSV

#### Function Data Details

- Function written in python. Don’t need to include def funcname()
- Dictionary fields should be filled with data fields. Fields can be strings or scalars
- Utility variable history passed to function. Used to create sequential patterns. **history[-1][‘foo’]** retrieves the field value of ‘foo’ from 1 timestep ago
- Several useful libraries are imported on your behalf:
  - Random
  - Numpy
  - String
  - Math
- Provides some syntactic sugar for adding randomness to datasets
  - If a field is set to a list-like, values are randomly sampled from set.Ex. fields[‘f’] = (‘A’, ‘B’, ‘C’, ‘D’) => Randomly sample ‘A’, ‘B’, ‘C’, D’Ex. Fields[‘foo’] = list(string.uppercase) => randomly sample from uppercase letters
  - If a field is set to a dict-like, values are randomly sampled  according to likelihood ratios.Ex. fields[‘f’] = {‘A’: 1.0, ‘B’:2.0} => Randomly sample ‘A’, ‘B’, where ‘B’ is twice as likely.

## Experiment Pane

- Show’s predicted vs. actual graphs
- If present, also shows anomaly score graph
- On right, shows predicted and active columns
- Shows encoder representations on the bottom
- At the very bottom, shows a whole bunch of textual output.
- Verbose output: captures everything from stdout while CLA processes a single record
