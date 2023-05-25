# Images

## JPG

- [jpegoptim](https://github.com/tjko/jpegoptim)

```shell
jpegoptim --strip-all <input>.jpg
```

## PNG

- [pngquant](https://pngquant.org/)

```shell
pngquant --quality=65-80 <input>.png
```

min and max are numbers in range 0 (worst) to 100 (perfect), similar to JPEG.

- [optipng](https://optipng.sourceforge.net/)

```shell
optipng -o7 -fix <input>.png
```

## Converting

- [Imagemagick](https://imagemagick.org) provides `convert` command.

Convert to PDF:

```shell
convert -resize 800x600 <input>.jpg <output>.pdf
```




