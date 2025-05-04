It is required to clone both the Community and Enterprise repositories to have a working Odoo Enterprise installation.



# Source install[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#source-install "Permalink to this headline")

The source ‘installation’ is not about installing Odoo but running it directly from the source instead.

Using the Odoo source can be more convenient for module developers as it is more easily accessible than using packaged installers.

It makes starting and stopping Odoo more flexible and explicit than the services set up by the packaged installers. Also, it allows overriding settings using [command-line parameters](https://www.odoo.com/documentation/17.0/developer/reference/cli.html#reference-cmdline) without needing to edit a configuration file.

Finally, it provides greater control over the system’s setup and allows to more easily keep (and run) multiple versions of Odoo side-by-side.

## Fetch the sources[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#fetch-the-sources "Permalink to this headline")

There are two ways to obtain the source code of Odoo: as a ZIP **archive** or through **Git**.

### Archive[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#archive "Permalink to this headline")

Community edition:

- [Odoo download page](https://www.odoo.com/page/download)
    
- [GitHub Community repository](https://github.com/odoo/odoo)
    
- [Nightly server](https://nightly.odoo.com/)
    

Enterprise edition:

- [Odoo download page](https://www.odoo.com/page/download)
    
- [GitHub Enterprise repository](https://github.com/odoo/enterprise)
    

### Git[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#git "Permalink to this headline")

 Note

It is required to have [Git](https://git-scm.com/) installed, and it is recommended to have a basic knowledge of Git commands to proceed.

To clone a Git repository, choose between cloning with HTTPS or SSH. In most cases, the best option is HTTPS. However, choose SSH to contribute to Odoo source code or when following the [Getting Started developer tutorial](https://www.odoo.com/documentation/17.0/developer/tutorials/server_framework_101.html).

LinuxWindowsMac OS

Clone with HTTPSClone with SSH

$ git clone https://github.com/odoo/odoo.git
$ git clone https://github.com/odoo/enterprise.git

 Note

**The Enterprise git repository does not contain the full Odoo source code**. It is only a collection of extra add-ons. The main server code is in the Community edition. Running the Enterprise version means running the server from the Community version with the `addons-path` option set to the folder with the Enterprise edition. ==It is required to clone both the Community and Enterprise repositories to have a working Odoo Enterprise installation.==

## Prepare[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#prepare "Permalink to this headline")

### Python[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#python "Permalink to this headline")

Odoo requires **Python 3.10** or later to run.

Changed in version 17: Minimum requirement updated from Python 3.7 to Python 3.10.

LinuxWindowsMac OS

Use a package manager ([Homebrew](https://brew.sh/), [MacPorts](https://www.macports.org/)) to download and install Python 3 if needed.

 Note

If Python 3 is already installed, make sure that the version is 3.10 or above, as previous versions are not compatible with Odoo.

LinuxWindowsMac OS

$ python3 --version

Verify that [pip](https://pip.pypa.io/) is also installed for this version.

LinuxWindowsMac OS

$ pip3 --version

### PostgreSQL[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#postgresql "Permalink to this headline")

Odoo uses PostgreSQL as its database management system.

LinuxWindowsMac OS

Use [Postgres.app](https://postgresapp.com/) to download and install PostgreSQL (supported version: 12.0 or above).

 Tip

To make the command line tools bundled with Postgres.app available, make sure to set up the `$PATH` variable by following the [Postgres.app CLI tools instructions](https://postgresapp.com/documentation/cli-tools.html).

By default, the only user is `postgres`. As Odoo forbids connecting as `postgres`, create a new PostgreSQL user.

LinuxWindowsMac OS

$ sudo -u postgres createuser -d -R -S $USER
$ createdb $USER

 Note

Because the PostgreSQL user has the same name as the Unix login, it is possible to connect to the database without a password.

### Dependencies[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#dependencies "Permalink to this headline")

LinuxWindowsMac OS

Odoo dependencies are listed in the `requirements.txt` file located at the root of the Odoo Community directory.

>  Tip
> 
> It can be preferable not to mix Python module packages between different instances of Odoo or with the system. However, it is possible to use [virtualenv](https://pypi.org/project/virtualenv/) to create isolated Python environments.

Navigate to the path of the Odoo Community installation (`CommunityPath`) and run **pip** on the requirements file:

$ cd /CommunityPath
$ pip3 install setuptools wheel
$ pip3 install -r requirements.txt

 Warning

Non-Python dependencies must be installed with a package manager ([Homebrew](https://brew.sh/), [MacPorts](https://www.macports.org/)).

1. Download and install the **Command Line Tools**:
    
    $ xcode-select --install
    
2. Use the package manager to install non-Python dependencies.
    

 Note

For languages using a **right-to-left interface** (such as Arabic or Hebrew), the `rtlcss` package is required.

LinuxWindowsMac OS

1. Download and install **nodejs** with a package manager ([Homebrew](https://brew.sh/), [MacPorts](https://www.macports.org/)).
    
2. Install `rtlcss`:
    
    $ sudo npm install -g rtlcss
    

 Warning

`wkhtmltopdf` is not installed through **pip** and must be installed manually in [version 0.12.6](https://github.com/wkhtmltopdf/packaging/releases/tag/0.12.6.1-3) for it to support headers and footers. Check out the [wkhtmltopdf wiki](https://github.com/odoo/odoo/wiki/Wkhtmltopdf) for more details on the various versions.

## Running Odoo[](https://www.odoo.com/documentation/17.0/administration/on_premise/source.html#running-odoo "Permalink to this headline")

Once all dependencies are set up, Odoo can be launched by running `odoo-bin`, the command-line interface of the server. It is located at the root of the Odoo Community directory.

To configure the server, either specify [command-line arguments](https://www.odoo.com/documentation/17.0/developer/reference/cli.html#reference-cmdline-server) or a [configuration file](https://www.odoo.com/documentation/17.0/developer/reference/cli.html#reference-cmdline-config).

 Tip

For the Enterprise edition, add the path to the `enterprise` add-ons to the `addons-path` argument. Note that it must come before the other paths in `addons-path` for add-ons to be loaded correctly.

Common necessary configurations are:

- PostgreSQL user and password.
    
- Custom addon paths beyond the defaults to load custom modules.
    

A typical way to run the server would be:

LinuxWindowsMac OS

$ cd /CommunityPath
$ python3 odoo-bin --addons-path=addons -d mydb

Where `CommunityPath` is the path of the Odoo Community installation, and `mydb` is the name of the PostgreSQL database.

After the server has started (the INFO log `odoo.modules.loading: Modules loaded.` is printed), open [http://localhost:8069](http://localhost:8069/) in a web browser and log into the Odoo database with the base administrator account: use `admin` as the email and, again, `admin` as the password.

 Tip

- From there, create and manage new [users](https://www.odoo.com/documentation/17.0/applications/general/users.html).
    
- The user account used to log into Odoo’s web interface differs from the [`--db_user`](https://www.odoo.com/documentation/17.0/developer/reference/cli.html#cmdoption-odoo-bin-r) CLI argument.
    

 See also

[The list of CLI arguments for odoo-bin](https://www.odoo.com/documentation/17.0/developer/reference/cli.html)