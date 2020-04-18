### Load values from properties file
* Use @value annotation for initializing value from properties file.

```
properties file -

value.from.file=Value got from the file
priority=Properties file
listOfValues=A,B,C

At Java -
@Value("${value.from.file}")
private String valueFromFile;
```
