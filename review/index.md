# Code Review Developer Guide

# 程式碼審查開發者指南

## Introduction {#intro}

## 簡介 {#intro}

A code review is a process where someone other than the author(s) of a piece of
code examines that code.

程式碼審查是一種流程，在這個流程中除了原始碼的作者以外，還有其他人會審查這段程式碼。

At Google, we use code review to maintain the quality of our code and products.

在 Google，我們使用程式碼審查來維持我們的程式碼和產品品質。

This documentation is the canonical description of Google's code review
processes and policies.

這份文件是 Google 代表程式碼審查過程與方針的權威說明。

This page is an overview of our code review process. There are two other large
documents that are a part of this guide:

這個頁面是我們的程式碼審查過程概述。還有兩份其他重要文件是本指南的一部分：

-   **[How To Do A Code Review](reviewer/index.md)**: A detailed guide for code
    reviewers.
-   **[The CL Author's Guide](developer/index.md)**: A detailed guide for
    developers whose CLs are going through review.


---

- **[如何進行程式碼審查](reviewer/index.md)**：針對程式碼審查者的詳盡指南。
- **[CL 作者指南](developer/index.md)**：針對正在進行審查的開發人員的詳盡指南。

## What Do Code Reviewers Look For? {#look_for}

## 程式碼審查者查詢什麼？ {#look_for}

Code reviews should look at:

程式碼審查應該關注：

-   **Design**: Is the code well-designed and appropriate for your system?
-   **Functionality**: Does the code behave as the author likely intended? Is
    the way the code behaves good for its users?
-   **Complexity**: Could the code be made simpler? Would another developer be
    able to easily understand and use this code when they come across it in the
    future?
-   **Tests**: Does the code have correct and well-designed automated tests?
-   **Naming**: Did the developer choose clear names for variables, classes,
    methods, etc.?
-   **Comments**: Are the comments clear and useful?
-   **Style**: Does the code follow our
    [style guides](http://google.github.io/styleguide/)?
-   **Documentation**: Did the developer also update relevant documentation?


---

- **設計**: 程式碼是否設計良好且適合您的系統？ 
- **功能性**: 程式碼是否按照作者的意圖運作？程式碼的運作方式對用戶來說是否良好？ 
- **複雜度**: 程式碼是否可以更簡單？另一個開發人員是否能夠在未來輕鬆理解和使用此代碼？ 
- **測試**: 程式碼是否具有正確且設計良好的自動化測試？ 
- **命名**: 開發人員對變數、類、方法等是否選擇了清晰的命名？ 
- **註釋**: 註釋是否清晰有用？ 
- **風格**: 程式碼是否遵循我們的[風格指南](http://google.github.io/styleguide/)？ 
- **檔案**: 開發人員是否也更新了相關檔案？

See **[How To Do A Code Review](reviewer/index.md)** for more information.

請檢視 **[進行程式碼審查的方法](reviewer/index.md)** 以瞭解更多資訊。

### Picking the Best Reviewers {#best_reviewers}

### 選擇最佳評論者 {#best_reviewers}

In general, you want to find the *best* reviewers you can who are capable of
responding to your review within a reasonable period of time.

一般來說，您會想尋找能夠在合理的時間內回覆您的評論的 *最佳* 審查者。

The best reviewer is the person who will be able to give you the most thorough
and correct review for the piece of code you are writing. This usually means the
owner(s) of the code, who may or may not be the people in the OWNERS file.
Sometimes this means asking different people to review different parts of the
CL.

最好的評論者是那些能夠為你撰寫的程式碼提供最全面且正確的評論的人。這通常意味著程式碼的所有者，他們可能是 OWNERS 檔案中的人，也可能不是。有時這意味著要求不同的人審查 CL 中的不同部分。

If you find an ideal reviewer but they are not available, you should at least CC
them on your change.

如果你找到了一位理想的審查者但他們不可用，你至少應該將他們抄送在你的更改中。

### In-Person Reviews (and Pair Programming) {#in_person}

### 面對面評論（和對擊式程式設計）{#in_person}

If you pair-programmed a piece of code with somebody who was qualified to do a
good code review on it, then that code is considered reviewed.

如果你與一個有資格對程式碼進行良好的程式碼審查的人進行了程式碼的對稱程式設計，那麼該程式碼被認為已經進行了審查。

You can also do in-person code reviews where the reviewer asks questions and the
developer of the change speaks only when spoken to.

您也可以進行面對面的程式碼審查，其中審查人員提問，而變更的開發人員則在被問到時才發言。

## See Also {#seealso}

## 參見 {#seealso}

-   [How To Do A Code Review](reviewer/index.md): A detailed guide for code
    reviewers.
-   [The CL Author's Guide](developer/index.md): A detailed guide for developers
    whose CLs are going through review.

---

- [如何進行程式碼審查](reviewer/index.md)：針對程式碼審查人員的詳細指南。
- [程式碼審查作者指南](developer/index.md)：針對經歷審查的開發人員的詳細指南。

