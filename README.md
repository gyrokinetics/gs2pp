# GS2 Post-Processing and Plotting

This is a tool and library for post-processing data from the gyrokinetic magnetised plasma turbulence code [GS2](http://gyrokinetics.sourceforge.net).

It consists of a command line tool and wrapper which provides an common interface to a series of separate packages, each of which presents a standardised interface to the wrapper. 

## Using the command line interface:

   $ gs2pp <package> <command> <package_function> <options>
   
where command is one of:

   plot # Display results using e.g. matplotlib
   netcdf # Write the results to a netcdf file
   json # Write the result to a json file
   
Options are package specific, with the following exceptions:

   -f filename # Name of file to write data to
   

## Standardised Interface

Each separate package within gs2pp defines the following standard function

   def gs2pp_interface( command, package_function, options ):

The parameters `command` and `package_function` are strings, and options is a dict. This function must return different things according to the value of command:

- `plot` an object which implements `plot` function and overloads the `+` operator
- `json` a json object (TBC)
- `netcdf` unspecified: in this case the subpackage writes the netcdf file itself


## CodeRunner Integration

The CodeRunner gs2 module will use the RubyPython bridge to access `gs2pp` via the wrapper. This will allow the functionality of `gs2pp` to be applied and combined across multiple gs2 runs managed by `coderunner`.

