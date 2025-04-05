##### **Identifying Commands**
**type**—Display a Command’s Type
The type command is a shell builtin that displays the kind of command the
shell will execute

**which**—Display an Executable’s Location
==Sometimes there is more than one version of an executable program installed on a system. ==
 mostly needed on larger servers. To determine the exact location of a given executable, the which command is used.
> [!NOTE] which command 
which works only for **executable programs**, **not builtins or aliases** that
are substitutes for actual executable programs. When we try to use which on
a shell builtin—for example, cd—we either get **no response** or get an **error**
message.
