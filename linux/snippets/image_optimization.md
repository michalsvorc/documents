# Image optimization

## JPG

```console
$ jpegoptim --strip-all <input>.jpg
```

Recursive:

```console
$ find ./ -type f \( -name "*.jpg" -o -name "*.jpeg" \) -exec jpegoptim --strip-all {} \;
```

## PNG

```console
$ optipng -o7 -fix <input>.png
```

Recursive:

```console
$ find ./ -type f -name "*.png" -exec optipng -o7 -fix {} \;
```

