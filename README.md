## ergodash_v99_ble
zmk - ergodash - trackpoint - bluetooth - split keyboard
![image](https://github.com/ouser555/ergodash_v99_ble/blob/main/pic/02.jpg)
![image](https://github.com/ouser555/ergodash_v99_ble/blob/main/pic/03.jpg)
![image](https://github.com/ouser555/ergodash_v99_ble/blob/main/pic/04.jpg)
## 版本特色
* zmk / bluetooth 5.2 nrf52840
* hot swappable key switches
* Per-Key RGB LED SK6812
* trackpoint => zmk官方尚未支援，未來會更新
* user interface => zmk官方尚未支援，未來會更新
* 110mAh
* 充電電流100mA，慢充延長電池壽命。
* 15分鐘未操作，進入睡眠模式，耗電流60~80uA左右
* 操作中待機，耗電流800uA左右
* 配對廣播狀態，耗電流1000uA左右


## 燒錄方式
* firmware資料夾內有left、right兩個資料夾，放左右手的燒錄檔(zmk.uf2)，
  左鍵點進檔案，然後右上方有download，點擊下載。
  
* 鍵盤連接電腦USB後，連按兩下鍵盤上的Reset鍵進入bootloader mode，

  成功會持續閃綠燈，電腦會把鍵盤辨識為一個隨身碟，
  
  從我的電腦打開這個隨身碟，把zmk.uf2複製進去，
  
  複製完即是燒錄完成，隨身碟會自動退出。
  
* 如果上述燒錄步驟正確的話，鍵盤為新的狀態，但之前已配對的資料還是會保留。


## 操作方式
* 左右手燒好各自的燒錄檔後可以兩邊同時按Reset鍵，讓兩邊鍵盤自動配對。

  正常情況下左右邊配對好就會一直保持著，除非刻意去改。
  
* 不使用TRRS線的設計，即使是USB有線模式，左右手鍵盤通訊還是使用無線。  

* 左邊鍵盤為主鍵盤，只有插左邊USB電腦端才會辨識為鍵盤。

* 左邊鍵盤插著USB即為USB模式，USB斷開即為藍牙模式。

* 可先使用USB模式測試左右鍵盤是否有配對成功。

* 藍牙模式與一般藍牙鍵盤配對使用方式無異。


## 更改按鍵映射功能
  * 目前沒有更改keycode的user interface，只能靠更改程式碼來改變鍵碼。
  
  * 可以用文字編輯器打開 ergodash/ergodash.keymap 修改需要的鍵碼，然後進行編譯燒錄。
  
  * https://github.com/ouser555/ergodash_v99_ble/blob/main/ergodash/ergodash.keymap
  
## 常用功能粗略介紹:
  
  * RGB (此版已預設3個RGB功能鍵)
    
    1. 最左下角往上第二個鍵為LOWER層切換鍵
    
    2. LOWER鍵按住，同時按上方第二個鍵為RGB開關。
    
    3. LOWER鍵按住，同時按上方第一個鍵為RGB色相切換。
    
      * 目前沒有設定更多RGB功能鍵
    
      * 其他請參照ZMK官方鍵碼
      * https://zmk.dev/docs/behaviors/underglow
    
      
  * 藍牙功能
    
      * 參照ZMK官方鍵碼
      * https://zmk.dev/docs/behaviors/bluetooth
      
    
  * 一般鍵碼
    
      * 參照ZMK官方鍵碼
      * https://zmk.dev/docs/codes/

## 編譯方式

* 1. 先建立ZMK開發環境
  * 在linux terminal底下，依照官網的說明無腦複製貼上執行幾乎可以完成所有步驟
  * https://zmk.dev/docs/development/setup
  * 如果是使用Debian/Ubuntu系統，選擇Debian/Ubuntu菜單即是Debian/Ubuntu的說明，
  * Windows編譯方式實際試過，有一些問題，請盡量使用其他方式。
  
  
* 2. 將ergodash資料夾
  * https://github.com/ouser555/ergodash_v99_ble/tree/main/ergodash
  * 放到ZMK/app/boards/shields/資料夾底下
  
  
  * 此時可以修改自己需要的 ergodash.keymap
  
  
  * 用terminal進到zmk/app/ 後執行
    * west build -d build/left -b nrfmicro_13 -- -DSHIELD=ergodash_left
    * west build -d build/right -b nrfmicro_13 -- -DSHIELD=ergodash_right
  
  
  * 成功後燒錄檔會放在
    * /zmk/app/build/left/zephyr/zmk.uf2
    * /zmk/app/build/right/zephyr/zmk.uf2


  ### 補充注意事項
  * 編譯已編譯過的鍵盤
    * 之前編譯過的鍵盤，會有一些檔案產生，並且被保留下來。
    * 這些檔案有時會直接套用在新編譯的鍵盤上，造成有些修改沒有生效，
    * 所以一般建議編譯時加上-p這個參數，在編譯時可以先清除掉這些檔案。
      
    * west build -p -d build/left -b nrfmicro_13 -- -DSHIELD=ergodash_left
    * west build -p -d build/right -b nrfmicro_13 -- -DSHIELD=ergodash_right


## 常見問題
* Q1:連按兩下Reset鍵進入bootloader模式，綠燈有閃爍，但是沒有辨識成隨身碟。

  A:應該是電腦驅動程式跑掉了。
  * 解決方式:
    1. 換USB孔試試看。
    2. 裝置管理員找到該裝置，重新安裝驅動。
    3. 重新開機。


* Q2:無法和主機成功配對

  A:應該是配對資料錯亂了，或是目前頻道已有其他配對資料。

  * 解決方式1:

    找到keymap裡面有沒有按鍵被設為 &bt BT_CLR
    按這個鍵可以清除目前鍵盤頻道的配對資料，然後就可以重新配對。
  
  * 解決方式2:

    到firmware/nrfmicro_13-settings_reset-zmk/底下，zmk.uf2燒錄檔，一樣點擊download下載。

    進入bootloader模式，把這個檔案燒進去，重置配對資訊。

    然後再重燒一次左右手的daochoc燒錄檔。

    兩邊燒完後同時按Reset鍵，左右手鍵盤連接後，再與電腦配對應該就可以成功配對。

* Q3:左右邊沒有辦法成功配對

  A:應該是配對資料錯亂了，或是目前頻道已有其他配對資料。

  * 解決方式:
    
    到firmware/nrfmicro_13-settings_reset-zmk/底下，zmk.uf2燒錄檔，一樣點擊download下載。

    進入bootloader模式，把這個檔案燒進去，重置配對資訊。

    然後再重燒一次左右手的ergodash燒錄檔。

    兩邊燒完後同時按Reset鍵，應該就可以重新配對。
