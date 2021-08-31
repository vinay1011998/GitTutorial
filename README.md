# Git Tutorial By - Abhishek Maheshwari

## Have commands that are used mostly in day-to-day life.

## To show branch in terminal
```
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

## Git commands: 
1. Git stash
2. Git checkout RCT-1925
3. Git pull origin RCT-1925
4. Git checkout RCT-1926
5. Git merge RCT-1925
6. Git stash pop

```
Error:  ActiveRecord::RecordNotUnique (PG::UniqueViolation: ERROR:  duplicate key value violates unique constraint "uploadable_expenses_pkey"
DETAIL:  Key (id)=(6) already exists.
```


## Solution:

1. ActiveRecord::Base.connection("DROP SEQUENCE uploadable_expenses_id_seq CASCADE;")
2.  ActiveRecord::Base.connection.execute("CREATE SEQUENCE uploadable_expenses_id_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE CACHE 1;")
3.  ActiveRecord::Base.connection.execute("ALTER TABLE ONLY uploadable_expenses ALTER COLUMN id SET DEFAULT nextval('uploadable_expenses_id_seq'::regclass);")
4.   ActiveRecord::Base.connection.execute("SELECT setval('uploadable_expenses_id_seq', COALESCE((SELECT MAX(id)+1 FROM uploadable_expenses), 1), false);")

