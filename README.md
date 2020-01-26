lesv.dev
========

This is a firebase hosted blog using hugo.  The raw files are stored on Github.

## How to stage & Edit

```sh
hugo new posts/topic.md
hugo server -D
```

## How to Deploy to firebase
change `draft: true` ==> `draft: false`

push to github should deploy to firebase site automatically. (github action)

## Update theme to latest

```sh
cd themes
git submodule update --remote --merge
```
