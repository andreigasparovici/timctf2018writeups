Holidays
=====

* Tools used: MonoDevelop, dotPeek

First, we decompiled the given executable using dotPeek by JetBrains, since it was a .NET Windows executable and we got the following code: [view code](https://pastebin.com/1Q54SJiX).

The first day of the holiday in Romania is 2018.6.16, so we changed ```DateTime.UtcNow``` in the __password__ variable with it.

Recompiling the code and running it (using MonoDevelop) gave us:

```
timctf{4_V3n17_v4c4nt4_M4r3}
```
