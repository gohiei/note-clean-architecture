# 領域驅動設計與簡潔架構入門實作

## 大綱

* 領域驅動設計
  * Domain-Driven Design (DDD) 簡介
* 看板系統簡介
  * ezKanban 實作練習 (1): 事件風暴與領域模型
  * ezKanban 實作練習 (2): 測試驅動開發

* 簡潔架構
  * 軟體架構的定義與目的
  * 簡潔架構三原則: 分層、相依性、跨層

* 參考書籍

## 領域驅動設計

* 何謂 Domain

  * Problem Domain
  
    * 應用程式邏輯所圍繞的知識和活動範圍
    * 在真實世界中，你的軟體所要解決的問題範圍
    * Domain 有大有小
 
  * Solution Domain

    * 採用 Machine/Computer 來解決問題
    * 需要塑模 (Domain Modeling)
    * 會產生 Domain Model - 可以用來***解決問題***就好

* 何謂 Driven
  * ~~Boss-Driven Design (BDD)~~
  * ~~Dealine-Driven Design (DDD)~~
  * Test-Driven Design (TDD)
  * Behavior-Driven Design (BDD)
  * Use-Case Driven/User Story Driven
  * DOmain-Driven Design (DDD)

* 何謂 Design
  * 設計就是決定產品的邊界
  * 設計就是決定你要設計什麼
  * 設計就是決定 Form 與 Context 的邊界(Boundry)
  * 用來找***作用力/限制條件(Force)***
  * Top-down 作法

* 領域驅動設計就是...
  * 開發軟體時專注於領域(domain)中的重要概念與商業邏輯(Business logic)，透過與領域專家(Domain Expert)***緊密溝通***，共同建立領域模型(Domain Model)，再以此領域模型作為軟體時做的基礎

