---
layout: post
title: Mac에서 Vim 명령모드 전환시 자동 한영 전환
feature-img: "assets/img/pexels/desk-messy.jpeg"
tags: [vim, esc]
---

이번에 mac을 다시 설정하면서 하나하나 설정 할 때마다 기록하기로 한다.


```bash
brew cask hammerspoon
```

hammerspoon에서 config를 다음과 같이 수정한다.
(웹 서핑으로 찾아낸 것. 예전에 찾은거라 저작권은 그분께 있음. 고마운분.)

esc를 누를 때 바로 한영 전환을 하면 다른 프로그램의 영향을 받으므로,
ctrl + [ 키를 누를 때 한영이 전환 되도록 설정

```lua
local caps_mode = hs.hotkey.modal.new()
local inputEnglish = "com.apple.keylayout.ABC"

local on_caps_mode = function()
    caps_mode:enter()
end

local off_caps_mode = function()

    caps_mode:exit()

    local input_source = hs.keycodes.currentSourceID()

    if not (input_source == inputEnglish) then
        hs.keycodes.currentSourceID(inputEnglish)
    end
    hs.eventtap.keyStroke({}, 'escape')
end

hs.hotkey.bind({'control'}, '[', on_caps_mode, off_caps_mode)
```