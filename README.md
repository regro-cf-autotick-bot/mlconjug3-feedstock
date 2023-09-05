About mlconjug3-feedstock
=========================

Feedstock license: [BSD-3-Clause](https://github.com/conda-forge/mlconjug3-feedstock/blob/main/LICENSE.txt)

Home: https://github.com/SekouDiaoNlp/mlconjug3

Package license: MIT

Summary: A Python library to conjugate French, English, Spanish, Italian, Portuguese and Romanian verbs using Machine Learning techniques.

Development: https://github.com/SekouDiaoNlp/mlconjug3

Documentation: https://mlconjug3.readthedocs.io/en/latest/

A Command Line application and Python library to conjugate verbs in French, English, Spanish, Italian, Portuguese and Romanian (more soon) using Machine Learning techniques.

Conjugate any verb in one of the supported languages, even completely new or made-up verbs, with the help of a pre-trained Machine Learning model.
The pre-trained models are composed of a binary feature extractor, a feature selector using Linear Support Vector Classification, and a classifier using Stochastic Gradient Descent.
Easily modify and retrain the models using any compatible classifiers from scikit-learn.
Uses Verbiste as the training data for the French model, and unsupervised learning techniques to generate the data for the English, Spanish, Italian, Portuguese and Romanian models.


Free software: MIT license

Documentation: https://mlconjug3.readthedocs.io.

SUPPORTED LANGUAGES:

-   French
-   English
-   Spanish
-   Italian
-   Portuguese
-   Romanian

FEATURES:

-   Command Line Interface tool.
-   Easy to use and intuitive API.
-   Includes pre-trained models with 99% + accuracy in predicting conjugation class of unknown verbs.
-   Easily train new models or add new languages.
-   Uses caching and multiprocessing for maximum performance.
-   Easily integrate mlconjug3 in your own projects.
-   Extensive documentation.
-   Powerful machine learning algorithms for accurate verb conjugation predictions.
-   Support for multiple languages including English, Spanish, French, and German.
-   Customizable settings to fine-tune performance and adapt to different use cases.
-   Robust error handling and troubleshooting capabilities.
-   Regular updates and improvements to ensure optimal performance.
-   Community support and contributions to continuously expand the library’s capabilities.
-   Integration with popular libraries such as scikit-learn and numpy for machine learning tasks.


Usage
=====

> **note**
>
> The default language is French.
> :   When called without specifying a language, the library will try to
>     conjugate the verb in French.
>
To use MLConjug3 from the command line:

    $ mlconjug3 manger

    $ mlconjug3 bring -l en

    $ mlconjug3 gallofar --language es

    $ mlconjug3 -o, --output (Path of the filename for storing the conjugation tables.)

    $ mlconjug3 -s, --subject (The subject format type for the conjugated forms). The
                       values can be 'abbrev' or 'pronoun'. The default value
                       is 'abbrev'.

    $ mlconjug3 -h Show the help menu


Current build status
====================


<table><tr><td>All platforms:</td>
    <td>
      <a href="https://dev.azure.com/conda-forge/feedstock-builds/_build/latest?definitionId=12459&branchName=main">
        <img src="https://dev.azure.com/conda-forge/feedstock-builds/_apis/build/status/mlconjug3-feedstock?branchName=main">
      </a>
    </td>
  </tr>
</table>

Current release info
====================

| Name | Downloads | Version | Platforms |
| --- | --- | --- | --- |
| [![Conda Recipe](https://img.shields.io/badge/recipe-mlconjug3-green.svg)](https://anaconda.org/conda-forge/mlconjug3) | [![Conda Downloads](https://img.shields.io/conda/dn/conda-forge/mlconjug3.svg)](https://anaconda.org/conda-forge/mlconjug3) | [![Conda Version](https://img.shields.io/conda/vn/conda-forge/mlconjug3.svg)](https://anaconda.org/conda-forge/mlconjug3) | [![Conda Platforms](https://img.shields.io/conda/pn/conda-forge/mlconjug3.svg)](https://anaconda.org/conda-forge/mlconjug3) |

Installing mlconjug3
====================

Installing `mlconjug3` from the `conda-forge` channel can be achieved by adding `conda-forge` to your channels with:

```
conda config --add channels conda-forge
conda config --set channel_priority strict
```

Once the `conda-forge` channel has been enabled, `mlconjug3` can be installed with `conda`:

```
conda install mlconjug3
```

or with `mamba`:

```
mamba install mlconjug3
```

It is possible to list all of the versions of `mlconjug3` available on your platform with `conda`:

```
conda search mlconjug3 --channel conda-forge
```

or with `mamba`:

```
mamba search mlconjug3 --channel conda-forge
```

Alternatively, `mamba repoquery` may provide more information:

```
# Search all versions available on your platform:
mamba repoquery search mlconjug3 --channel conda-forge

# List packages depending on `mlconjug3`:
mamba repoquery whoneeds mlconjug3 --channel conda-forge

# List dependencies of `mlconjug3`:
mamba repoquery depends mlconjug3 --channel conda-forge
```


About conda-forge
=================

[![Powered by
NumFOCUS](https://img.shields.io/badge/powered%20by-NumFOCUS-orange.svg?style=flat&colorA=E1523D&colorB=007D8A)](https://numfocus.org)

conda-forge is a community-led conda channel of installable packages.
In order to provide high-quality builds, the process has been automated into the
conda-forge GitHub organization. The conda-forge organization contains one repository
for each of the installable packages. Such a repository is known as a *feedstock*.

A feedstock is made up of a conda recipe (the instructions on what and how to build
the package) and the necessary configurations for automatic building using freely
available continuous integration services. Thanks to the awesome service provided by
[Azure](https://azure.microsoft.com/en-us/services/devops/), [GitHub](https://github.com/),
[CircleCI](https://circleci.com/), [AppVeyor](https://www.appveyor.com/),
[Drone](https://cloud.drone.io/welcome), and [TravisCI](https://travis-ci.com/)
it is possible to build and upload installable packages to the
[conda-forge](https://anaconda.org/conda-forge) [Anaconda-Cloud](https://anaconda.org/)
channel for Linux, Windows and OSX respectively.

To manage the continuous integration and simplify feedstock maintenance
[conda-smithy](https://github.com/conda-forge/conda-smithy) has been developed.
Using the ``conda-forge.yml`` within this repository, it is possible to re-render all of
this feedstock's supporting files (e.g. the CI configuration files) with ``conda smithy rerender``.

For more information please check the [conda-forge documentation](https://conda-forge.org/docs/).

Terminology
===========

**feedstock** - the conda recipe (raw material), supporting scripts and CI configuration.

**conda-smithy** - the tool which helps orchestrate the feedstock.
                   Its primary use is in the construction of the CI ``.yml`` files
                   and simplify the management of *many* feedstocks.

**conda-forge** - the place where the feedstock and smithy live and work to
                  produce the finished article (built conda distributions)


Updating mlconjug3-feedstock
============================

If you would like to improve the mlconjug3 recipe or build a new
package version, please fork this repository and submit a PR. Upon submission,
your changes will be run on the appropriate platforms to give the reviewer an
opportunity to confirm that the changes result in a successful build. Once
merged, the recipe will be re-built and uploaded automatically to the
`conda-forge` channel, whereupon the built conda packages will be available for
everybody to install and use from the `conda-forge` channel.
Note that all branches in the conda-forge/mlconjug3-feedstock are
immediately built and any created packages are uploaded, so PRs should be based
on branches in forks and branches in the main repository should only be used to
build distinct package versions.

In order to produce a uniquely identifiable distribution:
 * If the version of a package **is not** being increased, please add or increase
   the [``build/number``](https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html#build-number-and-string).
 * If the version of a package **is** being increased, please remember to return
   the [``build/number``](https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html#build-number-and-string)
   back to 0.

Feedstock Maintainers
=====================

* [@SekouDiaoNlp](https://github.com/SekouDiaoNlp/)

