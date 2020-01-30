# StockFLoatWindow
Lyon的股票浮動視窗


資料來源 台灣證卷所 https://www.twse.com.tw/zh/

上市櫃股票代號與分類 清單： 
  
    http://isin.twse.com.tw/isin/C_public.jsp?strMode=2

其中strMode=2就是上市，而strMode=4就是上櫃，接下來我們就來將此網頁下載下來吧！

Ref:https://www.finlab.tw/Python%EF%BC%9A%E5%A6%82%E4%BD%95%E7%8D%B2%E5%BE%97%E4%B8%8A%E5%B8%82%E4%B8%8A%E6%AB%83%E8%82%A1%E7%A5%A8%E6%B8%85%E5%96%AE/


台灣加權指數：
https://mis.twse.com.tw/stock/fibest.jsp?stock=t00


https://mis.twse.com.tw/stock/fibest.jsp?stock=70005X　精華元大66展02

    取得指數的方式如下：
    http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=指數代號&json=1&delay=0

    給個例子，同時取得上市與上櫃指數
    http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=tse_t00.tw|otc_o00.tw&json=1&delay=0


(tse|otc): 若是上市使用tse，若是上櫃則使用otc, 注意左右括號要拿掉
  上市:
  
    http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=tse_1101.tw|tse_1102.tw|tse_1103.tw&json=1&delay=0&_=1552123547443

  上櫃:

    http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=otc_70005X&json=1&delay=0 


    var hostname = window.location.hostname;
    apiBaseUrl = "https://" + hostname + "/stock/api/";
    
    https://mis.twse.com.tw/stock/api/fibest.jsp?stock=tpk
    
  
    http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=(tse|otc)_SYMBOL.tw_YYYYMMDD&json=1&delay=0

例如 http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=tse_3474.tw_20140801&json=1&delay=0 可以取得 2014/8/1 當日的華亞科的股價(經測試不打_20140801&仍可取得最新資料)

這次的API也可以進行串接，例如同時取得華亞科與精華的股價可以使用 | (pipe符號) 進行串接，例如
    
    http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=tse_3474.tw_20140804|otc_1565.tw_20140804&json=1&delay=0

取得指數的方式如下：
    
    http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=指數代號&json=1&delay=0

給個例子，同時取得上市與上櫃指數

    http://mis.twse.com.tw/stock/api/getStockInfo.jsp?ex_ch=tse_t00.tw|otc_o00.tw&json=1&delay=0

參數說明：
(tse|otc): 若是上市使用tse，若是上櫃則使用otc, 注意左右括號要拿掉
SYMBOL:則是4碼或6碼的股票代號
YYYYMMDD：則是當日日期

回傳的JSON欄位說明

    z	當盤成交價
    tv	當盤成交量
    v	累積成交量
    b	揭示買價(從高到低，以_分隔資料)
    g	揭示買量(配合b，以_分隔資料)
    a	揭示賣價(從低到高，以_分隔資料)
    f	揭示賣量(配合a，以_分隔資料)
    o	開盤
    h	最高
    l	最低
    y	昨收
    u	漲停價
    w	跌停價
    tlong	epoch毫秒數
    d	最近交易日期(YYYYMMDD)
    t	最近成交時刻(HH:MI:SS)
    c	股票代號
    n	公司簡稱
    nf	公司全名
