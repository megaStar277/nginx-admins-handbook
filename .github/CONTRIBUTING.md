# Contributing

  > _A real community, however, exists only when its members interact in a meaningful way that deepens their understanding of each other and leads to learning._

If you would like to support this project, have an interesting idea how to improve the operation of this tool, or if you found some errors - fork this, add your fixes, and add a pull request of your branch to the **master branch**.

## Using the issue tracker

The [issue tracker](https://github.com/trimstray/nginx-admins-handbook/issues) is
the preferred channel for bug reports, features requests and submitting pull requests, but please respect the following restrictions:

* Please **do not** use the issue tracker for personal support requests (use
  [Stack Overflow](https://stackoverflow.com) or IRC)

* Please **do not** derail or troll issues. Keep the discussion on topic and
  respect the opinions of others

## Signature of commit

Moving forward all commits to this project must include a "signed-off-by" line indicating the name and email address of the contributor signing off on the change. To enable signatures add the following lines to `.git/hooks/prepare-commit-msg` :

```
SOB=$(git var GIT_AUTHOR_IDENT | sed -n 's/^\(.*>\).*$/- signed-off-by: \1/p')
grep -qs "^$SOB" "$1" || echo "$SOB" >> "$1"
```

## Pull requests

When creating a pull request, please heed the following:

- Base your code on the latest master branch to avoid manual merges
- Code review may ensue in order to help shape your proposal
- Explain the problem and your proposed solution
