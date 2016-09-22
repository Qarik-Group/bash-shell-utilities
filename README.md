# bash-shell-utilities

This repository contains reusable shell modules. They are designed to be included into other scripts.


## Semanic Versioning Parsing and Comparing functions

The script follows the semantic versioning 2.0.0 specification.

### shl_semver

####vn_Parse

inputs: semanic-versioning-string  result-array-name

returns a string that contains an array declaration with 3 elements (version, prerelease, build)  
        use eval on the string to get the array into your scope

status code 0 for success  
1 for parsing error

Example:

    ```sh
        local _result _array _parts
        _array="$(vn_Parse "${_input}" "_parts")"
        _result=$?
        eval "${_array}"
    ```

####vn_Compare
    The compare function compares the version and if the prelease exists then it gets compared to.
    inputs: semanic-versioning-string1  semanic-versioning-string2
    returns status codes only

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
