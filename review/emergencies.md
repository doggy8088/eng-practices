# 緊急情況 (Emergencies)

有時候有些緊急的 CL 需要盡可能快地通過整個程式碼審查流程。

Sometimes there are emergency CLs that must pass through the entire code review
process as quickly as
possible.

## 什麼是緊急情況？ (What Is An Emergency?) {#what}

緊急程式庫 (CL) 將是一個「小」更改，允許主要的發佈繼續進行而不會復原，修復影響使用者產生重大影響的錯誤，在生產環境中處理迫切的法律問題，關閉主要的安全漏洞等。

An emergency CL would be a **small** change that: allows a major launch to
continue instead of rolling back, fixes a bug significantly affecting users in
production, handles a pressing legal issue, closes a major security hole, etc.

在緊急情況下，我們真的關心整個程式碼審查過程的速度，而不僅僅是[回覆速度](reviewer/speed.md)。在這種情況下，專家應更關心審查的速度和程式碼的正確性（它是否真正解決了緊急情況？），而不是其他任何事情。此外（很明顯地），當這些問題出現時，此類檢討應優先於所有其他程式碼檢討。

In emergencies we really do care about the speed of the entire code review
process, not just the [speed of response](reviewer/speed.md). In this case
*only*, the reviewer should care more about the speed of the review and the
correctness of the code (does it actually resolve the emergency?) than anything
else. Also (perhaps obviously) such reviews should take priority over all other
code reviews, when they come up.

然而，在緊急情況得以解決後，您應該重新審視緊急變更清單，並進行更全面的審查。

However, after the emergency is resolved you should look over the emergency CLs
again and give them a [more thorough review](reviewer/looking-for.md).

## 什麼不屬於緊急情況？ (What Is NOT An Emergency?) {#not}

為了明確起見，以下情況*不是*緊急情況：

- 希望在本週進行發佈，而非下週（除非有像是合作夥伴協議等實際的[死線](#deadlines) 所需）。
- 開發人員已花費很長時間在一個功能上，而且他們真的很想要讓 CL 成功送出。
- 審查者都在其他時區，目前是晚上或是他們正在外地。
- 週五這天快結束的時候，在開發人員準備開始週末生活之前，如果能夠讓 CL 成功送出，那就太好了。
- 經理表示，由於 [軟性（非硬性）期限](#deadlines)，這個審查必須在今天完成並檢查 CL 是否已經提交。
- 復原 CL 導致測試失敗或建置失敗。

To be clear, the following cases are *not* an emergency:

- Wanting to launch this week rather than next week (unless there is some
  actual [hard deadline](#deadlines) for launch such as a partner agreement).
- The developer has worked on a feature for a very long time and they really
  want to get the CL in.
- The reviewers are all in another timezone where it is currently nighttime or
  they are away on an off-site.
- It is the end of the day on a Friday and it would just be great to get this
  CL in before the developer leaves for the weekend.
- A manager says that this review has to be complete and the CL checked in
  today because of a [soft (not hard) deadline](#deadlines).
- Rolling back a CL that is causing test failures or build breakages.

等等就是這樣。

And so on.

## 什麼是硬期限？ (What Is a Hard Deadline?) {#deadlines}

一個硬期限是指如果你錯過了它，**會發生災難性的事情**。例如：

- 按照合約條款，在特定日期前提交您的程式碼是必要的。
- 如果產品在特定日期之前未發佈，它將會在市場上完全失敗。
- 有些硬體製造商每年只運送新硬體。如果您未能按時提交程式碼，根據您試圖運送的程式碼類型，這可能是災難性的。

A hard deadline is one where **something disastrous would happen** if you miss it. For example:

- Submitting your CL by a certain date is necessary for a contractual
  obligation.
- Your product will completely fail in the marketplace if not released by a
  certain date.
- Some hardware manufacturers only ship new hardware once a year. If you miss
  the deadline to submit code to them, that could be disastrous, depending on
  what type of code you're trying to ship.

推遲一週的發行並不會導致災難。錯過重要的會議可能會是災難，但通常不會。

Delaying a release for a week is not disastrous. Missing an important conference
might be disastrous, but often is not.

大多數的期限都是較為寬鬆的期限，而非嚴格的期限。它們代表了希望在某個特定時間內完成某項功能的願望。期限的確很重要，但您不應該為了達成它們而犧牲程式碼品質。

Most deadlines are soft deadlines, not hard deadlines. They represent a desire
for a feature to be done by a certain time. They are important, but you
shouldn't be sacrificing code health to make them.

如果您的發佈週期很長（數週），為了在下一個週期之前將功能新增到程式碼中，可能會有一些妥協程式碼審查品質的誘惑。然而，如果重複此模式，專案積累的技術債務會變得很難處理。如果開發人員經常在週期接近結束時提交必須加入的 CL，卻只進行了表面上的審查，那麼團隊應修改其流程，使大型功能更改在週期初期完成，並有足夠的時間進行良好的審查。

If you have a long release cycle (several weeks) it can be tempting to sacrifice
code review quality to get a feature in before the next cycle. However, this
pattern, if repeated, is a common way for projects to build up overwhelming
technical debt. If developers are routinely submitting CLs near the end of the
cycle that "must get in" with only superficial review, then the team should
modify its process so that large feature changes happen early in the cycle and
have enough time for good review.
