# 使用 iReport 5 免費開源軟體製作精美報表 #

電子報表在辦公室電腦化作業扮演重要的角色，由於需要合併處理數量龐大的資料，需要報表軟體才能省時不費力，例如 Crystal Report 與 Active Report 等都是知名的報表軟體。在全面採用自由軟體的工作環境中，我們使用開放源碼軟體 JasperReport 與 iReport 滿足報表需求。

## Part 2 ##

### 報表資料來源 ###

iReport 支援的資料來源種類非常多，使用上相當有彈性。以下是幾種常見的資料來源類型：

  * Database JDBC connection
  * XML file datasource
  * File CSV datasource
  * Hibernate connection
  * EJBQL connection
  * Microsoft Excel (xls) data source
  * Microsoft Excel 2007 (xlsx) data source
  * Remote XML file datasource
  * JSON datasource
  * MongoDB Connection
  * Hadoop Hive Connection

多數常用的關聯式資料庫，例如 MySQL、PostgreSQL、SQL Server 或 Oracle 都可以找到 JDBC（Java Database Connectivity）驅動程式，在 iReport 中只要選擇「Database JDBC connection」就能以 SQL 建立查詢，將資料庫查詢結果用於報表內容顯示。

### 變更資料庫來源:使用CVS ###

此章節將介紹如何使用CVS 作為資料庫來源

首先，我可以在主畫面看到如下圖圖示

![image](part2/datasource_set_btn.png)

點選之後會開啟 connections / datasources 的設定跳窗如下圖

![image](part2/datasource_set_win.png)

接著我們可以點選 畫面中的 new，將跳起下圖：

![image](part2/datasource_type_select.png)

讓我們選擇 __File CSV datasource__，點選 next 將進入CSV 設置畫面，視窗彈出後請先選擇 __Separators__如下圖

![image](part2/cvs_set1.png)

我們可以看到__Field separator(char)__ 預設值為 __Comma__ 也就是 ","，這邊我們不需調整

而原本預設的 __Row separator__ 為 New line(Windows)，因為目前運行的環境為ubuntu 請改選為 __New line(Unix)__

接著我們在回到 __Columns__ 頁籤，如下圖所示：

![image](part2/cvs_set2.png)

將Name填入，在此我們填入 orders

接著選擇您的 *.cvs 檔案所在位置

根據剛剛的設定的 __Field separator(char)__ 以及 __Row separator__，此時點選 __Get columns name from the first row of the file__ iReport 將自動將CVS 檔案中的第一行資料作為欄位抓取出來，讓我們點選 Save，如此一來就完成 File CSV datasource 的設置啦！

還記得之前 __Quick Start__ 章節的 __決定資料來源__ 步驟，我們只要將資料來源改選為剛剛設置命名為 orders的 File CSV datasource，之後的步驟則完全一樣，依然可以產生同樣的報表結果！

## 使用一維條碼

在使用報表時，很多時候我們需要條碼的協助，讓我們能夠更快得輸入或查詢資料，一方面可以避免輸入錯誤，在ireport裡就有內建barcode產生器可以很快速的產生條碼，只需要幾個步驟，再這為大家介紹。

首先可以看到在ireport 的右邊工具列有個palette 的 report Elements 如下圖：

![img](part2/barcode_1.png)

裡面有個 Barcode 的元件我們要使用他，只要將他拖拉到你預計需要顯示的地方，在拖拉完成之前我們可以看到他會提示詢問要用哪個套件產生barcode如下圖：

![img](part2/barcode_2.png)

根據，你想要產生的條碼形式，與encode的不同選擇所需要的套件，在這我們選擇 Barcode4j，可以看到選擇完成後在報表維護畫面就會有個條碼物件，接著我們就必須定義要用哪個欄位作為顯示的資料如下圖：

![img](part2/barcode_3.png)

當我們點選barcode物件時，可以在編輯畫面右下角的屬性看到__Code Expression__，在該欄位可以是靜態資料也可以是動態欄位，在此我們填入 ``$F{ORDERID}`` 也就是根據訂單編號來產生條碼，每一比資料都會產生不同的條碼，最後產生的結果如下：

![img](part2/barcode_4.png)

如此就完成條碼的產生，可以看到每個條碼，都根據ORDERID動態產生，就是如此的方便，除了二維條碼之外，如果要產生QR CODE 也是可以的，必須要額外使用QR CODE 產生器的套件。


## 加入圖檔

為大家介紹如何加入圖檔的顯示，一般來說，除了文字資料，若有圖片作為輔助，將更能協助報表內資料的辨識，在ireport，裡也有圖片元件可以使用，首先我們可以點選左邊palette 的 report Elements 裡的image，如下圖：

![img](part2/image_1.png)

