FFmpeg README
=============

FFmpeg is a collection of libraries and tools to process multimedia content
such as audio, video, subtitles and related metadata.

## Extensions by NodeMedia
* FLV support vp8 id=10
* FLV support vp9 id=11
* FLV support opus id=13

### Build from source
```
./configure --enable-small --disable-doc --enable-libsrt --enable-libfreetype \
  --enable-libspeex --enable-libx264 --enable-libx265 --enable-libvpx --enable-libopus \
  --enable-openssl --enable-gpl --enable-nonfree --enable-version3
```

### Examples of encoding parameters in action
The following shows CPU utilization at 25 fps for various frame sizes on a quad-core i5 3.6Ghz desktop running Linux:
|  Target Resolution| FFmpeg VP9 Parameters   | CPU / Speed (example)   |
| ------------ | ------------ | ------------ |
|3840x2160 (2160p)	|-r 30 -g 90 -s 3840x2160 -quality realtime -speed 5 -threads 16 -row-mt 1 -tile-columns 3 -frame-parallel 1 -qmin 4 -qmax 48 -b:v 7800k |	~88% 0.39x|
|2560x1440 (1440p)	|-r 30 -g 90 -s 2560x1440 -quality realtime -speed 5 -threads 16 -row-mt 1 -tile-columns 3 -frame-parallel 1 -qmin 4 -qmax 48 -b:v 6000k	|~86% 0.68x|
|1920x1080 (1080p)	|-r 30 -g 90 -s 1920x1080 -quality realtime -speed 5 -threads 8 -row-mt 1 -tile-columns 2 -frame-parallel 1 -qmin 4 -qmax 48 -b:v 4500k	|~82% 1.04x|
|1280x720 (720p)|	-r 30 -g 90 -s 1280x720 -quality realtime -speed 5 -threads 8 -row-mt 1 -tile-columns 2 -frame-parallel 1 -qmin 4 -qmax 48 -b:v 3000k	|~78% 1.77x|
|854x480 (480p)	|-r 30 -g 90 -s 854x480 -quality realtime -speed 6 -threads 4 -row-mt 1 -tile-columns 1 -frame-parallel 1 -qmin 4 -qmax 48 -b:v 1800k	|~64% 3.51x|
|640x360 (360p)|	-r 30 -g 90 -s 640x360 -quality realtime -speed 7 -threads 4 -row-mt 1 -tile-columns 1 -frame-parallel 0 -qmin 4 -qmax 48 -b:v 730k	|~62% 5.27x|
|426x240 (240p)	|-r 30 -g 90 -s 426x240 -quality realtime -speed 8 -threads 2 -row-mt 1 -tile-columns 0 -frame-parallel 0 -qmin 4 -qmax 48 -b:v 365k	|~66% 8.27x|

An example FFmpeg might look like this:
```
ffmpeg -re -i /home/id3as/Videos/demo.mp4 \
  -r 30 -g 90 -s 1280x720 -quality realtime -speed 5 -threads 8 -row-mt 1 \
  -tile-columns 2 -frame-parallel 1 -qmin 4 -qmax 48 -b:v 3000k -c:v vp9 \
  -b:a 128k -c:a libopus -f flv rtmp://192.168.0.2/live/demo
```

## Libraries

* `libavcodec` provides implementation of a wider range of codecs.
* `libavformat` implements streaming protocols, container formats and basic I/O access.
* `libavutil` includes hashers, decompressors and miscellaneous utility functions.
* `libavfilter` provides means to alter decoded audio and video through a directed graph of connected filters.
* `libavdevice` provides an abstraction to access capture and playback devices.
* `libswresample` implements audio mixing and resampling routines.
* `libswscale` implements color conversion and scaling routines.

## Tools

* [ffmpeg](https://ffmpeg.org/ffmpeg.html) is a command line toolbox to
  manipulate, convert and stream multimedia content.
* [ffplay](https://ffmpeg.org/ffplay.html) is a minimalistic multimedia player.
* [ffprobe](https://ffmpeg.org/ffprobe.html) is a simple analysis tool to inspect
  multimedia content.
* Additional small tools such as `aviocat`, `ismindex` and `qt-faststart`.

## Documentation

The offline documentation is available in the **doc/** directory.

The online documentation is available in the main [website](https://ffmpeg.org)
and in the [wiki](https://trac.ffmpeg.org).

### Examples

Coding examples are available in the **doc/examples** directory.

## License

FFmpeg codebase is mainly LGPL-licensed with optional components licensed under
GPL. Please refer to the LICENSE file for detailed information.

## Contributing

Patches should be submitted to the ffmpeg-devel mailing list using
`git format-patch` or `git send-email`. Github pull requests should be
avoided because they are not part of our review process and will be ignored.
