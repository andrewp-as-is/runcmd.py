[![](https://img.shields.io/pypi/pyversions/runcmd.svg?longCache=True)](https://pypi.org/pypi/runcmd/)
[![](https://img.shields.io/pypi/v/runcmd.svg?maxAge=3600)](https://pypi.org/pypi/runcmd/)
[![Travis](https://api.travis-ci.org/looking-for-a-job/runcmd.py.svg?branch=master)](https://travis-ci.org/looking-for-a-job/runcmd.py/)

#### Install
```bash
$ [sudo] pip install runcmd
```

#### Classes

###### `runcmd.Process`

Process class

method|description
-|-
`exc()`|raise OSError if status code is not 0. returns self
`__bool__()`|return True if status code is 0

@property|description
-|-
`args`|return arguments list
`code`|return status code
`err`|return stderr string
`ok`|return True if status code is 0, else False
`out`|return stdout string
`pid`|return rocess pid
`running`|return True if process is running, else False

#### Functions
function|description
-|-
`runcmd.run(args, cwd=None, background=False)`|run command and return Process object

#### Examples
```python
>>> import runcmd
>>> r = runcmd.run(["echo", "hello world"])
>>> r.code  # exit status code
0
>>> r.out  # stdout
'hello world'
>>> r.err  # stderr
''
>>> r.pid  # process pid
1234
```

background - add `background=True`
```python
>>> r = runcmd.run(["sleep","5"],background=True)
>>> while r.running:  # True if process is running and not "zombie process"
>>>     print("running")
```

`exc()` - raise exception if code is not `0`
```python
>>> runcmd.run(["ls"]).exc()              # code 0, ok
>>> runcmd.run(["mkdir", "/"]).exc()      # code 1, raise OSError
...
OSError: exited with code 1
mkdir: /: Is a directory
```

<p align="center"><a href="https://pypi.org/project/readme-md/">readme-md</a> - README.md generator</p>