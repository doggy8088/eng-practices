# 撰寫良好的 CL 描述 (Writing good CL descriptions)

CL (變更清單) 說明是一個公開紀錄，記錄了修改了哪些內容以及修改的原因。它將成為我們版本控制歷史的一個永久部分，可能會被除了審查者以外的數百人閱讀多年。

A CL description is a public record of **what** change is being made and **why**
it was made. It will become a permanent part of our version control history, and
will possibly be read by hundreds of people other than your reviewers over the
years.

未來的開發人員將會根據您的程式描述來搜尋您的 CL。也許有人在未來會因為模糊的記憶而尋找您的變更，但卻沒有具體的資訊。如果所有重要的資訊都在程式碼中而非描述中，他們將會很難定位您的 CL。

Future developers will search for your CL based on its description. Someone in
the future might be looking for your change because of a faint memory of its
relevance but without the specifics handy. If all the important information is
in the code and not the description, it's going to be a lot harder for them to
locate your CL.

## 第一行 (First Line) {#firstline}

- 正在做什麼的簡短摘要。(Short summary of what is being done.)
- 以命令的形式書寫完整的句子。(Complete sentence, written as though it was an order.)
- 空一行。(Follow by empty line.)

CL 的第一行描述應該是關於 CL 詳細做了什麼的短摘要，接著是空白行。這是出現在版本控制歷史總結的內容，因此它應該提供足夠的資訊，讓未來的程式碼搜尋者不必閱讀您的 CL 或整個描述，就可以理解您的 CL 實際上做了什麼或者它如何與其他 CL 不同。換句話說，第一行應該獨立存在，讓讀者能夠更快地瀏覽程式碼歷史。

The **first line** of a CL description should be a short summary of
*specifically* **what** *is being done by the CL*, followed by a blank line.
This is what appears in version control history summaries, so it should be
informative enough that future code searchers don't have to read your CL or its
whole description to understand what your CL actually *did* or how it differs
from other CLs. That is, the first line should stand alone, allowing readers to
skim through code history much faster.

請儘量讓你的第一行簡短、聚焦且直截了當。閱讀者的清晰度和實用性應該是最重要的關注點。

Try to keep your first line short, focused, and to the point. The clarity and
utility to the reader should be the top concern.

傳統上，CL 描述的第一行應該是一個完整的句子，就像是一個命令（祈使句）。例如，說「**刪除** FizzBuzz RPC，並**替換**為新系統。」而不是「**正在刪除** FizzBuzz RPC，並**正在替換**為新系統。」您不需要將描述的其餘部分寫成命令式的句子。

By tradition, the first line of a CL description is a complete sentence, written
as though it were an order (an imperative sentence). For example, say
\"**Delete** the FizzBuzz RPC and **replace** it with the new system." instead
of \"**Deleting** the FizzBuzz RPC and **replacing** it with the new system."
You don't have to write the rest of the description as an imperative sentence,
though.

## 具有資訊性的主體 (Body is Informative) {#informative}

