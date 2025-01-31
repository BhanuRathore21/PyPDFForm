# Releasing

A PyPDFForm release starts with the following steps:

* A release [issue](https://github.com/BhanuRathore21/PyPDFForm/issues/646) and [PR](https://github.com/BhanuRathore21/PyPDFForm/pull/647).
* A new [GitHub release](https://github.com/BhanuRathore21/PyPDFForm/releases) with auto-generated changelogs.

Once these steps are done, the CI for deployment will be triggered.

## Deploy process

When the GitHub release is created, it will trigger two different CIs:

* [Deploy](https://github.com/BhanuRathore21/PyPDFForm/actions/workflows/python-publish.yml), which will create the distribution and upload it to [PyPI](https://pypi.org/project/PyPDFForm/).
* [Deploy Docs](https://github.com/BhanuRathore21/PyPDFForm/actions/workflows/deploy-docs.yml), which will tear down and rebuild the [GitHub page](https://BhanuRathore21.github.io/PyPDFForm/) where the doc site is hosted.

## When are releases done?

It depends on the changes that are currently on the master branch but have not deployed yet. Generally speaking:

* Serious bugs are usually released immediately after they are fixed.
* New features can usually wait and are released on a weekly basis.
* Trivial changes are usually bundled with other changes and can wait indefinitely.
