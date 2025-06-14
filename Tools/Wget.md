Download a file from a given URL and save it in the current directory
```bash
wget http://example.com/file.zip
```

Download a file and save it with a different name
```bash
wget -O newname.zip http://example.com/file.zip
```

Download files in the background
wget -b http://example.com/file.zip

# Download a file and limit the download speed to reduce bandwidth usage
wget --limit-rate=200k http://example.com/file.zip

# Download files from a list of URLs provided in a text file
wget -i urls.txt

# Resume an incomplete download
wget -c http://example.com/file.zip

# Download a file while showing the progress in a more readable form
wget --show-progress http://example.com/file.zip

# Download a file without checking the server's SSL certificate
wget --no-check-certificate https://example.com/file.zip

# Download an entire website for offline browsing
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent http://example.com
# Download a file with HTTP authentication
wget --user=username --password=password http://example.com/secure-file.zip

# Download a file with cookies, useful for sites that require logins
wget --load-cookies cookies.txt http://example.com/file.zip

# Download a directory from an FTP server
wget -r ftp://example.com/pub/

# Download only files newer than the local version
wget -N http://example.com/file.zip

# Download a file only if it has been updated on the server
wget -S --spider http://example.com/file.zip

# Quietly download a file, continuing where it left of, if the connection
# fails. The file will be downloaded to the current working directory.
wget -qc http://example.com/file.zip

# Specify a location to download the given file.
wget -qcO [PATH] http://example.com/file.zip

# Download URL using the user agent string provided to the `-U` flag.
wget -U 'Mozilla/5.0' http://example.com/file.zip

 cheat:wget 
# To download <url>:
wget <url>
#
# To download multiples files with multiple URLs:
wget <url>...

# To download <url> and change its name:
wget <url> -O <outfile>

# To download <url> into <dir>:
wget -P <dir> <url>

# To continue an aborted downloaded:
wget -c <url>

# To parse a file that contains a list of URLs to fetch each one:
wget -i url_list.txt

# To mirror a whole page locally:
wget -pk <url>

# To mirror a whole site locally:
wget -mk <url>

# To download files according to a pattern:
wget http://example.com/files-{1..15}.tar.bz2

# To download all the files in a directory with a specific extension if directory indexing is enabled:
wget -r -l1 -A.extension http://example.com/directory

# To download only response headers (-S --spider) and display them on stdout (-O -).:
wget -S --spider -O - <url>

# To change the User-Agent to 'User-Agent: toto':
wget -U 'toto' <url>

# To download a file with specific speed EX:500kb/sec:
wget --limit-rate=500k <url>

 tldr:wget 
# wget
# Download files from the Web.
# Supports HTTP, HTTPS, and FTP.
# More information: <https://www.gnu.org/software/wget>.

# Download the contents of a URL to a file (named "foo" in this case):
wget https://example.com/foo

# Download the contents of a URL to a file (named "bar" in this case):
wget --output-document bar https://example.com/foo

# Download a single web page and all its resources with 3-second intervals between requests (scripts, stylesheets, images, etc.):
wget --page-requisites --convert-links --wait=3 https://example.com/somepage.html

# Download all listed files within a directory and its sub-directories (does not download embedded page elements):
wget --mirror --no-parent https://example.com/somepath/

# Limit the download speed and the number of connection retries:
wget --limit-rate=300k --tries=100 https://example.com/somepath/

# Download a file from an HTTP server using Basic Auth (also works for FTP):
wget --user=username --password=password https://example.com

# Continue an incomplete download:
wget --continue https://example.com

# Download all URLs stored in a text file to a specific directory:
wget --directory-prefix path/to/directory --input-file URLs.txt
