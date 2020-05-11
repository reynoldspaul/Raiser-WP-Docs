## Deploy

First build site

```
cd website
npm run build
```

Then push to gh-pages branch
```
cd ../
git checkout gh-pages

git add -f website/build/Riaser-Wp-Docs/ && git commit -m "Build"
git subtree push --prefix /website/build/Riaser-Wp-Docs/ origin gh-pages
```

Tutorial https://www.youtube.com/watch?v=dn4dgA51WNg