同樣的我們可以用拖拉的方式將該元件放到報表中，他可以是靜態資料也可以是動態的資料，靜態的部份就勢將你要顯示的圖檔路徑給定，那ireport就會根據你指定的圖檔做顯示，如果是動態的就必須有個規則，比如說我們同樣的用ORDERID當做動態給定圖檔的檔名設定方式如下圖：

![img](part2/image_2.png)

可以看到我們將 __Image Expression__ 設定為 ``"/home/spooky/ $"+$F{ORDERID}+".jpg"`` ，我們只要在指定的路徑放根據ORDERID編號命名圖檔檔名，ireport就會自動將圖檔載入，另外也許並不是每比資料都有對應的圖檔，故我們可以調整 ``On Error Type`` 如下圖：

![img](part2/image_3.png)

原本為 ``Error``，也就是說如果找不到圖檔報表就不會產生，這不是我們要的，因為實際上圖片的完善是需要一些時間，我們將其改為``blank`` 也就是說如果找不到圖片請ireport顯示空白，OK，設定完之後，我們來看結果，如下圖：

![img](part2/image_4.png)


設定好之後，一旦我們有訂單有需要在增或是調整圖片內容，我們只要替換圖檔就好，ireport就會自動將圖片顯示出來，是不是很簡單阿！





##地圖元件

地圖元件，就在11月底的時候 ireport 釋出 ５.0.0 的新功能，這邊介紹一下如何使用該元件，圖資來源就是google，首先同樣的在左邊palette 的 report Elements可以看到有個Map 元件，如下圖：

![img](part2/map_1.png)

把它拖拉到你想要放置地圖的地方，接著你需要知道你要插入地圖的位置的座標，可以利用google map把你想查的點查出來後取得座標，查出來以後我們將座標資訊輸入如下圖：

![img](part2/map_2.png)

可以看到他有兩個參數分別是 ``Lat. Expr`` ``Lon. Expr``，也就是經緯座標的輸入，然後我們可以看到下面還有個``Zoom. Expr`` 也就是縮放比例，這個也必須設置，不然地圖細節看不到，也就沒意義了，這邊將其設置為15，最後還有個``Language``的屬性，根據你的地圖所需要顯示語系做設置，這邊設定為 ``"zh-TW"``，OK，如此一來我們就可以看結果了，如下圖： 


![img](part2/map_3.png)

當然可以在搭配資料庫動態顯示地圖，比如說如範例報表可以顯示每個出貨地點的地圖，只要在欄位定義多個經緯度，如此就可以根據欄位作為資料來源，顯示每個出貨地點的地理資訊，如此一來，地圖呈現將會更加便利。



##QR CODE 的產生

開始說明如何使用ireport 產生QRCODE 之前，需要先說明，此為進階功能，讀者必須做一點程式開發，並且必須要有JAVA的開發環境，筆者為了簡化開發JAVA所需的引入套件，編譯以及包jar將使用 ``gradle`` 來做為 build script，可以把它想像成ant 的強化版，在這邊就不進一步敘述，重點還是放在產生QRCODE的所需步驟，透過這章節也將可以了解ireport 除了一些方便的報表製作的元件外，透過其內建的Scriptlet 可以方便的引入外部程式進行資料運算與處理，那我們就開始吧！

首先先簡單的說明一下要產生QRCODE的步驟：

1. 因為ireport並沒有內建的QRCODE generater，因次若要產生QRCODE我們需要使用外部套件，協助將資料進行轉換
2. 為了要能夠讓ireport的資料能夠交由別的程式進行處理，我們需要使用到ireport提供的scriptlet作為插件引入，自行定義的程式
3. 最後必須將處理結果，傳回ireport進行顯示，我們將透過ireport的變數物件``Variable``作為處理結果的容器，並且顯示在報表上面，步驟清楚了，再來就開始實作部分，首先必須先把相依套件準備好。

### 所需套件名稱與對應版本

下面是gradle所定義的套件相依性的程式碼：

	apply plugin: 'java'

	repositories {
    	mavenCentral()
	}
	dependencies {
    	compile group: 'com.google.zxing', name: 'javase', version: '2.1'
    	compile group: 'net.sf.jasperreports', name: 'jasperreports', version: '5.0.0'
    	compile group: 'com.lowagie', name:'itext', version:'2.1.7'
	}

其中各個套件使用目的如下：

* jasperreports: ireport的core，凡是需要實作ireport的相關功能都需要使用到此套件，為了產生QRCODE我們需要使用到ireport 的scriptlet，故我們必須 extends JRDefaultScriptlet，後續會在詳細說明
* itext: jasperreports在使用時需要用到itext套件，故必須引入
* zxing: 是google 的開源套件，就是要用來產生QRCODE image的

一旦相依套件準備好了我們就可以開始進行程式的開發。

### 製作Scriptlet產生QRCODE

