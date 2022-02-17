# git-practice-Hong-Shao  

## 基本介紹 GIT

---

### **簡史**

Linux kernel 是規模相當大的開放原始碼軟體專案。 Linux kernel 在 1991 年到 2002 年間的維護工作，幾乎都是透過補丁和壓縮檔來完成的。 在 2002 年時，Linux kernel 開始採用名為 BitKeeper 的商業分散式版本控制系統。  
在 2005 年時，開發 Linux kernel 的社群與開發 BitKeeper 的商業公司的合作關係結束，也就無法再免費使用該工具。 這就迫使了 Linux 社群（特別是 Linux 之父 Linus Torvalds）基於使用 BitKeeper 所學到的經驗，來開發自有的工具，花了兩周時間自己用 C 寫了一個分布式版本控制系統，因此 Git 便於 2005 年誕生。

### **使用緣由**

能夠將檔案復原到之前的狀態、將整個專案復原到先前的狀態、比對某一段時間的修改、查看最後是誰在哪個時間點做了錯誤的修改導致問題發生，誰在何時提出了某個功能缺陷⋯⋯等。如果做了一些傻事或者遺失檔案，能很容易地恢復到原先的樣子，但額外增加的工作量卻微乎其微。

#### **GIT vs. SVN**

1. 伺服器架構(Server Architecture)
   * Git: 每位開發者皆具有專案完整版本歷史拷貝(本地端)，而每當檔案發生改變時，皆在本地端進行改變，因此本地端的操作比較快。另外因為使用本地端資料，因此無須時刻連線於伺服器。
   * SVN: 只有開發者正在開發的文件或檔案才會出現在本地端，因此開發者必須時刻連線於伺服器。
   * 以效能而言，SVN的效能優於Git。
2. 分支(Branching)
   * Git: 分支只與特定的commit相關，並且可以隨時針對分支進行增刪查改，而不影響到提交。
   * SVN: 以資料夾的方式創建分支，但trunk的版本不會反映到分支中情況下，後續的將會出現許多問題(conflicts, missing files, and jumbled changes)，這將導致分支與合併變得更加複雜。
   * Conclusion: 在分支的部分，Git的分支應用相對有效。
3. 存取控制(Access Controls)
   * Git: 默認所有專案成員皆有相同的權限。
   * SVN: 可定義各個檔案或資料夾的讀取、寫入權限。
   * Conclusion: 皆有各自的方法能夠設定存取權限。
4. 可檢驗性(Auditability)
   * Git: 若是要改變repository的歷史紀錄，不需連上中央伺服器，可直接更改本地端的歷史紀錄，這些變化的追蹤會以repository等級為主。**非常不鼓勵改變repository的歷史紀錄！**
   * SVN: 若是要改變repository的歷史紀錄，需要連上中央伺服器，變化的追蹤以檔案等級為主。  
   * Conclusion:
5. 存儲需求(Storage Requirements)
   * Git: Git repository無法直接處理過大的檔案。GitHub中可使用git lfs的指令。
   * SVN: SVN repository能夠處理較大型的檔案，並且相較於Git占用更小的空間。
   * Conclusion: SVN在存儲需求中有較好的表現。
6. 可使用性(Usability)
   * Git: 使用命令列作為使用者介面，但語法較不友善於新手。
   * SVN: 使用命令列作為使用者介面，但對於非工程師想要管控非程式碼檔案時較容易。
   * Conclusion: SVN較容易學習。

