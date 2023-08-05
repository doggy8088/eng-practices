# 在程式碼審查中要注意的事項 (What to look for in a code review)

注意：在考量這些點時，請務必考慮[程式碼審查標準](standard.md)。

Note: Always make sure to take into account
[The Standard of Code Review](standard.md) when considering each of these
points.

## 設計 (Design)

在回顧中需要重點涵蓋的是變更清單的整體設計。變更清單中各個程式碼部分間的互動是否有意義？這種變更應該屬於您的程式碼庫還是函式庫？它是否與系統的其餘部分良好整合？此功能現在新增是否恰當？

The most important thing to cover in a review is the overall design of the CL.
Do the interactions of various pieces of code in the CL make sense? Does this
change belong in your codebase, or in a library? Does it integrate well with the
rest of your system? Is now a good time to add this functionality?

## 功能 (Functionality)

這個變更清單(CL)是否符合開發人員的意圖？開發人員意圖的內容是否對這段程式碼的使用者有益？「使用者」通常指最終使用者(當他們受到變更影響時)和開發人員(將來必須「使用」此程式碼的人)。

Does this CL do what the developer intended? Is what the developer intended good
for the users of this code? The "users" are usually both end-users (when they
are affected by the change) and developers (who will have to "use" this code in
the future).

通常，我們期望開發人員在程式碼測試完成後再進行程式碼審查。然而，作為審查者，你仍應該考慮邊緣情況、尋找並發問題、以用戶的角度思考，且確保在讀取程式碼時並未發現任何錯誤。

Mostly, we expect developers to test CLs well-enough that they work correctly by
the time they get to code review. However, as the reviewer you should still be
thinking about edge cases, looking for concurrency problems, trying to think
like a user, and making sure that there are no bugs that you see just by reading
the code.

如果需要的話，您可以驗證變更清單（CL） - 當 CL 產生使用者端影響（例如 UI 變更）時，審查者檢查 CL 行為是最重要的時候。當您只是閱讀程式碼時，很難理解一些變更會如何影響使用者。對於這樣的更改，如果在 CL 中套用和自行測試太麻煩，您可以要求開發人員向您展示功能的示範。

You *can* validate the CL if you want—the time when it's most important for a
reviewer to check a CL's behavior is when it has a user-facing impact, such as a
**UI change**. It's hard to understand how some changes will impact a user when
you're just reading the code. For changes like that, you can have the developer
give you a demo of the functionality if it's too inconvenient to patch in the CL
and try it yourself.

另一個需要在程式碼審查中特別考慮功能性的時間是，如果在 CL 中存在某種**並行程式設計**，理論上可能會導致死鎖或競態條件。這些問題通常很難僅透過運行程式碼就檢測到，通常需要開發人員和審查人員仔細思考，以確保沒有引入問題。(請注意，這也是不使用可能存在競態條件或死鎖的並發模型的一個很好的理由 - 它可能會使程式碼審查或理解程式碼變得非常複雜。)

Another time when it's particularly important to think about functionality
during a code review is if there is some sort of **parallel programming** going
on in the CL that could theoretically cause deadlocks or race conditions. These
sorts of issues are very hard to detect by just running the code and usually
need somebody (both the developer and the reviewer) to think through them
carefully to be sure that problems aren't being introduced. (Note that this is
also a good reason not to use concurrency models where race conditions or
deadlocks are possible—it can make it very complex to do code reviews or
understand the code.)

## 複雜度 (Complexity)

變更清單是否比它應該的複雜？在每個層面上檢查，逐行檢查是否太複雜？函式是否太複雜？類別是否太複雜？「太複雜」通常意味著「程式碼讀者無法快速理解」。它也可以意味著「當開發人員嘗試呼叫或修改此程式碼時，很可能會引入錯誤。」

Is the CL more complex than it should be? Check this at every level of the
CL—are individual lines too complex? Are functions too complex? Are classes too
complex? "Too complex" usually means **"can't be understood quickly by code
readers."** It can also mean **"developers are likely to introduce bugs when
they try to call or modify this code."**

一種特定的複雜度是**過度設計**，開發人員使程式碼更通用，或新增系統目前不需要的功能。評審者應特別注意過度工程。鼓勵開發人員解決他們現在知道需要解決的問題，而不是開發人員推測*未來*可能需要解決的問題。未來的問題應該在它到來並且您可以在物理宇宙中看到其實際形狀和要求時解決。

