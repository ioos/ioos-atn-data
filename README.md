# ioos-metadata
GitHub Pages for IOOS Metadata Profile with Jekyll Documentation Theme

See website at [https://ioos.github.io/ioos-metadata/](https://ioos.github.io/ioos-atn-data/)

## Contributing to the documentation
See [CONTRIBUTING](CONTRIBUTING.md).

## Deploying site locally
Requirements:
* bundle
* Jekyll

See [IOOS How To: Local Development with Jekyll](https://ioos.github.io/ioos-documentation-jekyll-skeleton/howto.html#local-development-with-jekyll).

Clone this repository:
```commandline
git clone https://github.com/ioos/ioos-atn-data.git
```
Checkout the gh-pages branch:
```commandline
git checkout gh-pages
```
To build the site, in the `ioos-atn-data/` directory run:
```commandline
bundle exec jekyll serve --config _config.yml --watch --verbose --incremental
```
This will deploy a website at: http://127.0.0.1:4000/ioos-atn-data/

Make edits to the appropriate markdown files in `_docs/`. 

If changing headers and menus, stop the running server by entering `ctrl-c` in the terminal. Then run:
```commandline
bundle exec jekyll clean
```
Then build the site again.
```commandline
bundle exec jekyll serve --config _config.yml --watch --verbose --incremental
```
And review at http://127.0.0.1:4000/ioos-atn-data/
