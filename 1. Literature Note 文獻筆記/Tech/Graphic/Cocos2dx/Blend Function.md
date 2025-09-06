---
tags: []
date: 2024-06-06
time: 14:30
---
# 一般Sprite的預設Blend Function

```cpp
// ccMacros.h
#define CC_BLEND_SRC GL_ONE
#define CC_BLEND_DST GL_ONE_MINUS_SRC_ALPHA

// CCSprite.cpp
m_sBlendFunc.src = CC_BLEND_SRC;
m_sBlendFunc.dst = CC_BLEND_DST;

```


# 高亮效果的Blend Function
```lua
local blendFunc = ccBlendFunc:new()
blendFunc.src = GL_SRC_ALPHA
blendFunc.dst = GL_ONE
sp:setBlendFunc(blendFunc)
```
常看到一些黑色底圖，都是會設定這個blend function。