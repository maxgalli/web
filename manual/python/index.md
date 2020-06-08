---
title: Python interface PyROOT
layout: single
sidebar:
  nav: "manual"
toc: true
toc_sticky: true
---

ROOT provides an interface to Python, which is enabled via a set of bindings called PyROOT.<br>
PyROOT is enabled by default in ROOT.

For using PyROOT, a Python version > 2.2 is required.<br>
The top level Python module `ROOT.py` is located in `$ROOTSYS/lib`. The `ROOT.py` module imports the `libPyROOT.so` ROOT extension module and performs an initialization similar to ROOT.

> **Python**
>
> The usage of Python with ROOT requires working knowledge of Python. For detailed information on Python, refer to Python language references such as [Python Language Reference](https://docs.python.org/3/reference/){:target="_blank"}.

{% include tutorials name="PyROOT" url="pyroot" %}

## Running PyROOT from the Python interpreter

Ensure that the Python command is executed where the `libPyROOT.so` ROOT extension module is located. This is the main entry point for any Python script using the ROOT classes.

PyROOT scripts work as a usual Python scripts. You just need to import ROOT:

```
import ROOT
```

_**Example**_

```
from ROOT import TCanvas, TF1

c1 = TCanvas( 'c1', 'Example with Formula', 200, 10, 700, 500 )

# Create a one dimensional function and draw it.
fun1 = TF1( 'fun1', 'abs(sin(x)/x)', 0, 10 )
c1.SetGrid()
fun1.Draw()
```


## Running Python from the ROOT/Cling interpreter

In ROOT can run any Python command via the {% include ref class="TPython" %} class.

 _**Example**_

{% highlight C++ %}
root [0] TPython::Exec( "print 1 + 1" )
2
root [1] auto b = (TBrowser*)TPython::Eval( "ROOT.TBrowser()" )
(class TObject*)0x8d1daa0
root [2] TPython::Prompt()
>>> i = 2^D
root [3] TPython::Prompt()
>>> print i
2
{% endhighlight %}


## MultiPython Build and Installation

Starting from version 6.22, PyROOT libraries are built by default with both Python3 and Python2 if a version of CMake >= 3.14 is used. For each Python version X.Y used to build PyROOT (e.g. 3.8, 2.7, etc.) the following libraries (containing the C++ extensions) will appear both in the build directory and in the installation directory:
- `libROOTPythonizationsX_Y.so`
- `libcppyX_Y.so`
- `libcppyy_backendX_Y.so`
The following pure Python packages will appear as well:
- `ROOT`
- `cppyy`
- `cppyy_backend`
- `JupyROOT`
- `JsMVA`
If no option is specified, PyROOT will be built for the most recent Python3 and Python2 versions that CMake can find. If only one version can be found, PyROOT will be built for only that version. Moreover, for a given Python installation to be considered, it must provide both the Python interpreter (binary) and the development package. To build PyROOT, it is thus suggested to verify that python-dev is present and [install it](https://pypi.org/project/python-dev-tools/) if not.
PyROOT can be built with only one version of Python even if multiple installations are present in the system. For this purpose, the option `-DPYTHON_EXECUTABLE=/path/to/python_exec` can be used to point to the desired Python installation.
