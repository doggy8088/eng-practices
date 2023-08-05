# 程式碼審查的速度 (Speed of Code Reviews)

## 為什麼程式碼審查應該要快速？ (Why Should Code Reviews Be Fast?) {#why}

在 Google，我們優化的是開發團隊共同製作產品的速度，而不是優化個別開發者編寫程式碼的速度。個體開發的速度是重要的，但不像整個團隊的速度那麼重要。

**At Google, we optimize for the speed at which a team of developers can produce
a product together**, as opposed to optimizing for the speed at which an
individual developer can write code. The speed of individual development is
important, it's just not *as* important as the velocity of the entire team.

當程式碼審查速度變慢時，會有幾件事情發生：

* **團隊的開發速度下降。** 是的，對於沒有快速回應的開發人員可以完成其他工作。然而，對於其餘團隊的新功能和錯誤修正被推遲了數天、數週或數月，因為每個程式碼提交等待審查和重新審查。
* **開發人員開始抗議程式碼審查流程。** 如果審查者只每隔幾天回應一次，但每次都要求主要更改，那麼對於開發人員來說，這可能很令人沮喪和困難。通常，這會表現為對審查者“嚴格程度”的抱怨。如果審查者要求*相同的實質性更改*（這些更改確實有助於改善程式碼健康狀況），但每次開發人員更新時都能*快速*回應，抱怨往往會消失。**關於程式碼審查流程的大多數抱怨實際上可以透過加快流程來解決。**
* **程式碼健康狀況可能會受到影響。** 當審查速度較慢時，增加了允許開發人員提交不太好的程式碼的壓力。慢審查也會抑制程式碼清理、重構和對現有程式碼提交的進一步改進。

When code reviews are slow, several things happen:

* **The velocity of the team as a whole is decreased.** Yes, the individual
  who doesn't respond quickly to the review gets other work done. However, new
  features and bug fixes for the rest of the team are delayed by days, weeks,
  or months as each CL waits for review and re-review.
* **Developers start to protest the code review process.** If a reviewer only
  responds every few days, but requests major changes to the CL each time,
  that can be frustrating and difficult for developers. Often, this is
  expressed as complaints about how "strict" the reviewer is being. If the
  reviewer requests the *same* substantial changes (changes which really do
  improve code health), but responds *quickly* every time the developer makes
  an update, the complaints tend to disappear. **Most complaints about the
  code review process are actually resolved by making the process faster.**
* **Code health can be impacted.** When reviews are slow, there is increased
  pressure to allow developers to submit CLs that are not as good as they
  could be. Slow reviews also discourage code cleanups, refactorings, and
  further improvements to existing CLs.

## 程式碼審查應該有多快？ (How Fast Should Code Reviews Be?) {#fast}

如果你當下沒有在進行專注的工作，**當程式碼回饋回來後，你應該儘快進行程式碼檢閱。**

If you are not in the middle of a focused task, **you should do a code review
shortly after it comes in.**

**一個工作日是回應程式審查請求的最長時限**（即第二天早上的第一件事）。

**One business day is the maximum time it should take to respond** to a code
review request (i.e., first thing the next morning).

遵循這些指導原則意味著一個典型的程式碼更新如果需要的話，可以在一天內得到多輪審查。

Following these guidelines means that a typical CL should get multiple rounds of
review (if needed) within a single day.

## 速度 vs. 中斷 (Speed vs. Interruption) {#中斷}

有一個情況，個人速度比團隊速度更重要。**如果你正在進行一個專注的任務，例如編寫程式碼，不要中斷自己來進行程式碼審查。**研究表明，開發人員在被打斷後重新進入順暢的開發流程可能需要很長時間。因此，打斷自己撰寫程式碼實際上比讓另一個開發人員等待一段時間進行程式碼審查*更*貴重。

There is one time where the consideration of personal velocity trumps team
velocity. **If you are in the middle of a focused task, such as writing code,
don't interrupt yourself to do a code review.**
Research has shown that it can
take a long time for a developer to get back into a smooth flow of development
after being interrupted. So interrupting yourself while coding is actually
*more* expensive to the team than making another developer wait a bit for a code
review.

相反的，等待你工作的斷點再回應請求進行審查。斷點可能是你目前的撰寫程式碼任務完成後、午餐後、從會議回來後或是從休息室回來後等等。

Instead, wait for a break point in your work before you respond to a request for
review. This could be when your current coding task is completed, after lunch,
returning from a meeting, coming back from the breakroom, etc.

## 快速回應 (Fast Responses) {#responses}

當我們談論程式碼審查速度時，我們關心的是“反應”時間，而不是 CL 需要多長時間才能完成整個審查並提交。整個過程也應該要快，但是“個別回覆”快速到來比整個過程快速更加重要。

When we talk about the speed of code reviews, it is the *response* time that we
are concerned with, as opposed to how long it takes a CL to get through the
whole review and be submitted. The whole process should also be fast, ideally,
but **it's even more important for the *individual responses* to come quickly
than it is for the whole process to happen rapidly.**

即使有時需要很長時間才能完成整個審查*過程*，但審查者在整個過程中快速回應，可以顯著緩解開發人員對“緩慢”的程式碼審查感到的挫敗感。

Even if it sometimes takes a long time to get through the entire review
*process*, having quick responses from the reviewer throughout the process
significantly eases the frustration developers can feel with "slow" code
reviews.

如果您忙於在 CL 到來時進行全面審查，您仍可以快速回覆，讓開發人員瞭解您何時會審查該 CL，建議其他可能能夠更快回覆的審查者，或[提供一些初始的整體評論](navigate.md)。(注意：這些都並不意味著您應該中斷編寫程式來傳送此類回覆 - 請在您的工作中合理的中斷點發送回覆。)

