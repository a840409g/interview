https://a840409g.github.io/interview/

本測驗用vue cli 以及 webpack 做出

1.商品數量、名稱以及圖片的部分用HTML寫出COMPONENT,商品的數量、其他數字顯示以及購買停售的狀態則透過METHODS以及DATA來做變更。

2.顯示倒數時間的部分用setInterval操作,並透過vue的created階段執行,使其能在網頁一出現時就能開始倒數。

  另外,時間的外框則透過倒數涵式改變data的time,並用if來判斷time現在的狀態並做出相對應的操作。
  
3.購買按鈕的部分,購買與預購是以商品數量做判斷,而停售則是time。
  預購數量的出現與否用v-if判斷status的狀況是否為預購，而確認數量框也是用v-if來判斷status是否為停售。
  
詳細程式碼附在編譯前檔案>src>component中。
