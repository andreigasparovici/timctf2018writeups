Strange behaviour
=====

* Tools used: unzip, binwalk, grep

After extracting the archive, a quick analysis with binwalk on the given file gives:

```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
86016         0x15000         JPEG image data, JFIF standard 1.02
124928        0x1E800         JPEG image data, JFIF standard 1.01
516096        0x7E000         JPEG image data, JFIF standard 1.01
3240397       0x3171CD        MySQL ISAM index file Version 4
6881280       0x690000        Zip archive data, at least v2.0 to extract, name: _rels/.rels
6881561       0x690119        Zip archive data, at least v2.0 to extract, name: docProps/app.xml
6881858       0x690242        Zip archive data, at least v2.0 to extract, name: docProps/core.xml
6882276       0x6903E4        Zip archive data, at least v2.0 to extract, name: xl/_rels/workbook.xml.rels
6882558       0x6904FE        Zip archive data, at least v2.0 to extract, name: xl/workbook.xml
6883122       0x690732        Zip archive data, at least v2.0 to extract, name: xl/styles.xml
6883922       0x690A52        Zip archive data, at least v2.0 to extract, name: xl/worksheets/_rels/sheet1.xml.rels
6884284       0x690BBC        Zip archive data, at least v2.0 to extract, name: xl/worksheets/sheet1.xml
6885858       0x6911E2        Zip archive data, at least v2.0 to extract, name: xl/sharedStrings.xml
6886682       0x69151A        Zip archive data, at least v2.0 to extract, name: [Content_Types].xml
6887716       0x691924        End of Zip archive

```

We extracted the files and ran an recursive grep:

```sh
grep -rl "timctf" .
```

and we found that the file containing the flag is xl/sharedStrings.xml

```sh
cat xl/sharedStrings.xml | grep timctf
```

This produced the flag:

```
timctf{d0nt_f0rg3t_t0_h4v3_fun}
```
