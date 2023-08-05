# 處理程式碼審查中的異議 (Handling pushback in code reviews)

有時開發人員會對程式碼審查提出異議。無論是他們不同意您的建議，還是抱怨您太嚴格，反饋都有可能發生。

Sometimes a developer will push back on a code review. Either they will disagree
with your suggestion or they will complain that you are being too strict in
general.

## 誰是對的？ (Who is right?) {#who_is_right}

當開發人員不同意您的建議時，請花些時間去考慮一下他們是不是正確的。通常，他們比您更接近程式碼，因此他們可能對其中某些方面有更好的洞見。他們的論點是否有道理？從程式碼健康度的角度來看是否合理？如果是，讓他們知道他們是對的，然後就讓問題解決。

When a developer disagrees with your suggestion, first take a moment to consider
if they are correct. Often, they are closer to the code than you are, and so
they might really have a better insight about certain aspects of it. Does their
argument make sense? Does it make sense from a code health perspective? If so,
let them know that they are right and let the issue drop.

然而，開發人員並非一直正確無誤。在這種情況下，審查者應進一步解釋為什麼他們認為自己的建議是正確的。一個好的解釋應該展現審查者對開發人員回覆的理解以及為什麼進行變更的額外資訊。

However, developers are not always right. In this case the reviewer should
further explain why they believe that their suggestion is correct. A good
explanation demonstrates both an understanding of the developer's reply, and
additional information about why the change is being requested.

特別是當審查者相信他們的建議能夠改進程式碼健康度時，如果他們認為由於改變而產生的程式碼品質提高可以證明額外的工作是有價值的，他們應繼續支援這項更改。**改善程式碼健康度往往是透過一小步實現的。**

In particular, when the reviewer believes their suggestion will improve code
health, they should continue to advocate for the change, if they believe the
resulting code quality improvement justifies the additional work requested.
**Improving code health tends to happen in small steps.**

有時候需要解釋幾輪建議，才能真正被理解。只要確保始終保持[禮貌](comments.md#courtesy)，並讓開發人員知道你*聽到*他們說的話，只是你不*同意*。

Sometimes it takes a few rounds of explaining a suggestion before it really
sinks in. Just make sure to always stay [polite](comments.md#courtesy) and let
the developer know that you *hear* what they're saying, you just don't *agree*.

## 惹惱開發人員 (Upsetting Developers) {#upsetting_developers}

有些審查人員認為，如果審查者堅持改進，開發人員會感到不悅。有時開發人員確實會感到不悅，但這種情況通常很短暫，之後他們會非常感謝你幫助他們提高程式碼品質。通常，如果您在評論中很[有禮貌](comments.md#courtesy)，開發人員實際上根本不會感到不悅，這種擔憂只存在於審查人員的腦海中。擾動通常更多地與評論的[撰寫方式](comments.md#courtesy)有關，而不是與審查者對程式碼品質的堅持。

Reviewers sometimes believe that the developer will be upset if the reviewer
insists on an improvement. Sometimes developers do become upset, but it is
usually brief and they become very thankful later that you helped them improve
the quality of their code. Usually, if you are [polite](comments.md#courtesy) in
your comments, developers actually don't become upset at all, and the worry is
just in the reviewer's mind. Upsets are usually more about
[the way comments are written](comments.md#courtesy) than about the reviewer's
insistence on code quality.

## 後續清理 (Cleaning It Up Later) {#later}

開發人員常常抱怨的原因是他們想要快速完成任務，並不願意再經歷一次審查才能提交程式碼。他們會承諾稍後會清理程式碼並呈現新的版本。然而，經驗告訴我們，隨著時間的推移，開發人員清理程式碼的意願將會下降。除非開發人員在提交程式碼後立即進行清理，否則這些問題通常都不會得到解決。這不是因為開發人員不負責任，而是因為他們有太多其他工作需要處理，清理工作往往會被遺忘。因此，在程式碼被提交到程式碼庫之前，強烈建議要求開發人員現在就清理他們的程式碼，而不是以後再說。讓人們「稍後再整理程式碼」是程式碼庫失陷的常見方式。

A common source of push back is that developers (understandably) want to get
things done. They don't want to go through another round of review just to get
this CL in. So they say they will clean something up in a later CL, and thus you
should LGTM *this* CL now. Some developers are very good about this, and will
immediately write a follow-up CL that fixes the issue. However, experience shows
that as more time passes after a developer writes the original CL, the less
likely this clean up is to happen. In fact, usually unless the developer does
the clean up *immediately* after the present CL, it never happens. This isn't
because developers are irresponsible, but because they have a lot of work to do
and the cleanup gets lost or forgotten in the press of other work. Thus, it is
usually best to insist that the developer clean up their CL *now*, before the
code is in the codebase and "done." Letting people "clean things up later" is a
common way for codebases to degenerate.

如果一個 CL 引入了新的複雜性，必須在提交之前清理掉，除非它是一個 [緊急情況](../emergencies.md)。如果 CL 揭示了周圍的問題，而它們現在無法解決，開發人員應該為清理問題提交一個 bug，並將其分配給自己，以免丟失。他們也可以在程式碼中寫一個 TODO 註解，參考已提交的 bug。

If a CL introduces new complexity, it must be cleaned up before submission
unless it is an [emergency](../emergencies.md). If the CL exposes surrounding
problems and they can't be addressed right now, the developer should file a bug
for the cleanup and assign it to themselves so that it doesn't get lost. They
can optionally also write a TODO comment in the code that references the filed
bug.

## 對嚴格性的一般抱怨 (General Complaints About Strictness) {#strictness}

如果你以前的程式碼審查比較寬鬆，現在轉為嚴格的話，有些開發人員會投訴得很大聲。提高程式碼審查[速度](speed.md)通常可以讓這些投訴消失。

If you previously had fairly lax code reviews and you switch to having strict
reviews, some developers will complain very loudly. Improving the
[speed](speed.md) of your code reviews usually causes these complaints to fade
away.

有時候這些抱怨需要數個月才會消失，但開發人員最終會意識到嚴格的程式碼審查所帶來的巨大價值，因為他們看到它們產生了多好的程式碼。有時候，最吵鬧的抗議者甚至會在某些事情發生後，真正看到你強制執行程式所帶來的價值，成為你最堅定的支持者。

Sometimes it can take months for these complaints to fade away, but eventually
developers tend to see the value of strict code reviews as they see what great
code they help generate. Sometimes the loudest protesters even become your
strongest supporters once something happens that causes them to really see the
value you're adding by being strict.

## 解決衝突 (Resolving Conflicts) {#conflicts}

如果你遵循了以上的步驟，但仍然遇到無法解決的開發者衝突，請參考《[程式碼審查標準](standard.md)》以便遵循指導原則並解決衝突。

If you are following all of the above but you still encounter a conflict between
yourself and a developer that can't be resolved, see
[The Standard of Code Review](standard.md) for guidelines and principles that
can help resolve the conflict.
