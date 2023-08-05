# 如何處理審查者意見 (How to handle reviewer comments)

當您發送一個供審查的 CL 時，您的審查者可能會對您的 CL 發表多條評論。下面是有關處理審查者評論的一些有用資訊。

When you've sent a CL out for review, it's likely that your reviewer will
respond with several comments on your CL. Here are some useful things to know
about handling reviewer comments.

## 不要把它當成個人攻擊 (Don't Take it Personally) {#personal}

審查的目標是維護我們程式碼庫和產品的品質。當審查者對您的程式碼提出評論時，請把這視為他們試圖幫助您、程式碼庫和 Google，而不是對您或您的能力的個人攻擊。

The goal of review is to maintain the quality of our codebase and our products.
When a reviewer provides a critique of your code, think of it as their attempt
to help you, the codebase, and Google, rather than as a personal attack on you
or your abilities.

有時審查者會感到沮喪，並在他們的評論中表達這種沮喪。雖然這對於審查者來說並不是一種好的實踐，但作為開發人員，您應該為此做好準備。問問自己："審查者試圖要傳達給我哪些建設性的內容？"，然後像他們實際說的那樣去操作。

Sometimes reviewers feel frustrated and they express that frustration in their
comments. This isn't a good practice for reviewers, but as a developer you
should be prepared for this. Ask yourself, "What is the constructive thing that
the reviewer is trying to communicate to me?" and then operate as though that's
what they actually said.

**永遠不要生氣回應程式碼審查的評論。**這是一種嚴重違反專業禮儀的行為，它將永遠存在於程式碼審查工具中。如果你因為太生氣或煩惱而無法友好地回應，那麼離開你的電腦一段時間，或做些其他事情，直到你感到足夠冷靜才能禮貌地回覆。

**Never respond in anger to code review comments.** That is a serious breach of
professional etiquette that will live forever in the code review tool. If you
are too angry or annoyed to respond kindly, then walk away from your computer
for a while, or work on something else until you feel calm enough to reply
politely.

通常情況下，如果審查者無法以有建設性且有禮貌的方式提供反饋，請親自向他們解釋。如果您無法當面或透過視訊通話與他們交談，請透過私人電子郵件與他們聯繫。以友好的方式告訴他們您不喜歡什麼，以及您希望他們做不同的事情。如果他們對這個私人討論也以非建設性的方式回應，或是沒有達到預期的效果，那就根據情況提升給您的經理。

In general, if a reviewer isn't providing feedback in a way that's constructive
and polite, explain this to them in person. If you can't talk to them in person
or on a video call, then send them a private email. Explain to them in a kind
way what you don't like and what you'd like them to do differently. If they also
respond in a non-constructive way to this private discussion, or it doesn't have
the intended effect, then
escalate to your manager as
appropriate.

## 修正程式碼 (Fix the Code) {#code}

如果審查人員表示無法理解您的程式碼，您應該首先澄清程式碼本身。如果程式碼無法澄清，則新增一個程式碼註解來解釋程式碼存在的原因。如果評論似乎毫無意義，那麼您的回應應該是在程式碼審查工具中進行解釋。

If a reviewer says that they don't understand something in your code, your first
response should be to clarify the code itself. If the code can't be clarified,
add a code comment that explains why the code is there. If a comment seems
pointless, only then should your response be an explanation in the code review
tool.

如果審查者沒有理解你的一些程式碼，未來閱讀這些程式碼的人可能也不會理解。在程式碼審查工具中撰寫回應並不會幫助未來閱讀程式碼的人，但是澄清你的程式碼或新增程式碼註解則能對他們有所幫助。

If a reviewer didn't understand some piece of your code, it's likely other
future readers of the code won't understand either. Writing a response in the
code review tool doesn't help future code readers, but clarifying your code or
adding code comments does help them.

## 協作思考 (Think Collaboratively) {#think}

撰寫一個 CL 可能需要很多工作。最後終於將它發送給審查者，並感到完成了，且確信不需要進一步的工作，這通常非常滿足。如果收到要求更改的評論，特別是您不同意的評論，可能會感到沮喪。

Writing a CL can take a lot of work. It's often really satisfying to finally
send one out for review, feel like it's done, and be pretty sure that no further
work is needed. It can be frustrating to receive comments asking for changes,
especially if you don't agree with them.

在這種情況下，請花些時間退一步並考慮審查者是否提供了有助於程式基礎和 Google 的有價值反饋。你應該始終首先問自己的問題是："我瞭解審查者的要求嗎？"

At times like this, take a moment to step back and consider if the reviewer is
providing valuable feedback that will help the codebase and Google. Your first
question to yourself should always be, "Do I understand what the reviewer is
asking for?"

如果你無法回答那個問題，請詢問審查者以取得澄清。

If you can't answer that question, ask the reviewer for clarification.

如果你理解了評論，但不同意它們，重要的是要以合作的方式思考，而不是以鬥爭或防禦的方式。

And then, if you understand the comments but disagree with them, it's important
to think collaboratively, not combatively or defensively:

不好：「不，我不打算這樣做。」

Bad: "No, I'm not going to do that."

好的："我因為這些優缺點和權衡而選擇了 X。我的理解是使用 Y 會更糟糕，因為這些原因。你是在暗示 Y 更好地滿足原始的權衡，我們應該不同地衡量權衡，還是其他什麼？"

Good: "I went with X because of [these pros/cons] with [these
tradeoffs].
My understanding is that using Y would be worse because of [these reasons]. Are
you suggesting that Y better serves the original tradeoffs, that we should weigh
the tradeoffs differently, or something else?"

請記住，**禮貌和尊重**應始終是首要考慮。如果您不同意審查者，請尋找合作方式：請求澄清，討論優缺點，並解釋為什麼您執行任務的方法對於程式碼庫、使用者和/或 Google 更優。

Remember,
**[courtesy and respect](https://chromium.googlesource.com/chromium/src/+/master/docs/cr_respect.md)
should always be a first priority**. If you disagree with the reviewer, find
ways to collaborate: ask for clarifications, discuss pros/cons, and provide
explanations of why your method of doing things is better for the codebase,
users, and/or Google.

有時候，你可能會對使用者、程式碼庫(codebase)或該項 CL 的情況有更多瞭解，而評審者可能尚未瞭解的內容。如適當地[修正程式碼](#code)，並透過討論與分享更多背景資訊來與評審者互動。通常，你可以基於技術事實與評審者達成共識。

Sometimes, you might know something about the users, codebase, or CL that the
reviewer doesn't know. [Fix the code](#code) where appropriate, and engage your
reviewer in discussion, including giving them more context. Usually you can come
to some consensus between yourself and the reviewer based on technical facts.

## 解決衝突 (Resolving Conflicts) {#conflicts}

解決衝突的第一步應該是嘗試與審查者達成共識。如果無法達成共識，請參閱[程式碼審查標準](../reviewer/standard.md)，其中提供了在這種情況下應遵循的原則。

Your first step in resolving conflicts should always be to try to come to
consensus with your reviewer. If you can't achieve consensus, see
[The Standard of Code Review](../reviewer/standard.md), which gives principles
to follow in such a situation.
