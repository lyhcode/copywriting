# iReport and Ubuntu Linux - Part I


###Introduction

ireport是個能夠自行定義報表格式的open source，也是目前全球最為流行的報表設計之一，在操作上擁有豐富的圖型設計介面，在國外已有非常完善的介紹，與參考資料，對於中文的部份，尚未有相關書籍進行介紹，在網路上也只有分散於個人部落格的相關文章，在此，將透過一系列的說明，帶領讀者熟悉此好用又強大的報表編輯軟體，從安裝，基礎設置，基本報表設計，到進階的報表使用編輯技巧，將一步步帶領讀者了解整個報表製作與運作過程。

![image](part1/ireport.jpg)

精確的來說，ireport是制作JasperReport的編輯器，而JasperReport又是什麼？他是報表制作程序，使用者需要按照它制定的規則編寫XML文件，建立所要產生的報表。能夠输出的文件格式包括PDF,HTML,XML,XLS,CSV等等。

JasperReport 的運作原理與java很像;java在編寫程式時是以java作為source code 透過compiler 編譯成class檔後執行。

而JasperReport有個對應的jrxml 作為編寫報表儲存程式碼，透過ireport enging編譯為jasper，實際在產生報表時只要有該檔案就可執行，不需要原始的jrxml，在ireport 編輯器上所做的任何修改，都會儲存於jrxml裡，其敘述方式為xml文檔格式，理論上，透過修改jrxml也可以做到動態產生報表格式。

一般來說如果要自己編寫jrxml，若是簡單的報表還好，複雜一點就要人命，沒辦法看到實際報表產出情形，簡直是瞎子摸象，需要耗費非常多的時間除錯！所以ireport就因應而生，協助使用者使用拖拉的方式完成報表，並且可立即檢視報表運作結果，因為ireport的出現，JasperReport才能被普及的運用


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

基本安裝完成了！


在開始使用之前，還有些問題需要解決
* ireport 並未內建產生PDF所需的字型
* 除了能夠產生PDF也要能夠正常顯示中文內容的PDF

為了讓irport有產生PDF所需要的字型，我們需要 __iText__

為了讓產生的PDF能夠正常顯示中文內容的PDF 我們需要 __iTextAsian__

iReport 很貼心的，在他的安裝路徑內皆已經內置這兩個jar

接著我們必須告訴ireport這兩個jar 所在位置，將他們加到classpath

請先點選上方 menubar的Tools中的options，如下圖：

![image](part1/menubar.png)

點選後會開啟設定畫面，請點選classpath頁籤

![image](part1/classpath.png)

接著點選頁面中的 add 按鈕，將目錄移至````~/iReport-4.8.0/ireport/modules/ext````

接著加入 __iText__ 以及 ___itext-asian.jar___ 如下圖

![image](part1/itext_itextasian_add.png)

如此以來就完成了！

![image](part1/classpath_add_fin.png)

###注意：classpath 設定完成要記得重啟ireport，設定才會生效


是不是很簡單？基礎設置完成後，我們就可以寫個簡單的報表了

##Quick Start

讓我們利用ireport的報表產生精靈一步步帶大家產生一個基本的報表，透過這樣的過程讓大家了解產生報表所需步驟，廢話不多說，讓我們開始吧！

首先，我們一樣從manu bar 點選 File 中的 New

![image](part1/new.png)

將會開啟下列畫面

![image](part1/new_file.png)

假設我們需要製作一份報表用來查詢___每天出貨完成的的訂單___，讓我一步步帶著大家將第一個報表完成

1. 決定報表樣式
	
	在製作一個報表時，我們必須將我們預期報表需要的樣子設計好，在這裡先選擇Simple Blue

讓我們點選 Launch Report Wizard，進入下一步驟

![image](part1/save_file.png)

2. 檔案儲存位置
	
	在此決定檔案的儲存位置，以及檔案名稱，既然我們要做是出貨單，就將Report name命名為shipReport，其中file 就會自動命名為shipReport.jrxml
	
點選下一步，開始設定資料庫來源

![image](part1/database_set.png)
 
3. 決定資料來源
	
	報表除了呈現格式外，還有很重要的資料來源，在這個步驟，我們要做的就是設定資料如何取得，在ireport裡可以設定多種資料來源舉凡主流的資料庫 mysql、mssql，到一般的試算表，excel、cvs，甚至是這幾年出現的nosql之資料庫MongoDB都在其支援範圍內，可說是總類繁多，在此就不贅述，讓我們從最簡單的開始，選擇ireprt內建的Simple Database，貼心的讓我們可以方便得測試報表的製作
	選擇資料來源後，當然還要決定我們要用的是哪個table的資料，既然我們要知道已出貨的訂單，就從orders開始，sql如下 
	
		select * from orders
		where SHIPPEDDATE is not null
		order by SHIPPEDDATE
	
	將無已出貨日期的訂單篩選掉，大家還記得我們要製作的是每天出貨完成的訂單喔！還有資料查詢呈現根據 SHIPPEDDATE(已出貨日期)
	
