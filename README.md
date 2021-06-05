# A New Approach to Overgenerating and Scoring Abstractive Summaries
We provide the source code for the paper  **"[A New Approach to Overgenerating and Scoring Abstractive Summaries](https://www.aclweb.org/anthology/2021.naacl-main.110.pdf)"** accepted at NAACL'21. If you find the code useful, please cite the following paper.

    @inproceedings{song2021new, 
        title={A New Approach to Overgenerating and Scoring Abstractive Summaries},
        author={Song, Kaiqiang and Wang, Bingqing and Feng, Zhe and Liu, Fei},
        booktitle={Proceedings of the 2021 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies},
        pages={1392--1404},
        year={2021}
    }

## Dependencies

The code is written in Python (v3.7) and Pytorch (v1.7+). We suggest the following enviorment:

* A Linux machine (Ubuntu) with GPU
* [Python (v3.7+)](https://www.anaconda.com/download/)
* [Pytorch (v1.7+)](https://pytorch.org/)
* [Pyrouge](https://pypi.org/project/pyrouge/)
* [transformers (v2.3.0)](https://github.com/huggingface/transformers)

HINT: Since huggingface transformers is alternating very fast, you may need to modify a lot of stuff if you want to use a new version. Contact me if you get any trouble on it.

To install pyrouge and transformers, run the command below:

```
$ pip install pyrouge transformers==2.3.0
```

## For generating summaries with varying length

Step 1: clone this repo. Download trained [Our model](), move it to the working folder and uncompress it.

```
$ git clone https://github.com/ucfnlp/varying-length-summ.git
$ mv models.zip varying-length-summ
$ cd varying-length-summ
$ unzip models.zip
```

Step 2: Generating summaries with varying length from a raw input file. 
```
$ python run.py --do_test --parallel --input data/input.txt
```

It will generate summaries of varying lengths coupled with its order information.

## For Selecting summaries with best quality binary classifer

Step 1: Follow the previous section about generating summaries with multiple length.

Step 2: Collect test set similar to ``data/gigaword_cls/test500*`` files:
    1) a source input file ``test500_input.txt``
    2) a target output file ``test500_output.txt``
    3) a label for whether the target summary is admissible for the source input. (all 0 if don't have labels)

HINT: one instance per line

Step 3: modify the test settings in ``settings/dataset/gigaword_cls``.

Step 4: Run the code below.
```
$ python run_classifier.py --do_test --parallel
```

It will generate a prediction of admissible probability in ``predict.txt``.

## For Selecting summaries with length reward reranking method
Step 1: Follow the previous section about generating summaries with multiple length.

Step 2: Run the code below.
```
$ python run_rerank.py
```
It will re-rank the summary with length rewards.


## For Data Downloading (500 inputs x 7 lengths)
Please refer to 
