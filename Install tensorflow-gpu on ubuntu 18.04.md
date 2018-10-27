## Tensorflow-GPU on ubuntu 18.04 & Remote desktop
### 歷經五小時，劫後餘生做個記錄 <br>
1. [從ubuntu 16.04升級至18.04](https://reurl.cc/R1EAe) <br>
	- 因為我之前做的隨身碟裡面是16.04，懶得重下載故用升級的 <br>	
	- 也可不升，但18.04據說有比較猛。<br>

2.	[顯示卡驅動](https://reurl.cc/N6L7n) <br>
	- [重要]剛灌好ubuntu時，是沒有顯示卡驅動的(看硬體資訊那邊可以發現)，需要自己去安裝。<br>
	- 顯卡驅動我本來是裝nvidia-390，但後來發現其實要裝396，否則會出問題如下。<br>
	```Internal: cudaGetDevice() failed. Status: CUDA driver version is insufficient for CUDA runtime version```<br>
	- 歸因於自動安裝好的CUDA版本跟我們自己裝的nvidia驅動版本不相容。<br>
	- 解決辦法：想辦法把驅動弄成nvidia-396。<br>
		- 法一：用[軟體與更新]跑更新，之後在[額外驅動程式]手動選396，按完套用後重開機就好。(需要跑一下下)
		- 法二：<br>
```sudo apt purge nvidia*```<br>
```sudo add-apt-repository ppa:graphics-drivers/ppa```<br>
```sudo apt install nvidia-driver-396```		

		- 註：打nvidia-smi，可以看顯卡當前狀況。

3.	[安裝Anaconda, tensorflow-gpu](https://reurl.cc/e87KM) <br>
	- 跟著此方法是最省事的(不確定windows能不能用)，在```conda install tensorflow-gpu```後，會自動安裝CUDA 9.0 & cuDNN 7.1，能省去下載CUDA, cuDNN以及版本不相容的問題。
	- 註：python3.7目前會有點問題，保險起見裝好anaconda後記得照文章所說建個3.6的環境
	- 裝ipykernel，可以更方便的切換kernel。<br>

4.	[遠端操控ubuntu](https://reurl.cc/R1EAe) <br>
	- 必須是固定IP，不能透過分享器。
	- 照文章所說操作即可用windows跟mac來遠端操控
	- Ubuntu 18.04的[桌面分享]藏在[分享]裡面(跟16.04不一樣)
