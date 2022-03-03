## ergodash_v99_ble
zmk - ergodash - trackpoint - bluetooth - split keyboard

## 版本特色
* zmk / bluetooth 5.2 nrf52840
* hot swappable key switches
* Per-Key RGB LED SK6812
* trackpoint => 尚未支援
* 110mAh

## 燒錄方式
* firmware資料夾內有left、right兩個資料夾，放左右手的燒錄檔(zmk.uf2)，
  右鍵選擇右上方的RAW按鈕，另存新檔。
* 鍵盤連接電腦USB後，連按兩下鍵盤上的Reset鍵進入bootloader mode，成功會持續閃綠燈，
  電腦會把鍵盤辨識為一個隨身碟，從我的電腦打開這個隨身碟，把zmk.uf2複製進去，
  複製完即是燒錄完成，隨身碟會自動退出。
* 如果上述燒錄步驟正確的話，鍵盤為新的狀態，但之前已配對的資料還是會保留。

## 操作方式
* 左右手燒好各自的燒錄檔後可以兩邊同時按Reset鍵，讓兩邊鍵盤自動配對。
  正常情況下左右邊配對好就會一直保持著，除非刻意去改。
* 左邊鍵盤為主鍵盤，只有插左邊USB電腦端才會辨識為鍵盤。
* 左邊鍵盤插著USB即為USB模式，USB斷開即為藍牙模式。
* 可先使用USB模式測試左右鍵盤是否有配對成功。
* 藍牙模式與一般藍牙鍵盤使用方式無異。

## 常見問題
* Q:連按兩下Reset鍵進入bootloader模式，綠燈有閃爍，但是沒有辨識成隨身碟。
* A:應該是電腦驅動程式跑掉了。
  * 解決方式:
    1. 換USB孔試試看。
    2. 裝置管理員找到該裝置，重新安裝驅動。
    3. 重新開機。

* Q:左右邊沒有辦法成功配對
  A:應該是配對資料錯亂了。
  * 解決方式:
    1.
  
*  
