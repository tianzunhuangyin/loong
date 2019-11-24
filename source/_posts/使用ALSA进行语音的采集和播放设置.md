[TOC]

# 使用ALSA进行语音的采集和播放设置

## 1.	设置硬件地址

### 1.	查看硬件相关地址

```
$:arecord -l
**** List of CAPTURE Hardware Devices ****
card 1: U0x46d0x825 [USB Device 0x46d:0x825], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

硬件地址为：**plughw:CARD=U0x46d0x825**

## 2.	打开设备并设置参数

### 1.	打开设备

```
int snd_pcm_open(snd_pcm_t **pcm, const char *name, snd_pcm_stream_t stream, int mode);
//参数说明		      pcm设备句柄，USB声卡的地址信息，播放、录音PCM流，打开模式
```

stream参考值

```
/** PCM stream (direction) */
typedef enum _snd_pcm_stream {
	/** Playback stream */
	SND_PCM_STREAM_PLAYBACK = 0,
	/** Capture stream */
	SND_PCM_STREAM_CAPTURE,
	SND_PCM_STREAM_LAST = SND_PCM_STREAM_CAPTURE
} snd_pcm_stream_t;
```

mode参考值

```
0 - 标准模式(阻塞打开)  默认模式
SND_PCM_ASYNC - 异步通知
SND_PCM_NONBLOCK - 非阻塞 读写PCM设备将立即返回
```

### 2.	分配snd_pcm_hw_params_t指针结构体

#### 1.	分配结构体

存有硬件地址信息

```
snd_pcm_hw_params_alloca(ptr)
```

#### 2.	初始化snd_pcm_hw_params_t指针结构体

```
snd_pcm_hw_params_any(snd_pcm_t *pcm, snd_pcm_hw_params_t *params);
//参数说明             pcm设备句柄，     硬件信息结构体
```

#### 3.	设置访问类型

访问类型指定将多通道数据存储在缓冲区中的方式。对于INTERLEAVED访问，缓冲区中的每个帧都包含通道的连续样本数据。对于16位立体声数据，这意味着缓冲区包含左右声道采样数据的交替字。对于非交错访问，每个周期首先包含第一个通道的所有样本数据，然后包含第二个通道的样本数据，依此类推。

```
int snd_pcm_hw_params_set_access(snd_pcm_t *pcm, snd_pcm_hw_params_t *params, 				 		snd_pcm_access_t _access);
//参数说明：                   	PCM句柄，      参数配置空间，		访问访问类型
```

_access参考值

```
SND_PCM_ACCESS_MMAP_INTERLEAVED 	通过简单的交错通道进行mmap访问

SND_PCM_ACCESS_MMAP_NONINTERLEAVED 		通过简单的非交错通道进行mmap访问

SND_PCM_ACCESS_MMAP_COMPLEX 	复杂布局的mmap访问
```

#### 4.	设置采样格式

```
int snd_pcm_hw_params_set_format(snd_pcm_t *pcm, snd_pcm_hw_params_t *params, 			 			snd_pcm_format_t val);
//参数说明：						PCM句柄，硬件信息结构体，格式值
```

val参考值

```
SND_PCM_FORMAT_U8 - Unsigned 8 bit 无符号8位
SND_PCM_FORMAT_S16_LE - Signed 16 bit Little Endian 有符号16为小端（所有数字的低位组放在最前面）
SND_PCM_FORMAT_S24_LE - Signed 24 bit Little Endian using low three bytes in 32-bit word
						有符号24位小端（使用32bit中的低三位bytes(1bytes = 8bit)）
```

#### 5.	设置通道数

```
int snd_pcm_hw_params_set_channels(snd_pcm_t *pcm, snd_pcm_hw_params_t *params, 
		unsigned int val);
//参数说明							PCM句柄，	硬件信息结构体，声道数（1表示单声道，2表示立体声）
```

#### 6.	设置采样率

```
int snd_pcm_hw_params_set_rate_near(snd_pcm_t *pcm, snd_pcm_hw_params_t *params, unsigned 			int *val, int *dir);
//参数说明 							PCM句柄，硬件信息结构体，近似目标速率/返回的近似设定速率，子单位方向
```

### 3.	应用参数

```
int snd_pcm_hw_params(snd_pcm_t *pcm, snd_pcm_hw_params_t *params);
//参数说明				PCM句柄，硬件信息结构体
```

### 4.	录音与播放

####  1.	录音

```
snd_pcm_sframes_t snd_pcm_readi(snd_pcm_t *pcm, void *buffer, snd_pcm_uframes_t size);
//参数说明		PCM句柄，缓冲区帧，读取大小
```

#### 2.	播放

```
snd_pcm_sframes_t snd_pcm_writei(snd_pcm_t *pcm, const void *buffer, snd_pcm_uframes_t size);
//参数说明		PCM句柄，缓冲区帧，写入大小
```

