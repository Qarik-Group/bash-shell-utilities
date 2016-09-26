# bash-shell-utilities

This repository contains reusable shell modules. They are designed to be included into other scripts.


## Semanic Versioning Parsing and Comparing functions

The script follows the semantic versioning 2.0.0 specification.

### shl_semver

#### vn_Parse

<dl>
<dt>inputs</dt>
<dd>semanic-versioning-string  result-array-name</dd>
</dl>

<dl>
<dt>returns</dt>
<dd>A string that contains an array declaration with 3 elements (version, prerelease, build)
<br/>use eval on the string to get the array into your scope
<br/><b><i>status codes</i></b>
<br/><b>0</b> for success
<br/><b>1</b> for parsing error
</dd>
</dl>


Example:

```sh
        local _result _array _parts
        _array="$(vn_Parse "${_input}" "_parts")"
        _result=$?
        eval "${_array}"
```

#### vn_Compare
The compare function compares the version and if the prerelease exists then it gets compared to. The prelease field can be with or without case sensitiviity.

<dl>
<dt>inputs</dt>
<dd>semanic-versioning-string1
semanic-versioning-string2
[sensitive|insensitive]
</dd>
</dl>

<dl>
<dt>returns</dt>
<dd>
<b><i>status codes only</i></b>
<br/><b>0</b> - versions strings are equal
<br/><b>1</b> - version string 1 is greater than version string 2
<br/><b>2</b> - version string 1 is less than version string 2
<br/><b>254</b> - semantic versioning string parsing error
<br/><b>255</b> - Argument count is incorrect
</dl>

```sh
    vn_Compare "$1" "$2"
    case $? in
        0) op='=';;
        1) op='>';;
        2) op='<';;
      254) op='~';;  # semantic versioning string parsing error
      255) op='!';;  # Argument count is incorrect
    esac
```

The test_shl_semver is the testing function where you can run and see examples.
