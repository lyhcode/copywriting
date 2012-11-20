# iReport and Ubuntu Linux - Part I


###Introduction

ireport是個能夠自行定義報表格式的open source，也是目前全球最為流行的報表設計之一，在操作上擁有豐富的圖型設計介面，在國外已有非常完善的介紹，與參考資料，對於中文的部份，尚未有相關書籍進行介紹，在網路上也只有分散於個人部落格的相關文章，在此，將透過一系列的說明，帶領讀者熟悉此好用又強大的報表編輯軟體，從安裝，基礎設置，基本報表設計，到進階的報表使用編輯技巧，將一步步帶領讀者了解整個報表製作與運作過程。

![image](part1/ireport.jpg)

ireport 的運作原理與java很像;java在編寫程式時是以java作為source code 透過compiler 編譯成class檔後執行。

而ireport有個對應的jrxml 作為編寫報表儲存程式碼，透過ireport enging編譯為jasper，實際在產生報表時只要有該檔案就可執行，不需要原始的jrxml，在ireport 編輯器上所做的任何修改，都會儲存於jrxml裡，其敘述方式為xml文檔格式，理論上，透過修改jrxml也可以做到動態產生報表格式

說了那麼多就讓我們開始使用ireport，看看他能為我們帶來什麼功能，下面將介紹安裝步驟



### Install

ireport的安裝檔可在 jaspersoft 的官網取得，網址如下：
	
	http://community.jaspersoft.com/project/ireport-designer

因為使用的是os 是 ubuntu 請下載 [iReport-4.8.0.tar.gz](http://sourceforge.net/projects/ireport/files/iReport/iReport-4.8.0/iReport-4.8.0.tar.gz/download)

目前，最新版本為 iReport-4.8.0

請將下載檔案放在 home 目錄，也就是 ~/

或者透過下列指令進行下載


``wget http://downloads.sourceforge.net/project/ireport/iReport/iReport-4.8.0/iReport-4.8.0.tar.gz ~/``

 接著進行解壓縮

``tar zxvf iReport-4.8.0.tar.gz``


在開始執行之前，我們必須先確保java jdk 已有安裝於系統內，可以使用下例指令進行java安裝

``sudo apt-get install openjdk-7-jdk``


幾個簡單步驟後，就可以開始執行ireport啦

``sh ~/iReport-4.8.0/bin/./ireport``

![image](part1/init_window.png)

下一小節將介紹一些基本的環境設置


### Configuration











