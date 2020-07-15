# poliastro performance benchmarks

## About

These benchmarks track the performance of various features in poliastro *over time*.

To view them, visit [this site](https://benchmarks.poliastro.space).

The benchmarks are run using [airspeed velocity](https://asv.readthedocs.io).

## For contributors

The `master` branch in this repository should not contain any results or
built website. Results should be added to the `results` branch, and
commits to the `results` branch trigger a build to the `gh-pages`
branch.

### Requirements

You will need to install the following system packages:

- git

As well as a working Python environment.
Python dependencies can be installed either with plain pip:

```
$ pip install -r requirements.txt
```

or using pip-tools:

```
$ pip-sync
```

### Configuring the machine

First of all, configure the machine. This has to be done only once,
and you can leave all the defaults. When finished, a file will be written
in your home directory that will contain the machine information:

```
$ asv machine
· No information stored about machine 'p38t'. I know about nothing.
  

I will now ask you some questions about this machine to identify it in the benchmarks.
...
$ cat ~/.asv-machine.json
{
    "p38t": {
        "arch": "x86_64",
        "cpu": "Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz",
        "machine": "p38t",
        "num_cpu": "4",
        "os": "Linux 5.4.0-40-generic",
        "ram": "16313376"
    },
    "version": 1
}
```

### Running the benchmarks

To run asv on the latest commit in the upstream poliastro master, you can do:

```
$ asv run
```

This will set up a temporary environment in which poliastro will be installed,
and the benchmark functions will be run multiple times and averaged to get
accurate timings.
The results from this will be saved into a `results/<machine-name>` directory,
which will store one file per commit (or more than one file
if the tests are set up to run for multiple Python or NumPy versions,
which is not the default configuration for these benchmarks).

Alternatively, you can install poliastro yourself (either from the package
or from a local checkout) and run:

```
$ asv dev
```

This will run the benchmarks against the local poliastro version
and will do some basic timing, but the timing will not be very accurate,
because this only runs each benchmark once instead of taking
an average of many runs. Nevertheless, it's a good way of making sure
things are running correctly and can still give order of magnitude timings.

asv can be given a range of commits. For example, to run the benchmarks
against **all the commits from the beginning until a certain tag**, you can do:

```
$ asv run v0.14.0
```

Notice that, to run the benchmarks against a specific commit,
you have to use a more involved syntax:

```
$ asv run v0.14.0^!
```

And to run against a range of commits:

```
$ asv run v0.13.0..v0.14.0
```

(see `man gitrevisions` for more information)

### Testing using Docker

To test locally using Docker, you can run:

```
$ docker run -it --rm --name p38t --hostname p38t -v $(pwd):/tmp --user $(id -u):$(id -g) python:3.8 bash
I have no name!@p38t:/$ python -m venv /tmp/.venv && source /tmp/.venv/bin/activate
(.venv) I have no name!@p38t:/$ cd /tmp && pip install -r requirements.txt
(.venv) I have no name!@p38t:/src$ export HOME=/tmp && asv machine
(.venv) I have no name!@p38t:~$ asv run
...
```

(notice that this will write some files in the working directory)
