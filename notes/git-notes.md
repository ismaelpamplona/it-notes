# GIT Notes

### Oficial Documentation: [https://git-scm.com/docs](https://git-scm.com/docs)

## GIT Workflow:

### youtube: [GIT Workflow - Georgia Tech - Software Development Process](https://www.youtube.com/watch?v=3a2x1iJFJWc&t=51s)

![Git Workflow](../images/gitworkflow.png)

## Basic commands:

```javascript
$ git init // Create an empty Git repository or reinitialize an existing one
$ git add . // This command updates the index using the current content found in the working tree, to prepare the content staged for the next commit.
$ git add someFile.js
$ git commit -m ¨some message¨ // Stores the current contents of the index in a new commit along with a log message from the user describing the changes.
$ git commit -a -m ¨some message¨ // Add and Commit at the same command - automatic stage files
$ git push -u origin master // Updates remote refs using local refs
```

```javascript
$ git fetch //
$ git merge //
$ git pull //
$ git diff HEAD //
$ git diff //
```
