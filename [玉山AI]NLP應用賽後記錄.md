<table>
    <tr>
        <td>玉山AI賽後記錄</td>
    </tr>
</table>

## 第零章 人工智慧學校-台中五期經理人班畢業
>  鳥類辨識系統--圖像辨識完成後，思考者仍需要更多類型的比賽，選擇了玉山AI與製造大數據競賽，一個是NLP、一個是數據分析..兩種來進行練習，本篇主要分享玉山AI的AML焦點人物的競賽過程；透過學校組長的幫助，找到了兩位技術班組員有興趣共同組隊參加，組成了3人隊伍，賽程如下:

![Alt text](https://imgur.com/gZpTSCR.png)

## 第一章 賽程學習紀錄
#### Step1：測試建模數據說明
1.  欄位:news_ID，Hyperlink，Content，Name
2.  筆數:5023筆新聞內文資料。
3.  有人名的筆數:372筆，占比率7.4%，因此你全部猜空白，也有93%的正確率。

#### Step2：爬蟲程式
1.  提供的新聞本文沒有完整內容，需要自己寫爬蟲程式。
2.  整理後新聞來源有30個平台，需要個別進行抓取進行模型訓練。
3.  colab範例程式參考:https://colab.research.google.com/drive/1IgM6L3XVLJZoEOP-2m1IBLO9SfGApQU9?usp=sharing

#### Step3：取得本文後的整理
1. 斷詞初步使用jieba，後面加上ckip斷詞(停用詞使用結巴)，繁體中文還是要用ckip，較正確地進行分類，但缺點是載入頗久。
2. 斷詞步驟:先載入ckip進行斷持，接著把斷詞的每個字進行停用字提除，最後在去除標點符號，在整理成詞庫。
3. colab範例程式參考:https://colab.research.google.com/drive/1IgM6L3XVLJZoEOP-2m1IBLO9SfGApQU9?usp=sharing

#### Step4：模型訓練
1. 模型參考LeeMeng大大的詳細的介紹，調整成單一個進行使用。
>  https://leemeng.tw/shortest-path-to-the-nlp-world-a-gentle-guide-of-natural-language-processing-and-deep-learning-for-everyone.html
2. LSTM模型步驟說明:

   a.  把文字變成數字(embedding)，好讓模型知道彼此間的關係來計算距離。
   
   b.  把文字縮為固定長度，我這邊計算後是設定200個字，過長截斷，過短補0。
   
   c.  拆分訓練與測試(9:1)。
   
   d.  送進模型進行訓練10回合。
   
![Alt text](https://imgur.com/bfmoXjD.png)

![Alt text](https://imgur.com/0KHL1Gv.png)

3.  最後正確率大概是97%，比93%好一點。
4.  colab範例程式參考:https://colab.research.google.com/drive/1IgM6L3XVLJZoEOP-2m1IBLO9SfGApQU9?usp=sharing

#### Step5：t-nse降維視覺化查看模型學習成果。
1. 因為實在不曉得模型學到了什麼，所以透過t-nse了解大概的情況，參考如下網址進行製作。
>  https://www.kaggle.com/jeffd23/visualizing-word-vectors-with-t-sne?select=train.csv.zip
2. 最後選擇關鍵文章才進行降維，如下能較清楚知道那些文字屬於關鍵或是需要再調整，注意繁體中文要多載入字型。
![Alt text](https://imgur.com/yykytIe.jpg)
3. colab範例程式參考:https://colab.research.google.com/drive/1IgM6L3XVLJZoEOP-2m1IBLO9SfGApQU9?usp=sharing

#### Step6：人名的擷取。
1. 我們透過CKIP判斷PERSON後進行百家姓提除一次，用正則表示剃除非中文並超過2-4個字。
2. 但仍有一些劉男，張女，張姓...等情況。

#### Step7：雲端平台環境的架設
1. 雲端平台因為GCP沒有提供GPU使用，玉山AI佛心提供了AZURE供參賽者使用。
2. 雲端架設CUDA與CUDNN，架設GPU環境，參考網址如下:
>  https://medium.com/@mikethreeacer/ubuntu-18-04-%E5%AE%89%E8%A3%9D-cuda-cudnn-anaconda-pytorch-1f170b3326a4#8272
3. 安裝anaconda後，有三個環境，如下參考:
![Alt text](https://imgur.com/lZWqEtz.png)
4. 將模型載入api，需注意先載入模型(app.run之前)，每次API呼叫只要判斷即可，另外因為thread問題，需要設置False。

## 第二章 賽後心得
#### 分數與心得
1. 最後一天壓秒參賽，大概落在351.8/374，大約94%，第一名除7瑱後估計是367/374，大約98%，這4%差距非常好奇如何進行的。
2. 過程滿辛苦的，每一步驟地克服都是要進行研究，最後感謝組員與學校組長以及社群上的人們的幫助。

###### 200807記錄。
