# My personal blog

Source code using [Hugo](https://gohugo.io/) to generate my own blog.

To start the server locally:

`hugo server -w`

## If you want to start your own blog from scratch:

### Using Mac:

```
brew update && brew install hugo
mkdir your_own_blog_directory
cd your_own_blog_directory
hugo new site .
hugo new post/welcome.md

```
then, [Choose a theme](http://themes.gohugo.io/) and:

```
git clone https://github.com/halogenica/beautifulhugo.git themes/beautifulhugo
hugo server -w
```

Now You're good to start your own blog as well...