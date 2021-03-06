# Strace Output I/O Analyzer.

The strace output I/O analyser is a tool to analyze the I/O behaviour of serial and parallel applications.
It traces the system calls and generates statistics for every accessed file.

## Getting Started

### Prerequisites
The strace output I/O analyzer requires
- strace to generate traces
- python 3.4 or greater to analyze the traces

### Installation
Just clone the directory from https://github.com/cniethammer/strace-analyzer and use the scripts.
No additional steps required.

### Usage:
#### Trace Generation
Generate a trace with the strace wrapper
```
  ./strace-wrapper.sh ./my_app [APP OPTIONS]
```
or use the strace-wrapper.sh for MPI parallel programs like
```
  mpirun [MPI OPTIONS] ./strace-wrapper.sh ./my_app [APP OPTIONS]
```
which will generate a set of strace log files - one for each MPI process.
The log files will be stored in a directory strace-logs under the current path.
If the directory does not exist, it will be created.
The LOGDIR variable may be used to specify another directory for the log files:
```
  LOGDIR=my_log_dir mpirun [MPI OPTIONS] ./strace-wrapper.sh ./my_app [APP OPTIONS]
```
#### Filtering MPI ranks
For MPI programs running with large number of processes the number of traced
processes may have to be narrowed down. The RANK_FILTER variable allows to
specify a regex pattern which is matched agains the MPI rank number. Only
processes with ranks matching this regex will be traced.
```
  RANK_FILTER='[0-4]' mpirun [MPI OPTIONS] ./strace-wrapper.sh ./my_app [APP OPTIONS]
```


#### Analyzing Traces

To analyze the created traces run

```
./strace_io_stats.py *.strace
```
To get help how to use and control strace_io_stats.py run
```
./strace_io_stats.py --help
```


## Legal Info and Contact
Copyright (c) 2017     HLRS, University of Stuttgart.
This software is published under the terms of the BSD license.

Contact: Christoph Niethammer <niethammer@hlrs.de>

