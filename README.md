About mlconjug3
===============

Home: https://github.com/SekouDiaoNlp/mlconjug3

Package license: MIT

Feedstock license: [BSD-3-Clause](https://github.com/conda-forge/mlconjug3-feedstock/blob/master/LICENSE.txt)

Summary: A Python library to conjugate French, English, Spanish, Italian, Portuguese and Romanian verbs using Machine Learning techniques.

Development: https://github.com/SekouDiaoNlp/mlconjug3

Documentation: https://mlconjug3.readthedocs.io/en/latest/

A Python library to conjugate verbs in French, English, Spanish, Italian, Portuguese and Romanian (more soon) using Machine Learning techniques.

Any verb in one of the supported language can be conjugated, as the module contains a Machine Learning model of how the verbs behave.

Even completely new or made-up verbs can be successfully conjugated in this manner.

The supplied pre-trained models are composed of:

-   a binary feature extractor,
-   a feature selector using Linear Support Vector Classification,
-   a classifier using Stochastic Gradient Descent.

MLConjug3 uses scikit-learn to implement the Machine Learning algorithms.

Users of the library can use any compatible classifiers from scikit-learn to modify and retrain the models.

The training data for the french model is based on Verbiste https://perso.b2b2c.ca/~sarrazip/dev/verbiste.html .

The training data for English, Spanish, Italian, Portuguese and Romanian was generated using unsupervised learning techniques using the French model as a model to query during the training.

WARNING
========

MLCONJUG3 now only supports Python 3.x as Python 2.x has been deprecated in 2020.

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

-   Easy to use API.
-   Includes pre-trained models with 99% + accuracy in predicting conjugation class of unknown verbs.
-   Easily train new models or add new languages.
-   Easily integrate MLConjug in your own projects.
-   Can be used as a command line tool.

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

To use MLConjug3 in a project with the provided pre-trained conjugation
models:

``` {.sourceCode .python}
import mlconjug3

# To use mlconjug3 with the default parameters and a pre-trained conjugation model.
default_conjugator = mlconjug3.Conjugator(language='fr')

# Verify that the model works
test1 = default_conjugator.conjugate("manger").conjug_info['Indicatif']['Passé Simple']['1p']
test2 = default_conjugator.conjugate("partir").conjug_info['Indicatif']['Passé Simple']['1p']
test3 = default_conjugator.conjugate("facebooker").conjug_info['Indicatif']['Passé Simple']['1p']
test4 = default_conjugator.conjugate("astigratir").conjug_info['Indicatif']['Passé Simple']['1p']
test5 = default_conjugator.conjugate("mythoner").conjug_info['Indicatif']['Passé Simple']['1p']
print(test1)
print(test2)
print(test3)
print(test4)
print(test5)

# You can now iterate over all conjugated forms of a verb by using the newly added Verb.iterate() method.
default_conjugator = mlconjug3.Conjugator(language='en')
test_verb = default_conjugator.conjugate("be")
all_conjugated_forms = test_verb.iterate()
print(all_conjugated_forms)
```

To use MLConjug3 in a project and train a new model:

``` {.sourceCode .python}
# Set a language to train the Conjugator on
lang = 'fr'

# Set a ngram range sliding window for the vectorizer
ngrange = (2,7)

# Transforms dataset with CountVectorizer. We pass the function extract_verb_features to the CountVectorizer.
vectorizer = mlconjug3.CountVectorizer(analyzer=partial(mlconjug3.extract_verb_features, lang=lang, ngram_range=ngrange),
                             binary=True)

# Feature reduction
feature_reductor = mlconjug3.SelectFromModel(mlconjug3.LinearSVC(penalty="l1", max_iter=12000, dual=False, verbose=0))

# Prediction Classifier
classifier = mlconjug3.SGDClassifier(loss="log", penalty='elasticnet', l1_ratio=0.15, max_iter=4000, alpha=1e-5, random_state=42, verbose=0)

# Initialize Data Set
dataset = mlconjug3.DataSet(mlconjug3.Verbiste(language=lang).verbs)
dataset.construct_dict_conjug()
dataset.split_data(proportion=0.9)

# Initialize Conjugator
model = mlconjug3.Model(vectorizer, feature_reductor, classifier)
conjugator = mlconjug3.Conjugator(lang, model)

#Training and prediction
conjugator.model.train(dataset.train_input, dataset.train_labels)
predicted = conjugator.model.predict(dataset.test_input)

# Assess the performance of the model's predictions
score = len([a == b for a, b in zip(predicted, dataset.test_labels) if a == b]) / len(predicted)
print('The score of the model is {0}'.format(score))

# Verify that the model works
test1 = conjugator.conjugate("manger").conjug_info['Indicatif']['Passé Simple']['1p']
test2 = conjugator.conjugate("partir").conjug_info['Indicatif']['Passé Simple']['1p']
test3 = conjugator.conjugate("facebooker").conjug_info['Indicatif']['Passé Simple']['1p']
test4 = conjugator.conjugate("astigratir").conjug_info['Indicatif']['Passé Simple']['1p']
test5 = conjugator.conjugate("mythoner").conjug_info['Indicatif']['Passé Simple']['1p']
print(test1)
print(test2)
print(test3)
print(test4)
print(test5)

# Save trained model
with open('path/to/save/data/trained_model-fr.pickle', 'wb') as file:
    pickle.dump(conjugator.model, file)
```



Current build status
====================


<table><tr><td>All platforms:</td>
    <td>
      <a href="https://dev.azure.com/conda-forge/feedstock-builds/_build/latest?definitionId=12459&branchName=master">
        <img src="https://dev.azure.com/conda-forge/feedstock-builds/_apis/build/status/mlconjug3-feedstock?branchName=master">
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

Once the `conda-forge` channel has been enabled, `mlconjug3` can be installed with:

```
conda install mlconjug3
```

It is possible to list all of the versions of `mlconjug3` available on your platform with:

```
conda search mlconjug3 --channel conda-forge
```


About conda-forge
=================

[![Powered by NumFOCUS](https://img.shields.io/badge/powered%20by-NumFOCUS-orange.svg?style=flat&colorA=E1523D&colorB=007D8A)](http://numfocus.org)

conda-forge is a community-led conda channel of installable packages.
In order to provide high-quality builds, the process has been automated into the
conda-forge GitHub organization. The conda-forge organization contains one repository
for each of the installable packages. Such a repository is known as a *feedstock*.

A feedstock is made up of a conda recipe (the instructions on what and how to build
the package) and the necessary configurations for automatic building using freely
available continuous integration services. Thanks to the awesome service provided by
[CircleCI](https://circleci.com/), [AppVeyor](https://www.appveyor.com/)
and [TravisCI](https://travis-ci.com/) it is possible to build and upload installable
packages to the [conda-forge](https://anaconda.org/conda-forge)
[Anaconda-Cloud](https://anaconda.org/) channel for Linux, Windows and OSX respectively.

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

