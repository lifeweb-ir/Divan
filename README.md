# DIVAN – Diverse Valuable NLP Dataset for PERSIAN

## Overview

DIVAN is a comprehensive Persian (Farsi) dataset designed for various Natural Language Processing tasks. It contains over 100 million records from diverse sources including social media posts, comments, news articles, and blog posts. With more than 8 billion tokens, DIVAN provides a rich resource for Persian language processing tasks.

## Dataset Details

| Information | Description |
|:-------------:|:-------------:|
| Dataset Name | DIVAN |
| Language | Persian (Farsi) |
| Domain | Social media, news, blogs |
| Number of Samples | 100 million |
| Number of Tokens | More than 8 billion |
| Dataset License | CC BY-SA 4.0 |
| Sources | X(twitter), News, Telegram channels, Wikipedia, Divar, DigiKala, etc. |
| Tasks | Fill-Mask (MLM), Text Generation, etc. |

## Installation

You can install and load this dataset using Hugging Face's datasets library:

- Install the datasets library
```bash
pip install datasets
```

## Dataset Structure

DIVAN is published as chunked Data Frames with 2 columns representing the text and the aimed platform:

- `text`: The text (posts or articles) in Persian.
- `platform`: The specific platform from which the text is retrieved.

The outputs are saved as 1 million-record parquet files which are accessible in this repository’s folders named after the platforms’ names.

## Usage Example

- Load the dataset
```python
from datasets import load_dataset

dataset = load_dataset("lifeweb-ai/Divan", token='HF_TOKEN')
```

- Load a specific platform
```python
from datasets import load_dataset

platform_title = 'news'
dataset = load_dataset("lifeweb-ai/Divan", data_files='{}/*.parquet'.format(platform_title), token='HF_TOKEN')
```

- Access a sample
```python
dataset['train'][0]
```


## Dataset Creation

After selecting the textually rich platforms the aimed data were retrieved and with the help of applying normalization to the initial corpus, the text got as clean as possible while any unnecessary characters for learning different NLP models or not related to the Persian Language were omitted. 

Every part of the normalization is sequentially explained below:

- finding email addresses and replacing them with “[email]”.
- finding different types of links and replacing all of them as “[httplink]”.
- finding the mentioned usernames and replacing them with “[user]”.
- removing newline signs.     
- removing Persian characters showing vowel sounds as well as the ones that are common with Arabic.
- replacing any Persian character that is not written in its standard font and converting them to one.
- removing cryptocurrency wallet addresses.
- removing different numeric formats like phone numbers, credit card numbers, or dates.
- Remove repeated characters and keep at most 3 sequentially repeated characters.
- calculating the ratio of Persian characters to the whole text and omitting non-Persian documents or ones that are considered Persian with a ratio of less than 80%.
- breaking hashtags in a way that a space will be added after “#” and if there’s any “_” in between, a space will be added before and after them as well.

There’s also another step to further clean the corpus called deduplication through which the total dataset gets assessed for the duplication ratio so that textual contents that are the same or more than 80% similar will get deleted.


## Platform Statistics

| Platform | Documents Count |
|:----------:|:-----------------:|
| X(twitter) | 50,000,000 |
| Telegram Channels | 15,000,000 |
| Telegram Groups | 2,300,000 |
| Blogs | 500,000 |
| News | 12,500,000 |
| Instagram Posts | 5,000,000 |
| Instagram Comments | 3,000,000 |
| Divar | 4,000,000 |
| Digikala | 5,000,000 |
| Eitaa | 2,000,000 |
| Wikipedia | 700,000 |
| **Total** | **100,000,000** |

## Citation

If you use this dataset in your research, please cite it as follows:
#### BibTeX

    @dataset{divan_dataset,
        author = {[LifeWeb AI team]},
        title = {DIVAN: Diverse Valuable NLP Dataset for PERSIAN},
        year = {2024},
        publisher = {Hugging Face},
        url = {https://huggingface.co/datasets/lifeweb-ai/divan}, 
    }

## License

This dataset is licensed under the [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/legalcode.en) license. For more details, please refer to the LICENSE file in this repository.


## Contact

For questions or feedback about this dataset, please contact us via [**HuggingFace**](https://huggingface.co/datasets/lifeweb-ai/Divan) and [**GitHub**](https://github.com/lifeweb-ir/Divan).
