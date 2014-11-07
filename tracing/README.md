Linux Kernel Tracing Experiments
================================

This sub-directory contains the scripts and tools used to study how Mininet interacts with the Linux kernel networking stack.

The following tools were used for learning how to interact with **ftrace** and dynamic kernel probes:

 * [perf-tools  (by Brendan Gregg)](https://github.com/brendangregg/perf-tools)
 * [trace-cmd  (by Steven Rostedt)](https://git.kernel.org/cgit/linux/kernel/git/rostedt/trace-cmd.git)


The `trace-cmd` tool was chosen to generate a trace for further analysis. This tool can collect data for the duration of a desired subprocess. This way, it is possible to directly trace a "ping test" on Mininet with the following command:

```
/root/trace-cmd/trace-cmd record -F -e all -p function_graph mn --topo single,2 --switch ovsk --test=pingall &> /dev/null
```

It is important to note that `trace-cmd` supports a number of trace plugins. The call graph tracer is used due to the async, event-oriented nature of the networking stack. Tracing only functions directly called by Mininet and its child processes would result in missing information (not displaying the code path for packets).

Using the call graph tracer system-wide results in a very large trace log. Thus, it is not available in the repository itself -- but can be [downloaded from Github](https://www.dropbox.com/s/lxlhktg8cp050ag/funcgraph-all-mininet-pingall.tar.xz) if desired. The Ubuntu 14.04 virtual machine used for generating this trace will be made available in a later date.

In order to understand what's happening during a Mininet experiment, a Python script was written to filter functions not directly relevant to this project. 

```
python2.7 cleanTrace.py INPUT_TRACE OUTPUT_TRACE
```

The resulting log can then be used to study the code paths from a networking perspective.


Pending Issues / Future Work
============================
 * Indicate the functions triggered by each step from the Mininet experiment
 * Generate a sequence(?) diagram based on the trace (with hosts / switches as the columns in the diagram)
