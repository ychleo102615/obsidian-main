---
tags: 
date: 2024-10-21
time: 10:11
---
# [Spine事件 & AnimationState回调函数](http://zh.esotericsoftware.com/spine-unity-events#Spine%E4%BA%8B%E4%BB%B6-amp;-AnimationState%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0)

![image](http://zh.esotericsoftware.com/img/spine-runtimes-guide/spine-unity/callbackchart.png)
像是complete和end的差異，從中的圖表就能看得很清楚。

[[2025-02-20|2025-02-20 週四, 11:00]]
今天問了cursor如何寫註解。

```lua
---@alias SpineAnimationEventType
---| `SP_ANIMATION_START` # 动画开始
---| `SP_ANIMATION_END` # 动画结束
---| `SP_ANIMATION_COMPLETE` # 动画完成
---| `SP_ANIMATION_EVENT` # 动画事件
SP_ANIMATION_START = 0
SP_ANIMATION_END = 1
SP_ANIMATION_COMPLETE = 2
SP_ANIMATION_EVENT = 3

---@param eventType SpineAnimationEventType 动画事件类型
---@param trackIndex number 轨道索引
function onAnimationEvent(eventType, trackIndex)
	-- 函数实现
end
```