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
# update_bashrc - Update this ~/.bashrc (loses existing settings and edits)

# Custom Aliases:
# h - Search command line history
# p/topcpu - Search running processes
# f - Find files in current folder
# countfiles - Count files in current folder
# ipview - Show current network connections
# openports - List open ports
# rebootsafe/rebootforce - Restart the server
# diskspace - Disk space used and free
# folders/folderssort - Folders and their relative size
# tree - List all items recursively from the current folder
# treed - List all directories recursively from the current folder
# mountedinfo - Displasy information about the current mounting
# mktar/mkbz2/mkgz - Create archives of common formats
# untar/unbz2/ungz - Unzip archives of common formats
# logs - Tail all log files in /var/log
# sha1 - Sha 1 from OpenSSL
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
# ../.../.... - Equivalent of doing up <n>
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

##############################################################################
#                               User Settings                                #
##############################################################################

# default - user@server ~/dir :) >
# verbose - (user@server)-(jobs)-(date)->
#           (~/currentDir)-(num_files files, folder_size kb)->
# time    - time user@hostname ~$

command_line="default"

enable_colours=true
enable_aliases=true
enable_fancy_terminal=true
enable_background_commands=true
enable_utility_commands=true
enable_process_commands=true
enable_information_commands=true
enable_misc_commands=true
enable_programmable_completion=true
enable_update=true

fix_common_typos=true
use_aptitude=true

version=2.0

##############################################################################
#                         Generic ~/.bashrc Settings                         #
##############################################################################

# Look for global definitions
if [ -f /etc/bashrc ]; then
   . /etc/bashrc
fi

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# Update window size after each command
shopt -s checkwinsize

# Fix less to be able to use non-text files
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# Set "**" to match all files and zero or more subdirectories
# shopt -s globstar

# Disable the bell sound from playing
if [[ $iatest > 0 ]]; then bind "set bell-style visible"; fi

# Set Nano to be the default editor
export EDITOR=nano
export VISUAL=nano


##############################################################################
#                          Command History Settings                          #
##############################################################################

# Ignore empty and duplicate history items
HISTCONTROL=ignoreboth

# Append instead of re-writing the history file
shopt -s histappend

# Allow ctrl-S for history navigation (with ctrl-R)
stty -ixon

# Expand the history stored
HISTSIZE=1000
HISTFILESIZE=20000

# Change the date-format to be more readable
export HISTTIMEFORMAT="[%Y-%m-%d %T] "

# Exclude ls, bg, fg and exit commands from the history
export HISTIGNORE="&:ls:[bf]g:exit"

##############################################################################
#                             Colour Variables                               #
##############################################################################

if [ "$enable_colours" == true ] ; then
  # Normal Colors
  Black='\e[0;30m'        # Black
  Red='\e[0;31m'          # Red
  Green='\e[0;32m'        # Green
  Yellow='\e[0;33m'       # Yellow
  Blue='\e[0;34m'         # Blue
  Purple='\e[0;35m'       # Purple
  Cyan='\e[0;36m'         # Cyan
  White='\e[0;37m'        # White

  # Bold
  BBlack='\e[1;30m'       # Black
  BRed='\e[1;31m'         # Red
  BGreen='\e[1;32m'       # Green
  BYellow='\e[1;33m'      # Yellow
  BBlue='\e[1;34m'        # Blue
  BPurple='\e[1;35m'      # Purple
  BCyan='\e[1;36m'        # Cyan
  BWhite='\e[1;37m'       # White

  # Background
  On_Black='\e[40m'       # Black
  On_Red='\e[41m'         # Red
  On_Green='\e[42m'       # Green
  On_Yellow='\e[43m'      # Yellow
  On_Blue='\e[44m'        # Blue
  On_Purple='\e[45m'      # Purple
  On_Cyan='\e[46m'        # Cyan
  On_White='\e[47m'       # White

  NC="\e[m"               # Color Reset

  RESET="\[\017\]"
  NORMAL="\[\033[0m\]"
  WHITE="\[\033[37;1m\]"
  BLUE="\[\033[34;1m\]"
  RED="\[\033[31;1m\]"
  YELLOW="\[\033[33;1m\]"
  GREEN="\[\033[32;1m\]"
  SUCCESS="${GREEN}:)${NORMAL}"
  FAILURE="${RED}:(${NORMAL}"
fi

##############################################################################
#                           Fancy Terminal Prompt                            #
##############################################################################