[第一行](#firstline) 應該是簡短而集中的摘要，其餘描述應填補細節並包含讀者需要全面瞭解變更清單的任何補充資訊。它可能包括正在解決的問題的簡要描述，以及為什麼這是最佳方法。如果有任何方法的缺點，也應該提到。如果適用，包括背景資訊，如錯誤編號、基準測試結果和設計文件的連結。

The [first line](#firstline) should be a short, focused summary, while the rest
of the description should fill in the details and include any supplemental
information a reader needs to understand the changelist holistically. It might
include a brief description of the problem that's being solved, and why this is
the best approach. If there are any shortcomings to the approach, they should be
mentioned. If relevant, include background information such as bug numbers,
benchmark results, and links to design documents.

如果您包含外部資源的連結，要考慮到因存取限制或保留政策，這些連結可能對未來讀者不可見。在可能的情況下，請提供足夠的上下文讓審查者和未來的讀者理解程式碼。

If you include links to external resources consider that they may not be visible
to future readers due to access restrictions or retention policies. Where
possible include enough context for reviewers and future readers to understand
the CL.

即使是小的 CL 也值得仔細關注，把這個 CL 放在情境中。

Even small CLs deserve a little attention to detail. Put the CL in context.

## 不良的 CL 說明 (Bad CL Descriptions) {#bad}

「修正錯誤」是不足的 CL 說明。是哪個錯誤？你採取了什麼措施來修復它？其他同樣糟糕的描述包括：

- "修正建置。"
- "新增補丁。"
- "將程式碼從 A 移動到 B。"
- "第一階段。"
- "新增方便的函式。"
- "刪除奇怪的 URL。"

"Fix bug" is an inadequate CL description. What bug? What did you do to fix it?
Other similarly bad descriptions include:

- "Fix build."
- "Add patch."
- "Moving code from A to B."
- "Phase 1."
- "Add convenience functions."
- "kill weird URLs."

Some of those are real CL descriptions. Although short, they do not provide
enough useful information.

其中一些是真正的指令列描述，雖然短，但它們沒有提供足夠有用的資訊。

## 良好的 CL 說明 (Good CL Descriptions) {#good}

以下是一些好的描述範例。

Here are some examples of good descriptions.

### 功能變更 (Functionality change)

範例：

> rpc: 移除 RPC 伺服器訊息 freelist 上的大小限制。
>
> FizzBuzz 等伺服器有非常大的訊息，可以從重複使用中受惠。
> 將 freelist 加大，並新增一個 goroutine，使其隨時間慢慢釋放 freelist 條目，以便閒置的伺服器最終釋放所有 freelist 條目。

Example:

> rpc: remove size limit on RPC server message freelist.
>
> Servers like FizzBuzz have very large messages and would benefit from reuse.
> Make the freelist larger, and add a goroutine that frees the freelist entries
> slowly over time, so that idle servers eventually release all freelist
> entries.

前幾個字描述 CL 實際上可以做什麼。其餘的描述談論了正在解決的問題，為什麼這是一個好的解決方案以及有關具體實施的更多資訊。

The first few words describe what the CL actually does. The rest of the
description talks about the problem being solved, why this is a good solution,
and a bit more information about the specific implementation.

### 重構 (Refactoring)

範例：

> 建立一個 Task，使用其 TimeStr 和 Now 方法的 TimeKeeper。
>
> 加入 Task 的 Now 方法，這樣可以刪除 borglet() getter 方法（僅被 OOMCandidate 使用，以呼叫 borglet 的 Now 方法）。這將取代在 Borglet 上代理到 TimeKeeper 的方法。
>
> 讓 Task 提供 Now 是消除對 Borglet 依賴的一個步驟。最終，依賴於從 Task 獲取 Now 的合作者應該改為直接使用 TimeKeeper，但這已是循序漸進重構的一個遷就。
>
> 繼續長期重構 Borglet 階層的目標。

Example:

> Construct a Task with a TimeKeeper to use its TimeStr and Now methods.
>
> Add a Now method to Task, so the borglet() getter method can be removed (which
> was only used by OOMCandidate to call borglet's Now method). This replaces the
> methods on Borglet that delegate to a TimeKeeper.
>
> Allowing Tasks to supply Now is a step toward eliminating the dependency on
> Borglet. Eventually, collaborators that depend on getting Now from the Task
> should be changed to use a TimeKeeper directly, but this has been an
> accommodation to refactoring in small steps.
>
> Continuing the long-range goal of refactoring the Borglet Hierarchy.

第一行描述了 CL 做什麼以及這與過去的不同之處。其餘的描述將談論特定的實現，CL 的上下文，解決方案並不理想，以及可能的未來方向。它還解釋了為什麼要進行這個更改。

The first line describes what the CL does and how this is a change from the
past. The rest of the description talks about the specific implementation, the
context of the CL, that the solution isn't ideal, and possible future direction.
It also explains *why* this change is being made.

### 小的 CL 需要一些背景說明 (Small CL that needs some context)

範例：

> 建立一個 Python3 的編譯規則，針對 status.py。
>
> 這讓已經在 Python3 上使用此規則的使用者能夠依賴原始 status 編譯規則旁邊的規則，而不是在他們自己的樹中的某個地方。它鼓勵新使用者盡可能使用 Python3，而不是 Python2，並顯著簡化一些目前正在開發的自動化建構檔案重構工具。

Example:

> Create a Python3 build rule for status.py.
>
> This allows consumers who are already using this as in Python3 to depend on a
> rule that is next to the original status build rule instead of somewhere in
> their own tree. It encourages new consumers to use Python3 if they can,
> instead of Python2, and significantly simplifies some automated build file
> refactoring tools being worked on currently.

第一句話描述實際正在做什麼。其餘的描述解釋了為什麼要進行更改，並為審查者提供了很多背景。

The first sentence describes what's actually being done. The rest of the
description explains *why* the change is being made and gives the reviewer a lot
of context.

## 使用標籤 (Using tags) {#tags}

標籤是手動輸入的標籤，可用於對 CL 進行分類。這些可以由工具支援，也可以只是由團隊慣例使用。

Tags are manually entered labels that can be used to categorize CLs. These may
be supported by tools or just used by team convention.

例如：

- "[標籤]"
- "[長一點的標籤]"
- "#標籤"
- "標籤:"

For example:

- "[tag]"
- "[a longer tag]"
- "#tag"
- "tag:"

使用標籤是可選的。

Using tags is optional.

在新增標籤時，需要考慮它們應該放在 CL 描述的正文部分還是第一行。限制在第一行使用標籤，因為這可能會遮蔽內容。

When adding tags, consider whether they should be in the [body](#informative) of
the CL description or the [first line](#firstline). Limit the usage of tags in
the first line, as this can obscure the content.

有標籤和沒有標籤的範例：

Examples with and without tags:

``` {.good}
// Tags are okay in the first line if kept short.
[banana] Peel the banana before eating.

// Tags can be inlined in content.
Peel the #banana before eating.

// Tags are optional.
Peel the banana before eating.

// Multiple tags are acceptable if kept short.
#banana #apple: Assemble a fruit basket.

// Tags can go anywhere in the CL description.
> Assemble a fruit basket.
>
> #banana #apple
```

``` {.bad}
// Too many tags (or tags that are too long) overwhelm the first line.
//
// Instead, consider whether the tags can be moved into the description body
// and/or shortened.
[banana peeler factory factory][apple picking service] Assemble a fruit basket.
```

## 產生的 CL 描述 (Generated CL descriptions)

有些程式碼變更是由工具產生的，盡可能使用此處的建議來描述它們。也就是說，它們的第一行應該是簡短、專注且獨立的，而程式碼變更的詳細描述應包含有用的細節，以幫助審查者和未來的程式碼搜尋者理解每個程式碼變更的影響。

Some CLs are generated by tools. Whenever possible, their descriptions should
also follow the advice here. That is, their first line should be short, focused,
and stand alone, and the CL description body should include informative details
that help reviewers and future code searchers understand each CL's effect.

## 在提交程式變更前請先檢閱說明 (Review the description before submitting the CL)

在進行程式碼審查期間，變更程式碼的可能性很高。在提交程式碼變更前，檢視變更的描述可以確保描述正確地反映程式碼的更改。

CLs can undergo significant change during review. It can be worthwhile to review
a CL description before submitting the CL, to ensure that the description still
reflects what the CL does.

下一步: [小的 CL 變更清單 (Small CLs)](small-cls.md)
