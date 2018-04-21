Foreign Language
=====
* Tools used: Virtual Box, Python
* We won't need to do any reverse on the executable, we could look at few outputs of the program and the rules will pop up immediatly:
    1. Reverse the input (`abc123` -> `321cba`)
    2. Split the resulted string in chunks of two and swap the members (`32|1c|ba` -> `23|c1|ab` -> `23c1ab`)
    3. Iterate over the string, if the charater is a letter add a random letter after it, else double the character (`2233c?11a?b?`, where `?` is a random char)
We write a Python script to reverse the algorithm and we got the flag.