if [ "$enable_fancy_terminal" == true ] ; then
  # Enable colours for grep, egrep, zgrep, etc.
  export CLICOLOR=1
  # This method is deprecated in a number of OS'
  # export GREP_OPTIONS='--color=auto'

  # Select Statement
  SELECT="if [ \$? = 0 ]; then echo \"${SUCCESS}\"; else echo \"${FAILURE}\"; fi"

  if [ "$command_line" == "default" ] ; then
    # <user>@<hostname> <working directory> <last command successful> >
    # codefined@server ~/working/directory :) >
    PS1="${RESET}${YELLOW}\h${NORMAL} ${BLUE}\w${NORMAL} \`${SELECT}\` ${YELLOW}>${NORMAL} "
  elif [ "$command_line" == "verbose" ] ; then
    # (<user>@<server>)-(<jobs>)-(<date>)-> 
    # (<~/currentDir>)-(<num files> files, <folder_size> kb)-> 
    PS1="\[\e[30;1m\]\[\016\]\[\017\](\[\e[31;1m\]\u@\h\[\e[30;1m\])-(\[\e[31;1m\]\j\[\e[30;1m\])-(\[\e[31;1m\]\@ \d\[\e[30;1m\])->\[\e[30;1m\]\n\[\016\]\[\017\](\[\[\e[32;1m\]\w\[\e[30;1m\])-(\[\e[32;1m\]\$(/bin/ls -1 | /usr/bin/wc -l | /bin/sed 's: ::g') files, \$(/bin/ls -lah | /bin/grep -m 1 total | /bin/sed 's/total //')b\[\e[30;1m\])-> \[\e[0m\]"
  elif [ "$command_line" == "time" ] ; then
    # (time) (user)@(hostname) ~$ 
    # 12:44:53 codefined@server ~$
    PS1="\[\033[35m\]\t\[\033[m\] \[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h \[\033[33;1m\]\w\[\033[m\]\$ "
  fi

  # Color for manpages
  export LESS_TERMCAP_mb=$'\E[01;31m'
  export LESS_TERMCAP_md=$'\E[01;31m'
  export LESS_TERMCAP_me=$'\E[0m'
  export LESS_TERMCAP_se=$'\E[0m'
  export LESS_TERMCAP_so=$'\E[01;44;33m'
  export LESS_TERMCAP_ue=$'\E[0m'
  export LESS_TERMCAP_us=$'\E[01;32m'
fi

##############################################################################
#                          Machine Specific Aliases                          #
##############################################################################

# Connect to a specific server
# alias <servername>='ssh <domain> -l <user> -p <port>'

# Alias to go to common locations
alias web='cd /var/www/html'

# Alias to mount ISO files (Note: sudo required for both commands)
# sudo mount -o loop /home/<iso>.iso /home/<mountDir>
# sudo umount /home/<iso>.iso

##############################################################################
#                               Command Aliases                              #
##############################################################################

# You can temporarily disable these by adding a "\" before the alias you wish
# to run.  For example, `ls` is aliased, but you can use the normal ls command
# with `\ls`

