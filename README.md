# vision inference benchmark

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/shloksatpathy/vision-inference-benchmark/blob/main/vision_inference_benchmark.ipynb)

GOAL: take a vision inference model through PyTorch baseline, ONNX Runtime, TensorRT FP16 and TensorRT INT8, measuring throughput, latency (p50, p95, p99), accuracy and VRAM at each stage.

## status

Under construction. Only the setup is done so far; none of the benchmark stages have been run.

| stage | status |
| --- | --- |
| Environment setup (GPU check, `ultralytics`, `onnx`) | done |
| PyTorch baseline: load YOLOv8n and run a single-image sanity check | done |
| PyTorch baseline: throughput, latency percentiles, accuracy, VRAM | todo |
| ONNX export and ONNX Runtime benchmark | todo |
| TensorRT FP16 | todo |
| TensorRT INT8 (with calibration) | todo |
| Results comparison table | todo |

## setup

- **Model:** YOLOv8n (`yolov8n.pt`, downloaded automatically by `ultralytics`).
- **Dataset:** 5,000 images with Pascal VOC-style XML annotations (`hard_hat_workers*.xml`) in `data/images` and `data/annotations`. `data/` is gitignored, so it has to be added locally or uploaded to Colab.
- **Runtime:** the notebook is written for Google Colab with an NVIDIA GPU. Use the badge above to open it.
- **Sanity-check image:** the single-image check reads `/content/images.jpeg`, so upload any test image to that path in Colab before running the cell.

## environment

Recorded from the last notebook run:

| component | version |
| --- | --- |
| GPU | NVIDIA Tesla T4 (15 GB) |
| Driver / CUDA | 580.82.07 / 13.0 |
| Python | 3.13 |
| `ultralytics` | 8.4.152 |
| `onnx` | 1.22.0 |

## metrics

For each stage the benchmark will record:

- throughput (images/s)
- latency p50 / p95 / p99
- accuracy
- peak VRAM

## files

- `vision_inference_benchmark.ipynb`: the benchmark notebook
- `data/`: images and annotations (not tracked)

## results

The full benchmark stages have not been run yet. The only number so far comes from the single-image sanity check (PyTorch, YOLOv8n, 448x640 input, T4). It is one cold run, not a benchmark:

| preprocess | inference | postprocess |
| --- | --- | --- |
| 107.0 ms | 18.4 ms | 51.4 ms |

The comparison table will go here once the stages are run.
