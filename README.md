# utl-flatten-a-diagonal-bock-matrix-into-rows

    Flatten a diagonal bock matrix into rows

    github
    https://tinyurl.com/y23aeyym
    https://github.com/rogerjdeangelis/utl-flatten-a-diagonal-bock-matrix-into-rows

    related to
    https://tinyurl.com/yyfcstxx
    https://communities.sas.com/t5/SAS-Programming/Proc-means-to-roll-up-data-or-datastep/m-p/600531


    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories


    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have;
      informat _543 _843 _K04 mmddyy10.;
      input LN_NO _543 _843 _K04;
      drop ln_no;
    cards4;
    1 09/26/2017 . .
    1 03/30/2018 . .
    1 09/18/2018 . .
    1 09/21/2018 . .
    1 03/25/2019 . .
    1 . 10/03/2017 .
    1 . 04/17/2018 .
    1 . 09/26/2018 .
    1 . 03/27/2019 .
    1 . . 10/03/2017
    1 . . 04/17/2018
    1 . . 09/26/2018
    1 . . 03/27/2019
    1 . . 10/08/2019
    ;;;;
    run;quit;

    WORK.HAVE total obs=14

             _543          _843          _K04

       09/26/2017             .             .
       03/30/2018             .             .
       09/18/2018             .             .
       09/21/2018             .             .
       03/25/2019             .             .
                .    10/03/2017             .
                .    04/17/2018             .
                .    09/26/2018             .
                .    03/27/2019             .
                .             .    10/03/2017
                .             .    04/17/2018
                .             .    09/26/2018
                .             .    03/27/2019
                .             .    10/08/2019

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    WORK.WANT total obs=5

          _543             _843       _K04

       09/26/2017    10/03/2017    10/03/2017
       03/30/2018    04/17/2018    04/17/2018
       09/18/2018    09/26/2018    09/26/2018
       09/21/2018    03/27/2019    03/27/2019
       03/25/2019             .    10/08/2019

    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;

    %array(dates,values=%varlist(have,prx=/_/ ));

    data want;
      merge
         %do_over(dates,phrase=
                  have(where=(? ne .) keep= ?)
         );
    run;quit;


