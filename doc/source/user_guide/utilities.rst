============
utilities.py
============

Download and management utilities for syncing time and auxiliary files

 - Can list a directory on a ftp host
 - Can download a file from a ftp or http host
 - Can download a file from PO.DAAC via https when WebDAV credentials are supplied
 - Checks MD5 hashes between local and remote files

`Source code`__

.. __: https://github.com/tsutterley/read-GRACE-harmonics/blob/main/gravity_toolkit/utilities.py


General Methods
===============


.. method:: gravity_toolkit.utilities.get_data_path(relpath)

    Get the absolute path within a package from a relative path

    Arguments:

        `relpath`: local relative path as list or string


.. method:: gravity_toolkit.utilities.get_hash(local)

    Get the MD5 hash value from a local file

    Arguments:

        `local`: path to file


.. method:: gravity_toolkit.utilities.url_split(s)

    Recursively split a url path into a list

    Arguments:

        `s`: url string


.. method:: gravity_toolkit.utilities.get_unix_time(time_string, format='%Y-%m-%d %H:%M:%S')

    Get the Unix timestamp value for a formatted date string

    Arguments:

        `time_string`: formatted time string to parse

    Keyword arguments:

        `format`: format for input time string


.. method:: gravity_toolkit.utilities.copy(source, destination, verbose=False, move=False)

    Copy or move a file with all system information

    Arguments:

        `source`: source file

        `destination`: copied destination file

    Keyword arguments:

        `verbose`: print file transfer information

        `move`: remove the source file


.. method:: gravity_toolkit.utilities.ftp_list(HOST,timeout=None,basename=False,pattern=None,sort=False)

    List a directory on a ftp host

    Arguments:

        `HOST`: remote ftp host path split as list

    Keyword arguments:

        `timeout`: timeout in seconds for blocking operations

        `basename`: return the file or directory basename instead of the full path

        `pattern`: regular expression pattern for reducing list

        `sort`: sort output list

    Returns:

        `output`: list of items in a directory

        `mtimes`: list of last modification times for items in the directory


.. method:: gravity_toolkit.utilities.from_ftp(HOST,timeout=None,local=None,hash='',chunk=16384,verbose=False,fid=sys.stdout,mode=0o775)

    Download a file from a ftp host

    Arguments:

        `HOST`: remote ftp host path split as list

    Keyword arguments:

        `timeout`: timeout in seconds for blocking operations

        `local`: path to local file

        `hash`: MD5 hash of local file

        `chunk`: chunk size for transfer encoding

        `verbose`: print file transfer information

        `fid`: open file object to print if verbose

        `mode`: permissions mode of output local file


.. method:: gravity_toolkit.utilities.check_connection(HOST)

    Check internet connection

    Arguments:

        `HOST`: remote http host


.. method:: gravity_toolkit.utilities.from_http(HOST,timeout=None,context=ssl.SSLContext(),local=None,hash='',chunk=16384,verbose=False,fid=sys.stdout,mode=0o775)

    Download a file from a http host

    Arguments:

        `HOST`: remote http host path split as list

    Keyword arguments:

        `timeout`: timeout in seconds for blocking operations

        `context`: SSL context for url opener object

        `local`: path to local file

        `hash`: MD5 hash of local file

        `chunk`: chunk size for transfer encoding

        `verbose`: print file transfer information

        `fid`: open file object to print if verbose

        `mode`: permissions mode of output local file


.. method:: gravity_toolkit.utilities.build_opener(username,password,context=ssl.SSLContext(),password_manager=False,get_ca_certs=False,redirect=False,authorization_header=True,urs=None)

    build urllib opener for NASA Earthdata or JPL PO.DAAC Drive with supplied credentials

    Arguments:

        `username`: NASA Earthdata username

        `password`: NASA Earthdata or JPL PO.DAAC WebDAV password

    Keyword arguments:

        `context`: SSL context for opener object

        `password_manager`: create password manager context using default realm

        `get_ca_certs`: get list of loaded “certification authority” certificates

        `redirect`: create redirect handler object

        `authorization_header`: add base64 encoded authorization header to opener

        `urs`: Earthdata login URS 3 host


