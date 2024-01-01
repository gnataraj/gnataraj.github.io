Difference Between git log and git reflog

`git log` and `git reflog` are both commands in Git, but they serve different purposes.

1. **git log:**
   - The `git log` command is used to display the commit history of a repository.
   - It shows a list of commits, starting with the most recent one, and includes information such as the commit hash, author, date, and commit message.
   - By default, it displays the commit history for the current branch.

   Example:
   ```bash
   git log
   ```

2. **git reflog:**
   - The `git reflog` command, on the other hand, is used to display the reference logs.
   - Reference logs are a history of where the `HEAD` and branch references have pointed to in the past.
   - It includes not only the commit history but also any changes in branch pointers, such as branch creations, checkouts, merges, and rebases.
   - `git reflog` is useful for recovering lost commits or branches.

   Example:
   ```bash
   git reflog
   ```

In summary, while `git log` shows the commit history of a branch, `git reflog` shows a more detailed history of reference changes, which includes movements of the `HEAD` and branch references. The `git reflog` can be particularly helpful for recovering from accidental changes or if you need to revisit a previous state of your repository.
