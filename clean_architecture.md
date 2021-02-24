Clean Architecture 無瑕的程式碼
===

A Craftsman's Guide to Software Structure and Design 整潔的軟體設計與架構篇

Programming Paradigms 程式設計範式
---
* Structured programming 結構化程式設計
* Object-orient programming 物件導向程式設計
* Functional programming 函數式程式設計

Design Principles 設計原則 (SOLID)
---

- SRP 單一職責原則
    * 一個模組應該只對唯一的一個角色負責

- OCP 開放-封閉原則
    * 一個軟體製品應該對於擴展是開放的，但對於修改是封閉的

- LSP Liskov替換原則
    * 指導「繼承的使用」，並涉及介面與實作
    * 看看違反原則時，系統的架構會發生什麼事

- ISP 介面隔離原則
    * 不要依賴於包含未使用的方法的類別

- DIP 依賴反向原則
    * 不要參考易變的具體類別
    * 不要從易變的具體類別衍生
    * 不要改寫具體函式
    * 永遠不要提到任何具體和易變的名稱
    * 只涉及抽象，不涉及具體

Component Cohesion Principles 元件內聚性原則
---

- REP 再使用性-發佈等價原則(The Reuse/Release Equivalence Principle)
    * 再使用性的細微度就是發佈的細微度

- CCP 共同封閉原則(The Common Closure Principle)
    * 把那些在同一時間和相同的原因改變的東西聚集在一起。把那些在不同的時間或不同的原因改變的東西分離開來。
    * 如同 SRP

- CRP 共同重複使用原則(The Common Reuse Principle)
    * 不要依賴於你不需要的東西
    * 如同 ISP

- 三者關係圖
![](https://i.imgur.com/EaB5yX2.png)

[圖片來源](https://medium.com/@f40507777/%E5%85%83%E4%BB%B6%E5%85%A7%E8%81%9A%E6%80%A7-1a1c334fc3f7)

Component Coupling 元件耦合性
---

用來處理元件之間的關係

- ADP 無環依賴原則 (The Acyclic Dependencies Principle)
    * 在元件的依賴關係圖中不允許出現環

- SDP 穩定依賴原則 (The Stable Dependencies Principle)
    * 朝著穩定的方向進行依賴

- SAP 穩定抽象原則 (The Stable Abstractions Principle)
    * 元件的抽象程度應該與元件的穩定程度一致

Architecture 架構
---
* 軟體架構的目的是最小化建置與維護「需求系統」所需要的人力資源。
* The goal of sofrware architecture is to minimize the human resources required to build and maintain the required system.
* 為了「開發」「部署」「運行」「維護」的目的

Clean Architecture 整潔的架構
---
* 層級：與輸入及輸出的距離。離系統的輸入和輸出越遠，策略的層級就越高
* (心得)就我的理解，輸入和輸出就是「易變」的東西，所以，高層級就是不易變的東西
* 依賴規則(Dependency Rule)
    * 原始碼依賴關係只能指向內部，朝向更高層級的策略
    * 內圈沒有任何東西可以對外圈的事情有所了解
    * Source code dependencies can only point inwards. 
    * Nothing in an inner circle can know anything at all about something in an outer circle.

![](https://i.imgur.com/ggI3lom.jpg)

[圖片來源](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)



