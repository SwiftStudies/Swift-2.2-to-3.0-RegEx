# Swift-2.2-to-3.0-RegEx
A simple set of regular expressions that make migrating from 2.2 to 3.0 easy

## Replacing 'standard' C-style for loops
Regular Expression  
    for[ \t]+var[ \t]+(i)[ \t]*=[ \t]*([\d]+|[:alnum:]+)[ \t]*;[ \t]*\1[ \t]*<[ \t]*([\d]+|[:alnum:]+)[ \t]*;[ \t]*\1\+\+

Replace with  
    for var $1 in $2..<$3

