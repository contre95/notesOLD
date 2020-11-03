# Regular Expression

### Most common character matches

* `.` -> Matches any character

* `/.` ->  the `.` character

* `/W` ->  any non-word character.

* `\w` ->  any word character.

* `\d` -> a digit character

* `\D` -> any non-digit character

* `^` ->  the position at the start of a string

  ​	`^123` on *1235123* will match **123**5123

* `$` -> the position at the end of a string

  ​	`123$` on *1235123* will match 1235**123**

  ###	Example

  To match the patter "*Xxxxx*." Where "x" denotes a word character, and X denotes a digit. The string must start with a digit and end with "." 

  Then the Regular expression should be -> "**^\d\w\w\w\w\.$**"

  

