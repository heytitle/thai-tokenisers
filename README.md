# Thai Word Tokenizers

[![](https://img.shields.io/docker/pulls/pythainlp/word-tokenizers.svg)](https://hub.docker.com/r/pythainlp/word-tokenizers/tags)![Publish Docker](https://github.com/PyThaiNLP/docker-thai-tokenizers/workflows/Publish%20Docker/badge.svg)

This repository is a collection of almost all Thai tokenisers that are publicly available. Having this collection allows us to try each algorithm as ease via Docker.

Technically, each project (called  `vendor`) has its own Docker image with a `entry` script and auxiliary scripts.
These scripts bring a unified interface, allowing us to run those algorithms in the same way.

## Vendors 
| Vendor | Alias | Available Methods | Container Profile |
|---|---|---| --- |
| [PyThaiNLP][pythainlp] | pythainlp | newmm, longest  | ![](https://images.microbadger.com/badges/image/pythainlp/word-tokenizers:pythainlp.svg)|
| [DeepCut][deepcut] | deepcut |  deepcut  | ![](https://images.microbadger.com/badges/image/pythainlp/word-tokenizers:deepcut.svg)|
| [CutKum][cutkum]  |  cutkum  | cutkum | ![](https://images.microbadger.com/badges/image/pythainlp/word-tokenizers:cutkum.svg)|
| [Sertis][sertis] | sertis | sertis | ![](https://images.microbadger.com/badges/image/pythainlp/word-tokenizers:sertis.svg) |
| [Thai Language Toolkit][tltk]  |  tltk | mm, ngram, colloc | ![](https://images.microbadger.com/badges/image/pythainlp/word-tokenizers:tltk.svg)|
| [Smart Word Analysis for Thai (SWATH)][swath] | swath | max, long |![](https://images.microbadger.com/badges/image/pythainlp/word-tokenizers:swath.svg) |
| [Chrome's v8Breakiterator][chromev8] | chrome | v8breakiterator |![](https://images.microbadger.com/badges/image/pythainlp/word-tokenizers:chrome.svg) |

Please see [Usages](#usages) for more details.

## Setup
- Pull necessary Docker images. Please check [Docker Hub][dockerhub] for the avaliable images.
  ```
  $ docker pull pythainlp/word-tokenizers:<vendor-alias>
  ```
## Usages
1. Put text files that you want to tokenise into `./data`.
2. Run the following command ...
  ```
  $ ./scripts/tokenise.sh <vendor-alias>-<method> <**filename**>
  ```
  Please check [Vendors section](#vendors) for vendors and methods included here.

### Example
Let's say you want to tokenise text in `./data/example.text` using PyThaiNLP's `newmm` algorithm. You can use the following command:
```
$ cat ./data/example.text
อันนี้คือตัวอย่าง

$ ./scripts/tokenise.sh pythainlp:newmm example.text
# Please be aware that you don't need to have ./data in front of the filename.
# Command Output
Tokenising example.text using vendor=pythainlp and method=newmm
CMD: docker run -v /Users/heytitle/projects/tokenisers-for-thai/data:/data  thai-tokeniser:pythainlp newmm example.text
100%|██████████| 1/1 [00:00<00:00, 151.70it/s]
Tokenising /data/example.text with newmm
Tokenised text is written to /data/example_tokenised-pythainlp-newmm.text

$ cat ./data/example_tokenised-pythainlp-newmm.text
อันนี้|คือ|ตัวอย่าง
```

## Development
### Architecture
TBD.

### Build a vendor's new Docker image
```
$ ./scripts/build <vendor>
```

### Push a new Docker image to Docker Hub
```
$ ./scripts/push <vendor>
```

## Acknowledgements
- This repository was initially done by [Pattarawat Chormai][pat], whiling interning at [Dr. Attapol Thamrongrattanarit's NLP Lab][ate], Chulalongkorn University, Bangkok, Thailand.

[pythainlp]: https://github.com/PyThaiNLP/pythainlp
[deepcut]: https://github.com/rkcosmos/deepcut
[cutkum]: https://github.com/pucktada/cutkum
[tltk]: https://pypi.python.org/pypi/tltk/
[swath]: https://github.com/tlwg/swath
[dockerhub]: https://hub.docker.com/r/pythainlp/word-tokenizers/tags
[ate]: https://attapol.github.io/lab.html
[sertis]: https://github.com/sertiscorp/thai-word-segmentation
[pat]: http://pat.chormai.org
[chromev8]: https://chromium.googlesource.com/external/v8-i18n/+/3bd86474e6728097a22381ce46f1efa5b0a3c7d5/src/break-iterator.cc
