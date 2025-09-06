
[repo](https://github.com/ychleo102615/ytsaver)

```shell
youtube-dl -x --audio-format mp3 https://www.youtube.com/watch?v=VIDEO_ID
# -x means extract
```

2023-06-29-週四, 22:24
---
今天更新指令後，想下載youtube影片會失敗。
本來是因為說下載速度有瓶頸，根據這個[連結](https://github.com/ytdl-org/youtube-dl/issues/32346)做修正。
但是現在連下載都辦不到了。

```shell
pip3 install git+https://github.com/ytdl-org/youtube-dl.git@9112e66    
```
這是安裝特定版本的指令

---
現在看起來應該不只我遇到這個問題
[回報](https://github.com/ytdl-org/youtube-dl/issues/31530)

