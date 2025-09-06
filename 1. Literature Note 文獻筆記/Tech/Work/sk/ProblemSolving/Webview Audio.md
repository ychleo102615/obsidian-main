Cocos-2dx使用simple audio engine 與 CCWebviewNode遇到的問題






# Bug 敘述

僅IOS發生，目測是靜默重連強制關閉web view時沒有觸發close callback。造成BGM沒有重啟

編號：286

git參考：848055

從影片中發現，立刻返回app時，webview沒有立刻關閉，且遊戲會播放bgm（代表WebViewLayer的closeCallback已被呼叫）。但是可能因為webview影片沒有立刻關閉，系統又把遊戲bgm卡了。





## 複測步驟：

### [重點復線步驟] 開起影片後切前後景

1.  開啟「大獎秀」，音效應關閉
    
2.  播放影片（可以多測試全螢幕、子母畫面、等到影片播完等情況）
    
3.  切換前後景，音效應「瞬間」回復，然後可能：
    
    1.  卡頓一下
        
    2.  音效漸出後回復
        
4.  重複1~3幾次
    

### 保險起見的其他測試

### 1. 單純開關webview

1.  開啟「大獎秀」，音效應關閉
    
2.  立刻關閉，音效應回復
    
3.  重複1~2 幾次
    

### 2. 開啟webview後切前後景

1.  開啟「大獎秀」，音效應關閉
    
2.  切換前後景後，webview自動關閉，音效應「瞬間」回復，並卡頓一下
    
3.  重複1~2 幾次
    

### 3. 單純開關影片

1.  開啟「大獎秀」，音效應關閉
    
2.  播放影片
    
3.  關閉影片、關閉webview，音效應回復
    
4.  重複1~3幾次
    

p.s. 音效「瞬間」回復代表此行為是AppDelegate切前後景時自動呼叫，非遊戲控制。

### 重啟問題原因：

base 3.4.7的修正後來發現沒有成功解決問題（光從onExit的時機無法等到webview影片播放完全清除，出現遊戲音效停止兩次的現象）

目前有思考兩種修改方式：

1.  待webview完全清除後再回復音效（參考[此方式]([https://stackoverflow.com/questions/31513846/uiwebview-not-stopping-immediately](https://stackoverflow.com/questions/31513846/uiwebview-not-stopping-immediately) ）：
    
    1.  將網頁內容設空並且待載入完成後再行exitcallback後，仍然無法解決問題。
        
        ```
        /‌/ BOGamesDev/projects/BOGames/Classes/Util/CCWebViewNode.cpp
        // 页面加载完成之后调用
        void CCWebViewNode::didFinishNavigationLuaCallback(int callback) {
            _impl->didFinishNavigationLuaCallback = callback;
        }
        ```
        
    2.  使用reload，並待載入完成後再行exitcallback，目前測起來應該有解決
        
2.  延遲後檢測音效是否有在播放，再回復音效：
    
    1.  此方式目前只有找到 audio.isMusicPlaying()，但是被webview中斷的音效用此方式無法判斷（仍然顯示true）
        

### 目前解法採用1-b