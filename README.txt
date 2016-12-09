# To push all files to the private folder:
git push -u origin master

# To push the web content up to the gh-pages
git subtree push --prefix _book origin gh-pages

# To force push to the gh-pages, disable branch protection on github 
# for that branch (via settings >> branches) then type:
git push origin `git subtree split --prefix _book master`:gh-pages --force