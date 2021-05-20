Frequently Asked Questions {#FAQ}
==========================

Summary
-------

-   [I need special command to get my
    code](#i-need-special-command-to-get-my-code)
-   [Can I checkout that branch?](#can-i-checkout-that-branch)
-   [Can I clone with my ssh keys?](#can-i-clone-with-my-ssh-keys)
-   [After init, my project has no
    code!](#after-init-my-project-has-no-code)
-   [The project is too big](#the-project-is-too-big)
-   [Java Out Of Memory Error](#java-out-of-memory-error)
-   [How can I run a very large
    project?](#how-can-i-run-a-very-large-project)
-   [Does exakat runs on Java 8?](#does-exakat-runs-on-java-8)
-   [Where can I find the report](#where-can-i-find-the-report)
-   [Can I run exakat on local code?](#can-i-run-exakat-on-local-code)
-   [Can I ignore a dir or a file?](#can-i-ignore-a-dir-or-a-file)
-   [Can I audit only one folder in
    vendor?](#can-i-audit-only-one-folder-in-vendor)
-   [Can I run Exakat with PHP 5?](#can-i-run-exakat-with-php-5)
-   [I get the error \'The executable \'ansible-playbook\' Vagrant is
    trying to run was not
    found\'](#i-get-the-error-the-executable-ansible-playbook-vagrant-is-trying-to-run-was-not-found)
-   [Can I run exakat on Windows?](#can-i-run-exakat-on-windows)
-   [Does exakat send my code to a central
    server?](#does-exakat-send-my-code-to-a-central-server)
-   [\"cat: write error: Broken pipe\" : is it
    bad?](#cat-write-error-broken-pipe-is-it-bad)

[I need special command to get my code](#i-need-special-command-to-get-my-code)
-------------------------------------------------------------------------------

If Exakat has no documented method to reach your code, you may use this
process :

    php exakat.phar init -p <your project name>
    cd ./projects/<your project name>
    mkdir code
    // here, do whatever it takes to put all your code in 'code' folder
    cd -
    php exakat.phar project -p <your project name>

Send a message on Github.com/exakat/exakat to mention your specific
method.

[Can I checkout that branch?](#can-i-checkout-that-branch)
----------------------------------------------------------

Currently (Version 0.12.2), there is no way to request a tag or a
branche or a revision when cloning the code.

The best way is to reach the \'code\' folder, and make the change there.
Unless with \'init\' or \'update\', exakat doesn\'t make any change to
the code.

    php exakat.phar init -p myProject -R url://my/git/repository 
    cd ./projects/myProject/code
    git branch notMasterBranch
    cd -
    php exakat.phar project -p myProject

[Can I clone with my ssh keys?](#can-i-clone-with-my-ssh-keys)
--------------------------------------------------------------

When using git, or any vcs, the current shell user\'s SSH keys may be
used to access the repository. When using a remote installation, or a
docker image, the keys won\'t be accessible.

The fallback solution is to init an empty project, clone the code from
the Shell (with the keys), and then run project.

    php exakat.phar init -p myProject
    cd ./projects/myProject
    git clone url://myprivate/git/repository code 
    cd -
    php exakat.phar project -p myProject

[After init, my project has no code!](#after-init-my-project-has-no-code)
-------------------------------------------------------------------------

Check in the projects/\<name\>/config.ini file : if values were
provided, you\'ll find them there.

In case the code was not found during init, then do the following :

::

:   cd projects/\<name\>/ git clone <ssh://project/URL> code cd -php
    exakat.phar files -p \<name\>

If you\'re using some other method than git, then just collect the code
in a \'code\' folder in the \<name\> project and run the \'files\'
command.

[The project is too big](#the-project-is-too-big)
-------------------------------------------------

There is a soft limit in config/exakat.ini, called \'token\_limit\' that
initially prevents analysis of projects over 1 million tokens. That\'s
roughly 125k LOC, more than most code source.

If you need to run exakat on larger sources, you may change this value
to make it as large as possible. Then, the physical capacities of the
machine, specially RAM, will be the actual limit.

It may be interesting to \'ignore\_dir\[\]\', from
projects/\<name\>/config.ini.

[Java Out Of Memory Error](#java-out-of-memory-error)
-----------------------------------------------------

By default, java is allowed to run with 512mb of RAM. That may be too
little for the code being studied.

Set the environment variable \$JAVA\_OPTIONS to give larger quantities
of RAM. For example : \'export JAVA\_OPTIONS=\'-Xms1024m -Xmx6096m\'; or
\'setenv JAVA\_OPTIONS=\'-Xms1024m -Xmx6096m\'

Xms is the memory allocation at start, and Xmx is the maximum
allocation. With some experimentation, 6G handles the largest

[How can I run a very large project?](#how-can-i-run-a-very-large-project)
--------------------------------------------------------------------------

Here are a few steps you can try when running exakat on a very large
project.

-   Update project/\<name\>/config.ini, and use ignore\_dirs\[\] and
    include\_dirs\[\] to exclude as much code as possible. Notably,
    frameworks, data in PHP files, tests, cache, translations, etc.
-   Set environment variable \$JAVA\_OPTIONS to large quantities of RAM
    : JAVA\_OPTIONS=\'-Xms1024m -Xmx6096m\';
-   Check that your installation is running with \'gsneo4j\' and not
    \'tinkergraph\', in config/exakat.ini.

[Does exakat runs on Java 8?](#does-exakat-runs-on-java-8)
----------------------------------------------------------

Exakat itself runs with PHP 7.0+. Exakat runs with a gremlin database :
gremlin-server 3.2.x is supported, which runs on Java 8.

Java 9 is experimental, and is being tested. Java 7 used to be working,
but is not supported anymore : it may still work, though.

[Where can I find the report](#where-can-i-find-the-report)
-----------------------------------------------------------

Reports are available after running at least the following commands :

    php exakat.phar init -p <your project name> -R <code source repo> 
    php exakat.phar project -p <your project name>

The default report is the HTML report, called \'Ambassador\'. You\'ll
find it in ./projects/\<your project name\>/report.

Other reports, build with \'report\' command, will also be saved there,
with different names.

[Can I run exakat on local code?](#can-i-run-exakat-on-local-code)
------------------------------------------------------------------

There are several ways to do that : use symbolic links, make a copy of
the source.

    php exakat.phar init -p <your project name> -R <path/to/the/code> -symlink 
    php exakat.phar init -p <your project name> -R <path/to/the/code> -copy 
    php exakat.phar init -p <your project name> -R <path/to/the/code> -git 

Symlink will branch exakat directly into the code; -copy makes a copy of
the code (this means the code will never be updated without manual
intervention); git (or other vcs) may also be used with local
repositories.

Exakat do not modify any existing source code : it only access it for
reading purpose, then works on a separated database. As a defensive
security measure, we suggest that exakat should work on a read-only copy
of the code.

[Can I ignore a dir or a file?](#can-i-ignore-a-dir-or-a-file)
--------------------------------------------------------------

Yes. After initing a project, open the projects/\<project
name\>/config.ini file, and update the ignore\_dir line. For example, to
ignore a behat test folder, and to ignore any file called \'license\' :

    ignore_dirs[] = '/behat/';
    ignore_dirs[] = 'license';

You may also include files, by using the include\_dir\[\] line.
Including files is processed after ignoring them, so you may include
files in folders that were previously ignored.

[Can I audit only one folder in vendor?]{.title-ref}
----------------------------------------------------

You can use ignore\_dirs to exclude everything in the source tree, then
use include\_dirs to include specific folders.

::

:   \# exclude everything ignore\_dirs\[\] = \'/\';

    \# include intended folder include\_dirs\[\] = \'/vendor/exakat\';

[Can I run Exakat with PHP 5?](#can-i-run-exakat-with-php-5)
------------------------------------------------------------

It is recommended to run exakat with PHP 7.4 or even 8.0. PHP 7.3 is
still possible, though not supported. PHP 7.2 and below won\'t work (we
checked).

Note that you may test your code on PHP 5.x, while running Exakat on PHP
7.4. There are 2 distinct configuration options in Exakat. \'php\' is
the path to the PHP binary that runs Exakat : this one should be PHP
7.0+. \'phpxx\' are the path to the PHP helpers, that are used to
tokenized and lint the target PHP code. This is where PHP 5.x may be
configured.

    ; where and which PHP executable are available
    php   = /usr/local/sbin/php74

    php52 = 
    php53 = /usr/local/sbin/php53
    php54 = 
    php55 = 
    php56 = 
    php70 = 
    php71 = 
    php72 = 
    php73 = 
    php74 = 
    php80 = 
    php81 = 

Above is an example of a exakat configuration file, where Exakat is run
with PHP 7.1 and process code with PHP 5.3.

[I get the error \'The executable \'ansible-playbook\' Vagrant is trying to run was not found\'](#i-get-the-error-the-executable-ansible-playbook-vagrant-is-trying-to-run-was-not-found)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

This error is displayed when the host machine doesn\'t have Ansible
installed. Install ansible, and try again to provision.

[Can I run exakat on Windows?](#can-i-run-exakat-on-windows)
------------------------------------------------------------

Currently, Windows is not supported, though it might be some day.

Until then, you may run Exakat with Vagrant, or with Docker.

[Does exakat send my code to a central server?](#does-exakat-send-my-code-to-a-central-server)
----------------------------------------------------------------------------------------------

When run from the sources, Exakat has everything it needs to fulfill its
mission. There is no central server that does the job, and requires the
transmission of the code.

When running an audit on the Saas service of Exakat, the code is
processed on our servers.

[\"cat: write error: Broken pipe\" : is it bad?](#cat-write-error-broken-pipe-is-it-bad)
----------------------------------------------------------------------------------------

Exakat currently runs some piped commands, with xargs so as to make some
operations parallel. When the following command ends up before the
reading all the data from the first command, such a warning is emitted.

It has no impact on exakat\'s processing of the code.

See also [cat: write error: Broken
pipe](https://askubuntu.com/questions/421663/cat-write-error-broken-pipe).

[Require a \[gremlin\]Argument]{.title-ref}
-------------------------------------------

Running an audit (project command) leads to an error message such as
this one :

::

:   2/2
    \[========================================================================\>\]
    100.00% 00:00:00

    Error : The request message was parseable, but the arguments
    supplied in the message were in conflict or incomplete. Check the
    message format and retry the request. : A message with an \[eval\]
    op code requires a \[gremlin\] argument.

    =================== SERVER TRACE ========================= array ( )
    ============================================================

    on file
    phar:///exakat-2.1.9/exakat.phar/vendor/brightzone/gremlin-php/src/Connection.php
    on line 847

This happens when exakat couldn\'t stop the gremlin database. You should
take it down manually, then restart the audit. No version update
necessary.

Get the process ID with the following command, and then, kill it.

::

:   ps aux \| grep gsneo4jv3.3.4 ps aux \| grep gremlin