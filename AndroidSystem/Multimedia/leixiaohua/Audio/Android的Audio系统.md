Audio 系统在 Android 中负责音频方面的数据流传输和控制功能,也负责音频设备的管理。这个部分作为 Android 的 Audio 系统的输入/输出层次,
一般负责播放 PCM 声音输出和从外部获取 PCM 声音,以及管理声音设备和设置。</br>

Audio 系统主要分成如下几个层次:</br>
(1)media 库提供的 Audio 系统本地部分接口;</br></br>
(2)AudioFlinger 作为 Audio 系统的中间层;</br>
(3)Audio 的硬件抽象层提供底层支持;</br>
(4)Audio 接口通过 JNI 和 Java 框架提供给上层。</br>
Audio 系统的各个层次接口主要提供了两方面功能:放音(Track)和录音(Recorder)。</br>

