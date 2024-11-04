# LLM-Based-APR
An attempt at Automated Program Repair using an LLM.

## RunBugRun Installation

### `rbugr`

As of today, we only support Ubuntu 22.04. For other distributions, please open an issue.
The `rbugr` utility is written in Ruby.
You'll need a recent version of Ruby (3.1) on your system (installed e.g. through [`rbenv`](https://github.com/rbenv/rbenv)).
In addition to a Ruby to run the utility, you'll need a Ruby to run Ruby submission programs. Here version 3.0, the version packaged by Ubuntu, is sufficient.

#### Prerequisities
Use the following to install the compilers/interpreters needed to run submission programs:
```
sudo apt-get install php-cli nodejs gcc g++ default-jdk ruby python3 golang-go bubblewrap
```

#### Installation
In order to install the utility itself do:
```
git clone https://github.com/giganticode/run_bug_run.git
cd run_bug_run
gem install bundler
bundle install
```

## Usage

### Download data

The `rbugr` helper utility can be used to manage dataset versions, obtain information on bugs, run bugs or evaluate the entire test set. 
To download the RunBugRun data at a particular version use:

```
$ bundle exec rbugr dataset download 0.0.1
```

### Sanity Check

It is advised to do a sanity check of your setup by evaluating the *fixed* program versions. You only need to run this for a few seconds to see if the installation is correct.
```
$ bundle exec rbugr eval --fixed --output-filename=sanity_check.json.gz
```
