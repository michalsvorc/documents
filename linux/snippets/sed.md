# sed

## Remove empty lines

```console
$ sed -i -- '/^\s*$/d' `find . -maxdepth 1 -type f ! -name '<filename>'`
```
