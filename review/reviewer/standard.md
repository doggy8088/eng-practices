# 程式碼審查的標準 (The Standard of Code Review)

程式碼審查的主要目的是確保 Google 程式碼庫的整體程式碼品質隨時間推移而得到改善。所有程式碼審查的工具和流程都是為此目的而設計的。

The primary purpose of code review is to make sure that the overall
code health of Google's code
base is improving over time. All of the tools and processes of code review are
designed to this end.

為了達成這個目標，必須平衡一系列的權衡取捨。

In order to accomplish this, a series of trade-offs have to be balanced.

首先，開發人員必須能夠在他們的任務上「取得進展」。如果您從未提交程式碼庫的改進，則程式碼庫永遠不會得到改進。此外，如果審閱者讓「任何」更改都變得非常困難，那麼開發人員將不會有動力在未來進行改進。

First, developers must be able to _make progress_ on their tasks. If you never
submit an improvement to the codebase, then the codebase never improves. Also,
if a reviewer makes it very difficult for _any_ change to go in, then developers
are disincentivized to make improvements in the future.

另一方面，審查者的責任是確保每個 CL 都有如此高的品質，以便其程式碼庫的整體程式碼健康狀況不會隨著時間而降低。這可能很棘手，因為通常情況下，程式碼庫隨著時間的推移會因程式碼健康程度的微小下降而退化，特別是當團隊面臨重要時間限制，他們覺得必須採取捷徑以實現目標時，情況更為如此。

On the other hand, it is the duty of the reviewer to make sure that each CL is
of such a quality that the overall code health of their codebase is not
decreasing as time goes on. This can be tricky, because often, codebases degrade
through small decreases in code health over time, especially when a team is
under significant time constraints and they feel that they have to take
shortcuts in order to accomplish their goals.

此外，審查者擁有並負責審查的程式碼。他們希望確保程式碼庫保持一致、可維護，以及其他在「[程式碼審查要注意的地方](looking-for.md)」中提到的事項。

Also, a reviewer has ownership and responsibility over the code they are
reviewing. They want to ensure that the codebase stays consistent, maintainable,
and all of the other things mentioned in
["What to look for in a code review."](looking-for.md)

因此，在程式碼審查中，我們將以下規則作為預期的標準：

Thus, we get the following rule as the standard we expect in code reviews:

一般來說，審查者應在程式碼已經明顯改善系統整體程式碼健康狀態的情況下，傾向於核准 CL，即使 CL 還不是完美的。

**In general, reviewers should favor approving a CL once it is in a state where
it definitely improves the overall
code health of the system
being worked on, even if the CL isn't perfect.**

這是所有程式碼審查指南中最重要的原則。

That is _the_ senior principle among all of the code review guidelines.

當然，這也有限制。例如，如果一個 CL 增加了一個特性，而審查者不想要這個特性，即使程式碼設計很好，審查者仍可以否決批准。

There are limitations to this, of course. For example, if a CL adds a feature
that the reviewer doesn't want in their system, then the reviewer can certainly
deny approval even if the code is well-designed.

一個重要的觀念是，「完美的」程式碼是不存在的，只有「更好的」程式碼。審查者不應要求作者在批准之前將 CL 的每一個細節都加以完善。相反，審查者應在進行變更建議時，平衡推動前進的需求和變更的重要性。審查者應尋求「持續改進」而非追求完美。如果一個 CL 整體上改善了系統的可維護性、可讀性和易懂性，那麼它不應因為不是「完美的」而延遲數天或數週。

A key point here is that there is no such thing as "perfect" code&mdash;there is
only _better_ code. Reviewers should not require the author to polish every tiny
piece of a CL before granting approval. Rather, the reviewer should balance out
the need to make forward progress compared to the importance of the changes they
are suggesting. Instead of seeking perfection, what a reviewer should seek is
_continuous improvement_. A CL that, as a whole, improves the maintainability,
readability, and understandability of the system shouldn't be delayed for days
or weeks because it isn't "perfect."

審查者應該始終可以隨意留下評論，表達某些方面可以更好，但如果這不是非常重要的話，可以在前面加上 "Nit:" 之類的字眼，讓作者知道這只是值得注意的細節，可以選擇忽略。

Reviewers should _always_ feel free to leave comments expressing that something
could be better, but if it's not very important, prefix it with something like
"Nit: " to let the author know that it's just a point of polish that they could
choose to ignore.

註：此文檔中沒有任何內容可以證明提交明顯惡化系統整體程式碼健康狀況（CLs）的行為是正當的。唯一可以這樣做的情況是在[緊急情況](../emergencies.md)下。