if [ "$enable_aliases" == true ] ; then
  # Aliases for the common editors
  alias spico='sedit'
  alias snano='sedit'

  # Edit this ~/.bashrc ffile
  alias bashrc='edit ~/.bashrc'

  # Make ls, dir, vdir and grep use colour if possible
  if [ -x /usr/bin/dircolors ]; then
      test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
      alias ls='ls --color=auto'
      alias dir='dir --color=auto'
      alias vdir='vdir --color=auto'

      alias grep='grep --color=auto'
      alias fgrep='fgrep --color=auto'
      alias egrep='egrep --color=auto'
  fi

  # Alias some common ls parameters to other commands
  alias la='ls -Alh' # show hidden files
  alias ls='ls -aFh --color=always' # add colors and file type extensions
  alias lx='ls -lXBh' # sort by extension
  alias lk='ls -lSrh' # sort by size
  alias lc='ls -lcrh' # sort by change time
  alias lu='ls -lurh' # sort by access time
  alias lr='ls -lRh' # recursive ls
  alias lt='ls -ltrh' # sort by date
  alias lm='ls -alh |more' # pipe through 'more'
  alias lw='ls -xAh' # wide listing format
  alias ll='ls -Fls' # long listing format
  alias labc='ls -lap' #alphabetical sort
  alias lf="ls -l | egrep -v '^d'" # files only
  alias ldir="ls -l | egrep '^d'" # directories only

  # Alias some common chmod amounts
  alias mx='chmod a+x'
  alias 000='chmod -R 000'
  alias 644='chmod -R 644'
  alias 666='chmod -R 666'
  alias 755='chmod -R 755'
  alias 777='chmod -R 777'

  # Add an "alert" alias for long running commands.  Use like so:
  #   sleep 10; alert
  alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

  # Go back to your previous directory
  alias back='cd "$OLDPWD"'

  # Watch logs
  alias logs="find /var/log -type f -exec file {} \; | grep 'text' | cut -d' ' -f1 | sed -e's/:$//g' | grep -v '[0-9]$' | xargs tail -f"

  if [ "$use_aptitude" == true ] ; then
    # Use Aptitude instead of Apt-get
    alias apt-get='aptitude'

    # Simplify Aptitude Commands
    alias install='sudo aptitude install'
    alias update='sudo aptitude update'
    alias upgrade='sudo aptitude upgrade'
    alias purge='sudo aptitude purge'
  fi

  if [ "$use_aptitude" = false ] ; then
    # Use Aptitude instead of Apt-get
    alias apt-get='aptitude'

    # Simplify Aptitude Commands
    alias install='sudo aptitude install'
    alias update='sudo aptitude update'
    alias upgrade='sudo aptitude upgrade'
    alias purge='sudo aptitude purge'
  fi


  # Prompt on (re)moving files and clobbering directories
  alias rm='rm -i'
  alias cp='cp -i'
  alias mv='mv -i'
  alias mkdir='mkdir -p'

  # Common aliases to change program defaults
  alias ping='ping -c 10'
  alias less='less -R'
  alias cls='clear'
  alias multitail='multitail --no-repeat -c'
  alias freshclam='sudo freshclam'
  alias vi='vim'
  alias svi='sudo vi'
  alias vis='vim "+set si"'

  # Pretty-print some PATH variables
  alias path='echo -e ${PATH//:/\\n}'
  alias libpath='echo -e ${LD_LIBRARY_PATH//:/\\n}'

  if [ "$fix_common_typos" = true ] ; then
    # Fix common typos
    alias xs='cd'
    alias vf='cd'
    alias moer='more'
    alias moew='more'
    alias kk='ll'
  fi

  # Redo the previous command as sudo
  alias please='sudo $(history -p !!)'
  alias redo='sudo $(history -p !!)'

  # Easier "cd" commannds
  alias home='cd ~'
  alias cd..='cd ..'

  # Alternatives to "up"
  alias .2='cd ../../'                        # Go back 2 directory levels
  alias .3='cd ../../../'                     # Go back 3 directory levels
  alias .4='cd ../../../../'                  # Go back 4 directory levels
  alias .5='cd ../../../../../'               # Go back 5 directory levels
  alias .6='cd ../../../../../../'            # Go back 6 directory levels
  alias ..='cd ..'
  alias ...='cd ../..'
  alias ....='cd ../../..'
  alias .....='cd ../../../..'

  # Search command line history
  alias h="history | grep "

  # Search running processes
  alias p="ps aux | grep "
  alias topcpu="/bin/ps -eo pcpu,pid,user,args | sort -k 1 -r | head -10"

  # Search files in the current folder
  alias f="find . | grep "

  # Count all files (recursively) in the current folder
  alias countfiles="for t in files links directories; do echo \`find . -type \${t:0:1} | wc -l\` \$t; done 2> /dev/null"

  # To see if a command is aliased, a file, or a built-in command
  alias checkcommand="type -t"

  # Show current network connections to the server
  alias ipview="netstat -anpl | grep :80 | awk {'print \$5'} | cut -d\":\" -f1 | sort | uniq -c | sort -n | sed -e 's/^ *//' -e 's/ *\$//'"

  # Show open ports
  alias openports='netstat -nape --inet'

  # Alias's for safe and forced reboots
  alias rebootsafe='sudo shutdown -r now'
  alias rebootforce='sudo shutdown -r -n now'

  # Alias's to show disk space and space used in a folder
  alias diskspace="du -S | sort -n -r |more"
  alias folders='du -h --max-depth=1'
  alias folderssort='find . -maxdepth 1 -type d -print0 | xargs -0 du -sk | sort -rn'
  alias tree='tree -CAhF --dirsfirst'
  alias treed='tree -CAFd'
  alias mountedinfo='df -hT'

  # Alias's for archives
  alias mktar='tar -cvf'
  alias mkbz2='tar -cvjf'
  alias mkgz='tar -cvzf'
  alias untar='tar -xvf'
  alias unbz2='tar -xvjf'
  alias ungz='tar -xvzf'

  # Show all logs in /var/log
  alias logs="sudo find /var/log -type f -exec file {} \; | grep 'text' | cut -d' ' -f1 | sed -e's/:$//g' | grep -v '[0-9]$' | xargs tail -f"

  # SHA1
  alias sha1='openssl sha1'
fi

##############################################################################
#                         Run Commands in Background                         #
##############################################################################

if [ "$enable_background_commands" == true ] ; then
  function example_background() { 
    command example_background "$@" & 
  }
fi

##############################################################################
#                           Custom Utility Commands                          #
##############################################################################

