---
title: "MicroPython外部中斷"
date: 2019-11-08
last_modified_at: 2019-11-08
categories:
  - blog
tags:
  - MicroPython
  - ESP8266
permalink: /blog/2019-11-08-01
---
首先我們需要一個中斷處理函數,該函數接受 [machine.Pin](http://docs.micropython.org/en/latest/library/machine.Pin.html#machine-pin) 類型的參數
```python
import machine
def handle_interrupt(pin:machine.Pin):
    print(pin.Value(0))
```
設置用作中斷的引脚
```python
import machine
gpio = machine.Pin(0,machine.Pin.IN,machine.Pin.PULL_UP)
gpio.irq(handler=handler_interrupt,trigger=machine.Pin.IRQ_FALLING,priority=1,wake=None,hard=False)
```
其中 machine.Pin.irq 方法參數為

- handler (可選,默認值為None) 是在中斷時調用的函數
- trigger (默認值為 (machine.Pin.IRQ_FALLING | machine.Pin.IRQ_RISING) )可以產生中斷的事件,可以使用 或 選擇多個情況,可能值為:
    - machine.Pin.IRQ_FALLING 在電平下降時中斷
    - machine.Pin.IRQ_RISING  在電平上升時中斷
    - machine.Pin.IRQ_LOW_LEVEL 低電平中斷
    - mcahine.Pin.IRQ_HIGH_LEVEL 高電平中斷
- priority (默認為1)設置中斷優先級
- wake (默認為None)選擇可喚醒系統的電源模式,可以使用 或 選擇多個電源模式,可能值為:
    - machine.IDLE 
    - machine.SLEEP
    - machine.DEEPSLEEP
- hard (默認False)設置硬中斷

