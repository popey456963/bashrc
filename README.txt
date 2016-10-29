##############################################################################
#                         Codefined's ~/.bashrc File                         #
##############################################################################

# A compiled list of commands to aid with everyday usage of bash.  Borrowed
# from many sources, including:
#   http://www.tldp.org/LDP/abs/html/sample-bashrc.html
#   http://ubuntuforums.org/showthread.php?t=679762
#   http://tinyurl.com/ultimate-bashrc-file
# This file couldn't be accomplished without the help of many people, to all of
# whom I give thanks.

# Installation Instructions:
# 1. Download this file `wget codefined.xyz/bashrc/bashrc.txt`
# 2. Merge/replace your bashrc file `mv bashrc.txt ~/.bashrc`
# 3. Add `. .bashrc` to your bash_profile file		
#      `echo ". .bashrc" >> ~/.bash_profile`		
# 4. Run either `. .bashrc` or restart the shell to see changes

# Command Reference:
# up <number> - Goes up a certain amount of directories
# extract <file> - Attempts to extract the file
# ff <string> - Finds a file by it's name
# maketar <dir> - Creates an archive (*.tar.gz) from given directory
# makezip <dir/file> - Creates a ZIP archive from a file or folder
# sanitize <dir/file> - Gives sane permissions to a file or folder
# my_ps - Lists your processes
# killps - Kills a process by name
# get_ip - Gets your current IP address
# host_information - Lists information about your host
# repeat <number> <command> - Repeats a command 'n' times
# ask - Prmopts the user whether to continue
# corename <file> - Get which process created a corefile
# edit <file> - Edit a file as your current user
# sedit <file> - Edit a file as root
# ftext <file> - Search for text in all files in the current folder
# cpp <file> - Copy a file with a progress bar
# cpg <src dir> <dest dir> - Copy and go to a directory
# mvg <src dir> <dest dir> - Move and go to a directory
# mkdirg <dir> - Make and go to a directory

# Custom Aliases:
# ll - List all files in detail
# la - Show hidden files
# l - Shortcut to ls (there are far more, visible on ln. 244)
# back - Go to previous directory
# apt-get - Aptitude
# logs - Watch the log file
# install/update/upgrade/purge - sudo aptitude <command>
# path - Pretty-print the current path
# libpath - Pretty-print the current library path
# please/redo - Runs the previous command as sudo
# .2/.3/.4/.5 - Equivalent of doing up <n>
# web - Go to the web directory (default: /var/www/html)
# bashrc - Edit this ~/.bashrc file
# home - Go to your home directory
# pwdtail - Returns the last two fields of the working directory
# distribution - Returns the current OS
# ver - Returns the current version of the OS
# install_deps - Install the dependencies required for this script
# netinfo - Returns network information
# whatsmyip - Returns the current IP address
# apachelog - Tail all Apache logs
# apachecfg - Edit the Apache config
# phpcfg - Edit the PHP config
# mysqlcfg - Edit the MySQL config
# trim (stream) - Removes leading and trailing whitespace
