![Bash Script Generator](https://cloud.githubusercontent.com/assets/9037816/22258834/0b837816-e231-11e6-971f-f2dd9b940e21.png)
# Bash Script Generator
Generates a Bash Script Template that handles Arguments and Flags Cleanly.

This GitHub Repository can be found at [bit.ly/bash-script-generator](http://bit.ly/bash-script-generator), and is released under the GNU v3 License, so hack away as long as you keep it open-source. To access the generator script directly, a convenient short link is provided: [bit.ly/generate-bash-script](http://bit.ly/generate-bash-script).

**Authored by: [Will Salemé](https://github.com/wsaleme)**

## Features
The following features are supported:

- Single dash and double dash options (`-d` OR `--date`)
- Boolean options (`-p` without a value)
- Compounded options (`-dpi` translates to `-d`, `-p` and `-i`)
- Multiple options exported in arrays (`--date foo1 --date foo2 --date foo3` exports to `"foo1", "foo2", etc`)
- Custom Methods
- Catch-all Method
- Arguments passed to custom methods

## Running the Generator
To run the generator you simply execute the command below from your terminal:

```
curl -Ls http://bit.ly/generate-bash-script | sh > ScriptFilename.sh
```

## Configuring the Generated Template
There will be a few options for you to configure the generated template, below is the reference:

### Script Name
`SCRIPT_NAME`

Displayed in the Help Message and Version Message.

### Script Version
`SCRIPT_VER`

Displayed in the Version Message.

### Script Options
`SCRIPT_OPTS`

This is where you will configure the script options/flags. This is provided by a compounded array `SCRIPT_OPTS`, where each array value contains the matching pattern and the variable name under which the provided value will be exported.

**Options Format:**

The `SCRIPT_OPTS` is an array who's keys are as follows: `<regex>:<varname>`

The first part before the colon is a standard Regex to match against the given options, i.e. `(-d|--date)` will match either `-d` or `--date` — you can append as many patterns as you want using the OR operator `|`.

The second part after the colon is the key used as the variable name. This name will be exported as `OPTS_<varname>`, i.e. `OPTS_DATE` in the case of a date option.

A complete example of this: `(-d|--date):DATE`

*Remember: Arrays in Bash are delimited with a space, i.e. `ARRAY=("foo" "bar" "baz")`*

**Important:** Options that are provided as `boolean` flag, i.e. no value is provided other than the flag itself, will be exported with the value of variable name. For example `OPTS_PUBLISH` will have the value `"OPTS_PUBLISH"`, this will let you know when you're provided `true` vs the `boolean` flag alone.

### Script Catch All
`SCRIPT_CATCHALL`

This will enable/disable the catch all method. Normally, you'd have to specify a script method, i.e. `script [options] operation [args]` but you may also want to skip the `operation` and simply execute `script [options] [args]` in which case you'd enable the Catch-All Option.

This will only accept `yes` or `no` for a value, otherwise, it defaults to disabling the Catch-All Method.

## Script Autocompletion
This script is equipped with an autocomplete helper method. Simply execute `<scriptname> generate-autocomplete` to generate an autocomplete script. This utilizes the `<scriptname> methods` method to get a list of all available methods/operations.

### Sourcing the Autocomplete Script
For the autocomplete to function, you will need to source it into your bash session, best place to do this is in your `~/.profile` by simply including `source path/to/autocomplete/script` and restarting your bash session. You may also include it in `/etc/profile` to provide it all users, although not recommended unless you know what you're doing.

*Notice: For autocompletion to operate properly, you MUST NOT start your method names with an underscore (`_`) as they're considered internal methods and will be omitted from method list.*

## To Do List
I'd like to see these implemented in the near future:

- Accepting compounded flags like `-dp` as `-d` and `-p` separately

## License and Disclaimer
This software is provided as-is and no warranties or guaranties are provided by the author. Use at your own risk. Distributed under the GNU v3 Open Source License.
