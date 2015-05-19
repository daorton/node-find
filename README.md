Because I can never remember the Linux find command syntax - requires node.js but no module dependencies.

Run as `node ff` or just `ff` from the shell.

```
usage: ff [options] dir1...
Find files satisfying a set of files and perform an action - like find with simplified syntax

 Filters:
  -name regex,  -^name regex    file name matches regex 
  -fname regex, -^fname regex   full path matches regex    
  -type regex,  -^type regex    entry type matches regex (types are 1 char in [fdlbcps])    
  -mtime time,  -^mtime time    modify time <= time    
  -atime time,  -^atime time    access time <= time  
  -ctime time,  -^ctime time    change / create time <= time  
  -btime time,  -^btime time    birth time <= time (see node fs.Stats) 
  -size size,   -^size size     file size <= size   
  -user regex,  -^user regex    file owner user / user ID matches regex  
  -group regex, -^group regex   file owner group / group ID matches regex   
  -perm regex,  -^perm regex    file permissions string / octal string matches regex  
  -suid,        -^suid          file has suid bit set
  -guid,        -^guid          file has guid bit set
  -sticky,      -^sticky        file has sticky bit set
 Modifiers:
  -i                            any regex's that follow are case insensitive  
  -e                            any access or line too long (grep) errors are silently ignored    
 Actions:
  -print                        print full path (default action) 
  -print0                       print full path with \0 separator for xargs
  -ls                           print ls type listing
  -stat                         print raw stat result in JSON format 
  -grep regex                   print lines in file matching regex   

 - regex "matches" means "contains" - use regex ^ and $ for beginning and end of string 
 - watch out for shell wildcards / globbing - safest to put regex in quotes 
 - regex chars used literally, e.g. "." need to be escaped ("any" char vs "period") 
 - time is a numeric value in seconds, numeric value can have a final m, h, d for minutes, hours, or days 
 - size is a numeric value in bytes, numeric value can have a final k, m, g for thousand, mega, or giga bytes 
 - permission is string like rwxrwxr-x or 775; a regex matching either will activate the filter 
 - user and group regex can match the string or numeric value to activate the filter 
 - all options, modifiers, actions, and dirs can be specified in any order; filters all must be satisfied to fire action 
 - find style "xdev" is default, i.e. don't descend dirs on other file systems 
 - linux getent command is spawned to get user and group names from system when needed 

 Examples:
  ff ~ -mtime 3m -type f -name '\.(js|cc|dart)$' -ls    # modified last 3 minutes, "file", extension is .js, .cc, or .dart 
  ff / -^user '(dave|0)' -ls -e                         # find files or dirs with owners other than dave or root (0), skip access errors 
  ff . -fname '/obj$' -type d -print0 | xargs -0 rm -rf # rm dirs containing path element "obj" 
  ff ~ -^size 10m -ls                                   # files with size > 10 000 000 bytes 
  ff ~ -size 0 -ls                                      # files with size == 0 bytes 
  ff ~ -type l -ls                                      # show links 
  ff ~ -type f -i -grep sqlite_busy                     # show lines in files containing case-insensitive SQLITE_BUSY 
 
```