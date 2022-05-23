# mac 工具
## alfred 4
主要：clipboard history
清除dns workflow
```
tell application "Google Chrome"
	open location "chrome://net-internals/#sockets"
	delay 1
	execute front window's active tab javascript "document.getElementById('sockets-view-flush-button').click()"
	close front window's active tab
	execute front window's active tab javascript "location.reload();"
end tell
```

## Moom
调整窗口大小

## HyperSwitch
同应用多窗口切换

## draw.io
画图

## switchHost
切换电脑host
