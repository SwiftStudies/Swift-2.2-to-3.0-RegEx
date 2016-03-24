# Swift-2.2-to-3.0-RegEx
A simple set of regular expressions that make migrating from 2.2 to 3.0 easy by running a project wide find and replace with regular expressions (see [this blog post](2016/3/23/quickly-dealing-with-swift-30s-removal-of-and-c-style-for-loops) for details if you aren't sure how to do that). Essentially this will save you from having to use XCode's fix-it's one at a time. 

These have been listed in order you should apply (for example, the more complex c-style for loop replacements first, before you get to simpler uses of ++ and --. 

If you have any improvements or additions, please fork and create a pull request. I would love to receive other contributions. 

## Replacing 'standard' C-style for loops
Regular Expression: `for[ \t]+var[ \t]+(i)[ \t]*=[ \t]*([\d]+|[:alnum:]+)[ \t]*;[ \t]*\1[ \t]*<[ \t]*([\d]+|[:alnum:]+)[ \t]*;[ \t]*\1\+\+`

Replace with `for var $1 in $2..<$3`

For example
```
  for var i=0;i<10;i++{
```

Would become
```
  for i in 0..<10{
```
  
## Replacing ++/--\<var> in parameters
Regular Expression: `(^[ \t]*[:alnum:]+)(\(|,)[ \t]*([\+-]){2}([:alnum:]+)`

Replace with `$4$3=1\n$1$2$4`

For example
```
  someFunction(++i,other)
```

Would become
```
  i+=1
  someFunction(i,other)
```

## Replacing \<var>++/-- in inline code
Regular Expression: `([:alnum:]+)([\+-]){2}`

Replace with `$1$2=1`

For example
```
  i++
```

Would become
```
  i+=1
```

## Replace ++/--\<var> in free space
Regular Expression: `^[ \t]*([\+-]){2}([:alnum:]+)`

Replace with `$2$1=1`

For example
```
  ++i
```  
Would become
```
  i+=1
```
