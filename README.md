# LLM-Based-APR
An attempt at Automated Program Repair using an LLM.

## RunBugRun Installation

### Data
RunBugRun's data can be downloaded in the form of gzipped JSONL files from [here](https://github.com/giganticode/run_bug_run_data) or downloaded directly with the `rbugr` utility.

### `rbugr`

As of today, we only support Ubuntu 22.04. For other distributions, please open an issue.
The `rbugr` utility is written in Ruby.
You'll need a recent version of Ruby (3.1) on your system (installed e.g. through [`rbenv`](https://github.com/rbenv/rbenv)).
In addition to a Ruby to run the utility, you'll need a Ruby to run Ruby submission programs. Here version 3.0, the version packaged by Ubuntu, is sufficient.

#### Prerequisities
Use the following to install the compilers/interpreters needed to run submission programs:
```
$ apt-get install php-cli nodejs gcc g++ default-jdk ruby python3 golang-go bubblewrap
```

#### Installation
In order to install the utility itself do:
```
$ git clone https://github.com/giganticode/run_bug_run.git
$ cd https://github.com/giganticode/run_bug_run.git
$ gem install bundler
$ bundle install
```

## Usage

### Download data

The `rbugr` helper utility can be used to manage dataset versions, obtain information on bugs, run bugs or evaluate the entire test set. 
To download the RunBugRun data at a particular version use:

```
$ bundle exec rbugr download 0.0.1
```

### Sanity Check

It is advised to do a sanity check of your setup by evaluating the *fixed* program versions.
```
$ bundle exec rbugr eval --fixed --output-filename=sanity_check.json.gz
```