接著我們將設定報表呈現所需要的欄位


![image](part1/fields_select.png)

4. 選取欄位
	
	上個步驟我們設定好了資料表，接著我們要設定所要呈現的欄位，為了能夠幫助出貨人員清楚知道出貨的資訊，我們當然要選擇最重要的資訊，在畫面中我們可以看到右欄列出了該table的所有欄位，我們可以在這挑選所需的欄位即可，挑選的欄位如畫面所示，必須讓出貨人員清楚知道每天預計交貨的訂單以及客戶，還有貨品需要送達的地址	
	
接者下一步，我們將決定資料的群組方式，為什麼要設群組？？讓我們看下去

![image](part1/group_set.png)

5. 群組設定

	群組的用意，簡單來說就是將餵進來的資料進行分類，ireport透過群組設定的方式，偵測設定群組欄位變化來進行自動分群，是不是很方便！一開始有說到我們需要製作一個方便出貨人員知道___每天___出貨完成的訂單有哪些，所以我們將畫面上的 Group 1設為 SHIPPEDDATE(出貨完成時間)，如此一來ireport在產生報表時，就會將資料呈現by出貨日期進行群組並列出每天出貨的訂單有哪些；而在畫面上我們可以看到其實可設定多組群組，道理是一樣的，只要兩種組合有所不同，就會自動換頁。
	
接著下一步就完成我們的每天完成出貨的報表設定囉，是不是很簡單！

![image](part1/report_buildFin.png)

讓我們接著看看產生好的報表呈現的樣子，如下圖


![image](part1/ireport_edit.png)

透過報表建立精靈，ireport已經根據我們所設定樣式，欄位，還有群組方式產生好報表的內容，我們只要在將畫面上的TITIE進行調整，就是一個可以用的報表啦，讓我們將 ___TITLE___ 改為 ___已出貨完成訂單___

接著我們就可看看成果囉，點選畫面中的preview，ireport就會將剛剛設定好的資料來源一筆筆的輸出到報表裡，並且根據出貨日期做分類，結果就如下圖所示

![image](part1/ireport_pre.png)

是不是一個簡單任務阿！

## pdf 輸出中文顯示


在一開始設置ireport時，有提到若要能夠讓pdf輸出中文正常，需要設置__iText__ 以及 ___itext-asian.jar___

除了classpath設置之外，在需要顯示中文的field 也要選擇正確的pdf字型

當您選擇需要顯示中文的欄位時在 __Properties__ 裡，需要調整下列參數

###Pdf font name: MSung-Light

###pdf enccoding: UniCNS-UCS2-H (Chinese traditional)

可參考下圖：

![image](part1/font_set.png)

產出的pdf如下圖，可以看到中文字型被正確的輸出。

![image](part1/pdf_preview.png)



## 變更資料庫來源:使用CVS

此章節將介紹如何使用CVS 作為資料庫來源

首先，我可以在主畫面看到如下圖圖示

![image](part1/datasource_set_btn.png)

點選之後會開啟 connections / datasources 的設定跳窗如下圖

![image](part1/datasource_set_win.png)

接著我們可以點選 畫面中的 new，將跳起下圖：

![image](part1/datasource_type_select.png)

讓我們選擇 __File CSV datasource__，點選 next 將進入CSV 設置畫面，視窗彈出後請先選擇 __Separators__如下圖

![image](part1/cvs_set1.png)

我們可以看到__Field separator(char)__ 預設值為 __Comma__ 也就是 ","，這邊我們不需調整

而原本預設的 __Row separator__ 為 New line(Windows)，因為目前運行的環境為ubuntu 請改選為 __New line(Unix)__

接著我們在回到 __Columns__ 頁籤，如下圖所示：

![image](part1/cvs_set2.png)

將Name填入，在此我們填入 orders

接著選擇您的 *.cvs 檔案所在位置

根據剛剛的設定的 __Field separator(char)__ 以及 __Row separator__，此時點選 __Get columns name from the first row of the file__ iReport 將自動將CVS 檔案中的第一行資料作為欄位抓取出來，讓我們點選 Save，如此一來就完成 File CSV datasource 的設置啦！

