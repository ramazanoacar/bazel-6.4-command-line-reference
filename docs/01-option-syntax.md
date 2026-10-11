## Option Syntax

Options can be passed to Bazel in different ways. Options that require a value
can be passed with either an equals sign or a space:

```
--<option>=<value>
--<option> <value>
```

Some options have a single character short form; in that case, the short form
has to be passed with a single dash and a space.

```
-<short_form> <value>
```

Boolean options can be enabled as follows:

```
--<option>
--<option>=[true|yes|1]
```

and disabled as follows:

```
--no<option>
--<option>=[false|no|0]
```

Tristate options are usually set to automatic by default, and can be
force-enabled as follows:

```
--<option>=[true|yes|1]
```

or force-disabled as follows:

```
--no<option>
--<option>=[false|no|0]
```