.. method:: gravity_toolkit.utilities.check_credentials()

    Check that entered `JPL PO.DAAC Drive`__ credentials are valid

    .. __: https://podaac-tools.jpl.nasa.gov/drive


.. method:: gravity_toolkit.utilities.podaac_list(HOST,username=None,password=None,build=True,timeout=None,parser=None,pattern='',sort=False)

    Download a file from the `JPL PO.DAAC Drive`__ https server

    Arguments:

        `HOST`: remote http host path split as list

    Keyword arguments:

        `username`: NASA Earthdata username

        `password`: JPL PO.DAAC Drive WebDAV password

        `build`: Build opener and check WebDAV credentials

        `timeout`: timeout in seconds for blocking operations

        `parser`: HTML parser for lxml

        `pattern`: regular expression pattern for reducing list

        `sort`: sort output list

    Returns:

        `colnames`: list of column names in a directory

        `collastmod`: list of last modification times for items in the directory

    .. __: https://podaac-tools.jpl.nasa.gov/drive



.. method:: gravity_toolkit.utilities.from_podaac(HOST,username=None,password=None,build=True,timeout=None,local=None,hash='',chunk=16384,verbose=False,fid=sys.stdout,mode=0o775)

    Download a file from `JPL PO.DAAC Drive`__ https server

    Arguments:

        `HOST`: remote http host path split as list

    Keyword arguments:

        `username`: NASA Earthdata username

        `password`: JPL PO.DAAC Drive WebDAV password

        `build`: Build opener and check WebDAV credentials

        `timeout`: timeout in seconds for blocking operations

        `local`: path to local file

        `hash`: MD5 hash of local file

        `chunk`: chunk size for transfer encoding

        `verbose`: print file transfer information

        `fid`: open file object to print if verbose

        `mode`: permissions mode of output local file

    .. __: https://podaac-tools.jpl.nasa.gov/drive


.. method:: gravity_toolkit.utilities.from_figshare(directory,article='7388540',timeout=None,context=ssl.SSLContext(),chunk=16384,verbose=False,fid=sys.stdout,pattern='',mode=0o775)

    Download `Sutterley and Velicogna (2019)`__ geocenter files from `figshare`_

    Arguments:

        `directory`: download directory

    Keyword arguments:
    
        `article`: figshare article number

        `timeout`: timeout in seconds for blocking operations

        `chunk`: chunk size for transfer encoding

        `verbose`: print file transfer information

        `fid`: open file object to print if verbose

        `pattern`: regular expression pattern for reducing list

        `mode`: permissions mode of output local file

    .. __: https://doi.org/10.3390/rs11182108

    .. _figshare: https://doi.org/10.6084/m9.figshare.7388540


.. method:: gravity_toolkit.utilities.from_csr(directory,timeout=None,context=ssl.SSLContext(),chunk=16384,verbose=False,fid=sys.stdout,mode=0o775)
    
    Download `satellite laser ranging (SLR)`__ files from the University of Texas Center for Space Research (UTCSR)

    Arguments:

        `directory`: download directory

    Keyword arguments

        `timeout`: timeout in seconds for blocking operations

        `context`: SSL context for url opener object
        
        `chunk`: chunk size for transfer encoding
        
        `verbose`: print file transfer information
        
        `fid`: open file object to print if verbose
        
        `mode`: permissions mode of output local file

    .. __: http://download.csr.utexas.edu/pub/slr/


.. method:: gravity_toolkit.utilities.icgem_list(host='http://icgem.gfz-potsdam.de/tom_longtime',timeout=None,parser=lxml.etree.HTMLParser())

    Parse table of gravity field models on the `GFZ International Centre for Global Earth Models (ICGEM)`__ server

    Keyword arguments:

        `host`: url for the GFZ ICGEM gravity field table

        `timeout`: timeout in seconds for blocking operations

        `parser`: HTML parser for lxml

    Returns:

        `colfiles`: dictionary of static file urls mapped by field name

    .. __: http://icgem.gfz-potsdam.de/
