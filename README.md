# GS2 Post-Processing and Plotting

This is a tool and library for post-processing data from the gyrokinetic magnetised plasma turbulence code [GS2](http://gyrokinetics.sourceforge.net).

It consists of a command line tool and wrapper which provides an common interface to a series of separate packages, each of which presents a standardised interface to the wrapper. 

## The command line interface:

    $ gs2pp <package> <command> <package_function> <options>
   
where command is one of:

1. `run`: a generic command which will simply run the analysis. Useful when analysis is complicated and it's more natural to write results and plots to file at the same time.
2. `plot`: display results to screen or save them to an image file.
3. `write`: write the results to a file (NetCDF, JSON, CSV) specified by command line argument or decided by package.
4. `return`: return a dict of results for further manipulation.
   
Options are package specific, with the following exceptions:

    -f filename # Name of file to write data to
    
E.g.

     $ gs2pp gs2_correlation netcdf all -f output.nc
   

## Standardised Package Interface

Each separate package within gs2pp defines the following standard function

    def gs2pp_interface( command, package_function, options ):

The parameters `command` and `package_function` are strings, and options is a dict. This function must do different things according to the value of `command`. The analysis package does *not* need to implement all `command` functions, only the ones which make sense for the package. The wrapper will handle exception handling to the user based on a (yet to be defined) way of getting the implemented methods from a given package.

