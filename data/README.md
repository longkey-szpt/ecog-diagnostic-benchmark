# Data: BCI Competition IV, Dataset 4

The benchmark uses BCI Competition IV, Dataset 4 (Miller & Schalk, 2008):
ECoG and synchronized data-glove recordings of three subjects performing
individual finger flexions. The data are public research recordings distributed
under the competition's terms.

## Download

Register (free) at <http://www.bbci.de/competition/iv/> and download
**Data set 4**, which contains six files per subject:

```
sub{n}_comp.mat        # train_data (ECoG), train_dg (glove), test_data (ECoG)
sub{n}_testlabels.mat  # test_dg (held-out glove labels)
```

Each subject's raw ECoG is 1000 Hz with 62 / 48 / 64 channels (sub1 / sub2 /
sub3); the glove is recorded at 25 Hz and zero-order-held to 1000 Hz in the
release.

## Placement

Each method reads the data from its own directory (path configurable in that
method's `config.py` or notebook):

- `wiener/code/data/` and `switching_lm/code/data/`: `sub{n}_comp.mat` +
  `sub{n}_testlabels.mat`
- `fingerflex/notebooks/data/pure_data/`: the same files

The raw `.mat` files are not distributed with this repository.

## Ethical note

The official dataset descriptor reports that each subject gave informed consent
and that the study was approved by the Harborview Hospital internal review
board. The recordings are reused here under that public release.