If you are too busy to do a full review on a CL when it comes in, you can still
send a quick response that lets the developer know when you will get to it,
suggest other reviewers who might be able to respond more quickly, or
[provide some initial broad comments](navigate.md). (Note: none of this means
you should interrupt coding even to send a response like this&mdash;send the
response at a reasonable break point in your work.)

重要的是，審查者花足夠的時間進行審查，以確保他們的 "LGTM" 意味著 "這個程式碼符合[我們的標準](standard.md)"。然而，個別回應仍然理想的應是[快速的](#fast)。

**It is important that reviewers spend enough time on review that they are
certain their "LGTM" means "this code meets [our standards](standard.md)."**
However, individual responses should still ideally be [fast](#fast).

## 跨時區評論 (Cross-Time-Zone Reviews) {#tz}

當處理時區差異時，請在作者的工作時間結束前回覆，以便他們有時間回應。如果他們已經完成當天的工作，請盡量確保你的回顧在他們第二天開始工作之前完成。

When dealing with time zone differences, try to get back to the author while
they have time to respond before the end of their working hours. If they have
already finished work for the day, then try to make sure your review is done
before they start work the next day.

## LGTM 評論 (LGTM With Comments) {#lgtm-with-comments}

為了加速程式碼審查，當審查者於程式碼審查時同時留下未解決的評論時，有些情況下他們應該給予 LGTM / Approval 以加快流程。這是在以下任一情況下完成的：

* 審查者相信開發人員將會適當地處理所有未解決的評論。
* 剩餘的更改是較小的，並不需要開發人員一定做。

In order to speed up code reviews, there are certain situations in which a
reviewer should give LGTM/Approval even though they are also leaving unresolved
comments on the CL. This is done when either:

* The reviewer is confident that the developer will appropriately address all
  the reviewer's remaining comments.
* The remaining changes are minor and don't *have* to be done by the
  developer.

如果沒有明確的說明，則審查者應該指定他們打算使用哪些選項。

The reviewer should specify which of these options they intend, if it is not
otherwise clear.

當開發者得到 "LGTM, Approval" 需要等待整整一天時，LGTM 帶有評論的功能尤其值得考慮，特別是當開發者和審查者位於不同的時區時。

LGTM With Comments is especially worth considering when the developer and
reviewer are in different time zones and otherwise the developer would be
waiting for a whole day just to get "LGTM, Approval."

## 大型 CL (Large CLs) {#large}

如果某人寄送給你一個巨大的程式碼審查，讓你不確定何時有時間審查，你應該詢問開發人員將 CL（程式碼變更）拆分成數個建立在彼此之上的小 CL，而非一個必須同時審查的巨大 CL。即使需要額外的工作量，這通常對審查者有很大的幫助。

If somebody sends you a code review that is so large you're not sure when you
will be able to have time to review it, your typical response should be to ask
the developer to
[split the CL into several smaller CLs](../developer/small-cls.md) that build on
each other, instead of one huge CL that has to be reviewed all at once. This is
usually possible and very helpful to reviewers, even if it takes additional work
from the developer.

如果一個 CL 不能被分成更小的 CL，而且你沒有時間快速檢閱整個 CL，那麼至少對 CL 的整體設計寫一些註解，並將其送回開發人員進行改進。作為審查者，你的目標之一應該是始終讓開發人員解除障礙或使他們能夠快速進行某些進一步的操作，而不犧牲程式碼的健康狀態。

If a CL *can't* be broken up into smaller CLs, and you don't have time to review
the entire thing quickly, then at least write some comments on the overall
design of the CL and send it back to the developer for improvement. One of your
goals as a reviewer should be to always unblock the developer or enable them to
take some sort of further action quickly, without sacrificing code health to do
so.

## 逐漸改善的程式碼審查 (Code Review Improvements Over Time) {#time}

如果你遵循這些準則，並且在程式碼審查方面嚴格要求自己，你會發現整個程式碼審查過程隨著時間的推移越來越快。開發人員會學習有關程式碼健康所需的標準，並向您傳送從一開始就很出色的 CL，需要越來越少的審查時間。審查人員學會了快速響應，並使審查過程不增加不必要的延遲。但是，請不要為了加快速度而妥協於[程式碼審查標準](standard.md)或質量的虛幻改善。長遠來看，這實際上並不會使任何事情發生得更快。

If you follow these guidelines and you are strict with your code reviews, you
should find that the entire code review process tends to go faster and faster
over time. Developers learn what is required for healthy code, and send you CLs
that are great from the start, requiring less and less review time. Reviewers
learn to respond quickly and not add unnecessary latency into the review
process.
But **don't compromise on
the [code review standards](standard.md) or quality for an imagined improvement
in velocity**&mdash;it's not actually going to make anything happen more
quickly, in the long run.

## 緊急情況 (Emergencies)

有些「[緊急情況](../emergencies.md)」需要CL非常迅速地通過整個審查過程，而且品質指導方針也會變得寬鬆。但請參閱「../emergencies.md#what」以瞭解哪些情況實際上符合緊急情況，哪些不符合。

There are also [emergencies](../emergencies.md) where CLs must pass through the
*whole* review process very quickly, and where the quality guidelines would be
relaxed. However, please see [What Is An Emergency?](../emergencies.md#what) for
a description of which situations actually qualify as emergencies and which
don't.

接下來: [如何編寫程式碼審查評論 (How to Write Code Review Comments)](comments.md)
