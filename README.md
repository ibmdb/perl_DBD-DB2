# perl_DBD-DB2
Repository for DBD::DB2 perl.
dlls for ActivePerl and Strawberry Perl i.e. 
Perl On Windows is using the particular version of MingGW gcc compiler,
which is throwing the compilation error for sqlext.h which is bundled
in our CLI Driver. Hence uploading the precompiled DBD::DB2 dll's in "Windows_Binary" folder.



## Pre-requisites

  The minimum perl version supported by driver is perl 5.8 and the latest version supported is perl 5.40.

*** *BEFORE* BUILDING, TESTING AND INSTALLING this you will need to:

    Build, test and install Perl 5 (Preferrably 5.006_00 or later)
    It is very important to TEST it and INSTALL it!

    Build, test and install the DBI module (at least DBI 1.21).
    It is very important to TEST it and INSTALL it!

    Remember to *read* the DBI README file and this one CAREFULLY!

    Ensure the following DB2 product is installed.

        DB2 Application Development Client v7.2 or later
            Included with the DB2 Personal Developer's Edition and the
            DB2 Universal Developer's Edition

    The Application Development Client can be downloaded here:

    http://www.ibm.com/software/data/db2/udb/support/
	GIT REPO: https://github.com/ibmdb/perl_DBD-DB2



*** BUILDING On UNIX(Tested on RHEL 10):

	export DB2_HOME=<path to CLI DRIVER installation>/clidriver
	export PERL5LIB=~/lib/perl5/lib/perl5/site_perl:$HOME/DBD-DB2-<latest_version>/tests:$HOME/DBD-DB2-<latest_version>/Constants
	
    perl Makefile.PL            # use a perl that's in your PATH
    make
    make test
    make install (if the tests look okay)
	
	NOTE: 
	For non root installation specify the installation into ~/lib/perl5 instead for non-root installation:

	perl Makefile.PL PREFIX=~/lib/perl5
	make
	make test
	make install
	
	On Windows:

    perl Makefile.PL
    nmake
    nmake test
    nmake install
	
*** BUILDING on AIX(tested on 1.86)

	Installation instruction for DBD::DB2 on AIX, with Perl 5.28.1:

	NOTE: I started with perl.rte 5.28.1.2 which was in 7200 TL4 SP2. I am using xlccmp.13.1.3 compiler.

	1)  UNPACK REQUIRED FILES

	Unpacked the following to /tmp/perl

	v10.5fp11_aix64_odbc_cli_32.tar
	DBI DBI-1.643.tar
	DBD-DB2-1.86.tar

	2) BUILD AND INSTALL DBI:

	cd /tmp/perl/DBI-1.643

	perl Makefile.PL
	make
	make test 
	make install 

	 
	3) BUILD AND INSTALL DBD::DB2

	cd  /tmp/perl/DBD-DB2-<latest_version>

	export DB2_HOME=/tmp/perl/odbc_cli_32/clidriver
	export PERL5LIB=/usr/opt/perl5/lib/site_perl/5.28.1/aix-thread-multi/:/tmp/perl/DBD/DBD-DB2-<latest_version>/tests:/tmp/perl/DBD/DBD-DB2-<latest_version>/Constants

*** TESTING:
	Set the DB2_USER & DB2_PASSWD as env variable. If the same is not set, it will be picked from connection.pl
    All Platforms:
    Edit the file connection.pl in the folder tests so that it looks like the following:

    $USERID="userid";
    $PASSWORD="password";
    $PORT=50000;
    $HOSTNAME="localhost";
    $DATABASE="database";
    $PROTOCOL="TCPIP";

    The next section has details about the trusted context user. If you dont have trusted users set specifically, then you may leave this section as is and the testcase for the trusted context would fail. This is an expected behavior.

    The details for fakeport etc can be left untouched.

    Run the test suite by running the following command:
    $ perl run-tests.pl

*** IF YOU HAVE PROBLEMS:

    Please read the CAVEATS files which includes important
    information, including tips and workarounds for various
    platform-specific problems.


*** SUPPORT INFORMATION:

    Technical support for the DBD::DB2 driver is provided by IBM through
    its service agreements for DB2 UDB.  Information on DB2 UDB service
    agreements and support can be found on the Web at

        http://www.software.ibm.com/data/db2/db2tech

    For other DBD::DB2 information, please see

        http://www.software.ibm.com/data/db2/perl

    For documentation about DB2 and CLI, please see:

        http://publib.boulder.ibm.com/infocenter/db2help/index.jsp

    Comments/suggestions/enhancement requests may be raised at

        Github Repo(https://github.com/ibmdb/perl_DBD-DB2)

    Please see the following files for more information:
        CAVEATS - important build/usage information
        DB2.pod - an example perl script
                - an explanation of attribute hashes

*** MAILING LISTS

    As a user or maintainer of a local copy of DBD::DB2, you need
    to be aware of the following addresses:

    The DBI mailing lists located at

        dbi-announce@perl.org          for announcements
        dbi-dev@perl.org               for developer/maintainer discussions
        dbi-users@perl.org             for end user level discussion and help

    To subscribe or unsubscribe to each individual list please see

        http://lists.perl.org/

    or send an empty email to the following addresses

        dbi-announce-subscribe@perl.org
        dbi-dev-subscribe@perl.org
        dbi-users-subscribe@perl.org
