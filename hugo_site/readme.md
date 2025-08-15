# Hugo Blog site

This is a static blog site using Hugo with theme Papermod.  
Hugo is a versatile and powerful static website generator. 
Papermod is a custom theme developed for Hugo. 

To run and build the website, first install Papermod theme by 

```
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

Then use commands,

```
# Preview
hugo server -O  # -O flag will open the browser
# Build
hugo build 
```

For more, check the article [blog with github action](https://harryhanyuhao.github.io/harryhanYuhao/posts/blog_with_github_action/).