還記得之前 __Quick Start__ 章節的 __決定資料來源__ 步驟，我們只要將資料來源改選為剛剛設置命名為 orders的 File CSV datasource，之後的步驟則完全一樣，依然可以產生同樣的報表結果！

## 使用一維條碼

在使用報表時，很多時候我們需要條碼的協助，讓我們能夠更快得輸入或查詢資料，一方面可以避免輸入錯誤，在ireport裡就有內建barcode產生器可以很快速的產生條碼，只需要幾個步驟，再這為大家介紹。

首先可以看到在ireport 的右邊工具列有個palette 的 report Elements 如下圖：

![img](part1/barcode_1.png)

裡面有個 Barcode 的元件我們要使用他，只要將他拖拉到你預計需要顯示的地方，在拖拉完成之前我們可以看到他會提示詢問要用哪個套件產生barcode如下圖：

![img](part1/barcode_2.png)

根據，你想要產生的條碼形式，與encode的不同選擇所需要的套件，在這我們選擇 Barcode4j，可以看到選擇完成後在報表維護畫面就會有個條碼物件，接著我們就必須定義要用哪個欄位作為顯示的資料如下圖：

![img](part1/barcode_3.png)

當我們點選barcode物件時，可以在編輯畫面右下角的屬性看到__Code Expression__，在該欄位可以是靜態資料也可以是動態欄位，在此我們填入 ``$F{ORDERID}`` 也就是根據訂單編號來產生條碼，每一比資料都會產生不同的條碼，最後產生的結果如下：

![img](part1/barcode_4.png)

如此就完成條碼的產生，可以看到每個條碼，都根據ORDERID動態產生，就是如此的方便，除了二維條碼之外，如果要產生QR CODE 也是可以的，必須要額外使用QR CODE 產生器的套件。


## 加入圖檔

為大家介紹如何加入圖檔的顯示，一般來說，除了文字資料，若有圖片作為輔助，將更能協助報表內資料的辨識，在ireport，裡也有圖片元件可以使用，首先我們可以點選左邊palette 的 report Elements 裡的image，如下圖：

![img](part1/image_1.png)

同樣的我們可以用拖拉的方式將該元件放到報表中，他可以是靜態資料也可以是動態的資料，靜態的部份就勢將你要顯示的圖檔路徑給定，那ireport就會根據你指定的圖檔做顯示，如果是動態的就必須有個規則，比如說我們同樣的用ORDERID當做動態給定圖檔的檔名設定方式如下圖：

![img](part1/image_2.png)

可以看到我們將 __Image Expression__ 設定為 ``"/home/spooky/ $"+$F{ORDERID}+".jpg"`` ，我們只要在指定的路徑放根據ORDERID編號命名圖檔檔名，ireport就會自動將圖檔載入，另外也許並不是每比資料都有對應的圖檔，故我們可以調整 ``On Error Type`` 如下圖：

![img](part1/image_3.png)

原本為 ``Error``，也就是說如果找不到圖檔報表就不會產生，這不是我們要的，因為實際上圖片的完善是需要一些時間，我們將其改為``blank`` 也就是說如果找不到圖片請ireport顯示空白，OK，設定完之後，我們來看結果，如下圖：

![img](part1/image_4.png)


設定好之後，一旦我們有訂單有需要在增或是調整圖片內容，我們只要替換圖檔就好，ireport就會自動將圖片顯示出來，是不是很簡單阿！





##地圖元件

地圖元件，就在11月底的時候 ireport 釋出 ５.0.0 的新功能，這邊介紹一下如何使用該元件，圖資來源就是google，首先同樣的在左邊palette 的 report Elements可以看到有個Map 元件，如下圖：

![img](part1/map_1.png)

把它拖拉到你想要放置地圖的地方，接著你需要知道你要插入地圖的位置的座標，可以利用google map把你想查的點查出來後取得座標，查出來以後我們將座標資訊輸入如下圖：

![img](part1/map_2.png)

可以看到他有兩個參數分別是 ``Lat. Expr`` ``Lon. Expr``，也就是經緯座標的輸入，然後我們可以看到下面還有個``Zoom. Expr`` 也就是縮放比例，這個也必須設置，不然地圖細節看不到，也就沒意義了，這邊將其設置為15，最後還有個``Language``的屬性，根據你的地圖所需要顯示語系做設置，這邊設定為 ``"zh-TW"``，OK，如此一來我們就可以看結果了，如下圖： 


![img](part1/map_3.png)

當然可以在搭配資料庫動態顯示地圖，比如說如範例報表可以顯示每個出貨地點的地圖，只要在欄位定義多個經緯度，如此就可以根據欄位作為資料來源，顯示每個出貨地點的地理資訊，如此一來，地圖呈現將會更加便利。





