# DNA_FSM
Use finite-state machine to find gene.

## 目標
    輸入一串以核甘酸ATGC組成的染色體序列，三個為一組基因碼，以ATG為開頭，結束於TAA、TAG或TGA，若序列中
    找不到基因碼則顯示no gene is found

## 條件限制
    1.基因碼為3的倍數
    2.只有1種開頭ATG，結尾有3種TAA、TAG或TGA

## 有限狀態機
    主要有兩個東西：「狀態」，「動作」，總共4個動作：「進入動作」、「退出動作」、「輸入動作」、「轉移動作」
    「狀態」外圍有兩個橋接：進入狀態時的「進入動作」、離開狀態時的「退出動作」
    「輸入動作」是根據當前狀態與輸入條件進行，也就是說在「狀態」內，會遭遇某些條件而有所動作，條件是被輸入到狀態內的
    「轉移動作」是在特定轉移時進行，能轉換從這個「狀態」轉移到其他「狀態」
   [有限狀態機wiki](https://zh.wikipedia.org/wiki/%E6%9C%89%E9%99%90%E7%8A%B6%E6%80%81%E6%9C%BA)

## 虛擬碼
    1 建立對照表，ATGC對應0123
    2 用對照表建立start矩陣與end矩陣，前者紀錄A到T到G順序(A接下來要接T，T要接到G)，後者依此類推
    3 輸入染色體序列
    4 逐一讀取字元，直到讀到A，開啟找開始基因碼ATG的狀態
        4.1 查對照表取得直行位置
        4.2 遇到字元是A時開啟開始狀態，紀錄開始字元數
        4.3 下個迴圈查找start矩陣看狀態，若開始狀態開啟，將直行的數字給橫列，對應字元移動的順序，紀錄開始字元數
        4.4 達到開始字元數3，紀錄開始位置，將開始字元數與開始狀態歸零
    5 有了開始位置，照步驟4找T開頭的結束基因碼
        5.1 找到結束基因碼，紀錄頭尾都有的情況，紀錄結束位置，印出基因碼，開始和結束的位置都歸零
    6 循環4到5步驟

## 結果
![image](https://github.com/leodflag/DNA_FSM/blob/master/DNA_FSM_result.png)
