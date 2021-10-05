# utl-computing-maxs-and-mins-of-all-numeric-and-character-variables-using-sql-arrays
Computing maxs and mins of all numeric and character variables using sql arrays
    Computing maxs and mins of all numeric and character variables using sql arrays

    github
    https://tinyurl.com/3n5ewhu3
    https://github.com/rogerjdeangelis/utl-computing-maxs-and-mins-of-all-numeric-and-character-variables-using-sql-arrays


    SAS Forum
    https://communities.sas.com/t5/SAS-Programming/SAS-Arrays/m-p/772154

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

     SASHELP.CARS


     Middle Observation(214 ) of sashelp.cars - Total Obs 428

      -- CHARACTER --             Sample Value        Label

     MAKE                C13      Kia                 MAKE
     MODEL               C40      Sedona LX           MODEL
     TYPE                C8       Sedan               TYPE
     ORIGIN              C6       Asia                ORIGIN
     DRIVETRAIN          C5       Front               DRIVETRAIN

      -- NUMERIC --
     MSRP                N8       20615               MSRP
     INVOICE             N8       19400               INVOICE
     ENGINESIZE          N8       3.5                 Engine Size (L)
     CYLINDERS           N8       6                   CYLINDERS
     HORSEPOWER          N8       195                 HORSEPOWER
     MPG_CITY            N8       16                  MPG (City)
     MPG_HIGHWAY         N8       22                  MPG (Highway)
     WEIGHT              N8       4802                Weight (LBS)
     WHEELBASE           N8       115                 Wheelbase (IN)
     LENGTH              N8       194                 Length (IN)

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    * macro array of all ames;

    %array(_vs,values=%varlist(sashelp.cars));

    /*
    %put &=_vs1;
    %put &=_vs2;
    %put &=_vsn;

    _VS1=MAKE
    _VS2=MODEL
    ...
    _VSN=15
    */

    proc sql;
      create
          table want as
      select
          %do_over(_vs,phrase=%str(
              min(?) as min_?
             ,max(?) as max_?)
             ,between=comma)
      from
          sashelp.cars
    ;quit;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    Middle Observation(1 ) of Last dataset = WORK.WANT - Total Obs 1


     -- CHARACTER --
    MIN_MAKE            C13      Acura
    MAX_MAKE            C13      Volvo

    MIN_MODEL           C40      3.5 RL 4dr
    MAX_MODEL           C40       xB

    MIN_TYPE            C8       Hybrid
    MAX_TYPE            C8       Wagon

    MIN_ORIGIN          C6       Asia
    MAX_ORIGIN          C6       USA

    MIN_DRIVETRAIN      C5       All
    MAX_DRIVETRAIN      C5       Rear


     -- NUMERIC --
    MIN_MSRP            N8       10280
    MAX_MSRP            N8       192465

    MIN_INVOICE         N8       9875
    MAX_INVOICE         N8       173560

    MIN_ENGINESIZE      N8       1.3
    MAX_ENGINESIZE      N8       8.3

    MIN_CYLINDERS       N8       3
    MAX_CYLINDERS       N8       12

    MIN_HORSEPOWER      N8       73
    MAX_HORSEPOWER      N8       500

    MIN_MPG_CITY        N8       10
    MAX_MPG_CITY        N8       60

    MIN_MPG_HIGHWAY     N8       12
    MAX_MPG_HIGHWAY     N8       66

    MIN_WEIGHT          N8       1850
    MAX_WEIGHT          N8       7190

    MIN_WHEELBASE       N8       89
    MAX_WHEELBASE       N8       144

    MIN_LENGTH          N8       143
    MAX_LENGTH          N8       238
