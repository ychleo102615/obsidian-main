---
tags: []
date: 2024-05-08
time: 16:25
---
壓縮雲霄飛車小遊戲時用的指令
```shell
ffmpeg -i 5.movie.mov -vf "scale=720:-2" -crf 30 -c:v libx264 -preset veryslow -c:a aac -b:a 128k -r 24 output.mp4
```

以前壓縮影片的腳本  `compress_video.command`
```shell
cd "$(dirname "$0")"
read filename
ffmpeg -i "$filename" -vf scale=720:-2 5.movie.mp4
```

[preset 相關說明](https://magiclen.org/x264-preset/)

vf -> video filter

- `-vf "scale=1280:-2"`: 这个参数用于调整视频的分辨率。在这个例子中，视频的宽度会被调整为1280像素，而高度会按比例自动调整，以保持视频的宽高比。
- `-c:v libx264`: 这个参数指定视频编码器为 libx264，它是一个高效的 H.264 编码器。
- `-crf 23`: 这个参数控制视频的质量。CRF（Constant Rate Factor）值越低，视频的质量就越高，但文件大小也会越大。通常，CRF 值在 18 到 28 之间是合理的范围。在这个例子中，我选择了 23，你可以根据自己的需求调整这个值。
- `-preset medium`: 这个参数指定了编码器的预设。预设越低，压缩效率就越高，但编码时间也会增加。通常，`medium` 是一个平衡了压缩效率和编码时间的预设。
- `-c:a aac -b:a 128k`: 这个参数指定了音频编码器为 AAC，并且设置音频的比特率为 128k。你可以根据需要调整音频的比特率。