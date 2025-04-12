
```docker run -d ubuntu:14.04 /bin/bash -c "while true; do echo hello  world;done"

bash interprets the following options when it is invoked:
-c string,If the -c option is present, then commands are read from string. If there are arguments after the string, they are assigned to the positional parameters, starting with $0.

Without the `-c`, the `"while true..."` string is taken to be a filename for `bash` to open.
