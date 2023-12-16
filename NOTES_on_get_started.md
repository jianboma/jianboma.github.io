# Notes get on started

## Notes
```sh
bundle install
# assuming pip is your Python package manager
pip install jupyter
bundle exec jekyll serve --lsi
```

If you want to add projects, add it in `_pages/projects.md`. I explicitly moved the projects.md to hidden. This is applied to teaching, repositories, and people if you want to.


## CV
For editing cv, the content is edited in [cv.yaml](_data/cv.yml).

## editing about me
The `About` is [about.md](_pages/about.md).

## change theme color
https://github.com/alshedivat/al-folio/tree/master?tab=readme-ov-file#theming

The backround color can be changed as well. `--global-code-bg-color` in [_themes.scss](_sass/_themes.scss) is used to change the background color of highlighed content. I've changed it to green-color-lime from pink.