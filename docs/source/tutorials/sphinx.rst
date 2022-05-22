Sphinx Tutorial
===============

Create a Documentation
----------------------

.. code ::

    $ sphinx-quickstart


Prepare Local Repository
------------------------


Github Workflow
+++++++++++++++

Github Workflow can be used to automatically build the documentation using make html every time sources change. 

.. code ::

    name: Sphinx build

    on: push

    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v2
        - name: Build HTML
          uses: ammaraskar/sphinx-action@0.4
        - name: Upload artifacts
          uses: actions/upload-artifact@v1
          with:
            name: html-docs
            path: docs/build/html/
        - name: Deploy
          uses: peaceiris/actions-gh-pages@v3
          if: github.ref == 'refs/heads/main'
          with:
            github_token: ${{ secrets.GITHUB_TOKEN }}
            publish_dir: docs/build/html