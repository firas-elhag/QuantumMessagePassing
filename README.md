# Quantum Message Passing for Traffic Forecasting

This repository accompanies our work on quantum message passing for traffic
forecasting. The paper is currently under submission to a journal; the code
will be released here after acceptance. For now, the repository provides the
data used in the experiments.

## Data

Both files are from the METR-LA benchmark, used unchanged as released with
DCRNN (Li et al., 2018; <https://github.com/liyaguang/DCRNN>).

| File | Contents |
| --- | --- |
| `tgcn_original/data/metr-la.h5` | Speed readings from 207 loop-detector sensors in Los Angeles, `[timesteps, 207 sensors]`, in mph |
| `tgcn_original/data/adj_mx.pkl` | The sensor graph, as Gaussian-kernel road-distance weights |

## How the experiments use it

- **Subnetwork.** A 50-node subnetwork grown greedily from sensor 0 by
  cumulative symmetrized edge weight. The selection is deterministic (no
  random choice at any step), so the same 50 sensors are obtained every time.
- **Splits.** Contiguous in time, 70/10/20 for training, validation and test,
  applied before windowing so no window crosses a split boundary.
- **Normalization.** Z-score statistics are computed from the raw training
  split only (σ = 19.4237 mph for this subnetwork).
- **Task.** 12 input steps (60 minutes), evaluated at the 15-minute horizon.

## Attribution

If you use this data, please cite the original release:

```bibtex
@inproceedings{li2018diffusion,
  title     = {Diffusion Convolutional Recurrent Neural Network: Data-Driven Traffic Forecasting},
  author    = {Li, Yaguang and Yu, Rose and Shahabi, Cyrus and Liu, Yan},
  booktitle = {International Conference on Learning Representations (ICLR)},
  year      = {2018}
}
```
