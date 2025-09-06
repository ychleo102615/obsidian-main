---
tags: 
date: 2024-01-17
time: 11:07
---
- GameUpdate(Updater?) downloadAndUncompress     應該是專案lua檔中解壓縮檔案的功能
- 所以應該是下載、解壓所的功能留在cpp端，讓lua去呼叫它


`OPEN_UPDATE`這個flag似乎是關乎遊戲能否像貪玩那樣熱更遊戲。（但是模擬器或是自己建的安裝包應該都是不行自己熱更。）



## 研究熱更流程
```
HTTP requst
LogoLayer:sendRequest
	LHttpManager.httpCompleted
LogoLayer:tryNextAPIDomain


LogoLayer:checkBaseUpdate
	GameHelper.requestModuleVersions
		GameUpdate.requestVersions
	
	UpdateHelper(GameUpdateHelper).start
		GameUpdate.start
			downloadAndUncompress
				(C++)AssetsManager::update



url: host/pkds/packages/ios/pkds0.2.4-0.2.5
```

## 自行新增cpp檔
遇到的幾個雷點：
1. 檔案如果是從xcode外新增，在xcode中還是要額外加入其reference，不然xcode中看不到
2. `Build Phases -> Compile Sources`我還要再裡面把新增的檔案加進去，不然會出現`Undefined Symbols`
3. 找不到`CCHttpRequest`，是因為沒有`#include cocos-ext.h`，還要`USING_NS_CC_EXT`
4. 要注意函數簽章（this 不是 CCObject ，不符合接口）




一些全域變數，長得像kCC....的，有被標記在`GlobalDef.lua`。


`coroutine.wrap(), coroutine.yield(), coroutine.resume()`
~~我覺得不是很有必要使用。他們的好處應該是，讓不同執行緒的工作，可以用看起來像是一段普通走過去的程式一樣使用（不用等事件跳來跳去）。~~
~~這樣反而有種變複雜的感覺。~~
我後來發現，像是如果要處理多緒的行為的話，這種方式會比較好。

```lua
coroutine.wrap(function()
    local schedulerId;
	local thread = coroutine.running()
    local result;
    schedulerId = scheduler.scheduleUpdateGlobal(function()
        if not self.fetcher:hasFetched() then
            print("fetching...");
            return;
        end
        scheduler.unscheduleGlobal(schedulerId);
        result = self.fetcher:getFetchStatus();
        if result == kGameNamesFetch_success then
            self:_onFetchSucess();
        else
            print("fetch failed");
        end
        coroutine.resume(thread);
    end);
    coroutine.yield();

	-- 這行可以等到可能好幾秒以後，收到結果後才執行
    print("get Result" .. tostring(result));
end)();
```


[[2024-02-02|2024-02-02, 14:52]]
### 刪除zip檔
```lua
-- GameUpdate.start()
FileUtil.rmZip(GameUpdate.getStoragePath() .. packageName .. ".zip");
```
