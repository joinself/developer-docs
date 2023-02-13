# Developer Documentation

## Installation

- install Hugo: https://gohugo.io/installation/
- clone the repo: `git clone git@github.com:joinself/developer-docs.git`
- change directory: `cd developer-docs`
- remove the cached themes: `rm --cached themes -r`
- add the dot theme submodule: `git submodule add https://github.com/themefisher/dot-hugo-documentation-theme themes/dot`
- start the server: `hugo serve --ignoreCache --disableFastRender --noHTTPCache -w -v`


## License

The gem is available as open source under the terms of the [MIT License](LICENSE).
