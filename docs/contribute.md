# How to contribute to this document? 

This website is hosted on Github pages and created using [`mkdocs`][mkdocs] and
is hosted on Github via Github Actions. Any commit done on the `main` branch
will trigger the rendering of the webpage. To make changes to this documents, is
important to understan the structure of `mkdocs`. 

## Documentation stucture

The main configuration file for `mkdocs` is `mkdocs.yml` at the root of the repo
folder. All details related to general configuration, such as the navigation
tree (`nav`) or the configuration of new plugins. To create a new section, you
just need to create a markdown document (the extension is `.md`) and put it in
the right category. For instance, we can create a new section `new_doc` under
_General Advice_ by changing our config file:  

``` yaml title="mkdocs.yml"
nav:
  - Home: index.md
  - General Advice: 
    - 'new_doc.md'
```

!!! warning "YAML is tricky"
    Remember YAML documents are indented, so keep consistency between each of the
    levels of the document. Not keeping this consistency can break the correct
    flow of the pages.

Not every change in the documents involve modifying the `mkdocs.yml`. If you
only want to change an _existing_ section, you can just easily just change the
document in the `docs/` folder. You can follow the [Markdown documentation][mddocs] 
to modify the documents. Additionaly, you can check out some of the additional
Python-flavored Markdown plugins from the Material theme [docs][material].

## Local rendering

Github actions are limited. Despite using a small instance and a lightweight
configuration, we only have a limited number of runs available. Thus, to avoid
running out of computing hours, you can render the document locally and see live
changes on your own browser. You will need `python>=3.8` and _hopefully_ a
virtual environment. 

!!! note 
    If you are new to Python. You can try the Miniconda distribution. Is a
    simple way to get a fast running Python environment without much
    configuration. Check out the latest version [here][conda] and use it to
    create a virtual environment (some tips [here][condaenv]). For more advance
    users, there is also a `pyenv` alternative.

Once you have your prefered Python version you can just:

=== "conda"

    ``` bash
    conda env create --file environment.yml --force
    conda activate mkdocs_echolab

    ```

=== "pyenv"

    ``` bash
    pyenv virtualenv 3.8 mkdocs_echolab
    pyenv local mkdocs_echolab
    pip install -r requirements.txt

    ```

Now, make sure you are in the root of the repo folder and render the document in
your `localhost` by using: `mkdocs serve`. Notice that any change you make to
this documents will be automatically made on the web browser.

## Password protected content 🔒

This webpage is open to the public. Nonetheless, we can password-protect a page,
or a complete section using the many plugins in `mkdocs`. To add a
password-protected document, you just need to change the header of the Markdown
file you want to change. Python Markdown allows YAML header configurations to
each `md` file, thus you need to change the key in `password`. For example: 

``` yaml 
---
author: topcat
date: %today
password: this_is_a_safe_password
---
# A password protected document

```

## Contribution Etiquette

Before submitting any change, we go by the mantra: "never commit to the main
branch". Sometimes 💩 happens, and that why [Oh Shit Git][git] exists, but in
principle you do not commit to the `main` branch. When working in this document
the rules of engagement are defined by branching and PR submission. To do this,
simply create a new branch: `git checkout <name of new branch>` and make all
changes there. After pushing all changes to Github, you can create a Pull
Request in the repository. 

Once a PR is discussed and approved by other member of the lab, you can accept
the change and merge any changes into the document.

!!! warning 
    Be careful with merge conflicts. Is possible that some merge conflicts might
    arise if there are changes in conflicting lines. You can always brute force
    the merge by using the `--force` flag, or just by forcing it on the PR. This
    might be the right call 95% of the times, be sure of not be the 5%. 

[condaenv]: https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html
[conda]: https://docs.conda.io/en/latest/miniconda.html
[mkdocs]: https://www.mkdocs.org/
[mddocs]: https://www.markdownguide.org/cheat-sheet/
[material]: https://squidfunk.github.io/mkdocs-material/setup/extensions/python-markdown/
[git]: https://ohshitgit.com/


