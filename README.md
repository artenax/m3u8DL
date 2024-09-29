# m3u8DL
Cross-platform DASH/HLS/MSS download tool. Supports on-demand and live streaming (DASH/HLS).

If you encounter a bug, first check if the software is the latest version (if it is a Release version, we recommend downloading the latest autobuild version from the [Actions](https://github.com/nilaoda/N_m3u8DL-RE/actions) page to see if the problem has been fixed). If you make sure the version is up to date and the problem still exists, you can go to the [Issues](https://github.com/nilaoda/N_m3u8DL-RE/issues) section to see if anyone else has encountered it, and then ask again if no one has mentioned your problem.

---

Terminal in older Windows versions, may not support this program, alternative: run it in [cmder](https://github.com/cmderdev/cmder).   
Arch Linux package is available from AUR: [n-m3u8dl-re-bin](https://aur.archlinux.org/packages/n-m3u8dl-re-bin), [n-m3u8dl-re-git](https://aur.archlinux.org/packages/n-m3u8dl-re-git)
.
```bash
# Arch Linux (binary)
yay -Syu n-m3u8dl-re-bin

# Arch Linux (build from source code)
yay -Syu n-m3u8dl-re-git
```
---

# Command line options
```
Description:
  N_m3u8DL-RE (Beta version) 20240630

Usage:
  m3u8DL <input> [options]

Arguments:
  <input>  Input Url or File

Options:
  --tmp-dir <tmp-dir>                      Set temporary file directory
  --save-dir <save-dir>                    Set output directory
  --save-name <save-name>                  Set output filename
  --base-url <base-url>                    Set BaseURL
  --thread-count <number>                  Set download thread count [default: 2]
  --download-retry-count <number>          The number of retries when download segment error [default: 3]
  --force-ansi-console                     Force assuming the terminal is ANSI-compatible and interactive
  --no-ansi-color                          Remove ANSI colors
  --auto-select                            Automatically selects the best tracks of all types [default: False]
  --skip-merge                             Skip segments merge [default: False]
  --skip-download                          Skip download [default: False]
  --check-segments-count                   Check if the actual number of segments downloaded matches the expected number 
                                           [default: True]
  --binary-merge                           Binary merge [default: False]
  --use-ffmpeg-concat-demuxer              When merging with ffmpeg, use the concat demuxer instead of the concat protocol 
                                           [default: False]
  --del-after-done                         Delete temporary files when done [default: True]
  --no-date-info                           Date information is not written during muxing [default: False]
  --no-log                                 Disable log file output [default: False]
  --write-meta-json                        Write meta json after parsed [default: True]
  --append-url-params                      Add Params of input Url to segments, useful for some websites, such as kakao.com 
                                           [default: False]
  -mt, --concurrent-download               Concurrently download the selected audio, video and subtitles [default: False]
  -H, --header <header>                    Pass custom header(s) to server, Example:
                                           -H "Cookie: mycookie" -H "User-Agent: iOS"
  --sub-only                               Select only subtitle tracks [default: False]
  --sub-format <SRT|VTT>                   Subtitle output format [default: SRT]
  --auto-subtitle-fix                      Automatically fix subtitles [default: True]
  --ffmpeg-binary-path <PATH>              Full path to the ffmpeg binary, like C:\Tools\ffmpeg.exe
  --log-level <DEBUG|ERROR|INFO|OFF|WARN>  Set log level [default: INFO]
  --ui-language <en-US|zh-CN|zh-TW>        Set UI language
  --urlprocessor-args <urlprocessor-args>  Give these arguments to the URL Processors.
  --key <key>                              Pass decryption key(s) to mp4decrypt/shaka-packager. format:
                                           --key KID1:KEY1 --key KID2:KEY2
  --key-text-file <key-text-file>          Set the kid-key file, the program will search the KEY with KID from the file.(Very 
                                           large file are not recommended)
  --decryption-binary-path <PATH>          Full path to the tool used for MP4 decryption, like C:\Tools\mp4decrypt.exe
  --use-shaka-packager                     Use shaka-packager instead of mp4decrypt to decrypt [default: False]
  --mp4-real-time-decryption               Decrypt MP4 segments in real time [default: False]
  -R, --max-speed <SPEED>                  Set speed limit, Mbps or Kbps, for example: 15M 100K.
  -M, --mux-after-done <OPTIONS>           When all works is done, try to mux the downloaded streams. Use "--morehelp 
                                           mux-after-done" for more details
  --custom-hls-method <METHOD>             Set HLS encryption method 
                                           (AES_128|AES_128_ECB|CENC|CHACHA20|NONE|SAMPLE_AES|SAMPLE_AES_CTR|UNKNOWN)
  --custom-hls-key <FILE|HEX|BASE64>       Set the HLS decryption key. Can be file, HEX or Base64
  --custom-hls-iv <FILE|HEX|BASE64>        Set the HLS decryption iv. Can be file, HEX or Base64
  --use-system-proxy                       Use system default proxy [default: True]
  --custom-proxy <URL>                     Set web request proxy, like http://127.0.0.1:8888
  --custom-range <RANGE>                   Download only part of the segments. Use "--morehelp custom-range" for more details
  --task-start-at <yyyyMMddHHmmss>         Task execution will not start before this time
  --live-perform-as-vod                    Download live streams as vod [default: False]
  --live-real-time-merge                   Real-time merge into file when recording live [default: False]
  --live-keep-segments                     Keep segments when recording a live (liveRealTimeMerge enabled) [default: True]
  --live-pipe-mux                          Real-time muxing to TS file through pipeline + ffmpeg (liveRealTimeMerge enabled) 
                                           [default: False]
  --live-fix-vtt-by-audio                  Correct VTT sub by reading the start time of the audio file [default: False]
  --live-record-limit <HH:mm:ss>           Recording time limit when recording live
  --live-wait-time <SEC>                   Manually set the live playlist refresh interval
  --live-take-count <NUM>                  Manually set the number of segments downloaded for the first time when recording live 
                                           [default: 16]
  --mux-import <OPTIONS>                   When MuxAfterDone enabled, allow to import local media files. Use "--morehelp 
                                           mux-import" for more details
  -sv, --select-video <OPTIONS>            Select video streams by regular expressions. Use "--morehelp select-video" for more 
                                           details
  -sa, --select-audio <OPTIONS>            Select audio streams by regular expressions. Use "--morehelp select-audio" for more 
                                           details
  -ss, --select-subtitle <OPTIONS>         Select subtitle streams by regular expressions. Use "--morehelp select-subtitle" for 
                                           more details
  -dv, --drop-video <OPTIONS>              Drop video streams by regular expressions.
  -da, --drop-audio <OPTIONS>              Drop audio streams by regular expressions.
  -ds, --drop-subtitle <OPTIONS>           Drop subtitle streams by regular expressions.
  --ad-keyword <REG>                       Set URL keywords (regular expressions) for AD segments
  --morehelp <OPTION>                      Set more help info about one option
  --version                                Show version information
  -?, -h, --help                           Show help and usage information
```

<details>
<summary>More Help</summary> 

```
./m3u8DL --morehelp select-video
More Help:

  --select-video

Select video streams by regular expressions. OPTIONS is a colon separated list of:

id=REGEX:lang=REGEX:name=REGEX:codecs=REGEX:res=REGEX:frame=REGEX
segsMin=number:segsMax=number:ch=REGEX:range=REGEX:url=REGEX
plistDurMin=hms:plistDurMax=hms:bwMin=int:bwMax=int:role=string:for=FOR

* for=FOR: Select type. best[number], worst[number], all (Default: best)

Examples: 
# select best video
-sv best
# select 4K+HEVC video
-sv res="3840*":codecs=hvc1:for=best
# Select best video with duration longer than 1 hour 20 minutes 30 seconds
-sv plistDurMin="1h20m30s":for=best
-sv role="main":for=best
# Select video with bandwidth between 800Kbps and 1Mbps
-sv bwMin=800:bwMax=1000
```
</details>

# Screenshots

![RE1](img/RE.gif)

Parallel downloads + auto-mixing


![RE2](img/RE2.gif)

## Live broadcast

Record a TS live feed:

[click to show](http://pan.iqiyi.com/file/paopao/W0LfmaMRvuA--uCdOpZ1cldM5JCVhMfIm7KFqr4oKCz80jLn0bBb-9PWmeCFZ-qHpAaQydQ1zk-CHYT_UbRLtw.gif)

Record a live MPD feed:

[click to show](http://pan.iqiyi.com/file/paopao/nmAV5MOh0yIyHhnxdgM_6th_p2nqrFsM4k-o3cUPwUa8Eh8QOU4uyPkLa_BlBrMa3GBnKWSk8rOaUwbsjKN14g.gif)

Real-time mixing of audio and video with the help of ffmpeg during the recording process.
```
ffmpeg -readrate 1 -i 2022-09-21_19-54-42_V.mp4 -i 2022-09-21_19-54-42_V.chi.m4a -c copy 2022-09-21_19-54-42_V.ts
```
In newer versions (>=v0.1.5), try turning on `live-pipe-mux` instead of the above command

**Special Note: If the network environment is not stable enough, please do not enable `live-pipe-mux`. In-pipe data reading is handled by ffmpeg, which is prone to losing live data in some environments**.

## Donations

<a href="https://www.buymeacoffee.com/nilaoda" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>
