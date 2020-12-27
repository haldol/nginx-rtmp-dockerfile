NGINX RTMP Dockerfile
=====================

This Dockerfile installs NGINX configured with `nginx-rtmp-module`, ffmpeg
and some default settings for HLS live streaming.

**Note: in the current state, this is just an experimental project to play with
RTMP and HLS.**


How to use
----------

0. Clone this repository, open command prompt or powershell or your favorite
   linux shell to that folder

1. Build and run the container (`docker build -t nginx_rtmp .` &
   `docker run -p 1935:1935 -p 8080:80 --rm nginx_rtmp`).

2.1  For RTMP in to HLS trascoded out:
   Stream your live content to `rtmp://localhost:1935/encoder/stream_name` where
   `stream_name` is the name of your stream.

   -- In Safari, VLC or any HLS compatible browser / player, open
   `http://localhost:8080/hls/stream_name.m3u8`. Note that the first time,
   it might take a few (10-15) seconds before the stream works. This is because
   when you start streaming to the server, it needs to generate the first
   segments and the related playlists.

2.2   For RTMP Push in and RTMP Pull out:
   Stream your live content to `rtmp://localhost:1935/big/stream_name` where
   `stream_name` is the name of your stream

   -- In your RTMP Pull tool (vMix, whatever else), open `rtmp://localhost:1935/small/stream_name`
   and take in whatever is being pushed on `/big/stream_name` as a 720p stream.

** If you don't wanna do 720, or want to change the names of these endpoints, or
   delete some of them, edit the nginx.conf file, and rerun step 1.



Links
-----

* http://nginx.org/
* https://github.com/arut/nginx-rtmp-module
* https://www.ffmpeg.org/
* https://obsproject.com/