if [ "$enable_utility_commands" == true ] ; then
  # Allow `up 4` instead of `cd ../../../..`
  function up () {
    local d=""
    limit=$1
    for ((i=1 ; i <= limit ; i++))
      do
        d=$d/..
      done
    d=$(echo $d | sed 's/^\///')
    if [ -z "$d" ]; then
      d=..
    fi
    cd $d
  }

  # Edit files using the default editor
  edit ()
  {
    if [ "$(type -t nano)" = "file" ]; then
      nano -c "$@"
    elif [ "$(type -t pico)" = "file" ]; then
      pico "$@"
    else
      nano -c "$@"
    fi
  }
  sedit ()
  {
    if [ "$(type -t nano)" = "file" ]; then
      sudo nano -c "$@"
    elif [ "$(type -t pico)" = "file" ]; then
      sudo pico "$@"
    else
      sudo nano -c "$@"
    fi
  }

  # Searches for text in all files in the current folder
  ftext ()
  {
    # -i case-insensitive
    # -I ignore binary files
    # -H causes filename to be printed
    # -r recursive search
    # -n causes line number to be printed
    # optional: -F treat search term as a literal, not a regular expression
    # optional: -l only print filenames and not the matching lines ex. grep -irl "$1" *
    grep -iIHrn --color=always "$1" . | less -r
  }

  # Extract lots of files via one command
  extract () {
    for archive in $*; do
      if [ -f $archive ] ; then
        case $archive in
          *.tar.bz2)   tar xvjf $archive    ;;
          *.tar.gz)    tar xvzf $archive    ;;
          *.bz2)       bunzip2 $archive     ;;
          *.rar)       rar x $archive       ;;
          *.gz)        gunzip $archive      ;;
          *.tar)       tar xvf $archive     ;;
          *.tbz2)      tar xvjf $archive    ;;
          *.tgz)       tar xvzf $archive    ;;
          *.zip)       unzip $archive       ;;
          *.Z)         uncompress $archive  ;;
          *.7z)        7z x $archive        ;;
          *)           echo "don't know how to extract '$archive'..." ;;
        esac
      else
        echo "'$archive' is not a valid file!"
      fi
    done
  }

  # Find a file by it's name
  function ff() { 
    find . -type f -iname '*'"$*"'*' -ls ; 
  }

  # Creates an archive (*.tar.gz) from given directory.
  function maketar() { 
    tar cvzf "${1%%/}.tar.gz"  "${1%%/}/"; 
  }

  # Create a ZIP archive of a file or folder.
  function makezip() { 
    zip -r "${1%%/}.zip" "$1" ; 
  }

  # Make your directories and files access rights sane.
  function sanitize() { 
    chmod -R u=rwX,g=rX,o= "$@" ;
  }

  # Copy file with a progress bar
  cpp()
  {
    set -e
    strace -q -ewrite cp -- "${1}" "${2}" 2>&1 \
    | awk '{
    count += $NF
    if (count % 10 == 0) {
      percent = count / total_size * 100
      printf "%3d%% [", percent
      for (i=0;i<=percent;i++)
        printf "="
        printf ">"
        for (i=percent;i<100;i++)
          printf " "
          printf "]\r"
        }
      }
    END { print "" }' total_size=$(stat -c '%s' "${1}") count=0
  }

  # Copy and go to the directory
  cpg ()
  {
    if [ -d "$2" ];then
      cp $1 $2 && cd $2
    else
      cp $1 $2
    fi
  }

  # Move and go to the directory
  mvg ()
  {
    if [ -d "$2" ];then
      mv $1 $2 && cd $2
    else
      mv $1 $2
    fi
  }

  # Create and go to the directory
  mkdirg ()
  {
    mkdir -p $1
    cd $1
  }

  #Automatically do an ls after each cd
  # cd ()
  # {
  #   if [ -n "$1" ]; then
  #     builtin cd "$@" && ls
  #   else
  #     builtin cd ~ && ls
  #   fi
  # }

  # Returns the last 2 fields of the working directory
  pwdtail ()
  {
    pwd|awk -F/ '{nlast = NF -1;print $nlast"/"$NF}'
  }

  # Show the current distribution
  distribution ()
  {
    local dtype
    # Assume unknown
    dtype="unknown"
    
    # First test against Fedora / RHEL / CentOS / generic Redhat derivative
    if [ -r /etc/rc.d/init.d/functions ]; then
      source /etc/rc.d/init.d/functions
      [ zz`type -t passed 2>/dev/null` == "zzfunction" ] && dtype="redhat"
    
    # Then test against SUSE (must be after Redhat,
    # I've seen rc.status on Ubuntu I think? TODO: Recheck that)
    elif [ -r /etc/rc.status ]; then
      source /etc/rc.status
      [ zz`type -t rc_reset 2>/dev/null` == "zzfunction" ] && dtype="suse"
    
    # Then test against Debian, Ubuntu and friends
    elif [ -r /lib/lsb/init-functions ]; then
      source /lib/lsb/init-functions
      [ zz`type -t log_begin_msg 2>/dev/null` == "zzfunction" ] && dtype="debian"
    
    # Then test against Gentoo
    elif [ -r /etc/init.d/functions.sh ]; then
      source /etc/init.d/functions.sh
      [ zz`type -t ebegin 2>/dev/null` == "zzfunction" ] && dtype="gentoo"
    
    # For Mandriva we currently just test if /etc/mandriva-release exists
    # and isn't empty (TODO: Find a better way :)
    elif [ -s /etc/mandriva-release ]; then
      dtype="mandriva"

    # For Slackware we currently just test if /etc/slackware-version exists
    elif [ -s /etc/slackware-version ]; then
      dtype="slackware"

    fi
    echo $dtype
  }

  # Show the current version of the operating system
  ver ()
  {
    local dtype
    dtype=$(distribution)

    if [ $dtype == "redhat" ]; then
      if [ -s /etc/redhat-release ]; then
        cat /etc/redhat-release && uname -a
      else
        cat /etc/issue && uname -a
      fi
    elif [ $dtype == "suse" ]; then
      cat /etc/SuSE-release
    elif [ $dtype == "debian" ]; then
      lsb_release -a
      # sudo cat /etc/issue && sudo cat /etc/issue.net && sudo cat /etc/lsb_release && sudo cat /etc/os-release # Linux Mint option 2
    elif [ $dtype == "gentoo" ]; then
      cat /etc/gentoo-release
    elif [ $dtype == "mandriva" ]; then
      cat /etc/mandriva-release
    elif [ $dtype == "slackware" ]; then
      cat /etc/slackware-version
    else
      if [ -s /etc/issue ]; then
        cat /etc/issue
      else
        echo "Error: Unknown distribution"
        exit 1
      fi
    fi
  }

  # Automatically install the needed support files for this .bashrc file
  install_deps ()
  {
    local dtype
    dtype=$(distribution)

    if [ $dtype == "redhat" ]; then
      sudo yum install multitail tree joe
    elif [ $dtype == "suse" ]; then
      sudo zypper install multitail
      sudo zypper install tree
    elif [ $dtype == "debian" ]; then
      sudo apt-get install multitail tree
    elif [ $dtype == "gentoo" ]; then
      sudo emerge multitail
      sudo emerge tree
    elif [ $dtype == "mandriva" ]; then
      sudo urpmi multitail
      sudo urpmi tree
    elif [ $dtype == "slackware" ]; then
      echo "No install support for Slackware"
    else
      echo "Unknown distribution"
    fi
  }

  # Show current network information
  netinfo ()
  {
    echo "--------------- Network Information ---------------"
    /sbin/ifconfig | awk /'inet addr/ {print $2}'
    echo ""
    /sbin/ifconfig | awk /'Bcast/ {print $3}'
    echo ""
    /sbin/ifconfig | awk /'inet addr/ {print $4}'

    /sbin/ifconfig | awk /'HWaddr/ {print $4,$5}'
    echo "---------------------------------------------------"
  }

  # IP address lookup
  alias whatismyip="whatsmyip"
  function whatsmyip ()
  {
    # Dumps a list of all IP addresses for every device
    # /sbin/ifconfig |grep -B1 "inet addr" |awk '{ if ( $1 == "inet" ) { print $2 } else if ( $2 == "Link" ) { printf "%s:" ,$1 } }' |awk -F: '{ print $1 ": " $3 }';

    # Internal IP Lookup
    echo -n "Internal IP: " ; /sbin/ifconfig eth0 | grep "inet addr" | awk -F: '{print $2}' | awk '{print $1}'

    # External IP Lookup
    echo -n "External IP: " ; wget http://smart-ip.net/myip -O - -q
  }

  # View Apache logs
  apachelog ()
  {
    if [ -f /etc/httpd/conf/httpd.conf ]; then
      cd /var/log/httpd && ls -xAh && multitail --no-repeat -c -s 2 /var/log/httpd/*_log
    else
      cd /var/log/apache2 && ls -xAh && multitail --no-repeat -c -s 2 /var/log/apache2/*.log
    fi
  }

  # Edit the Apache configuration
  alias apacheconfig="apachecfg"
  apachecfg ()
  {
    if [ -f /etc/httpd/conf/httpd.conf ]; then
      sedit /etc/httpd/conf/httpd.conf
    elif [ -f /etc/apache2/apache2.conf ]; then
      sedit /etc/apache2/apache2.conf
    else
      echo "Error: Apache config file could not be found."
      echo "Searching for possible locations:"
      sudo updatedb && locate httpd.conf && locate apache2.conf
    fi
  }

  # Edit the PHP configuration file
  alias phpconfig="phpcfg"
  phpcfg ()
  {
    if [ -f /etc/php.ini ]; then
      sedit /etc/php.ini
    elif [ -f /etc/php/php.ini ]; then
      sedit /etc/php/php.ini
    elif [ -f /etc/php5/php.ini ]; then
      sedit /etc/php5/php.ini
    elif [ -f /usr/bin/php5/bin/php.ini ]; then
      sedit /usr/bin/php5/bin/php.ini
    elif [ -f /etc/php5/apache2/php.ini ]; then
      sedit /etc/php5/apache2/php.ini
    else
      echo "Error: php.ini file could not be found."
      echo "Searching for possible locations:"
      sudo updatedb && locate php.ini
    fi
  }

  # Edit the MySQL configuration file
  alias mysqlconfig="mysqlcfg"
  mysqlcfg ()
  {
    if [ -f /etc/my.cnf ]; then
      sedit /etc/my.cnf
    elif [ -f /etc/mysql/my.cnf ]; then
      sedit /etc/mysql/my.cnf
    elif [ -f /usr/local/etc/my.cnf ]; then
      sedit /usr/local/etc/my.cnf
    elif [ -f /usr/bin/mysql/my.cnf ]; then
      sedit /usr/bin/mysql/my.cnf
    elif [ -f ~/my.cnf ]; then
      sedit ~/my.cnf
    elif [ -f ~/.my.cnf ]; then
      sedit ~/.my.cnf
    else
      echo "Error: my.cnf file could not be found."
      echo "Searching for possible locations:"
      sudo updatedb && locate my.cnf
    fi
  }

  # Trim leading and trailing spaces (for scripts)
  trim()
  {
    local var=$@
    var="${var#"${var%%[![:space:]]*}"}"  # remove leading whitespace characters
    var="${var%"${var##*[![:space:]]}"}"  # remove trailing whitespace characters
    echo -n "$var"
  }
fi

##############################################################################
#                           Custom Process Commands                          #
##############################################################################

if [ "$enable_process_commands" == true ] ; then
  # Find your processes
  function my_ps() { 
    ps $@ -u $USER -o pid,%cpu,%mem,bsdtime,command ; 
  }

  # Kill by process name
  function killps() {
    local pid pname sig="-TERM"
    if [ "$#" -lt 1 ] || [ "$#" -gt 2 ]; then
      echo "Usage: killps [-SIGNAL] pattern"
      return;
    fi
    if [ $# = 2 ]; then sig=$1 ; fi
    for pid in $(my_ps| awk '!/awk/ && $0~pat { print $1 }' pat=${!#} )
    do
      pname=$(my_ps | awk '$1~var { print $5 }' var=$pid )
      if ask "Kill process $pid <$pname> with signal $sig?"
        then kill $sig $pid
      fi
    done
  }
fi

##############################################################################
#                         Custom Information Commands                        #
##############################################################################

if [ "$enable_information_commands" == true ] ; then
  function get_ip() {
    MY_IP=$(/sbin/ifconfig eth0 | awk '/inet/ { print $2 } ' |
      sed -e s/addr://)
    echo ${MY_IP:-"Not connected"}
  }

  # Get host information
  function host_information()
  {
      echo -e "\nYou are logged on ${BRed}$HOST"
      echo -e "\n${BRed}Additional information:$NC " ; uname -a
      echo -e "\n${BRed}Users logged on:$NC " ; w -hs |
               cut -d " " -f1 | sort | uniq
      echo -e "\n${BRed}Current date :$NC " ; date
      echo -e "\n${BRed}Machine stats :$NC " ; uptime
      echo -e "\n${BRed}Memory stats :$NC " ; free
      echo -e "\n${BRed}Local IP Address :$NC" ; get_ip
      echo -e "\n${BRed}Open connections :$NC "; netstat -pan --inet;
      echo
  }
fi

##############################################################################
#                           Miscellaneous Commands                           #
##############################################################################

if [ "$enable_misc_commands" == true ] ; then
  # Repeat a function 'n' times
  #   repeat <number> <command>
  function repeat() {
      local i max
      max=$1; shift;
      for ((i=1; i <= max ; i++)); do
          eval "$@";
      done
  }

  # Ask whether something should be done
  #   ask <question>
  function ask() {
      echo -n "$@" '[y/n] ' ; read ans
      case "$ans" in
          y*|Y*) return 0 ;;
          *) return 1 ;;
      esac
  }

  # Get who created a corefile
  #   corename <file>
  function corename()
  {
      for file ; do
          echo -n $file : ; gdb --core=$file --batch | head -1
      done
  }
fi

##############################################################################
#                               Update Checker                               #
##############################################################################

# Pings my server to see if a new version has been released.  If it has, this
# function will do nothing but alert the user (this seems wise considering it
# is grabbing the update over HTTP).
if [ "$enable_update" == true ] ; then
  url="bash.sinisterheavens.com?a="
  uuid=$(blkid | grep -oP 'UUID="\K[^"]+' | sha256sum | awk '{print $1}')
  new_version=$(wget $url$uuid -q -O -)
  if [ $(echo " $new_version > $version" | bc) -eq 1 ] ; then
    echo "Your version of .bashrc (v${version}) is outdated, the latest \
version is v${new_version}"
    echo "You might consider grabbing the latest version from http://co\
defined.xyz/bashrc/bashrc.txt"
    echo "Or you can run 'update_bashrc' which will update it automatically"
  fi
  update_bashrc() {
    if ask "Are you sure?  This downloads the script over HTTP."; then
      mv -fv ~/.bashrc ~/.bashrc.old
      wget http://codefined.xyz/bashrc/bashrc.txt -O ~/.bashrc
    fi
  }
fi

##############################################################################
#                          Programmable Completion                           #
##############################################################################

if [ "$enable_programmable_completion" == true ] ; then

  # Ignore case on auto-completion
  # Note: bind used instead of sticking these in .inputrc
  if [[ $iatest > 0 ]]; then bind "set completion-ignore-case on"; fi

  # Show auto-completion list automatically, without double tab
  if [[ $iatest > 0 ]]; then bind "set show-all-if-ambiguous On"; fi

  # Enable auto-complete for programs
  if ! shopt -oq posix; then
    if [ -f /usr/share/bash-completion/bash_completion ]; then
      . /usr/share/bash-completion/bash_completion
    elif [ -f /etc/bash_completion ]; then
      . /etc/bash_completion
    fi
  fi

  shopt -s extglob

  complete -A hostname   rsh rcp telnet rlogin ftp ping disk
  complete -A export     printenv
  complete -A variable   export local readonly unset
  complete -A enabled    builtin
  complete -A alias      alias unalias
  complete -A function   function
  complete -A user       su mail finger

  complete -A helptopic  help     # Currently same as builtins.
  complete -A shopt      shopt
  complete -A stopped -P '%' bg
  complete -A job -P '%'     fg jobs disown

  complete -A directory  mkdir rmdir
  complete -A directory   -o default cd

  # Compression
  complete -f -o default -X '*.+(zip|ZIP)'  zip
  complete -f -o default -X '!*.+(zip|ZIP)' unzip
  complete -f -o default -X '*.+(z|Z)'      compress
  complete -f -o default -X '!*.+(z|Z)'     uncompress
  complete -f -o default -X '*.+(gz|GZ)'    gzip
  complete -f -o default -X '!*.+(gz|GZ)'   gunzip
  complete -f -o default -X '*.+(bz2|BZ2)'  bzip2
  complete -f -o default -X '!*.+(bz2|BZ2)' bunzip2
  complete -f -o default -X '!*.+(zip|ZIP|z|Z|gz|GZ|bz2|BZ2)' extract


  # Documents - Postscript,pdf,dvi.....
  complete -f -o default -X '!*.+(ps|PS)'  gs ghostview ps2pdf ps2ascii
  complete -f -o default -X \
  '!*.+(dvi|DVI)' dvips dvipdf xdvi dviselect dvitype
  complete -f -o default -X '!*.+(pdf|PDF)' acroread pdf2ps
  complete -f -o default -X '!*.@(@(?(e)ps|?(E)PS|pdf|PDF)?\
  (.gz|.GZ|.bz2|.BZ2|.Z))' gv ggv
  complete -f -o default -X '!*.texi*' makeinfo texi2dvi texi2html texi2pdf
  complete -f -o default -X '!*.tex' tex latex slitex
  complete -f -o default -X '!*.lyx' lyx
  complete -f -o default -X '!*.+(htm*|HTM*)' lynx html2ps
  complete -f -o default -X \
  '!*.+(doc|DOC|xls|XLS|ppt|PPT|sx?|SX?|csv|CSV|od?|OD?|ott|OTT)' soffice

  # Multimedia
  complete -f -o default -X \
  '!*.+(gif|GIF|jp*g|JP*G|bmp|BMP|xpm|XPM|png|PNG)' xv gimp ee gqview
  complete -f -o default -X '!*.+(mp3|MP3)' mpg123 mpg321
  complete -f -o default -X '!*.+(ogg|OGG)' ogg123
  complete -f -o default -X \
  '!*.@(mp[23]|MP[23]|ogg|OGG|wav|WAV|pls|\
  m3u|xm|mod|s[3t]m|it|mtm|ult|flac)' xmms
  complete -f -o default -X '!*.@(mp?(e)g|MP?(E)G|wma|avi|AVI|\
  asf|vob|VOB|bin|dat|vcd|ps|pes|fli|viv|rm|ram|yuv|mov|MOV|qt|\
  QT|wmv|mp3|MP3|ogg|OGG|ogm|OGM|mp4|MP4|wav|WAV|asx|ASX)' xine

  complete -f -o default -X '!*.pl'  perl perl5

  #  This is a 'universal' completion function - it works when commands have
  #+ a so-called 'long options' mode , ie: 'ls --all' instead of 'ls -a'
  #  Needs the '-o' option of grep
  #+ (try the commented-out version if not available).

  #  First, remove '=' from completion word separators
  #+ (this will allow completions like 'ls --color=auto' to work correctly).

  COMP_WORDBREAKS=${COMP_WORDBREAKS/=/}

  _get_longopts()
  {
    #$1 --help | sed  -e '/--/!d' -e 's/.*--\([^[:space:].,]*\).*/--\1/'| \
    #grep ^"$2" |sort -u ;
      $1 --help | grep -o -e "--[^[:space:].,]*" | grep -e "$2" |sort -u
  }

  _longopts()
  {
      local cur
      cur=${COMP_WORDS[COMP_CWORD]}

      case "${cur:-*}" in
         -*)      ;;
          *)      return ;;
      esac

      case "$1" in
         \~*)     eval cmd="$1" ;;
           *)     cmd="$1" ;;
      esac
      COMPREPLY=( $(_get_longopts ${1} ${cur} ) )
  }
  complete  -o default -F _longopts configure bash
  complete  -o default -F _longopts wget id info a2ps ls recode

  _make()
  {
      local mdef makef makef_dir="." makef_inc gcmd cur prev i;
      COMPREPLY=();
      cur=${COMP_WORDS[COMP_CWORD]};
      prev=${COMP_WORDS[COMP_CWORD-1]};
      case "$prev" in
          -*f)
              COMPREPLY=($(compgen -f $cur ));
              return 0
              ;;
      esac;
      case "$cur" in
          -*)
              COMPREPLY=($(_get_longopts $1 $cur ));
              return 0
              ;;
      esac;

      # ... make reads
      #          GNUmakefile,
      #     then makefile
      #     then Makefile ...
      if [ -f ${makef_dir}/GNUmakefile ]; then
          makef=${makef_dir}/GNUmakefile
      elif [ -f ${makef_dir}/makefile ]; then
          makef=${makef_dir}/makefile
      elif [ -f ${makef_dir}/Makefile ]; then
          makef=${makef_dir}/Makefile
      else
         makef=${makef_dir}/*.mk         # Local convention.
      fi

      #  Before we scan for targets, see if a Makefile name was
      #+ specified with -f.
      for (( i=0; i < ${#COMP_WORDS[@]}; i++ )); do
          if [[ ${COMP_WORDS[i]} == -f ]]; then
              # eval for tilde expansion
              eval makef=${COMP_WORDS[i+1]}
              break
          fi
      done
      [ ! -f $makef ] && return 0

      # Deal with included Makefiles.
      makef_inc=$( grep -E '^-?include' $makef |
                   sed -e "s,^.* ,"$makef_dir"/," )
      for file in $makef_inc; do
          [ -f $file ] && makef="$makef $file"
      done

      #  If we have a partial word to complete, restrict completions
      #+ to matches of that word.
      if [ -n "$cur" ]; then gcmd='grep "^$cur"' ; else gcmd=cat ; fi

      COMPREPLY=( $( awk -F':' '/^[a-zA-Z0-9][^$#\/\t=]*:([^=]|$)/ \
                                 {split($1,A,/ /);for(i in A)print A[i]}' \
                                  $makef 2>/dev/null | eval $gcmd  ))

  }

  complete -F _make -X '+($*|*.[cho])' make gmake pmake

  _killall()
  {
      local cur prev
      COMPREPLY=()
      cur=${COMP_WORDS[COMP_CWORD]}

      #  Get a list of processes
      #+ (the first sed evaluation
      #+ takes care of swapped out processes, the second
      #+ takes care of getting the basename of the process).
      COMPREPLY=( $( ps -u $USER -o comm  | \
          sed -e '1,1d' -e 's#[]\[]##g' -e 's#^.*/##'| \
          awk '{if ($0 ~ /^'$cur'/) print $0}' ))

      return 0
  }

  complete -F _killall killall killps
fi

PATH=$PATH:$HOME/.local/bin # Add custom bins to PATH
