# 小的 CL 變更清單 (Small CLs)

## 為什麼要寫小的 CL？ (Why Write Small CLs?) {#why}

小而簡單的變更清單是：

- **更快地進行審查。** 審查者比將 30 分鐘專門用於審查一個大的 CL，更容易找到數次 5 分鐘來審查小的 CL。
- **更仔細地進行審查。** 對於大的變更，審查者和作者往往會因為大量的詳細評論來回移位而感到沮喪，有時甚至會錯過或忽略重要點。
- **較不容易引入錯誤。** 由於進行較少的變更，您和審查者可以更容易地有效推理 CL 的影響並確認是否引入了錯誤。
- **在被拒絕時減少浪費的工作。** 如果您編寫了一個龐大的 CL，然後您的審查者說整個方向錯了，那麼您就浪費了很多工作。
- **更容易合併。** 在大的 CL 上工作需要很長時間，因此當您進行合併操作時會遇到很多衝突，而且您還需要經常進行合併。
- **更方便設計。** 改進小的變更的設計和程式碼更容易，而詳細修改大變更的所有細節要更困難。
- **在審查時的阻礙更少。** 傳送自包含的整個變更的部分可以讓您在等待當前 CL 審查時繼續撰寫程式碼。
- **還原更簡單。** 大的 CL 將更有可能觸及在初始 CL 提交和復原 CL 之間被更新的檔案，從而使復原變得更加複雜 (中間的 CL 可能也需要復原)。

Small, simple CLs are:

- **Reviewed more quickly.** It's easier for a reviewer to find five minutes several times to review small CLs than to set aside a 30 minute block to review one large CL.
- **Reviewed more thoroughly.** With large changes, reviewers and authors tend to get frustrated by large volumes of detailed commentary shifting back and forth—sometimes to the point where important points get missed or dropped.
- **Less likely to introduce bugs.** Since you're making fewer changes, it's easier for you and your reviewer to reason effectively about the impact of the CL and see if a bug has been introduced.
- **Less wasted work if they are rejected.** If you write a huge CL and then your reviewer says that the overall direction is wrong, you've wasted a lot of work.
- **Easier to merge.** Working on a large CL takes a long time, so you will have lots of conflicts when you merge, and you will have to merge frequently.
- **Easier to design well.** It's a lot easier to polish the design and code health of a small change than it is to refine all the details of a large change.
- **Less blocking on reviews.** Sending self-contained portions of your overall change allows you to continue coding while you wait for your current CL in review.
- **Simpler to roll back.** A large CL will more likely touch files that get updated between the initial CL submission and a rollback CL, complicating the rollback (the intermediate CLs will probably need to be rolled back too).

請注意，**審查者有權因變更過於龐大而直接拒絕您的變更。**通常他們會感謝您的貢獻，但要求您將其拆成一系列較小的變更。在您已經編寫變更之後，將其拆分可能需要很多工作，或需要花費很多時間爭論審查者為什麼要接受您的大型變更。在最初就編寫小的變更會更容易。

Note that **reviewers have discretion to reject your change outright for the sole reason of it being too large.** Usually they will thank you for your contribution but request that you somehow make it into a series of smaller changes. It can be a lot of work to split up a change after you've already written it, or require lots of time arguing about why the reviewer should accept your large change. It's easier to just write small CLs in the first place.

## 什麼是小？ (What is Small?) {#what_is_small}

通常而言，對於 CL (程式碼變更清單) 來說，**適當的大小為一項自包含的改變**。這代表：

