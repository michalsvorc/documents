# ffmpeg

- [Encoding - mpabo.com](http://www.mpabo.com/2014/12/14/ffmpeg-and-x264-encoding-guide/)

## Print video metadata

```console
$ ffprobe <input-video>
```

## webm

- [Encoding - pcode.nl](https://encrypted.pcode.nl/blog/2010/10/17/encoding-webm-using-ffmpeg/)

```console
$ ffmpeg -i <input> -s 1280x720 -preset slow -b 3900k -pass 1 -an -f webm -y <output>.webm
$ ffmpeg -i <input> -s 1280x720 -preset slow -b 3900k -pass 2 -acodec libvorbis -ab 100k -f webm -y <output>.webm
```

## mp4

```console
$ ffmpeg -i <input> -acodec aac -strict experimental -ac 2 -ab 128k -vcodec libx264 -preset slow -f mp4 -crf 22 -s 640x360 <output>.mp4
```

## ogg (if you want to support older Firefox)

```console
$ ffmpeg2theora <input> -o <output>.ogv -x 640 -y 360 --videoquality 5 --audioquality 0  --frontend
```

## Get screenshot at a given time

```console
$ ffmpeg -ss 01:23:45 -i input -vframes 1 -q:v 2 output.jpg
```