程式碼如下：

	package com.smlsun.ireport;
	import com.google.zxing.BarcodeFormat;
	import com.google.zxing.WriterException;
	import com.google.zxing.common.BitMatrix;
	import com.google.zxing.qrcode.QRCodeWriter;
	import com.google.zxing.client.j2se.MatrixToImageWriter;
	import net.sf.jasperreports.engine.JRDefaultScriptlet;
	import net.sf.jasperreports.engine.JRScriptletException;

	public class QRCodeScriptlet extends JRDefaultScriptlet {
	    public void afterDetailEval() throws JRScriptletException {
	        QRCodeWriter writer = new QRCodeWriter();
	        BitMatrix matrix = null;

	        try {
	            matrix = writer.encode(getFieldValue("ORDERID").toString(), BarcodeFormat.QR_CODE, 256, 256);
	            this.setVariableValue("BarCodeImage", MatrixToImageWriter.toBufferedImage(matrix) );
	        } catch (WriterException e) {
	            e.printStackTrace();
	        }
	    }
	}
	
上述得程式中我們可以看到class extends JRDefaultScriptlet 並且實作了 ``afterDetailEval()``這個void ，也就是說當Detail band 報表展開完成後，將開觸動此void

接著可以看到在程式中 ``QRCodeWriter writer = new QRCodeWriter();``就是用來產生QRCODE 的物件，接著 ``BitMatrix matrix``將承接 ``QRCodeWriter``產生後的資料，然後在透過 ``MatrixToImageWriter``將 ``BitMatrix``所承接的資料轉換為 Image。

其中資料來源將透過``getFieldValue("ORDERID")`` 取得報表中從Data Source取得的欄位內容進行轉換，並且將轉換好的圖片檔塞入變數``BarCodeImage``，透過 `` this.setVariableValue("BarCodeImage", BufferedImage)``

如此一來最難的JAVA程式就算完成了，接著我們必須將他打包成jar檔，在此筆者的jar檔檔名為``ireprt-qrcode.jar``，引入ireport的classpath，並且別忘了相依的套件也必須一併引入才行，連同``zxing``，``jasperreports``還有``itext``，結果如下圖：


![img](part2/qrcode_1.png)


就算完成產生QRCODE的Scriptlet並且載入ireport接著下一步驟。

### ireport 綁定 Scriptlet

首先我們必須將剛剛完成並切引入ireport的jar註冊到scriptlet，我們可以在左邊的 report inspector，看到有個Scriptlets，將其打開並且點選底下的REPORT，如下圖

![img](part2/qrcode_2.png)

要定義載入的class，可以看到右邊的REPORT - Properties，下面有個Scriptlet Class，如下圖

![img](part2/qrcode_3.png)

鍵入剛剛完成的class package 路徑 ``com.smlsun.ireport.QRCodeScriptlet``，OK～如此一來就算將我們寫的scriptlets註冊到ireport了！

### 建立 BarCodeImage  Viariable 


然後我們必須創建一個變數``Viariables``，作為scriplet處理結果的容器，也因此我們需要建立一個這樣的變數，操作方式如下圖：

![img](part2/qrcode_4.png)

在 Viariables 上面用滑鼠右鍵，點選Add Variable，在Viariables下面將多一個 variable1，需要在定義他的 Properties，如下圖：

![img](part2/qrcode_5.png)

在剛剛的程式碼中我們將承接變數的名稱命名將Name 改為``BarCodeImage``

還記得剛剛得程式中我們需將scriptlet處理結果置於 BarCodeImage這個variable，因為最後產生的QRCODE是圖片的形式所以需指定型態為``BufferedImage``，所以需將 Variable Class 更改為``java.awt.image.BufferedImage``，需特別提醒，下拉選單是挑不到的，請直接鍵入，並且記得大小寫必須一致。

最後我們必須將``Calculation``設定為 ``System``，也就是告訴ireport此變數執行的運算的是系統定義，其他還有很多不同的運算式像是``Count`` ``Sum`` ``Average``等，在這邊不細談。

### 使用 ireport image Element 顯示QRCODE

就快完成了！剩下最後一哩，我們需要之前有說明過的image Element作為做後呈現的媒介，同樣我們將image拖拉到我們需要呈現QCODE的位置，編輯該元件的Properties，如下圖

![img](part2/qrcode_6.png)

在Image Expression裡我們需要填入剛剛建立並且設定好的 ``$V{BarCodeImage}``，前置詞``$V``代表為 Viariable，表示image元件呈現內容的來源為``$V{BarCodeImage}``，而``$V{BarCodeImage}``將會承接 ``QRCodeScriptlet``處理結果，整個運作路徑就清楚了，最後就可以來看運作結果了，如下圖：

![img](part2/qrcode_7.png)


QRCODE產生完成！透過實作產生QRCODE將更了解ireport的運作，可以有更多延伸，比如說第三方的圖表呈現，或者引入html 都可以很方便做到，透過Scriptlet也可以簡化報表製作的複雜度，有些運算在ireport內很難設定，但用程式處理也許就有現成的程式碼可以使用，像QRCODE就是一個很好的例子。



