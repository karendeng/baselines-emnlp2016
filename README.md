Phrase-based Machine Translation is State-of-the-Art for Automatic Grammatical Error Correction
===============================================================================================

This repository contains baseline models, training scripts, and
instructions on how to reproduce our results for our state-of-art grammar
correction system from M. Junczys-Dowmunt, R. Grundkiewicz: [_Phrase-based
Machine Translation is State-of-the-Art for Automatic Grammatical Error
Correction_](http://www.aclweb.org/anthology/D/D16/D16-1161.pdf), EMNLP 2016.


Citation
--------

    @InProceedings{junczysdowmunt-grundkiewicz:2016:EMNLP2016,
      author    = {Junczys-Dowmunt, Marcin  and  Grundkiewicz, Roman},
      title     = {Phrase-based Machine Translation is State-of-the-Art for
                   Automatic Grammatical Error Correction},
      booktitle = {Proceedings of the 2016 Conference on Empirical Methods in
                   Natural Language Processing},
      month     = {November},
      year      = {2016},
      address   = {Austin, Texas},
      publisher = {Association for Computational Linguistics},
      pages     = {1546--1556},
      url       = {https://aclweb.org/anthology/D16-1161}
    }


Outputs
-------

Outputs generated by our models for the CoNLL-2014 test set are available in
the folder `outputs`. These correspond to Table 4 of our paper. See the README
in that folder for more information.


Baseline models
---------------

You can download and run [our baseline
models](http://odkrywka.wmi.amu.edu.pl/static/data/baselines-emnlp2016/models.tgz)
(558M).

    models/
    ├── data
    │   ├── lm.cor.kenlm
    │   ├── osm.kenlm
    │   └── phrase-table.0-0.gz
    ├── moses.dense-cclm.mert.avg.ini
    ├── moses.dense.mert.avg.ini
    ├── moses.sparse-cclm.mert.avg.ini
    ├── moses.sparse.mert.avg.ini
    └── sparse
        ├── moses.cc.sparse
        └── moses.wiki.sparse

The four configuration `*.ini` files corresponds to the last four systems
described in Table 4.

To use the models you have to install [Moses
decoder](https://github.com/moses-smt/mosesdecoder) (branch `master`) It has to
be compiled with support for 9-gram kenLM language models, e.g.:

    /usr/bin/bjam -j16 --max-kenlm-order=9

The language model data are available in separate packages:

* [Wikipedia language model](http://odkrywka.wmi.amu.edu.pl/static/data/baselines-emnlp2016/wikilm.tgz) (22G)
* [Common Crawl language model](http://odkrywka.wmi.amu.edu.pl/static/data/baselines-emnlp2016/cclm.tgz) (26G)

    wikilm/
    ├── wiki.blm
    ├── wiki.classes.gz
    └── wiki.wclm.kenlm
    cclm/
    ├── cc.classes.gz
    ├── cc.kenlm
    └── cc.wclm.kenlm

Adjust absolute paths in `moses.*.ini` files. You can do this by replacing
`/path/to/` with the path to the directory where you downloaded models and
language models. Finally, run _moses_, e.g.:

    /path/to/mosesdecoder/bin/moses -f moses.dense.mert.avg.ini < input.txt

The input file should contain one sentence per line and each sentence has to
follow the Moses tokenization.


Training models
---------------

Training is described in the README in the folder `train`.
