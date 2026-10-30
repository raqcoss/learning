# Easy Phython
## Strings
### String Formatting with `%`
The `%` operator after the string is used to combine a string with variables. The `%` operator will replace the `%s` in the string with the string variable that comes after it.

If you’d like to print a variable that is an integer, you can “pad” it with zeros using `%02d`. The `0` means “pad with zeros”, the `2` means to pad to 2 characters wide, and the `d` means the number is a signed integer (can be positive or negative).

```
day = 6
print "03 - %s - 2019" %  (day)
# 03 - 6 - 2019
print "03 - %02d - 2019" % (day)
# 03 - 06 - 2019

g = "Golf"
h = "Hotel"
print "%s, %s" % (g, h)
```
## Date and Time

```
from datetime import datetime
datetime.now()
# 2023-10-24 17:19:24.602167
now = datetime.now()

print now.year
print now.month
print now.day
print now.hour
print now.minute
print now.second


```
### mm/dd/yyyy Format
```
print '%02d/%02d/%04d' % (now.month, now.day, now.year)
```


