# Adding multiple remotes (for push)
This allows you to push to multiple place but only fetch from one remote

```shell
git remote add all originalurl
git remote set-url --push all otherurl
# Repeat for as many remotes as you like
git remote set-url --push --add all originalurl
git push -u all main
```
where:
- originalurl = The url you want to fetch from
- otherurl = The other url you want to push to

After doing this
```shell
git remote -vv
```
Should show multiple push urls for all