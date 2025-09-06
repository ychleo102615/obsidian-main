# 學到的東西
- DDD架構實作
- Emmylua註解的寫法

# 優點
- 後期分工明確
- 新增、調整功能時，有自信其它功能的程式碼不會被影響到（只要entity沒有動到）
- 在了解Clean architecture 的情況下，程式碼易於理解。即使幾個月沒碰程式碼，應該也可快速上手。

# 缺點
- 初期開發速度慢
- 程式碼整體較繁冗
- 以前端來說，有時候先做view才會對元件的功能有更好的理解，這違反開發順序。若非語言為lua，開發上應該會比較困難

# 可調整處
- 省略port類型檔案，命名風格保留精神即可（例：類型newRoundUseCasse不存在，但是newRoundController仍以該變數命名儲存newRoundService元件）
- 省略controller類型檔案，從這次專案來說，該類型檔案也沒有做到特別的事，一樣用變數命名保留精神即可
- 建立delayManager協助presenter進行非動畫的延遲呼叫功能

