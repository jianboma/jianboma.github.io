# Notes get on started

## Notes
```sh
bundle install
# assuming pip is your Python package manager
pip install jupyter
conda activate torch19py38 # activate your python virtual environment
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

## Add papers 
Papers can be added to the [papers.bib](_bibliography/papers.bib) page. Add pdf and preview into fields pdf={xx.pdf}, preview={xx.png}. Pdf should be put into assets/pdf and image put into assets/img/publication_preview 

## add pages into the project

For example, add [diffusion model](_projects/diffusion_models). Add a markdown into this folder. Add the category into the `display_categories` field in the [markdown file](_pages/projects.md).