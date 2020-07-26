
# Git_Docs
This Repository explains about Git Rebase concepts like Interactive rebase feature the Squashing, Deleting, Reordering the commits.

## GIT REBASE USECASES:

**Deleting a commit from middle of the branch || Squashing (merging) two or more commits.**

Consider you have following commits in your branch. git log will show this branch commit information. 

    --------------------------------------------------------------------------------------------
    1.
    commit a99f47413b7f01f8ffc1c3e64695add8ce53dfc7 (HEAD -> testSquash, upstream/dev)
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Thu Dec 26 12:53:01 2019 +0530
    
         First Commit.
    
    2.
    commit 44760b01ccbdffc46bdb3a5df60e3faf73a5b9cb
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Tue Nov 26 14:53:20 2019 +0530
    
         Second Commit.
    
    3.
    commit e38ab9e6a8518377838e00996837b8413d41ec12
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Mon Nov 25 19:20:42 2019 +0530
    
        Third Commit.
    
    4.
    commit d3f87796f2e1a84fdb857eb6bfc464a8b19a2c86
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Fri Nov 22 15:29:11 2019 +0530
    
         Fourth Commit
    
    5.
    commit 40f412d272188d644374923617b35d4902bb3dd4
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Thu Nov 21 16:51:47 2019 +0530
    
         Fifth Commit
    
    -----------------------------------------------------------------------------------------------

*Your requirement is to remove the commit 3 & 4 (e38ab9e6a8518377838e00996837b8413d41ec12 & d3f87796f2e1a84fdb857eb6bfc464a8b19a2c86) from the current branch.*


Command to remove your 3 and 4 commits.

   **`git rebase -i SHA(commit-id)`**

# Example:

        

In above command you need to replace SHA(commit-id) word with your 5'th commit id. 
          
       git rebase -i 40f412d272188d644374923617b35d4902bb3dd4
    
       why we are using 5'th commit hash here. Because to remove a commit from the branch we need mention the next ( following ) commit id as an argument to the rebase command. In our case we need to remove 3rd & 4th commit, so next to 4th commit 5th commit is placed. Hence we are replacing the 5th commit hash id.

       After entering this commit `git rebase -i 40f412d272188d644374923617b35d4902bb3dd4` you get this below editor popup |  






------
    pick d3f8779 Fourth commit.
    pick e38ab9e Third Commit.
    pick 44760b0 Second Commit.
    pick a99f474 First commit.
    
    # Rebase 40f412d..a99f474 onto 40f412d (4 commands)
    #
    # Commands:
    # p, pick = use commit
    # r, reword = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    # s, squash = use commit, but meld into previous commit
    # f, fixup = like "squash", but discard this commit's log message
    # x, exec = run command (the rest of the line) using shell
    # d, drop = remove commit
    #
    # These lines can be re-ordered; they are executed from top to bottom.
    #
    # If you remove a line here THAT COMMIT WILL BE LOST.
    #
    # However, if you remove everything, the rebase will be aborted.
    #
    # Note that empty commits are commented out
    
 ------



In this editor your commits will be viewed in reversed order. Here we can do two things either Deleting a commit or Squashing a commit.

Deleting a commit is simple just replace the pick word with drop or d. Example given below.





    ---------------------------------------------------------------------------
    pick d3f8779 Fourth Commit.
    pick e38ab9e Third Commit.
    d 44760b0 Second Commit.
    pick a99f474 First Commit.
    
    # Rebase 40f412d..a99f474 onto 40f412d (4 commands)
    #
    # Commands:
    # p, pick = use commit
    # r, reword = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    # s, squash = use commit, but meld into previous commit
    # f, fixup = like "squash", but discard this commit's log message
    # x, exec = run command (the rest of the line) using shell
    # d, drop = remove commit
    #
    # These lines can be re-ordered; they are executed from top to bottom.
    #
    # If you remove a line here THAT COMMIT WILL BE LOST.
    #
    # However, if you remove everything, the rebase will be aborted.
    #
    # Note that empty commits are commented out
    
    -----------------------------------------------------------------------------
---------    
    In above editor, you can see clearly that we are droping the second commit because we replaced the pick word with 'd' (i.e drop). For reference trying git log once squashing is done. New commit history was given below.

---------
        --------------------------------------------------------------------------------------------
    
    1.
    commit a99f47413b7f01f8ffc1c3e64695add8ce53dfc7 (HEAD -> testSquash, upstream/dev)
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Thu Dec 26 12:53:01 2019 +0530
    
         First Commit.
    
    2.
    commit e38ab9e6a8518377838e00996837b8413d41ec12
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Mon Nov 25 19:20:42 2019 +0530
    
        Third Commit.
    
    3.
    commit d3f87796f2e1a84fdb857eb6bfc464a8b19a2c86
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Fri Nov 22 15:29:11 2019 +0530
    
         Fourth Commit
    
    4.
    commit 40f412d272188d644374923617b35d4902bb3dd4
    Author: GnanaJeyam <gnanajeyam95@gmail.com>
    Date:   Thu Nov 21 16:51:47 2019 +0530
    
         Fifth Commit
    
    -----------------------------------------------------------------------------------------------
------


Now we can try squashing the commits (merging multiple commits). Again we entering the same command `git rebase -i 40f412d272188d644374923617b35d4902bb3dd4` same editor will open.

    ---------------------------------------------------------------------------
    pick d3f8779 Fourth Commit.
    pick e38ab9e Third Commit.
    s 44760b0 Second Commit.
    pick a99f474 First Commit.
    
    # Rebase 40f412d..a99f474 onto 40f412d (4 commands)
    #
    # Commands:
    # p, pick = use commit
    # r, reword = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    # s, squash = use commit, but meld into previous commit
    # f, fixup = like "squash", but discard this commit's log message
    # x, exec = run command (the rest of the line) using shell
    # d, drop = remove commit
    #
    # These lines can be re-ordered; they are executed from top to bottom.
    #
    # If you remove a line here THAT COMMIT WILL BE LOST.
    #
    # However, if you remove everything, the rebase will be aborted.
    #
    # Note that empty commits are commented out
    
    -----------------------------------------------------------------------------


We are changing the pick to d in Second commit and pressing Yes. The new updated editor can be seen below.


    -----------------------------------------------------------------------------
    # This is a combination of 2 commits.
    # This is the 1st commit message:
    
    Second Commit.
    
    # This is the commit message #2:
    
     Third Commit.
    
    #
    # interactive rebase in progress; onto 40f412d
    # Last commands done (3 commands done):
    #    pick e38ab9e Fix : TFS/ASM coverage area count issue fixed.
    #    squash 44760b0 Added Sendgrid API key.
    # Next command to do (1 remaining command):
    #    pick a99f474 Consul Temporary IP was changed.
    # You are currently rebasing branch 'testSquash' on '40f412d'.
    #
    
                                                                               [ Read 27 lines ]
    ^G Get Help     ^O Write Out    ^W Where Is     ^K Cut Text     ^J Justify      ^C Cur Pos      M-U Undo        M-A Mark Text   M-] To Bracket  M-▲ Previous
    ^X Exit         ^R Read File    ^\ Replace      ^U Uncut Text   ^T To Spell     ^_ Go To Line   M-E Redo        M-6 Copy Text   M-W WhereIs NextM-▼ Next
    
    --------------------------------------------------------------------------------

*In the above you can see multiple commit message ( Second Commit. and Third Commit. ). Now change the commit as your wish, once after completion press Yes and close the editor. Finally Second and Third Commit merged into single commit.*

*Hope you learn something*

**Happy learning !**
