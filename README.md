# Git Tutorial By - Abhishek Maheshwari

## Have commands that are used mostly in day-to-day life.
1. git init 
2. git add file_name
3. git commit -m "First commit"
4. git remote add origin http_url
5. git push -u origin master  
 
## To show branch in terminal
```
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

## Git commands: 
1. Git stash - Temporary store the code and make changes to required branch and when this code needs use git stash pop.
2. Git checkout RCT-1925
3. Git pull origin RCT-1925
4. Git checkout RCT-1926
5. Git merge RCT-1925
6. Git stash pop
7. git stash clear - Chnages that are saved temporary are now not avaialble.

```
Error:  ActiveRecord::RecordNotUnique (PG::UniqueViolation: ERROR:  duplicate key value violates unique constraint "uploadable_expenses_pkey"
DETAIL:  Key (id)=(6) already exists.
```

## Solution:

1. ActiveRecord::Base.connection("DROP SEQUENCE uploadable_expenses_id_seq CASCADE;")
2. ActiveRecord::Base.connection.execute("CREATE SEQUENCE uploadable_expenses_id_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE CACHE 1;")
3. ActiveRecord::Base.connection.execute("ALTER TABLE ONLY uploadable_expenses ALTER COLUMN id SET DEFAULT nextval('uploadable_expenses_id_seq'::regclass);")
4. ActiveRecord::Base.connection.execute("SELECT setval('uploadable_expenses_id_seq', COALESCE((SELECT MAX(id)+1 FROM uploadable_expenses), 1), false);")

## Some more commands with explaination
1. git restore --staged file_name : Done to change file back into the staging(untracked files) i.e after git add it revert back to git status.  
2. git reset last_3rd_commit_id : wish to remove any specific commit from git log/history.Commits are build one over the other if you want to delete last 2 commits then copy the commit id of last 3rd commit. Now the first 2 commit files changes are in the staging area.
3. git remote -v : shows all the urls attached to the folder.
4. git merge branch_name - to merge branch into other.
5. git remote add upstream url :  from where you have forked the project is known as Upstream url by convention. This is done when we want to contribute to the project and fork it and make changes in local i.e Open Source Contribution. Origin is your personal.
6. git fetch --all --prune : fetch all the commit from the upstream(remote) branch and also fetch the deleted commits(prune)
7. git reset --hard upstream/main : reset to the main branch of upstream so that we can maintain the remote main with our repo(local) main and see the commits that are being added to the main of the upstream.
8. then do - git push origin main : to make changes to our main branch. 
9. git pull upstream main : is same as steo from 6-8. Basically, pull = fetch + merge
10. git rebase -i commit_id : above which you aregoing to merge all the commits in a one single commit
   - pick d8279dd8 1
   - s vw13414hw 2  --> s stands for squish
   - s g234wu453 3
   - pick s53265 4  --> pick means I am taking this commmit.
   - then use :x to mention the message for new commit. 
   -   ==> the first three commit will be merge to commit 1 and 4th commit is treated as individual commit.

## Note : One branch is associated with 1 pull request, you can not create multiple pull request with single branch.
