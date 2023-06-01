## JVAV 教學https://openhome.cc/Gossip/JavaEssence/
### ★JVM：https://openhome.cc/Gossip/JavaEssence/WhyJVM.html
- java檔編譯為class的byte檔後由JVM編譯為相應的機器碼
- JVM有個很重要的觀念就是：
「對於Java程式而言，其實它只認識一種作業系統（或說是一種機器），這個系統叫作JVM，
而對於JVM而言，位元碼檔案就是它的可執行檔案！也就是副檔名為.class的檔案。
Java程式理想上，並不用理會真正執行於哪個平台之上，它只要知道如何執行於JVM之上就可以了，
至於JVM實際上如何與底層平台作溝通，則是JVM自己的事！」
### ★JRE：https://openhome.cc/Gossip/JavaEssence/WhatJRE.html
- （Java Runtime Environment）
- 有javac所以單純執行不須編譯為class檔時只需安裝JRE，稱為public JRE
- 執行Java的標準API(JAVA SE)和打包工具等等
### ★JDK：https://openhome.cc/Gossip/JavaEssence/InstallJDK.html
- JDK就包括了JRE，JRE包括了Java SE API與JVM
- 有java指令，可將.java檔編譯為.class檔，所以開發人員必備
- 還有包含private JRE用來執行內部的lib
***
### ★javac
- 編譯java檔為class檔
### ★java
- 編譯為class檔
  ```
  javac -encoding utf-8 <java file>
  ```
- 執行class檔
- 執行class檔時須注意package路徑，或是使用-cp來指定
  ```
  package name = com.example
  class name = Demo
  目前path與Demo.class相同
  java -cp ..\.. com.example.Demo
  ..\..表示切回上2層目錄，這樣package and class才對的上com.example.Demo
  ```
### ★transient
- 不會被序列化，該物件不會被寫入文件、或通過網路傳輸
### ★volatile
- 多個thred同時修改一個值時，能確保都可以讀取到最新的數值
### ★Synchronized
- 一次只能執行一個
