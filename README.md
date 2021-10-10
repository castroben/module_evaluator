# module_evaluator

This repository contains a module evaluator system built using Java as a coding language and Maven as a build tool. The repository contains a perl script used to obtain some of the statistics needed to evaluate the modules. This perl script can be found at http://cloc.sourceforge.net/.The purpose of this system is to evaluate NPM modules by providing a url to its repository on github.com or on npmjs.com.

This system uses 5 metrics to evaluate a module:
  1. Bus factor score.
  2. Responsive maintainer score.
  3. Correctness score.
  4. Ramp up score.
  5. License score.

To obtain the scores, the system implements two main methods:
  1. Request module information from Github's REST API.
  2. Temporarily cloning and analyzing the module on the local machine.

### interface
This repository contains an executable bash script labeled 'run'. There are 3 modes of operation for the system, and the mode of operation is specified in the parameter to the bash script.

##### mode1 - "./run install"
Under this mode, our system will install maven on your local machine and will build a single .jar executable containing all the dependencies for the project.
##### mode2 - "./run <SampleURLFilepath>"
Under this mode, our system will read urls inside the filepath passed as a parameter. Our system currently supports two types of url formats: "github.com/<repositoryOwner>/<repositoryName>" and "npmjs.com/package/<repositoryName>". If the urls in the filepath specified do not match these formats, the system will not crash but produce a zero output for all the invalid urls.
##### mode3 - "./run test"
Under this mode, our system executes our entire test suite and reports two outcomes: total tests passed and total line coverage.
### output
The system will output a lsit of URLS to the standard output with the following format:
URL NET_SCORE RAMP_UP_SCORE CORRECTNESS_SCORE BUS_FACTOR_SCORE RESPONSIVE_MAINTAINER_SCORE LICENSE_SCORE
  
## environment variables - very important
In order for this system to work correctly, three enviroment variables must be set: LOG_LEVEL, LOG_FILE, GITHUB_TOKEN. Without these enviroment variables, the systems cannot output any useful information, therefore if the systems does not detect these environment variables, it will exit(1).

  LOG_FILE - this variable contains the full path of the file where all the logging statements will go.
  
  LOG_LEVEL - specifies the verbosity level of the logs. 0-silent, 1-info, 2-debug.
  
  GITHUB_TOKEN - Github personal access token used to make all the API calls needed to evaluate the modules.
  
  In addition to this, perl must be installed in the local machine running this script. The appropriate environment variable must be set to be able to execure perl scripts with "perl <options> <perlscript>"