A particular type of complexity is **over-engineering**, where developers have
made the code more generic than it needs to be, or added functionality that
isn't presently needed by the system. Reviewers should be especially vigilant
about over-engineering. Encourage developers to solve the problem they know
needs to be solved *now*, not the problem that the developer speculates *might*
need to be solved in the future. The future problem should be solved once it
arrives and you can see its actual shape and requirements in the physical
universe.

## 測試 (Tests)

根據需求要求進行單元、整合或端對端測試。一般而言，測試應與生產程式碼在同一變更清單中新增，除非該變更清單處理緊急情況。

Ask for unit, integration, or end-to-end
tests as appropriate for the change. In general, tests should be added in the
same CL as the production code unless the CL is handling an
[emergency](../emergencies.md).

請確保變更清單中的測試是正確、明智和有用的。測試本身不會測試，我們很少為測試編寫測試 - 人必須確保測試是有效的。

Make sure that the tests in the CL are correct, sensible, and useful. Tests do
not test themselves, and we rarely write tests for our tests—a human must ensure
that tests are valid.

當程式碼錯誤時，測試會實際失敗嗎？如果程式碼在它們下面變更，它們是否會開始產生錯誤陽性？每個測試是否提出簡單有效的斷言？測試是否在不同的測試方法之間適當地分離？

Will the tests actually fail when the code is broken? If the code changes
beneath them, will they start producing false positives? Does each test make
simple and useful assertions? Are the tests separated appropriately between
different test methods?

請記得測試也是需要維護的程式碼。 不要因為測試不是主要二進位檔的一部分，就在測試中接受複雜性。

Remember that tests are also code that has to be maintained. Don't accept
complexity in tests just because they aren't part of the main binary.

## 命名 (Naming)

開發者為每個東西取了好名字嗎？一個好的名字應該足夠長，以便完全傳達該項目的內容或功能，而不至於太長而難以閱讀。

Did the developer pick good names for everything? A good name is long enough to
fully communicate what the item is or does, without being so long that it
becomes hard to read.

## 註解 (Comments)

這位開發人員是否使用易懂的英文書寫清晰的註解？所有的註解是否都是必要的？通常當註解解釋了程式碼存在的原因時就很有用，而不是解釋程式碼在做什麼。如果程式碼本身並不清晰，那麼就應該簡化程式碼。也有一些例外情況（例如常規表達式和複雜演算法通常受益於解釋其操作的註解），但大多數註解都是提供程式碼本身所不能包含的資訊，比如決策背後的原因。

Did the developer write clear comments in understandable English? Are all of the
comments actually necessary? Usually comments are useful when they **explain
why** some code exists, and should not be explaining *what* some code is doing.
If the code isn't clear enough to explain itself, then the code should be made
simpler. There are some exceptions (regular expressions and complex algorithms
often benefit greatly from comments that explain what they're doing, for
example) but mostly comments are for information that the code itself can't
possibly contain, like the reasoning behind a decision.

檢視此變更清單之前的評論可能有所幫助。也許現在可以刪除一個 TODO，刪除建議不要進行此更改的評論，等等。

It can also be helpful to look at comments that were there before this CL. Maybe
there is a TODO that can be removed now, a comment advising against this change
being made, etc.

請注意，註解與類別、模組或函式的*文件*有所不同，後者應表達一段程式碼的目的，如何使用它以及在使用時的行為。

Note that comments are different from *documentation* of classes, modules, or
functions, which should instead express the purpose of a piece of code, how it
should be used, and how it behaves when used.

## 風格 (Style)

