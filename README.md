# simonmedia
SimonMedia is a minimalist yet powerful low latency streaming server that supports rtmp/srt/webRTC streaming, rtmp/srt/webRTC/http | ws flv/http | ws fmp4/hls-fmp4 streaming, fmp4 recording,real-time screenshot, and transcoding
# srt
video support h264/h265/AV1  
audio support PCMA/PCMU/AAC/OPUS
## push
ffmpeg -rtsp_transport tcp -re -i rtsp://username:password@ip:port/xx -c:v libx264 -c:a pcm_alaw -ar 8k -ac 1 -g 50 -pes_payload_size 0 -f mpegts srt://127.0.0.1:1936?streamid=live/test10,m=publish  
ffmpeg -rtsp_transport tcp -re -i rtsp://username:password@ip:port/xx -c:v libx264 -c:a libopus -ar 48k -ac 2 -bf 0 -g 50 -pes_payload_size 0 -f mpegts srt://127.0.0.1:1936?streamid=live/test10,m=publish  
ffmpeg -rtsp_transport tcp -re -i rtsp://username:password@ip:port/xx -c:v libaom-av1 -g 50 -c:a libopus -ar 48k -ac 2 -cpu-used 8 -row-mt 1 -tile-columns 2 -tile-rows 2 -pix_fmt yuv420p -f mpegts srt://127.0.0.1:1936?streamid=live/test10,m=publish
## pull
srt://127.0.0.1:1936?streamid=live/test10,m=subscribe
# RTMP
video support h264/h265/AV1  
audio support PCMA/PCMU/AAC/OPUS
## push
ffmpeg -rtsp_transport tcp -re -i rtsp://username:password@ip:port/xx -c:v libx264 -c:a pcm_alaw -ar 8k -ac 1 -g 50 -f flv rtmp://127.0.0.1:1935/live/test10  
ffmpeg -rtsp_transport tcp -re -i rtsp://username:password@ip:port/xx -c:v libx264 -c:a libopus -ar 48k -ac 2 -bf 0 -g 50 -f flv rtmp://127.0.0.1:1935/live/test10  
ffmpeg -rtsp_transport tcp -re -i rtsp://username:password@ip:port/xx -c:v libaom-av1 -g 50 -c:a libopus -ar 48k -ac 2 -cpu-used 8 -row-mt 1 -tile-columns 2 -tile-rows 1 -pix_fmt yuv420p -flags +global_header -f flv rtmp://127.0.0.1:1935/live/test10
## pull
rtmp://127.0.0.1:1935/live/test10
# WebRTC
video support h264/h265/AV1  
audio support PCMA/PCMU/OPUS
## push
ffmpeg -rtsp_transport tcp -re -i rtsp://username:password@ip:port/xx -c:v libx264 -c:a libopus -ar 48k -ac 2 -bf 0 -g 50 -ts_buffer_size 1048576 -f whip http://127.0.0.1:9999/webrtc/whip?streamId=test10  
ffmpeg -rtsp_transport tcp -re -i rtsp://username:password@ip:port/xx -c:v libaom-av1 -g 50 -c:a libopus -ar 48k -ac 2 -cpu-used 8 -row-mt 1 -tile-columns 2 -tile-rows 2 -pix_fmt yuv420p -ts_buffer_size 1048576 -f whip http://127.0.0.1:9999/webrtc/whip?streamId=test10
## pull
http://127.0.0.1:9999/webrtc/whep?streamId=test10
# Usage
Extract stream_server.7z  
linux use stream_server,windows use stream_server.exe  
./stream_server -config=./config.yml  
webUI: open http://127.0.0.1:9999 in browser  
## play url
http|ws-flv  
(http|ws)://127.0.0.1:9999/flv/test10.flv  
http|ws-fmp4  
(http|ws)://127.0.0.1:9999/fmp4/test10.mp4  
hls-fmp4  
http://127.0.0.1:9999/hls/fmp4/test10.m3u8  
webRTC  
http://127.0.0.1.200:9999/webrtc/whep?streamId=test10  
rtmp  
rtmp://127.0.0.1:1935/live/test10  
srt  
srt://127.0.0.1:1936?streamid=live/test10,m=subscribe  
## playback url
http://127.0.0.1:9999/hls/vod/fmp4/test10.m3u8?startTime=20260123210000&endTime=20260124210000  
## Real-time screenshot
http://127.0.0.1:9999/picture/screenshot?streamId=test10