- CL 的變更應該只針對一件事情，這通常只是一個功能的一部分，而不是整個功能。通常，相較於太大的 CL，寫較小的 CL 會更好一些。與您的審查者合作找出可以接受的大小。
- CL 應[包含相關的測試程式碼](#test_code)。
- 審查者需要瞭解 CL 的一切(除了未來的開發)是在 CL 本身、CL 的描述、現有的程式碼函式庫或他們已經檢查過的 CL 中。
- 在 CL 審查後系統將繼續為使用者和開發人員提供良好的功能。
- CL 的規模不應該太小，其影響難以理解。如果您新增了一個 API，應在同一個 CL 中包含 API 的用法，以便審查者更好地理解 API 的使用方式。這也可以避免未使用的 API 納入檢查。

In general, the right size for a CL is **one self-contained change**. This means that:

- The CL makes a minimal change that addresses **just one thing**. This is
  usually just one part of a feature, rather than a whole feature at once. In
  general it's better to err on the side of writing CLs that are too small vs.
  CLs that are too large. Work with your reviewer to find out what an
  acceptable size is.
- The CL should [include related test code](#test_code).
- Everything the reviewer needs to understand about the CL (except future
  development) is in the CL, the CL's description, the existing codebase, or a
  CL they've already reviewed.
- The system will continue to work well for its users and for the developers
  after the CL is checked in.
- The CL is not so small that its implications are difficult to understand. If
  you add a new API, you should include a usage of the API in the same CL so
  that reviewers can better understand how the API will be used. This also
  prevents checking in unused APIs.

關於「太大」的界定並沒有硬性的規則。通常來說，100 行是單一變更清單(CL)合理的大小，而 1000 行就太大了，但這取決於您的審查者的判斷。一個變更跨越的檔案數量也會影響其「大小」。一個 200 行在一個檔案的變更可能還好，但是跨越 50 個檔案就通常太大了。

There are no hard and fast rules about how large is "too large." 100 lines is
usually a reasonable size for a CL, and 1000 lines is usually too large, but
it's up to the judgment of your reviewer. The number of files that a change is
spread across also affects its "size." A 200-line change in one file might be
okay, but spread across 50 files it would usually be too large.

請記得，雖然你從寫程式碼最開始就參與其中，但審查者常常沒有上下文。對你而言，看起來尺寸合適的程式碼審查可能對審查者來說是難以負荷的。當你不確定時，給審查者的 CL 應比你認為需要寫的還要小。很少有審查者會抱怨 CL 太小。

Keep in mind that although you have been intimately involved with your code from
the moment you started to write it, the reviewer often has no context. What
seems like an acceptably-sized CL to you might be overwhelming to your reviewer.
When in doubt, write CLs that are smaller than you think you need to write.
Reviewers rarely complain about getting CLs that are too small.

## 何時能接受大型 CL？ (When are Large CLs Okay?) {#large_okay}

有一些情況下，大幅度的變更沒有那麼糟糕：

- 通常情況下，刪除整個檔案被視為一行變更，因為審查者並不需要花太長時間進行審查。
- 有時候大型 CL 是由完全信任的自動重構工具產生的，審查者的工作只是驗證並確定他們確實想要進行變更。這樣的 CL 可能會更大，儘管上面提到的一些注意事項（例如合併和測試）仍然適用。

There are a few situations in which large changes aren't as bad:

- You can usually count deletion of an entire file as being just one line of
  change, because it doesn't take the reviewer very long to review.
- Sometimes a large CL has been generated by an automatic refactoring tool
  that you trust completely, and the reviewer's job is just to verify and say
  that they really do want the change. These CLs can be larger, although some
  of the caveats from above (such as merging and testing) still apply.

## 高效撰寫小型 CL (Writing Small CLs Efficiently) {#efficiently}

如果您撰寫了一個小 CL，然後等待您的審查者批准它，然後再撰寫下一個 CL，那麼您將浪費很多時間。因此，您希望找到某種不會在等待審查時阻礙您工作的方式。這可能包括同時進行多個項目的工作、找到同意立即提供幫助的審查者、進行面對面的審查、進行配對程式設計或按照某種方式分割您的 CL，以使您可以立即繼續工作。

If you write a small CL and then you wait for your reviewer to approve it before
you write your next CL, then you're going to waste a lot of time. So you want to
find some way to work that won't block you while you're waiting for review. This
could involve having multiple projects to work on simultaneously, finding
reviewers who agree to be immediately available, doing in-person reviews, pair
programming, or splitting your CLs in a way that allows you to continue working
immediately.

## 分割 CLs (Splitting CLs) {#splitting}

當要處理具有潛在相依關係的多個 CL 工作時，通常在開始撰寫程式碼之前，先從高層次考慮如何分割和組織這些 CL 會很有幫助。

When starting work that will have multiple CLs with potential dependencies among
each other, it's often useful to think about how to split and organize those CLs
at a high level before diving into coding.

除了方便作者管理和組織程式碼，也能讓程式碼審查者更容易進行審查，進而提高程式碼審查效率。

Besides making things easier for you as an author to manage and organize your
CLs, it also makes things easier for your code reviewers, which in turn makes
your code reviews more efficient.

以下是一些將工作分解為不同 CL 的策略。

Here are some strategies for splitting work into different CLs.

### 堆疊多個變更 (Stacking Multiple Changes on Top of Each Other) {#stacking}

一種分割 CL 而不會阻礙自己的方式是寫一個小的 CL，將其傳送進行審查，然後立即開始編寫另一個基於第一個 CL 的 CL。大多數版本控制系統都有這種功能。

One way to split up a CL without blocking yourself is to write one small CL,
send it off for review, and then immediately start writing another CL *based* on
the first CL. Most version control systems allow you to do this somehow.

### 依檔案拆分 (Splitting by Files) {#splitting-files}

將 CL (變更清單) 拆分的另一種方法是將檔案分組成需要不同審查者但本身是獨立變更的內容。

Another way to split up a CL is by groupings of files that will require
different reviewers but are otherwise self-contained changes.

例如：您送出一份修改 Protocol Buffer 的程式碼的 CL (變更清單)，另一份為使用該 proto 程式碼的變更。 您必須先提交 proto CL，然後才能提交程式碼 CL，但它們都可以同時審查。 如果您這樣做，您可能希望通知兩組審查者關於您寫的另一份 CL，以便他們瞭解您的變更背景。

For example: you send off one CL for modifications to a protocol buffer and
another CL for changes to the code that uses that proto. You have to submit the
proto CL before the code CL, but they can both be reviewed simultaneously. If
you do this, you might want to inform both sets of reviewers about the other CL
that you wrote, so that they have context for your changes.

另一個例子：您傳送一個 CL 進行程式碼變更，另一個 CL 用於使用該程式碼的配置或實驗；如果必要，這也更容易復原，因為配置/實驗檔案有時會比程式碼變更更快地推送到生產環境。

Another example: you send one CL for a code change and another for the
configuration or experiment that uses that code; this is easier to roll back
too, if necessary, as configuration/experiment files are sometimes pushed to
production faster than code changes.

### 水平分割 (Splitting Horizontally) {#splitting-horizontally}

考慮建立共用程式碼或存根(stubs)，以協助隔離技術堆疊層之間的變更。這不僅有助於加快開發，也鼓勵在層之間進行抽象。

Consider creating shared code or stubs that help isolate changes between layers
of the tech stack. This not only helps expedite development but also encourages
abstraction between layers.

例如：您使用客戶端、API、服務和資料模型層建立了一個計算機應用程式。共享的 proto 簽名可以抽象出服務和資料模型層。同樣，API 存根可以將客戶端程式碼的實現與服務程式碼分離開來，使它們能夠獨立前進。類似的想法也可以應用於更細粒度的函式或類別層級的抽象。

For example: You created a calculator app with client, API, service, and data
model layers. A shared proto signature can abstract the service and data model
layers from each other. Similarly, an API stub can split the implementation of
client code from service code and enable them to move forward independently.
Similar ideas can also be applied to more granular function or class level
abstractions.

### 垂直分割 (Splitting Vertically) {#splitting-vertically}

與分層、水平方法不同，您可以將程式碼分解為較小的、全棧、垂直特性。這些特性中的每一個都可以是獨立的並行實現軌道。這使得一些軌道可以前進，而其他軌道正在等待審查或反饋。

Orthogonal to the layered, horizontal approach, you can instead break down your
code into smaller, full-stack, vertical features. Each of these features can be
independent parallel implementation tracks. This enables some tracks to move
forward while other tracks are awaiting review or feedback.

回到我們從[水平分割](#splitting-horizontally)範例中的計算機。現在你想要支援新的運算符，例如乘法和除法。你可以將此拆分為實現乘法和除法作為單獨的垂直或子功能，即使它們可能有一些重疊，例如共享按鈕樣式或共享驗證邏輯。

Back to our calculator example from
[Splitting Horizontally](#splitting-horizontally). You now want to support new
operators, like multiplication and division. You could split this up by
implementing multiplication and division as separate verticals or sub-features,
even though they may have some overlap such as shared button styling or shared
validation logic.

### 水平和垂直分割 (Splitting Horizontally & Vertically) {#splitting-grid}

為了更進一步，您可以結合這些方法，並繪製出一個執行計劃表，其中每個儲存格都是其自己獨立的 CL，在從模型（在底部）往上到客戶端的過程中開始。

| 層級    | 功能: 乘法      | 功能: 除法                   |
| ------- | --------------- | ---------------------------- |
| Client  | 新增按鈕        | 新增按鈕                     |
| API     | 新增端點        | 新增端點                     |
| Service | 實現轉換        | 共用轉換邏輯以供乘法使用乘法 |
| Model   | 新增 proto 定義 | 新增 proto 定義              |

To take this a step further, you could combine these approaches and chart out an
implementation plan like this, where each cell is its own standalone CL.
Starting from the model (at the bottom) and working up to the client:

| Layer   | Feature: Multiplication   | Feature: Division                              |
| ------- | ------------------------- | ---------------------------------------------- |
| Client  | Add button                | Add button                                     |
| API     | Add endpoint              | Add endpoint                                   |
| Service | Implement transformations | Share transformation logic with multiplication |
| Model   | Add proto definition      | Add proto definition                           |

## 區分重構 (Separate Out Refactorings) {#refactoring}

通常最好將重構與功能變更或錯誤修復分成不同的確認清單(CL)。例如，移動和重新命名類別應該在不同的 CL 中，不同於修復該類別中的錯誤。當它們是分開的時候，對於審查者來說更容易理解每個 CL 引入的變更。

It's usually best to do refactorings in a separate CL from feature changes or
bug fixes. For example, moving and renaming a class should be in a different CL
from fixing a bug in that class. It is much easier for reviewers to understand
the changes introduced by each CL when they are separate.

小的清理工作，例如修正本地變數的名稱，可以包含在功能變更或錯誤修正程式碼變更列表中。然而，如果重構的範圍太大，會導致目前程式碼變更列表的審查變得更加困難，那麼這就取決於開發人員和審查者的判斷了。

Small cleanups such as fixing a local variable name can be included inside of a
feature change or bug fix CL, though. It's up to the judgment of developers and
reviewers to decide when a refactoring is so large that it will make the review
more difficult if included in your current CL.

## 將相關的測試程式碼放在同一個 CL 中 (Keep related test code in the same CL) {#test_code}

CL 應包含相關的測試程式碼。請記住，這裡的「小」是指 CL 應該聚焦於概念上的想法，而不是單純的行數。

CLs should include related test code. Remember that [smallness](#what_is_small)
here refers the conceptual idea that the CL should be focused and is not a
simplistic function on line count.

任何新增或修改程式邏輯的程式變更記錄(CL)，都應該附上新的或更新後符合新行為的測試。純粹的重構(CL)（並非用來改變行為），也應包含測試；理想情況下，這些測試已經存在，但如果沒有，您應該加入它們。

A CL that adds or changes logic should be accompanied by new or updated tests
for the new behavior. Pure refactoring CLs (that aren't intended to change
behavior) should also be covered by tests; ideally, these tests already exist,
but if they don't, you should add them.

*獨立的*測試修改可以先放在單獨的 CL 中，類似於[重構指南](#refactoring)。包括：

- 驗證既有的提交的程式碼是否符合新的測試。
  - 確保重要的邏輯被測試覆蓋。
  - 增加對受影響程式碼進行後續重構的信心。例如，如果您想重構尚未被測試覆蓋的程式碼，則在提交重構變更之前提交測試變更，可以確保所測試的行為在重構之前和之後不會改變。
- 重構測試程式碼（例如引入輔助函式）。
- 引入較大的測試框架程式碼（例如整合測試）。

*Independent* test modifications can go into separate CLs first, similar to the [refactorings guidelines](#refactoring). That includes:

- Validating pre-existing, submitted code with new tests.
  - Ensures that important logic is covered by tests.
  - Increases confidence in subsequent refactorings on affected code. For
    example, if you want to refactor code that isn't already covered by
    tests, submitting test CLs *before* submitting refactoring CLs can
    validate that the tested behavior is unchanged before and after the
    refactoring.
- Refactoring the test code (e.g. introduce helper functions).
- Introducing larger test framework code (e.g. an integration test).

## 不要破壞建置作業 (Don't Break the Build) {#break}

如果您有幾個相互依存的 CL，您需要找到一種方式，確保在提交每個 CL 後整個系統仍然正常運作。否則，您可能會在您的 CL 提交之間的幾分鐘（甚至如果您後面的 CL 提交發生了意外故障，這段時間可能會更長）為您所有的同事開發人員破壞建置作業。

If you have several CLs that depend on each other, you need to find a way to
make sure the whole system keeps working after each CL is submitted. Otherwise
you might break the build for all your fellow developers for a few minutes
between your CL submissions (or even longer if something goes wrong unexpectedly
with your later CL submissions).

## 無法讓 CL 變的更小 (Can't Make it Small Enough) {#cant}

有時你會發現似乎必須要使用大 CL 的情況。但這很少是真的。經常練習使用小 CL 撰寫的作者幾乎總是可以找到將功能分解為一系列小變更的方法。

Sometimes you will encounter situations where it seems like your CL *has* to be
large. This is very rarely true. Authors who practice writing small CLs can
almost always find a way to decompose functionality into a series of small
changes.

在寫一個大的 CL 前，請考慮是否可以先用一個僅進行重構的 CL 鋪路，以實現一個更清晰的實作方式。與你的隊友交談，看看是否有任何想法可以將功能拆分成較小的 CL 實現。

Before writing a large CL, consider whether preceding it with a refactoring-only
CL could pave the way for a cleaner implementation. Talk to your teammates and
see if anybody has thoughts on how to implement the functionality in small CLs
instead.

如果所有這些選項失敗（這應該是非常罕見的情況），請事先獲得審查者的同意來審閱大型 CL，因此他們將會被警告即將到來的事情。在這種情況下，預計要花很長時間進行審查，要特別注意不引入錯誤並勤於編寫測試。

If all of these options fail (which should be extremely rare) then get consent
from your reviewers in advance to review a large CL, so they are warned about
what is coming. In this situation, expect to be going through the review process
for a long time, be vigilant about not introducing bugs, and be extra diligent
about writing tests.

接下來: [如何處理審查者意見 (How to Handle Reviewer Comments)](handling-comments.md)
