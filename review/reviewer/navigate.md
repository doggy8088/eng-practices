# 審查時導覽 CL (Navigating a CL in review)

## 摘要 (Summary)

現在您已經知道 [要尋找什麼](looking-for.md)，最有效管理跨多個檔案的評論的方法是什麼？

1.這個更改有道理嗎？它有良好的[描述](../developer/cl-descriptions.md)嗎？
2.首先看最重要的更改部分，整體設計是否良好？
3.按適當的順序檢視更換部分的其餘部分。

Now that you know [what to look for](looking-for.md), what's the most efficient
way to manage a review that's spread across multiple files?

1.Does the change make sense? Does it have a good
  [description](../developer/cl-descriptions.md)?
2.Look at the most important part of the change first. Is it well-designed
  overall?
3.Look at the rest of the CL in an appropriate sequence.

## 步驟一：對變更進行全面檢視 (Step One: Take a broad view of the change) {#step_one}

請檢視[CL描述](../developer/cl-descriptions.md)，以及CL的整體功能。這個更改是否合理？如果這個更改本來就不應該發生，請立即回覆並解釋為什麼不應該進行更改。當您拒絕這樣的更改時，也建議向開發人員建議他們應該做什麼。

Look at the [CL description](../developer/cl-descriptions.md) and what the CL
does in general. Does this change even make sense? If this change shouldn't have
happened in the first place, please respond immediately with an explanation of
why the change should not be happening. When you reject a change like this, it's
also a good idea to suggest to the developer what they should have done instead.

例如，您可以說「看起來你在這方面做了很好的工作，謝謝！但是，我們實際上正在朝著刪除您在這裡正在修改的 FooWidget 系統的方向前進，因此我們現在不想對其進行任何新的修改。要不試試重構我們的新 BarWidget 類別？」

For example, you might say "Looks like you put some good work into this, thanks!
However, we're actually going in the direction of removing the FooWidget system
that you're modifying here, and so we don't want to make any new modifications
to it right now. How about instead you refactor our new BarWidget class?"

請注意，審查者不僅拒絕了目前的 CL，並提供了一個替代建議，而且他們用了 *有禮貌的* 方式。這種禮貌是重要的，因為我們希望展現即使意見不同，我們也尊重彼此身為開發人員的事實。

Note that not only did the reviewer reject the current CL and provide an
alternative suggestion, but they did it *courteously*. This kind of courtesy is
important because we want to show that we respect each other as developers even
when we disagree.

如果你得到超過幾個代表你不想做的更改的 CLs，你應該考慮重新檢討你的團隊開發流程或外部貢獻者的發布流程，以增加在撰寫 CLs 之前的溝通。在人們做了大量工作並需要丟棄或大幅重寫之前告訴他們“不行”是更好的做法。

If you get more than a few CLs that represent changes you don't want to make,
you should consider re-working your team's development process or the posted
process for external contributors so that there is more communication before CLs
are written. It's better to tell people "no" before they've done a ton of work
that now has to be thrown away or drastically re-written.

## 第二步：檢查 CL 的主要部分 (Step Two: Examine the main parts of the CL) {#step_two}

尋找此 CL 中的「主要」部分。通常，會有一個檔案有最多的邏輯變更，並且是此 CL 的主要部分。先看這些主要部分，可以幫助你釐清所有較小部分的內容，並且加速程式碼審查的進行。如果這個 CL 太大，而你無法判斷哪些部分是主要部分，可以問開發人員要先看哪些部分，或是請他們將這個 CL 拆成多個較小的 CL。

Find the file or files that are the "main" part of this CL. Often, there is one
file that has the largest number of logical changes, and it's the major piece of
the CL. Look at these major parts first. This helps give context to all of the
smaller parts of the CL, and generally accelerates doing the code review. If the
CL is too large for you to figure out which parts are the major parts, ask the
developer what you should look at first, or ask them to
[split up the CL into multiple CLs](../developer/small-cls.md).

如果您發現該部分存在重大的設計問題，即使現在沒有時間重新審查整個 CL ，也應立即傳送評論。事實上，重新審查整個 CL 可能是浪費時間的，因為如果設計問題足夠嚴重，那麼正在審查的其他程式碼將會消失，對主要問題已經沒有任何影響。

If you see some major design problems with this part of the CL, you should send
those comments immediately, even if you don't have time to review the rest of
the CL right now. In fact, reviewing the rest of the CL might be a waste of
time, because if the design problems are significant enough, a lot of the other
code under review is going to disappear and not matter anyway.

有兩個主要的原因使立即傳送這些重要的設計意見非常重要：

- 開發者們往往會先發送程式碼變更，然後在等待審查時立即開始基於該程式碼變更進行新工作。如果您正在審查的程式碼變更存在重大設計問題，則他們在稍後的程式碼變更中也將需要重新進行工作。在有問題的設計上進行太多額外工作之前，您應該立即發現它們。
- 重大設計更改所需的時間比小更改長。大多數開發人員都有期限；為了在程式碼庫中擁有優質程式碼並仍然符合期限，開發人員需要盡快開始對程式碼變更進行任何重大重構。

There are two major reasons it's so important to send these major design
comments out immediately:

- Developers often mail a CL and then immediately start new work based on that
  CL while they wait for review. If there are major design problems in the CL
  you're reviewing, they're also going to have to re-work their later CL. You
  want to catch them before they've done too much extra work on top of the
  problematic design.
- Major design changes take longer to do than small changes. Developers nearly
  all have deadlines; in order to make those deadlines and still have quality
  code in the codebase, the developer needs to start on any major re-work of
  the CL as soon as possible.

## 步驟三：以適當的順序瀏覽其餘的 CL (Step Three: Look through the rest of the CL in an appropriate sequence) {#step_three}

一旦確定 CL 整體上沒有主要的設計問題，請嘗試找出一個邏輯序列來檢視檔案，同時確保您沒有漏掉任何檔案。通常，在您查閱了主要的檔案後，簡單地按照程式碼檢閱工具呈現檔案的順序來逐一檢查每個檔案。有時候，在閱讀主要程式碼之前，先閱讀測試程式碼也很有幫助，因為這樣您就可以瞭解這個變更應該如何運作。

Once you've confirmed there are no major design problems with the CL as a whole,
try to figure out a logical sequence to look through the files while also making
sure you don't miss reviewing any file. Usually after you've looked through the
major files, it's simplest to just go through each file in the order that
the code review tool presents them to you. Sometimes it's also helpful to read the tests
first before you read the main code, because then you have an idea of what the
change is supposed to be doing.

接下來: [程式碼審查的速度 (Speed of Code Reviews)](speed.md)
