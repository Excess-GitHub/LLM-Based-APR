# LLM-Based-APR
An attempt at Automated Program Repair using an LLM.

## Prerequisite for LLM Model Evaluation
In order to evaluate your LLM on the APR task you need to set up the RunBugRun Executable Dataset.

### RunBugRun Installation

#### `rbugr`

As of today, rbugr only supports Ubuntu 22.04.

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

The `rbugr` utility is written in Ruby.
You'll need a recent version of Ruby (3.1) on your system (installed e.g. through [`rbenv`](https://github.com/rbenv/rbenv)).
In addition to a Ruby to run the utility, you'll need a Ruby to run Ruby submission programs. Here version 3.0, the version packaged by Ubuntu, is sufficient.

#### rbenv Installation
Step 1: Get rbenv

   1. Clone rbenv into `~/.rbenv`.
  
       ```
       git clone https://github.com/rbenv/rbenv.git ~/.rbenv
       ```
  
  2. Set up your shell to load rbenv.
  
      ```
      ~/.rbenv/bin/rbenv init
      ```
  
  3. Restart your shell so that these changes take effect. (Opening a new terminal tab will usually do it.)

Step 2: Install Ruby 3.1

  1. Install ruby-build to get rbenv install
     
       ```
       git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
       ```
       ```
       git -C "$(rbenv root)"/plugins/ruby-build pull
       ```
  
  2. Use rbenv install
     
       ```
       # install a Ruby version:
       rbenv install 3.1.0
       ```
  
  3. Set the run_bug_run folder to use Ruby 3.1
     
       ```
       cd run_bug_run
       # choose Ruby version 3.1.0:
       rbenv local 3.1.0
       ```

### RunBugRun Usage

#### Download dataset

The `rbugr` helper utility can be used to manage dataset versions, obtain information on bugs, run bugs or evaluate the entire test set. 
To download the RunBugRun data at a particular version use:

```
bundle exec rbugr dataset download 0.0.1
```

#### Sanity Check

It is advised to do a sanity check of your setup by evaluating the *fixed* program versions. You only need to run this for a few seconds to see if the installation is correct.
```
bundle exec rbugr eval --fixed --output-filename=sanity_check.json.gz
```

#### Evaluation

In order to evaluate your LLM's output use the following

`bundle exec rbugr eval './output.jsonl' --output-filename='./eval.json.gz'`

The 'output.jsonl' file must be in the following format:

```
{id: BUG_ID, preds: [FIX_CANDIDATE_CODE1, FIX_CANDIDATE_CODE2, ...]}
...
```

### Analysis of Evaluation

Once evaluated you can use `rbugr analyze` to calculate various evaluation metrics.
For instance:
```
$ bundle exec rbugr analyze './eval.json.gz'
```
You can use `--by-language` to get a per-language break-down of performance.

You can also check exactly which buggy code files failed to be fixed by using:
```
bundle exec rbugr failing './eval.json.gz'
```