在 Google，我們為所有主要的語言，甚至大部分不太常用的語言都有[程式碼風格指南](http://google.github.io/styleguide/)，請確保變更清單符合適當的程式碼風格指南。

We have [style guides](http://google.github.io/styleguide/) at Google for all
of our major languages, and even for most of the minor languages. Make sure the
CL follows the appropriate style guides.

如果您想要改進一些風格，但風格指南中沒有提到，請在您的評論中加上「Nit:」作為字首，讓開發人員知道這只是您認為可以改善程式碼但不是必要的細微意見。不要僅基於個人風格偏好而阻止變更清單被提交。

If you want to improve some style point that isn't in the style guide, prefix
your comment with "Nit:" to let the developer know that it's a nitpick that you
think would improve the code but isn't mandatory. Don't block CLs from being
submitted based only on personal style preferences.

CL 的作者不應包含主要的樣式變更和其他變更。這會使得很難看出 CL 中正在進行的更改，也會使合併和回退變得更加複雜，造成其他問題。例如，如果作者想要重新格式化整個檔案，請讓他們將重格式化作為一個 CL 發送給你，然後再傳送另一個 CL 來進行功能更改。

The author of the CL should not include major style changes combined with other
changes. It makes it hard to see what is being changed in the CL, makes merges
and rollbacks more complex, and causes other problems. For example, if the
author wants to reformat the whole file, have them send you just the
reformatting as one CL, and then send another CL with their functional changes
after that.

## 一致性 (Consistency)

如果現有的程式碼與風格指南不一致怎麼辦？根據我們的 [程式碼審查原則](standard.md#principles)，風格指南是絕對的權威：如果風格指南要求某些內容，這 CL 就應該遵循這些指南。

What if the existing code is inconsistent with the style guide? Per our
[code review principles](standard.md#principles), the style guide is the
absolute authority: if something is required by the style guide, the CL should
follow the guidelines.

在某些情況下，風格指南僅是提供建議而非強制規定。在這些情況下，應根據判斷，決定新的程式碼是否應與建議或周圍的程式碼保持一致。傾向於遵循風格指南，除非當地的不一致會太令人困惑。

In some cases, the style guide makes recommendations rather than declaring
requirements. In these cases, it's a judgment call whether the new code should
be consistent with the recommendations or the surrounding code. Bias towards
following the style guide unless the local inconsistency would be too confusing.

如果沒有其他規則適用，作者應該與現有的程式碼保持一致性。

If no other rule applies, the author should maintain consistency with the
existing code.

無論如何，都要鼓勵作者提交錯誤報告並新增一個待辦事項來清理現有的程式碼。

Either way, encourage the author to file a bug and add a TODO for cleaning up
existing code.

## 文件 (Documentation)

如果一個 CL 更改了使用者建立、測試、互動或釋出程式碼的方式，請檢查是否也更新相關的文件，包括 README、g3doc 頁面和任何已產生的參考文件。 如果變更清單刪除或不推薦使用的程式碼，請考慮是否應刪除相關的文件。如果有缺少文件，請詢問相關人員。

If a CL changes how users build, test, interact with, or release code, check to
see that it also updates associated documentation, including
READMEs, g3doc pages, and any generated
reference docs. If the CL deletes or deprecates code, consider whether the
documentation should also be deleted.
If documentation is
missing, ask for it.

## 每一行 (Every Line) {#every-line}

通常情況下，應檢視您被指定審查的*每行*程式碼。像資料檔案、產生的程式碼或大型資料結構這樣的東西有時可以掃描，但不要掃描人寫的類、函式或程式碼塊，並假設其中的內容沒有問題。顯然，某些程式碼比其他程式碼更需要仔細檢查-這是您必須做出的判斷-但您至少應確保您*理解*所有程式碼的運作方式。

In the general case, look at *every* line of code that you have been assigned to
review. Some things like data files, generated code, or large data structures
you can scan over sometimes, but don't scan over a human-written class,
function, or block of code and assume that what's inside of it is okay.
Obviously some code deserves more careful scrutiny than other code&mdash;that's
a judgment call that you have to make&mdash;but you should at least be sure that
you *understand* what all the code is doing.

如果你發現程式碼太難閱讀而減緩了審查速度，你應該告訴開發人員，在嘗試審查之前等待他們澄清。在 Google，我們招聘優秀的軟體工程師，而你就是其中之一。如果你無法理解程式碼，其他開發人員也很可能無法理解。因此，當你要求開發人員澄清時，你也在幫助未來的開發人員理解這段程式碼。

If it's too hard for you to read the code and this is slowing down the review,
then you should let the developer know that
and wait for them to clarify it before you try to review it. At Google, we hire
great software engineers, and you are one of them. If you can't understand the
code, it's very likely that other developers won't either. So you're also
helping future developers understand this code, when you ask the developer to
clarify it.

如果你瞭解程式碼，但是你覺得自己不太適合審查某部分，確保讓這個 CL 有合格的審查者(參考 : #every-line-exceptions)，尤其是針對隱私、安全性、併發性、可訪問性、國際化等複雜問題。

If you understand the code but you don't feel qualified to do some part of the
review, [make sure there is a reviewer](#every-line-exceptions) on the CL who is
qualified, particularly for complex issues such as privacy, security,
concurrency, accessibility, internationalization, etc.

### 例外情況 (Exceptions) {#every-line-exceptions}

如果你需要檢查每一行，但這對你來說不合理，該怎麼辦呢？例如，在變更清單上有多個審查者，你可能會被要求：

* 檢視屬於較大變更的某些檔案。
* 檢視變更中的某些方面，例如高層次設計、隱私或安全影響等。

What if it doesn't make sense for you to review every line? For example, you are
one of multiple reviewers on a CL and may be asked:

* To review only certain files that are part of a larger change.
* To review only certain aspects of the CL, such as the high-level design,
  privacy or security implications, etc.

在這些情況下，請在評論中註明您審查的部分。建議使用“帶有評論的 LGTM”。

In these cases, note in a comment which parts you reviewed. Prefer giving
[LGTM with comments](speed.md#lgtm-with-comments).

如果您希望在確認其他審查者已經檢查完變更清單的其他部分後給予 LGTM，請在評論中明確註明以設定期望。一旦變更清單達到所需狀態，請[快速回應](speed.md#responses)。

If you instead wish to grant LGTM after confirming that other reviewers have
reviewed other parts of the CL, note this explicitly in a comment to set
expectations. Aim to [respond quickly](speed.md#responses) once the CL has
reached the desired state.

## 背景說明 (Context)

通常，在廣泛的背景下檢視變更清單會很有幫助。通常，程式碼審查工具僅會顯示正在更改部分周圍的幾行程式碼。有時您需要檢視整個檔案以確保更改實際上是有意義的。例如，您可能只會看到新增了四行新的程式碼，但當您檢視整個檔案時，您會發現這四行程式碼實際上位於一個50行的方法中，現在真正需要將其拆分為較小的方法。

It is often helpful to look at the CL in a broad context. Usually the code
review tool will only show you a few lines of code around the parts that are
being changed. Sometimes you have to look at the whole file to be sure that the
change actually makes sense. For example, you might see only four new lines
being added, but when you look at the whole file, you see those four lines are
in a 50-line method that now really needs to be broken up into smaller methods.

在考慮系統整體時，思考變更清單(CL)的用途非常有用。這個 CL 是否提高了整個系統的程式碼健康度，還是讓整個系統變得更複雜、測試程度更少等等？**不要接受會降低系統程式碼健康度的 CL**。大部分的系統是透過許多累積增加的小變更變得複雜，所以防止新變更中出現任何小的複雜性是很重要的。

It's also useful to think about the CL in the context of the system as a whole.
Is this CL improving the code health of the system or is it making the whole
system more complex, less tested, etc.? **Don't accept CLs that degrade the code
health of the system.** Most systems become complex through many small changes
that add up, so it's important to prevent even small complexities in new
changes.

## 優秀表現 (Good Things) {#good-things}

如果您在 CL 中看到什麼優秀表現，請告訴開發人員，尤其是當他們以出色的方式解決了您的意見中的一個問題。程式碼審查通常只關注錯誤，但它們應該提供鼓勵和感謝好的實踐。從教導的角度來看，告訴開發人員他們做對了什麼事情，有時甚至比告訴他們錯了什麼事情更有價值。

If you see something nice in the CL, tell the developer, especially when they
addressed one of your comments in a great way. Code reviews often just focus on
mistakes, but they should offer encouragement and appreciation for good
practices, as well. It’s sometimes even more valuable, in terms of mentoring, to
tell a developer what they did right than to tell them what they did wrong.

## 概要 (Summary)

在進行程式碼審查時，您應該確保：

* 程式碼設計良好。
* 功能對程式碼使用者很好。
* 任何 UI 更改都是明智的並且看起來很好。
* 任何平行程式設計都是安全的。
* 程式碼沒有比它需要的更複雜。
* 開發者沒有實現未來可能需要但現在不知道需要的東西。
* 程式碼有適當的單元測試。
* 測試設計良好。
* 開發者對一切使用清晰的名稱。
* 註解清晰有用，大多數解釋「為什麼」而不是「什麼」。
* 程式碼適當地記錄（通常在 g3doc 中）。
* 程式碼符合我們的樣式指南。

In doing a code review, you should make sure that:

* The code is well-designed.
* The functionality is good for the users of the code.
* Any UI changes are sensible and look good.
* Any parallel programming is done safely.
* The code isn't more complex than it needs to be.
* The developer isn't implementing things they *might* need in the future but
  don't know they need now.
* Code has appropriate unit tests.
* Tests are well-designed.
* The developer used clear names for everything.
* Comments are clear and useful, and mostly explain *why* instead of *what*.
* Code is appropriately documented (generally in g3doc).
* The code conforms to our style guides.

記得審查**每一行**程式碼，關注其**上下文**，確保**提高程式碼健康度**，並讚揚開發者的**優秀表現**。

Make sure to review **every line** of code you've been asked to review, look at
the **context**, make sure you're **improving code health**, and compliment
developers on **good things** that they do.

下一步：[審查時導覽 CL (Navigating a CL in Review)](navigate.md)
