# whisper.cpp Windows binary w/ Vulkan GPU support

Get `whisper.cpp-windows-vulkan.zip` from the [Releases page](https://github.com/jerryshell/whisper.cpp-windows-vulkan-bin/releases)

More usage: [ggml-org/whisper.cpp](https://github.com/ggml-org/whisper.cpp)

## Example: download and transcribe YouTube video

Using bash command

## Download video

```shell
yt_vod_url="https://www.youtube.com/watch?v=UF8uR6Z6KLc";
yt-dlp \
    -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best" \
    -o "video/1.mp4" \
    --no-simulate \
    --no-write-auto-subs \
    --restrict-filenames \
    --embed-thumbnail \
    --embed-chapters \
    --xattrs \
    "${yt_vod_url}";
```

## Extract audio and resample

```shell
ffmpeg \
    -i "video/1.mp4" \
    -hide_banner \
    -vn \
    -loglevel error \
    -ar 16000 \
    -ac 1 \
    -c:a pcm_s16le \
    -y \
    "video/1.wav";
```

## Transcribe

```shell
./whisper-cli \
    -m "model/ggml-large-v3-turbo-q8_0.bin" \
    -f "video/1.wav" \
    -osrt;
```