* Paul Rauner's 3 pillars of DDD 
![](https://i.imgur.com/CN6QcwX.jpg)

* DDD重要觀念/名詞
  * Context
  * Domain
  * Domain Model
  * Uniquitious Language
  * Bounded Context
  * Strategic Design and Tactical Design
  * Domain Event
  * CQRS
  * ~~Event Sourcing~~

* DDD Overview
![](https://i.imgur.com/kwdXZPg.png)

* How to define bounded contexts?
  * Business boundaries/organization structures
  * Activities that, from an actor's perspectives, belong together
  * One-way information flow
  * Different meaning for the same noun
  * Different triggers (time vs. on demand) bounded contexts.
  * ***資料複製***是解耦的做法之一

* Domain Events
  * 領域專家/利益關係人感興趣的***事件***
    * 例如，已下單、已付款
  * 典型用途
    * 狀態同步 - eventual consistency
    * Event sourcing

## 看板系統簡介

* 看板系統(Kanban System)
  * 視覺化工作流程
  * 限制WIP
  * 管理工作流(Lead Time 交期/前置時間)
  * (ezKanban) https://ssl-ezscrum.csie.ntut.edu.tw/ezKanban-stable

* 事件風暴(Event Storming)便利貼
  * ***Domain Event***: 過去式, ex: User Created
  * Command: Create User
  * Read Model: 下決定的資訊, ex: username, password
  * Actor: 動作的人, ex: user, system
  * External System: google, sms
  * Policy(Rule/Process): 完成後要觸發的行為, ex: 建立預設個人頁面
  * Aggregate: 名詞, 初步可以無腦參考 Domain Event, 但還是要回頭檢視

* 便利貼
![](https://i.imgur.com/xuWPk1u.png)
(No database schema + no pineapple)

* 使用階段與時機
![](https://i.imgur.com/zZivVp0.png)

* 事件風暴執行步驟 (DDD: Collaborative Modeling)
  1. 找和領域相關的人來開會
  2. 新增 Domain Event，"各自操作，無需討論"
  3. 合併相同概念的 Domain Event，並決定好命名
  4. 如果有 Question，也請新增 (hot spots)
  5. 想像一個由左至右的時間軸，排列 Domain Event 產生順序
  6. 建立 Boundry Context，訂定名稱，並決定主要領域(Core Domain)
  7. 新增 Actor/External System/Question
  8. --- Big Picture END ---
  9. 新增 Command
  10. 新增 Read Model，可以落實為輸入參數
  11. 新增 Policy
  12. 如果 Policy 要觸發某些 Command，請把關係線拉出來表達
  13. --- Process Modelling END ---
  14. 新增 Aggregates，無腦新增名詞即可
  15. 透過 Aggragates，產生初步的 Domain Model
  16. 透過 Example 來檢視 Domain Model 是否合適 (迭代)
  17. --- Software Design END ---
  18. 最後可以補上一些自己想要的輔助資訊
  19. 例如：UI示意圖，Bounded Context 太大，適當地採用線來區隔

* 經過事件風暴，我們可以得到領域模型(Domain Model)

  * 結果: Domain Modeling
![](https://i.imgur.com/p4s1c08.png)
(事件風暴便利貼)

  * 結果: Domain Model
![](https://i.imgur.com/wn05dBI.png)
(領域模型 Domain Model)

## 簡潔架構(Clean Architecture)

* Why
  * 因為 DDD 的 Layered Architecture 並沒有多加著墨說明

* 軟體架構 Software Archiecture

  * The architecture of a software is the ***shape*** given to that system by those who build it.
  * The form of that shape is in the division of the system into ***components***, the ***arrangement*** of those components, and the ways in which those components ***communicate*** with each other.

* 軟體架構形狀的目的
  * The purpose of the shape is to facilitate the ****development****, ***deployment***, ***operation***, and ***maintenance*** of the software system containsed within it.
  * Defer commitment (延遲承諾)

* 雖然軟體架構與功能無關，但好的架構要能夠讓使用者看得出系統的功能

  * 例如，透過資料夾結構，可以看出大概要做什麼東西

* The ultimate goal of software architecture is to ***minimize*** the lifetime cost of the system and to ***maximize*** programmer productivity.

* 軟體架構師 Software Architect
  * Software architect is a programmer; and continues to be a programmer.
  * They cannot do their jobs properly if they are not experiencing the problems that they are creating for the rest of the programmers.

* A good architect maxinmizes the number of decisions not made.

* 整潔架構三原則
  * 分層原則
  * 相依性原則
  * 跨層原則

* 整潔架構
![](https://i.imgur.com/ggI3lom.jpg)

* 分層原則
  * 離 I/O 越遠的層級越高
  * 四個預設階層
    * Entities: Domain model object, 存放核心商業邏輯
    * Use Cases: 應用程式邏輯, 呼叫 Entities 或是 Repository 提供應用程式對外的服務
    * Interface Adapters: 將外部資料與呼叫介面透過此層轉呼叫 Use Cases，如此一來 Use Cases 就可以與I/O或是應用程式框架無關
    * Frameworks and Drivers: 包含應用程式框架、資料庫。鮮少有複雜的商業邏輯位於這一層。

* 相依性原則 Dependency Rule
  * 程式碼相依性必須只能往內，指向更高層級的策略

* 依賴反轉示意
![](https://i.imgur.com/Xx6of3A.png)

* 跨層原則
  * 定義雙向介面

![](https://i.imgur.com/tnIJI2n.png)

# Put it all together (DDD+ES+CA+TDD)

![](https://i.imgur.com/i6ELfj5.png)

* Examples

```
src/
├── common
│   ├── AggregateRoot.js
│   ├── DomainEvent.js
│   └── DomainEventBus.js
├── entities
│   ├── board
│   ├── card
│   ├── lane
│   └── workflow
│       ├── Events.js
│       └── Workflow.js
└── usecase
    ├── board
    ├── card
    ├── lane
    └── workflow
        ├── CreateWorkflowUseCase.js
        ├── CreateWorkflowUseCaseInput.js
        ├── CreateWorkflowUseCaseOutput.js
        ├── WorkflowRepository.js
        └── tests
```

```
.
├── account
│   ├── src
│   │   ├── main
│   │   │   ├── java/ntut/csie/sslab
│   │   │   │   └── account
│   │   │   │       ├── application
│   │   │   │       │   └── springboot
│   │   │   │       │       └── web
│   │   │   │       │           ├── config
│   │   │   │       │           │   ├── AccountDataSourceConfiguration.java
│   │   │   │       │           │   ├── AccountEventBusInjection.java
│   │   │   │       │           │   ├── RepositoryInjection.java
│   │   │   │       │           │   └── UseCaseInjection.java
│   │   │   │       │           └── AccountWebMain.java
│   │   │   │       └── users
│   │   │   │           ├── command
│   │   │   │           │   ├── adapter
│   │   │   │           │   │   ├── encyption
│   │   │   │           │   │   │   └── BCryptImpl.java
│   │   │   │           │   │   ├── repository
│   │   │   │           │   │   │   ├── UserData.java
│   │   │   │           │   │   │   ├── UserMapper.java
│   │   │   │           │   │   │   ├── UserRepositoryImpl.java
│   │   │   │           │   │   │   └── UserRepositoryPeer.java
│   │   │   │           │   │   └── restcontroller
│   │   │   │           │   │       ├── RegisterController.java
│   │   │   │           │   │       └── UnregisterController.java
│   │   │   │           │   ├── entity
│   │   │   │           │   │   ├── event
│   │   │   │           │   │   │   ├── EmailChanged.java
│   │   │   │           │   │   │   ├── ManagerUnregisteredUser.java
│   │   │   │           │   │   │   ├── NicknameChanged.java
│   │   │   │           │   │   │   ├── PasswordChanged.java
│   │   │   │           │   │   │   ├── Unregistered.java
│   │   │   │           │   │   │   ├── UserLoggedIn.java
│   │   │   │           │   │   │   ├── UserLoggedInFail.java
│   │   │   │           │   │   │   ├── UserRegistered.java
│   │   │   │           │   │   │   └── UserRegisteredFail.java
│   │   │   │           │   │   ├── Role.java
│   │   │   │           │   │   ├── User.java
│   │   │   │           │   │   └── UserBuilder.java
│   │   │   │           │   └── usecase
│   │   │   │           │       ├── user
│   │   │   │           │       │   ├── register
│   │   │   │           │       │   │   ├── RegisterInput.java
│   │   │   │           │       │   │   ├── RegisterOutput.java
│   │   │   │           │       │   │   ├── RegisterUseCase.java
│   │   │   │           │       │   │   └── RegisterUseCaseImpl.java
│   │   │   │           │       │   └── unregister
│   │   │   │           │       │       ├── UnregisterInput.java
│   │   │   │           │       │       ├── UnregisterOutput.java
│   │   │   │           │       │       ├── UnregisterUseCase.java
│   │   │   │           │       │       └── UnregisterUseCaseImpl.java
│   │   │   │           │       ├── Encrypt.java
│   │   │   │           │       └── UserRepository.java
│   │   │   │           └── query
│   │   │   │               ├── adapter
│   │   │   │               │   ├── presenter
│   │   │   │               │   │   └── get
│   │   │   │               │   │       ├── GetUserPresenter.java
│   │   │   │               │   │       └── UserViewModel.java
│   │   │   │               │   ├── repository
│   │   │   │               │   │   └── UserQueryRepositoryImpl.java
│   │   │   │               │   └── restcontroller
│   │   │   │               │       └── GetUserController.java
│   │   │   │               └── usecase
│   │   │   │                   ├── user
│   │   │   │                   │   └── get
│   │   │   │                   │       ├── GetUserInput.java
│   │   │   │                   │       ├── GetUserOutput.java
│   │   │   │                   │       ├── GetUserUseCase.java
│   │   │   │                   │       └── GetUserUseCaseImpl.java
│   │   │   │                   ├── ConvertUserToDto.java
│   │   │   │                   ├── UserDto.java
│   │   │   │                   └── UserQueryRepository.java
│   │   │   └── resources
│   │   │       └── application.properties
│   │   └── test
│   │       ├── java
│   │       │   └── ntut
│   │       │       └── csie
│   │       │           └── sslab
│   │       │               └── account
│   │       │                   ├── users
│   │       │                   │   ├── command
│   │       │                   │   │   ├── entity
│   │       │                   │   │   │   └── UserTest.java
│   │       │                   │   │   └── usecase
│   │       │                   │   │       └── user
│   │       │                   │   │           ├── RegisterUseCaseTest.java
│   │       │                   │   │           └── UnregisterUseCaseTest.java
│   │       │                   │   └── query
│   │       │                   │       └── user
│   │       │                   │           └── GetUserUseCaseTest.java
│   │       │                   ├── AbstractSpringBootJpaTest.java
│   │       │                   └── JpaApplicationTest.java
│   │       └── resources
│   │           ├── logback.xml
│   │           └── test.properties
│   ├── account.iml
│   └── pom.xml
├── board
│   ├── src
│   │   ├── main
│   │   │   ├── java/ntut/csie/sslab/kanban
│   │   │   │   ├── adapter
│   │   │   │   │   ├── controller
│   │   │   │   │   │   └── rest
│   │   │   │   │   │       └── springboot
│   │   │   │   │   │           ├── board
│   │   │   │   │   │           │   ├── create
│   │   │   │   │   │           │   │   └── CreateBoardController.java
│   │   │   │   │   │           │   └── getcontent
│   │   │   │   │   │           │       └── GetBoardContentController.java
│   │   │   │   │   │           ├── card
│   │   │   │   │   │           │   ├── changedeadline
│   │   │   │   │   │           │   │   └── ChangeCardDeadlineController.java
│   │   │   │   │   │           │   ├── changedescription
│   │   │   │   │   │           │   │   └── ChangeCardDescriptionController.java
│   │   │   │   │   │           │   ├── changeestimate
│   │   │   │   │   │           │   │   └── ChangeCardEstimateController.java
│   │   │   │   │   │           │   ├── changenote
│   │   │   │   │   │           │   │   └── ChangeCardNoteController.java
│   │   │   │   │   │           │   ├── changetype
│   │   │   │   │   │           │   │   └── ChangeCardTypeController.java
│   │   │   │   │   │           │   ├── create
│   │   │   │   │   │           │   │   └── CreateCardController.java
│   │   │   │   │   │           │   ├── delete
│   │   │   │   │   │           │   │   └── DeleteCardController.java
│   │   │   │   │   │           │   └── get
│   │   │   │   │   │           │       └── GetCardController.java
│   │   │   │   │   │           ├── lane
│   │   │   │   │   │           │   ├── create
│   │   │   │   │   │           │   │   ├── CreateStageController.java
│   │   │   │   │   │           │   │   └── CreateSwimLaneController.java
│   │   │   │   │   │           │   ├── get
│   │   │   │   │   │           │   │   └── GetLaneController.java
│   │   │   │   │   │           │   └── rename
│   │   │   │   │   │           │       └── RenameLaneController.java
│   │   │   │   │   │           └── workflow
│   │   │   │   │   │               ├── create
│   │   │   │   │   │               │   └── CreateWorkflowController.java
│   │   │   │   │   │               └── get
│   │   │   │   │   │                   └── GetWorkflowController.java
│   │   │   │   │   ├── gateway
│   │   │   │   │   │   ├── eventbus
│   │   │   │   │   │   │   └── google
│   │   │   │   │   │   │       ├── NotifyBoardAdapter.java
│   │   │   │   │   │   │       └── NotifyWorkflowAdapter.java
│   │   │   │   │   │   └── repository
│   │   │   │   │   │       └── springboot
│   │   │   │   │   │           ├── board
│   │   │   │   │   │           │   ├── BoardData.java
│   │   │   │   │   │           │   ├── BoardMapper.java
│   │   │   │   │   │           │   ├── BoardMemberData.java
│   │   │   │   │   │           │   ├── BoardMemberDataId.java
│   │   │   │   │   │           │   ├── BoardMemberMapper.java
│   │   │   │   │   │           │   ├── BoardRepositoryImpl.java
│   │   │   │   │   │           │   ├── BoardRepositoryPeer.java
│   │   │   │   │   │           │   ├── BoardWorkflowMapper.java
│   │   │   │   │   │           │   ├── CommittedWorkflowData.java
│   │   │   │   │   │           │   └── CommittedWorkflowMapper.java
│   │   │   │   │   │           ├── card
│   │   │   │   │   │           │   ├── CardData.java
│   │   │   │   │   │           │   ├── CardMapper.java
│   │   │   │   │   │           │   ├── CardRepositoryImpl.java
│   │   │   │   │   │           │   └── CardRepositoryPeer.java
│   │   │   │   │   │           └── workflow
│   │   │   │   │   │               ├── CommittedCardData.java
│   │   │   │   │   │               ├── CommittedCardDataId.java
│   │   │   │   │   │               ├── CommittedCardMapper.java
│   │   │   │   │   │               ├── LaneData.java
│   │   │   │   │   │               ├── LaneMapper.java
│   │   │   │   │   │               ├── WorkflowData.java
│   │   │   │   │   │               ├── WorkflowMapper.java
│   │   │   │   │   │               ├── WorkflowRepositoryImpl.java
│   │   │   │   │   │               └── WorkflowRepositoryPeer.java
│   │   │   │   │   └── presenter
│   │   │   │   │       ├── board
│   │   │   │   │       │   └── getcontent
│   │   │   │   │       │       ├── BoardContentViewModel.java
│   │   │   │   │       │       └── GetBoardContentPresenter.java
│   │   │   │   │       ├── card
│   │   │   │   │       │   └── get
│   │   │   │   │       │       ├── CardViewModel.java
│   │   │   │   │       │       ├── GetCardPresenter.java
│   │   │   │   │       │       └── GetCardsByLaneIdViewModel.java
│   │   │   │   │       ├── lane
│   │   │   │   │       │   └── get
│   │   │   │   │       │       ├── GetLanePresenter.java
│   │   │   │   │       │       └── LaneViewModel.java
│   │   │   │   │       └── workflow
│   │   │   │   │           └── get
│   │   │   │   │               ├── GetWorkflowPresenter.java
│   │   │   │   │               └── WorkflowViewModel.java
│   │   │   │   ├── application
│   │   │   │   │   └── springboot
│   │   │   │   │       └── web
│   │   │   │   │           ├── config
│   │   │   │   │           │   ├── KanbanDataSourceConfiguration.java
│   │   │   │   │           │   ├── RepositoryInjection.java
│   │   │   │   │           │   ├── RepositoryPeerInjection.java
│   │   │   │   │           │   └── UseCaseInjection.java
│   │   │   │   │           └── EzKanbanWebMain.java
│   │   │   │   ├── entity
│   │   │   │   │   └── model
│   │   │   │   │       ├── board
│   │   │   │   │       │   ├── event
│   │   │   │   │       │   │   ├── BoardCommittedToTeam.java
│   │   │   │   │       │   │   ├── BoardCreated.java
│   │   │   │   │       │   │   ├── BoardDeleted.java
│   │   │   │   │       │   │   ├── BoardEntered.java
│   │   │   │   │       │   │   ├── BoardLeft.java
│   │   │   │   │       │   │   ├── BoardMemberAdded.java
│   │   │   │   │       │   │   ├── BoardMemberRemoved.java
│   │   │   │   │       │   │   ├── BoardRenamed.java
│   │   │   │   │       │   │   ├── BoardUncommittedFromTeam.java
│   │   │   │   │       │   │   ├── WorkflowCommitted.java
│   │   │   │   │       │   │   └── WorkflowUncommitted.java
│   │   │   │   │       │   ├── Board.java
│   │   │   │   │       │   ├── BoardBuilder.java
│   │   │   │   │       │   ├── BoardMember.java
│   │   │   │   │       │   ├── BoardMemberBuilder.java
│   │   │   │   │       │   ├── BoardMemberType.java
│   │   │   │   │       │   ├── BoardSession.java
│   │   │   │   │       │   └── CommittedWorkflow.java
│   │   │   │   │       ├── card
│   │   │   │   │       │   ├── event
│   │   │   │   │       │   │   ├── CardBlocked.java
│   │   │   │   │       │   │   ├── CardCreated.java
│   │   │   │   │       │   │   ├── CardDeadlineChanged.java
│   │   │   │   │       │   │   ├── CardDeleted.java
│   │   │   │   │       │   │   ├── CardDescriptionChanged.java
│   │   │   │   │       │   │   ├── CardEstimateChanged.java
│   │   │   │   │       │   │   ├── CardNoteChanged.java
│   │   │   │   │       │   │   ├── CardTypeChanged.java
│   │   │   │   │       │   │   ├── CardUnblocked.java
│   │   │   │   │       │   │   ├── CategoryAssigned.java
│   │   │   │   │       │   │   ├── CategoryUnassigned.java
│   │   │   │   │       │   │   ├── TagAssigned.java
│   │   │   │   │       │   │   └── TagUnassigned.java
│   │   │   │   │       │   ├── Card.java
│   │   │   │   │       │   ├── CardBuilder.java
│   │   │   │   │       │   ├── CardType.java
│   │   │   │   │       │   └── CommittedTask.java
│   │   │   │   │       └── workflow
│   │   │   │   │           ├── event
│   │   │   │   │           │   ├── CardCommitted.java
│   │   │   │   │           │   ├── CardMoved.java
│   │   │   │   │           │   ├── CardUncommitted.java
│   │   │   │   │           │   ├── LaneRenamed.java
│   │   │   │   │           │   ├── LaneWipChanged.java
│   │   │   │   │           │   ├── StageCreated.java
│   │   │   │   │           │   ├── StageDeleted.java
│   │   │   │   │           │   ├── StageMoved.java
│   │   │   │   │           │   ├── SwimLaneCreated.java
│   │   │   │   │           │   ├── SwimLaneDeleted.java
│   │   │   │   │           │   ├── WipLimitSet.java
│   │   │   │   │           │   ├── WorkflowCreated.java
│   │   │   │   │           │   ├── WorkflowDeleted.java
│   │   │   │   │           │   └── WorkflowRenamed.java
│   │   │   │   │           ├── CommittedCard.java
│   │   │   │   │           ├── Lane.java
│   │   │   │   │           ├── LaneBuilder.java
│   │   │   │   │           ├── LaneLayout.java
│   │   │   │   │           ├── LaneType.java
│   │   │   │   │           ├── NullLane.java
│   │   │   │   │           ├── Stage.java
│   │   │   │   │           ├── SwimLane.java
│   │   │   │   │           ├── WipLimit.java
│   │   │   │   │           ├── Workflow.java
│   │   │   │   │           └── WorkflowBuilder.java
│   │   │   │   └── usecase
│   │   │   │       ├── board
│   │   │   │       │   ├── create
│   │   │   │       │   │   ├── CreateBoardInput.java
│   │   │   │       │   │   ├── CreateBoardUseCase.java
│   │   │   │       │   │   └── CreateBoardUseCaseImpl.java
│   │   │   │       │   ├── getcontent
│   │   │   │       │   │   ├── GetBoardContentInput.java
│   │   │   │       │   │   ├── GetBoardContentOutput.java
│   │   │   │       │   │   ├── GetBoardContentUseCase.java
│   │   │   │       │   │   └── GetBoardContentUseCaseImpl.java
│   │   │   │       │   ├── BoardDto.java
│   │   │   │       │   ├── BoardMemberDto.java
│   │   │   │       │   ├── BoardRepository.java
│   │   │   │       │   ├── CommittedWorkflowDto.java
│   │   │   │       │   ├── ConvertBoardMemberToDto.java
│   │   │   │       │   ├── ConvertBoardToDto.java
│   │   │   │       │   └── ConvertCommittedWorkflowToDto.java
│   │   │   │       ├── card
│   │   │   │       │   ├── create
│   │   │   │       │   │   ├── CreateCardInput.java
│   │   │   │       │   │   ├── CreateCardUseCase.java
│   │   │   │       │   │   └── CreateCardUseCaseImpl.java
│   │   │   │       │   ├── delete
│   │   │   │       │   │   ├── DeleteCardInput.java
│   │   │   │       │   │   ├── DeleteCardUseCase.java
│   │   │   │       │   │   └── DeleteCardUseCaseImpl.java
│   │   │   │       │   ├── edit
│   │   │   │       │   │   ├── deadline
│   │   │   │       │   │   │   ├── ChangeCardDeadlineInput.java
│   │   │   │       │   │   │   ├── ChangeCardDeadlineUseCase.java
│   │   │   │       │   │   │   └── ChangeCardDeadlineUseCaseImpl.java
│   │   │   │       │   │   ├── description
│   │   │   │       │   │   │   ├── ChangeCardDescriptionInput.java
│   │   │   │       │   │   │   ├── ChangeCardDescriptionUseCase.java
│   │   │   │       │   │   │   └── ChangeCardDescriptionUseCaseImpl.java
│   │   │   │       │   │   ├── estimate
│   │   │   │       │   │   │   ├── ChangeCardEstimateInput.java
│   │   │   │       │   │   │   ├── ChangeCardEstimateUseCase.java
│   │   │   │       │   │   │   └── ChangeCardEstimateUseCaseImpl.java
│   │   │   │       │   │   ├── note
│   │   │   │       │   │   │   ├── ChangeCardNoteInput.java
│   │   │   │       │   │   │   ├── ChangeCardNoteUseCase.java
│   │   │   │       │   │   │   └── ChangeCardNoteUseCaseImpl.java
│   │   │   │       │   │   ├── type
│   │   │   │       │   │   │   ├── ChangeCardTypeInput.java
│   │   │   │       │   │   │   ├── ChangeCardTypeUseCase.java
│   │   │   │       │   │   │   └── ChangeCardTypeUseCaseImpl.java
│   │   │   │       │   │   ├── EditCardInput.java
│   │   │   │       │   │   ├── EditCardOutput.java
│   │   │   │       │   │   ├── EditCardUseCase.java
│   │   │   │       │   │   └── EditCardUseCaseImpl.java
│   │   │   │       │   ├── get
│   │   │   │       │   │   ├── GetCardInput.java
│   │   │   │       │   │   ├── GetCardOutput.java
│   │   │   │       │   │   ├── GetCardUseCase.java
│   │   │   │       │   │   └── GetCardUseCaseImpl.java
│   │   │   │       │   ├── CardDto.java
│   │   │   │       │   ├── CardRepository.java
│   │   │   │       │   └── ConvertCardToDto.java
│   │   │   │       ├── eventhandler
│   │   │   │       │   ├── NotifyBoard.java
│   │   │   │       │   └── NotifyWorkflow.java
│   │   │   │       ├── lane
│   │   │   │       │   ├── get
│   │   │   │       │   │   ├── GetLaneInput.java
│   │   │   │       │   │   ├── GetLaneOutput.java
│   │   │   │       │   │   ├── GetLaneUseCase.java
│   │   │   │       │   │   └── GetLaneUseCaseImpl.java
│   │   │   │       │   ├── rename
│   │   │   │       │   │   ├── RenameLaneInput.java
│   │   │   │       │   │   ├── RenameLaneUseCase.java
│   │   │   │       │   │   └── RenameLaneUseCaseImpl.java
│   │   │   │       │   ├── stage
│   │   │   │       │   │   ├── create
│   │   │   │       │   │   │   ├── CreateStageInput.java
│   │   │   │       │   │   │   ├── CreateStageUseCase.java
│   │   │   │       │   │   │   └── CreateStageUseCaseImpl.java
│   │   │   │       │   │   └── get
│   │   │   │       │   │       ├── GetStagesByWorkflowIdInput.java
│   │   │   │       │   │       ├── GetStagesByWorkflowIdOutput.java
│   │   │   │       │   │       ├── GetStagesByWorkflowIdUseCase.java
│   │   │   │       │   │       └── GetStagesByWorkflowIdUseCaseImpl.java
│   │   │   │       │   ├── swimLane
│   │   │   │       │   │   └── create
│   │   │   │       │   │       ├── CreateSwimLaneInput.java
│   │   │   │       │   │       ├── CreateSwimLaneUseCase.java
│   │   │   │       │   │       └── CreateSwimLaneUseCaseImpl.java
│   │   │   │       │   ├── LaneDto.java
│   │   │   │       │   ├── StageDto.java
│   │   │   │       │   └── SwimLaneDto.java
│   │   │   │       ├── workflow
│   │   │   │       │   ├── create
│   │   │   │       │   │   ├── CreateWorkflowInput.java
│   │   │   │       │   │   ├── CreateWorkflowUseCase.java
│   │   │   │       │   │   └── CreateWorkflowUseCaseImpl.java
│   │   │   │       │   ├── get
│   │   │   │       │   │   ├── GetWorkflowInput.java
│   │   │   │       │   │   ├── GetWorkflowOutput.java
│   │   │   │       │   │   ├── GetWorkflowUseCase.java
│   │   │   │       │   │   └── GetWorkflowUseCaseImpl.java
│   │   │   │       │   ├── CommittedCardDto.java
│   │   │   │       │   ├── ConvertCommittedCardToDto.java
│   │   │   │       │   ├── ConvertLaneToDto.java
│   │   │   │       │   ├── ConvertWorkflowsToDto.java
│   │   │   │       │   ├── WorkflowDto.java
│   │   │   │       │   └── WorkflowRepository.java
│   │   │   │       └── ClientBoardContentMightExpire.java
│   │   │   └── resources
│   │   │       └── application.properties
│   │   └── test
│   │       ├── java/ntut/csie/sslab/kanban
│   │       │   ├── adapter
│   │       │   │   └── gateway
│   │       │   │       └── repository
│   │       │   │           └── springboot
│   │       │   │               ├── board
│   │       │   │               │   └── BoardRepositoryImplTest.java
│   │       │   │               └── workflow
│   │       │   │                   ├── LaneMapperTest.java
│   │       │   │                   └── WorkflowRepositoryTest.java
│   │       │   ├── entity
│   │       │   │   └── model
│   │       │   │       ├── board
│   │       │   │       │   ├── BoardDomainEventTest.java
│   │       │   │       │   └── BoardTest.java
│   │       │   │       ├── card
│   │       │   │       │   └── CardTest.java
│   │       │   │       └── workflow
│   │       │   │           ├── LaneTest.java
│   │       │   │           ├── StageTest.java
│   │       │   │           └── WorkflowTest.java
│   │       │   └── usecase
│   │       │       ├── board
│   │       │       │   ├── CreateBoardUseCaseTest.java
│   │       │       │   └── GetBoardContentUseCaseTest.java
│   │       │       ├── card
│   │       │       │   ├── ChangeCardDeadlineUseCaseTest.java
│   │       │       │   ├── ChangeCardDescriptionUseCaseTest.java
│   │       │       │   ├── ChangeCardEstimateUseCaseTest.java
│   │       │       │   ├── ChangeCardNoteUseCaseTest.java
│   │       │       │   ├── ChangeCardTypeUseCaseTest.java
│   │       │       │   ├── CreateCardUseCaseTest.java
│   │       │       │   ├── DeleteCardUseCaseTest.java
│   │       │       │   └── GetCardUseCaseTest.java
│   │       │       ├── lane
│   │       │       │   ├── CreateStageUseCaseTest.java
│   │       │       │   ├── CreateSwimLaneUseCaseTest.java
│   │       │       │   ├── GetLaneUseCaseTest.java
│   │       │       │   └── RenameLaneUseCaseTest.java
│   │       │       ├── workflow
│   │       │       │   ├── CreateWorkflowUseCaseTest.java
│   │       │       │   └── GetWorkflowUseCaseTest.java
│   │       │       ├── AbstractSpringBootJpaTest.java
│   │       │       └── JpaApplicationTest.java
│   │       └── resources
│   │           ├── logback.xml
│   │           └── test.properties
│   ├── board.iml
│   └── pom.xml
├── dddcore
│   ├── src
│   │   └── main/java/ntut/csie/sslab
│   │       └── ddd
│   │           ├── adapter
│   │           │   ├── gateway
│   │           │   │   └── GoogleEventBus.java
│   │           │   └── presenter
│   │           │       ├── cqrs
│   │           │       │   ├── CqrsCommandPresenter.java
│   │           │       │   └── CqrsCommandViewModel.java
│   │           │       ├── Presenter.java
│   │           │       └── ViewModel.java
│   │           ├── model
│   │           │   ├── common
│   │           │   │   ├── Contract.java
│   │           │   │   ├── DateProvider.java
│   │           │   │   ├── PostconditionViolationException.java
│   │           │   │   └── PreconditionViolationException.java
│   │           │   ├── AggregateRoot.java
│   │           │   ├── DomainEvent.java
│   │           │   ├── DomainEventBus.java
│   │           │   ├── Entity.java
│   │           │   └── ValueObject.java
│   │           └── usecase
│   │               ├── cqrs
│   │               │   ├── Command.java
│   │               │   ├── CqrsCommandOutput.java
│   │               │   ├── ExitCode.java
│   │               │   └── Query.java
│   │               ├── AbstractRepository.java
│   │               ├── Input.java
│   │               ├── Output.java
│   │               ├── Result.java
│   │               └── UseCase.java
│   ├── dddcore.iml
│   └── pom.xml
├── monomain
│   ├── src
│   │   └── main
│   │       ├── java/ntut/csie/sslab
│   │       │   └── ezkanban
│   │       │       ├── application
│   │       │       │   └── springboot
│   │       │       │       └── web
│   │       │       │           └── config
│   │       │       │               ├── AccountDataSourceConfiguration.java
│   │       │       │               ├── KanbanDataSourceConfiguration.java
│   │       │       │               └── TeamDataSourceConfiguration.java
│   │       │       └── MonoMain.java
│   │       └── resources
│   │           └── application.properties
│   ├── monomain.iml
│   └── pom.xml
├── team
│   ├── src
│   │   ├── main
│   │   │   ├── java/ntut/csie/sslab
│   │   │   │   └── team
│   │   │   │       ├── application
│   │   │   │       │   └── springboot
│   │   │   │       │       └── web
│   │   │   │       │           ├── config
│   │   │   │       │           │   └── TeamEventBusInjection.java
│   │   │   │       │           └── TeamMain.java
│   │   │   │       └── entity
│   │   │   │           └── model
│   │   │   │               └── team
│   │   │   │                   ├── event
│   │   │   │                   │   ├── BoardCommittedToTeam.java
│   │   │   │                   │   ├── BoardMovedToProject.java
│   │   │   │                   │   ├── BoardMovedToTrash.java
│   │   │   │                   │   ├── BoardRemovedFromProject.java
│   │   │   │                   │   ├── BoardRestored.java
│   │   │   │                   │   ├── BoardUncommittedFromTeam.java
│   │   │   │                   │   ├── CommittedBoardRenamed.java
│   │   │   │                   │   ├── ProjectCreated.java
│   │   │   │                   │   ├── ProjectDeleted.java
│   │   │   │                   │   ├── ProjectRenamed.java
│   │   │   │                   │   ├── TeamCreated.java
│   │   │   │                   │   ├── TeamDeleted.java
│   │   │   │                   │   └── TeamMemberAdded.java
│   │   │   │                   ├── Board.java
│   │   │   │                   ├── BoardId.java
│   │   │   │                   ├── Project.java
│   │   │   │                   ├── ProjectId.java
│   │   │   │                   ├── Role.java
│   │   │   │                   ├── Team.java
│   │   │   │                   ├── TeamBuilder.java
│   │   │   │                   ├── TeamId.java
│   │   │   │                   ├── TeamMember.java
│   │   │   │                   └── TeamName.java
│   │   │   └── resources
│   │   │       └── application.properties
│   │   └── test/java/ntut/csie/sslab/team
│   │       └── entity
│   │       └── model
│   │       └── team
│   │           ├── ProjectTest.java
│   │           └── TeamTest.java
│   ├── pom.xml
│   └── team.iml
├── README.md
├── ezKanban.iml
├── kanban.iml
└── pom.xml
```

## 參考書籍

* [Clean Architecture (Martin/Unicle Bob)](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164/ref=sr_1_1?crid=Y0BWFNN1YTF3&keywords=clean+architecture&qid=1571383127&s=books&sprefix=clean+ar%2Cstripbooks-intl-ship%2C309&sr=1-1)
* [Implementing Domain-Driven Design (Vaughn)](https://www.amazon.com/-/zh_TW/dp/B00BCLEBN8/ref=sr_1_3?crid=2RGMP787ZO42W&dchild=1&keywords=domain-driven+design&qid=1617954050&s=books&sprefix=Domain-%2Cstripbooks-intl-ship%2C347&sr=1-3)
* [Domain-Driven Design (Eric Evans)](https://www.amazon.com/-/zh_TW/dp/0321125215/ref=sr_1_1?dchild=1&keywords=domain-driven+design&qid=1617954228&s=books&sr=1-1)