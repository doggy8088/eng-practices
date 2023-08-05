# 如何編寫程式碼審查評論 (How to write code review comments)

## 摘要 (Summary)

- 要友善。
- 解釋你的推論。
- 在明示指令與僅指出問題與讓開發者自行決定之間取得平衡。
- 鼓勵開發者簡化程式碼或新增程式碼註解，而非僅解釋複雜程度給你聽。

---

- Be kind.
- Explain your reasoning.
- Balance giving explicit directions with just pointing out problems and letting the developer decide.
- Encourage developers to simplify code or add code comments instead of just explaining the complexity to you.

## 禮貌 (Courtesy)

一般而言，在檢閱開發者的程式碼時，保持禮貌尊重並清楚明確地提供幫助是非常重要的。其中一個方法是確保您一直對「程式碼」進行評論，不要對「開發者」進行評論。您不必總是遵循此實踐，但在說出可能令人不悅或有爭議的內容時，您應該絕對使用它。例如:

In general, it is important to be
[courteous and respectful](https://chromium.googlesource.com/chromium/src/+/master/docs/cr_respect.md)
while also being very clear and helpful to the developer whose code you are
reviewing. One way to do this is to be sure that you are always making comments
about the *code* and never making comments about the *developer*. You don't
always have to follow this practice, but you should definitely use it when
saying something that might otherwise be upsetting or contentious. For example:

不好：「為什麼**你**在這裡使用執行緒，當明顯沒有從並發中獲得任何好處？」

Bad: "Why did **you** use threads here when there's obviously no benefit to be
gained from concurrency?"

好的："這裡的併發模型正在增加系統的複雜度，但我沒有看到任何實際的效能收益。由於沒有效能收益，最好讓此程式碼成為單線程，而不是使用多執行緒。"

Good: "The concurrency model here is adding complexity to the system without any
actual performance benefit that I can see. Because there's no performance
benefit, it's best for this code to be single-threaded instead of using multiple
threads."

## 解釋原因 (Explain Why) {#why}

從上面的「好」範例中，你會注意到一件事——它有助於開發人員瞭解為什麼你要這樣評論。你並不總是需要在評論中包含這些資訊，但有時候在你的意圖、你所遵循的最佳實踐，或你的建議如何改善程式碼健康方面，提供更多解釋是合適的。

One thing you'll notice about the "good" example from above is that it helps the
developer understand *why* you are making your comment. You don't always need to
include this information in your review comments, but sometimes it's appropriate
to give a bit more explanation around your intent, the best practice you're
following, or how your suggestion improves code health.

## 提供指導 (Giving Guidance) {#guidance}

通常開發者有責任修復 CL，而不是審查者的責任。您不需要對解決方案進行詳細的設計或為開發者編寫程式碼。

**In general it is the developer's responsibility to fix a CL, not the
reviewer's.** You are not required to do detailed design of a solution or write
code for the developer.

然而，這並不意味著審查者應該沒有幫助性。一般來說，您應該在指出問題和提供直接指導之間取得適當的平衡。指出問題並讓開發人員做出決策通常有助於開發人員學習，並且更容易進行程式碼審查。它也可能會帶來更好的解決方案，因為開發人員比審查者更接近程式碼。

This doesn't mean the reviewer should be unhelpful, though. In general you
should strike an appropriate balance between pointing out problems and providing
direct guidance. Pointing out problems and letting the developer make a decision
often helps the developer learn, and makes it easier to do code reviews. It also
can result in a better solution, because the developer is closer to the code
than the reviewer is.

然而，有時直接的指示、建議甚至是程式碼會更有幫助。程式碼審查的主要目標是獲取最佳的 CL。次要目標是提高開發人員的技能，以便隨著時間的推移，他們需要的審查越來越少。

However, sometimes direct instructions, suggestions, or even code are more
helpful. The primary goal of code review is to get the best CL possible. A
secondary goal is improving the skills of developers so that they require less
and less review over time.

請記住，人們學習的方式不僅是從改進之處，也有從他們做得好的地方進行強化。如果您在程式碼上看到您喜歡的地方，也請提供評論！例如：開發人員整理了混亂的演算法，新增了出色的測試覆蓋率，或者是您作為審查者從程式碼中學到了東西。與所有評論一樣，請說明您為什麼喜歡某些部分，進一步鼓勵開發人員繼續使用良好的做法。

Remember that people learn from reinforcement of what they are doing well and
not just what they could do better. If you see things you like in the CL,
comment on those too! Examples: developer cleaned up a messy algorithm, added
exemplary test coverage, or you as the reviewer learned something from the CL.
Just as with all comments, include [why](#why) you liked something, further
encouraging the developer to continue good practices.

## 標記評論的嚴重性 (Label comment severity) {#label-comment-severity}

請考慮對您的評論進行嚴重程度標記，區分必要的更改和指導方針或建議。

Consider labeling the severity of your comments, differentiating required
changes from guidelines or suggestions.

以下是一些範例：

> 次要注意: 這只是小事情。從技術上講，你應該這麼做，但它不會對事情產生巨大的影響。
>
> 選擇性 (或考慮): 我認為這可能是一個好主意，但不是嚴格要求的。
>
> FYI: 我不期望您在此 CL 中這樣做，但您可能會發現這對未來思考有所幫助。

Here are some examples:

> Nit: This is a minor thing. Technically you should do it, but it won’t hugely
> impact things.
>
> Optional (or Consider): I think this may be a good idea, but it’s not strictly
> required.
>
> FYI: I don’t expect you to do this in this CL, but you may find this
> interesting to think about for the future.

這使得審查意圖明確化，有助於作者優先考慮各種評論的重要性。它還有助於避免誤解，例如，如果沒有評論標籤，作者可能會將所有評論解釋為必填，即使有些評論僅用於提供資訊或是選擇性的。

This makes review intent explicit and helps authors prioritize the importance of
various comments. It also helps avoid misunderstandings; for example, without
comment labels, authors may interpret all comments as mandatory, even if some
comments are merely intended to be informational or optional.

## 接受解釋 (Accepting Explanations) {#explanations}

如果您要求開發人員解釋您不瞭解的一段程式碼，通常應該導致他們更清晰地**重寫程式碼**。偶爾，在程式碼中新增注釋也是一種適當的反應，只要不僅僅是解釋過於複雜的程式碼。

If you ask a developer to explain a piece of code that you don't understand,
that should usually result in them **rewriting the code more clearly**.
Occasionally, adding a comment in the code is also an appropriate response, as
long as it's not just explaining overly complex code.

**只在程式碼審查工具中撰寫解釋不利於未來讀者閱讀程式碼。** 除非在某些情況下才可接受，例如當您審查一個您不是很熟悉的區域且開發人員解釋了一些正常程式碼讀者已經知道的內容。

**Explanations written only in the code review tool are not helpful to future
code readers.** They are acceptable only in a few circumstances, such as when
you are reviewing an area you are not very familiar with and the developer
explains something that normal readers of the code would have already known.

接下來: [處理程式碼審查中的異議 (Handling Pushback in Code Reviews)](pushback.md)