Note: Nothing in this document justifies checking in CLs that definitely
_worsen_ the overall code health of the system. The only time you would do that
would be in an [emergency](../emergencies.md).

## 導師指導 (Mentoring)

程式碼審查可以扮演一個教導開發者學習語言、框架或一般軟體設計原則的重要角色。留下有幫助開發者學習新知的評論始終是可以的。分享知識是改善系統程式碼健康狀態的重要部分。但請記住，如果您的評論僅僅是教育性的，但不是必須符合本文件所描述的標準，請在前面加上“Nit:”或以其他方式表明它對於作者解決這個以修復問題不是必要的。

Code review can have an important function of teaching developers something new
about a language, a framework, or general software design principles. It's
always fine to leave comments that help a developer learn something new. Sharing
knowledge is part of improving the code health of a system over time. Just keep
in mind that if your comment is purely educational, but not critical to meeting
the standards described in this document, prefix it with "Nit: " or otherwise
indicate that it's not mandatory for the author to resolve it in this CL.

## 原則 (Principles) {#principles}

* 技術事實和資料優先於意見和個人偏好。

* 在風格問題上，[風格指南](http://google.github.io/styleguide/)是絕對權威。任何純粹風格的點（空白等），如果不在風格指南中，就是個人喜好的問題。風格應與原先的風格保持一致。如果沒有先前的風格，則接受作者所寫的風格。

* **軟體設計的方面幾乎從不是純風格問題或個人偏好。**它們基於基本原則，應該依據這些原則進行衡量，而不是根據個人意見進行衡量。有時會有一些有效的選項。如果作者可以透過資料或根據可靠的工程原則證明幾種方法同樣有效，那麼審查者應該接受作者的偏好。否則，選擇是由軟體設計的標準原則所獨裁決定。

* 如果沒有其他規則適用，那麼審查者可能會要求作者與當前程式碼庫中的內容保持一致，前提是這不會惡化系統的整體程式碼健康狀況。

---

* Technical facts and data overrule opinions and personal preferences.

* On matters of style, the [style guide](http://google.github.io/styleguide/)
  is the absolute authority. Any purely style point (whitespace, etc.) that is
  not in the style guide is a matter of personal preference. The style should
  be consistent with what is there. If there is no previous style, accept the
  author's.

* **Aspects of software design are almost never a pure style issue or just a
  personal preference.** They are based on underlying principles and should be
  weighed on those principles, not simply by personal opinion. Sometimes there
  are a few valid options. If the author can demonstrate (either through data
  or based on solid engineering principles) that several approaches are
  equally valid, then the reviewer should accept the preference of the author.
  Otherwise the choice is dictated by standard principles of software design.

* If no other rule applies, then the reviewer may ask the author to be
  consistent with what is in the current codebase, as long as that doesn't
  worsen the overall code health of the system.

## 解決衝突 (Resolving Conflicts) {#conflicts}

在進行程式碼審查的任何衝突中，第一步應該是開發者和審查者基於這份文件和其他文件，例如[CL作者指南](../developer/index.md)和[審查者指南](index.md)，嘗試達成共識。

In any conflict on a code review, the first step should always be for the
developer and reviewer to try to come to consensus, based on the contents of
this document and the other documents in
[The CL Author's Guide](../developer/index.md) and this
[Reviewer Guide](index.md).

當達成共識變得特別困難時，與其僅透過程式碼審查意見試圖解決衝突，與審查者和作者進行面對面會議或視訊會議可能有所幫助。（如果您這麼做了，請務必記錄討論結果，作為未來讀者的意見。）

When coming to consensus becomes especially difficult, it can help to have a
face-to-face meeting or a video conference between the reviewer and the author, instead of
just trying to resolve the conflict through code review comments. (If you do
this, though, make sure to record the results of the discussion as a comment on
the CL, for future readers.)

如果那無法解決情況，最常見的解決辦法是進行升級。通常的升級路徑是進行更廣泛的團隊討論，讓技術領導發表意見，從程式碼維護者那裡獲取決策，或請求工程經理的幫助。**不要讓程式碼審查因為作者和審查者無法達成一致而拖延。**

If that doesn't resolve the situation, the most common way to resolve it would
be to escalate. Often the
escalation path is to a broader team discussion, having a Technical Lead weigh in, asking
for a decision from a maintainer of the code, or asking an Eng Manager to help
out. **Don't let a CL sit around because the author and the reviewer can't come
to an agreement.**

接下來: [在程式碼審查中要注意的事項 (What to look for in a code review)](looking-for.md)