[Difference](https://www.perforce.com/blog/vcs/git-vs-svn-what-difference)

### **何謂版本控制**

版本控制是一種記錄一個或多個文件內容變化，以便未來查閱特定版本更動情況的系統。  
它允許你將檔案復原到之前的狀態、將整個專案復原到先前的狀態、比對某一段時間的修改、查看最後是誰在哪個時間點做了錯誤的修改導致問題發生，誰在何時提出了某個功能缺陷⋯⋯等。  

## **版本控制的邏輯說明**

---

使用Git是因為需要進行版本控制，雖然手動的方法也能夠達成相似的效果，例如：Git branch 就能夠使用資料夾/檔案名稱進行管理、 Git merge 能夠自行觀察檔案差異進行修改。上述的情況皆需要耗費大量的時間與精力，才能夠完成版本的控管，若是資料量加大，內容更多，這將導致合併人員或相關工作出現錯誤，如果沒有及時發現最後可能導致不可挽回的後果。  
因此我們使用 Git 協助我們進行版本控制，將上述需要手動執行的任務交由系統進行，將不同的檔案進行整合，同個檔案若是被同時更改，則會判斷是否更改同一行的資訊，再決定是否會拋出錯誤碼，此時才需要相關人員進行手動的更改，大量減少了前段敘述中的手動操作中的錯誤，甚至可以避免出現潛藏的致命性錯誤。

## **Git 常用指令集介紹**

---

* git init

    ``` Bash
    # 創建.git，進行初始化，追蹤檔案
    $ git init 
    ```

* git config

    ``` Bash
    # 設定專案的使用者名稱及電子郵件，每次commit後會使用這些資訊

    # 當前的專案。若username包含空格，請用""
    $ git config user.name <username>
    $ git config user.email <your email>
    # 所有的專案
    $ git config --global user.name "<username>"
    $ git config --global user.email <your email>

    # 查看當前資訊
    $ git config --list
    # 查看特定資訊
    $ git config <key>
    ```

* git clone

    ``` Bash
    # 複製網路上某個repository到本機上
    $ git clone <url>
    ```

* git pull

    ``` Bash
    # git pull == git fetch + git merge
    # 拉取目前分支的遠端資料，更新目前的工作目錄
    $ git pull
    # 拉取所有分支的遠端資料，更新目前的工作目錄
    $ git pull --all
    # 更新本地工作目錄(移除遠端中已不存在的檔案與分支)
    $ git pull --prune, -p
    # 為避免無謂的merge message可使用此指令
    # 1.暫存本地 repo. 從上次 pull 之後的變更
    # 2. 回復到上次 pull 時的情況
    # 3. 套用遠端的變更
    # 4. 最後再套用剛暫存下來的本地變更。
    $ git pull --rebase
    # 強制pull
    $ git pull -f <src>:<des>
    ```

* git fetch

    ``` Bash
    # 取得並導入自動建立的分支中，可以切換FETCH_HEAD
    # 取得遠端數據庫的最新歷史記錄，當前分支
    $ git fetch
    # 取得遠端數據庫的最新歷史記錄，所以分支
    $ git fetch --all
    # 強制
    $ git fetch -f <src>:<des>
    # 更新本地repo.
    $ git fetch --prune, -p
    ```

* git push

    ``` Bash
    # 將本地目前分支的提交，送至遠端repo. 
    $ git push
    # 將本地特定分支的提交，送至遠端repo. 中特定的分支
    $ git push origin <src>:<des>
    # 本地端創建分之後第一次上傳
    $ git push -u
    # 將本地所有分支的提交，送至遠端repo.
    $ git push --all
    # 刪除遠端repo. 的分支
    $ git push origin :<des>
    # 強制將commit推上遠端repo.
    # 使用時機: 整理歷史紀錄、只用於自己的分支
    $ git push -f
    ```

* git add

    ``` Bash
    # 將修改過的檔案加入staging area
    $ git add <folder name or file name>

    # 將所有修改過的檔案加入staging area
    # 兩指令根據執行時的目錄而有不同的效果
    # 目前目錄底下所有變動的檔案
    $ git add . 
    # 整個專案所有變動的檔案
    $ git add -A, --all
    ```

* git diff

    ``` Bash
    # 目前暫存區、HEAD所指的commit間的差異
    $ git diff --cached
    # 目前暫存區、HEAD所指的commit間有差異的檔案名稱
    $ git diff --cached --name-only
    # 比較此commit與目前HEAD的差異
    $ git diff <hash code>
    # 比較兩commit的差異
    $ git diff <hash code> <hash code>
    # 工作目錄、暫存區之間的差異
    $ git diff
    ```

* git rm

    ``` Bash
    # 移除檔案，並將其加入staging area
    $ rm <file name>
    $ git add <file name>
    # 結合上述兩個指令
    $ git rm <file name>
    ```

* git commit

    ``` Bash
    # 撰寫此次送繳到local repo.的message

    # 將所以有變更過的檔案加入staging area，並轉寫訊息
    $ git add .
    $ git commit -m <message>
    # 結合上述兩個指令
    $ git commit -a -m <message>
    # 覆寫目前分支最後的commit message
    $ git commit --amend <message>
    ```

* git branch

    ``` Bash
    # 創建一個新的分支，並給予名稱
    $ git branch <name>
    # 刪除本地端已經合併了(merged)的分支
    $ git branch -d, --delete <name>
    # 刪除本地端分支，即便它並未合併(merged)
    $ git branch -D <branch>
    # 刪除遠端已經合併了(merged)的分支
    $ git branch -d -r <branch>
    # 重新命名目前的分支
    $ git branch -m, --move <name>
    # 重新命名一個分支
    $ git branch -m, --move <old> <new>

    # 列出本地端所有分支
    $ git branch
    $ git branch -l, --list
    # 列出所有的分支(including local and remote)
    $ git branch -a, --all
    # 列出已合併過的分支(merged)
    $ git branch --merged
    ```

* git checkout

    ``` Bash
    # 切換到某個分支
    $ git checkout <branch name>
    # 切換到某個分支，若分支不存在則建立一個
    $ git checkout -b <branch name>

    # 若是不小心刪除檔案，可以使用此指令拉回此檔案
    $ git checkout <file name>
    # 將某個檔案切回2個版本前
    $ git checkout head~2 <file name>
    # 回到先前的某個commit狀況
    $ git checkout <commit hash code>
    ```

    > **[Git Checkout - 回到過去，重新開始](https://gitbook.tw/chapters/branch/branch-from-old-commit)**

* git merge

  * Merge
  * Fast Forward Merge: 沒有新的commit
  * Squash and Merge
  * Rebase and Merge
  [...](https://lukemerrett.com/different-merge-types-in-git/)

  ``` Bash
  # 合併分支(可能會產生conflict，需額外處理)
  $ git merge <branch name>
  ```

* git rebase

    ``` Bash
    # 合併分支(可能會產生conflict，需額外處理)
    $ git rebase <branch name>
    # 進入改變commit內容的互動介面
    # hash code: 從現在追溯到特定commit
    $ git rebase -i <hash code>
    ```

    > ["git rebase -i" use](https://www.gss.com.tw/blog/%E4%BD%BF%E7%94%A8-git-rebase-interactive-%E6%A8%A1%E5%BC%8F%E6%95%B4%E7%90%86-commit)

* git log

    ``` bash
    # 列出所有的commit log
    $ git log
    # 列出commit log(-2: 最新的兩行)
    $ git log -2
    # 列出commit log，但每個commit只有1行
    $ git log --oneline
    # 列出所有的git command與變動
    # 只要HEAD有變動，都會有資料
    $ git log -r
    ```

* git status

    ``` Bash
    # 列出工作區中檔案的狀況

    # 列出所有檔案的情況
    $ git status
    $ git status .
    # 列出特定資料夾中檔案的情況
    $ git status <folder name>
    # 以簡潔的格式輸出結果
    # ??: untracked
    # A_: new
    # _M: Modified but not added
    # M_: Modified and added
    # MM: Modified again after added
    # _D: deleted project file
    $ git status -s, --short
    ```

* git reset

    ``` Bash
    # 將added的檔案撤回
    $ git reset
    # 回復到某個commit的時候
    $ git reset <hash code>
    # 回復到HEAD的前一個版本
    $ git reset HEAD~
    # 回復到HEAD的前兩個版本
    $ git reset HEAD~2

    # 若執行完上述後兩個指令但又要切回HEAD
    # 此時的hash code需要是原本版本的hash code
    $ git reset <hash code>
    # 若是忘記則使用此指令
    # 列出每個指令的SHA-1值，[只列最近的3個紀錄]
    $ git log -g [-3]
    $ git reflog [-3]
    # --hard可以強迫放棄reset之後修改的檔案
    $ git reset <hash code> --hard
    # ORIG_HEAD 會記錄「危險操作」之前 HEAD 的位置
    # 危險操作包含分支合併、rebase
    # options: 
    # 1. --hard: 強迫放棄所有檔案
    # 2. --mixed: 保留檔案變更
    # 3. --soft: 變更過的檔案放入index
    $ git reset ORIG_HEAD [options]
    ```

    > [Detailed Git Rebase](https://gitbook.tw/chapters/branch/merge-with-rebase)

* git tag

    ``` Bash
    # 將commit加上tag，通常用在版本號上
    $ git tag <tag> <hash code>
    $ git tag -d <tag>
    $ git tag --delete origin <tag>
    ```

更多指令請上 [Git Document](https://git-scm.com/doc)

## **.gitignore 配置**

---

在.gitignore撰寫特定規則，可以忽略不想要上傳的檔案，被忽略的檔案就不會被加入倒staging area，後續就不會被上傳到Remote Repository中，可應用於避免機密資料上傳至網路上。

```` Bash
# 直接寫入檔案名稱
secret.yml
# 所有副檔名為tmp的檔案
*.tmp
# 某目錄底下的sqlite3檔案
/db/*.sqlite3
# 忽略整個資料夾
/src/
# 允許上述規則中的個別檔案加入索引，使用"!"作為反邏輯
!abc.tmp
!/db/db1.sqlite3
````

## **分支的使用方法**

---

利用分支可以將修改記錄的整體流程分開儲存，讓分支間不受彼此分支的影響，所以在同一個數據庫裡可以同時進行多個不同的修改。

``` Bash
# 創建本地端分支
$ git branch <branch name>
# 切換分支[若是分支不存在，則建立分支]
$ git checkout [-b] <branch name>
# 合併分支至目前的分支中
$ git merge <branch name>
# 刪除本地端分支
$ git branch -d <branch name>
# 刪除遠端分支(仍需進行push)
$ git branch -d -r <branch name>
# 上傳分支(第一次上傳需設定upstream)
$ git push -u <branch name>
# 刪除遠端分支
$ git push origin :<branch name>

# 上傳、拉取所有分支
$ git push --all
$ git fetch --all
$ git pull --all
```

#### **合併分支的方法**

* Merge
修改內容的歷史記錄會維持原狀，但是**合併後的歷史紀錄會變得更複雜**。

* Rebase
修改內容的歷史記錄會接在要合併的分支後面，合併後的歷史記錄會比較清楚簡單，但是**會比使用 merge 更容易發生衝突**。

> note: 看圖片比較容易了解。

## **Commit 介紹及使用**

---

我們可以透過指令，將先前加入索引的文件提交出去，使其在本地端轉換為一個新的版本，之後再使用push指令上傳至遠端儲藏室。

### **git commit 指令使用**

``` bash
# commit message(basic)
$ git commit -m "<your message>"
# 更改上一次的commit訊息
$ git commit --amend -m "<your message>"
```

#### **commit message**

* header: type + [scope] + subject
  * type: feat, fix, docs, style, refactor, perf, test, chore, revert
  * scope: 影響的範圍，是可選的欄位。
  * subject: 簡短描述。
* body: 詳細敘述，說明程式碼變動的項目與原因，還有與先前行為的對比。
* footer: 任務編號，紀錄不兼容的紀錄

## **GitFlow 介紹**

---

* master: 穩定、隨時可上線的版本。內容皆源自合併其他分支，其中因為是穩定版本，因此在commit上會打上版本號。
  > 版本號 (Semantic Versioning)
  > major.minor.patch => 1.0.0, 2.5.3  
  > major: 做了不相容的 API 修改  
  > minor: 做了向下相容的功能性新增  
  > patch: 做了向下相容的問題修正  
* develop: 開發的基礎分支，當要新增功能的時候，所有的 Feature 分支都是從這個分支切出去的。功能完成後，也會合併回來。
* hotfix: 線上產品發生緊急問題的時候，會從 Master 分支開一個 Hotfix 分支出來進行修復，Hotfix 分支修復完成之後，會合併回 Master 分支，也同時會合併一份到 Develop 分支。
* release: Develop 分支夠成熟了，就可以把 Develop 分支合併到 Release 分支，在這邊進行算是上線前的最後測試。測試完成後，Release 分支將會同時合併到 Master 以及 Develop 這兩個分支上。
* feature: 新增功能的時候使用 Feature 分支，Feature 分支都是從 Develop 分支來的，完成之後會再併回 Develop 分支。

> note: branch naming  
>  
> 1. Start branch name with a Group word
> 2. Use Unique ID in branch names
> 3. Use Hyphen or Slash as Separators
> 4. Git branch with Author Name
> 5. Avoid using numbers only  
> 6. Avoid using all naming convention simultaneously
> 7. Avoid long descriptive names for long-lived branches
