# min(DALL·E)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kuprel/min-dalle/blob/main/min_dalle.ipynb) &nbsp;
[![Replicate](https://replicate.com/kuprel/min-dalle/badge)](https://replicate.com/kuprel/min-dalle)

This is a minimal implementation of Boris Dayma's [DALL·E Mini](https://github.com/borisdayma/dalle-mini).  It has been stripped to the bare essentials necessary for doing inference, and converted to PyTorch.  To run the torch model, the only third party dependencies are numpy and torch.  Flax is used to convert the weights (which can be saved with `torch.save` once the model is loaded), and wandb is only used to download the models.

It currently takes about 10 seconds to generate an avocado armchair with DALL·E Mega in PyTorch on Colab with a reusable model and high-RAM GPU runtime.

### Setup

Run `sh setup.sh` to install dependencies and download pretrained models.  The models can also be downloaded manually here: 
[VQGan](https://huggingface.co/dalle-mini/vqgan_imagenet_f16_16384), 
[DALL·E Mini](https://wandb.ai/dalle-mini/dalle-mini/artifacts/DalleBart_model/mini-1/v0/files), 
[DALL·E Mega](https://wandb.ai/dalle-mini/dalle-mini/artifacts/DalleBart_model/mega-1-fp16/v14/files)

### Usage

Use the python script `image_from_text.py` to generate images from the command line.  Note: the command line script loads the models and parameters each time.  To load a model once and generate multiple times, initialize either `MinDalleTorch` or `MinDalleFlax`, then call `generate_image` with some text and a seed.  See the colab for an example.

### Examples

```
python image_from_text.py --text='artificial intelligence' --torch
```
![Alien](examples/artificial_intelligence.png)


```
python image_from_text.py --text='a comfy chair that looks like an avocado' --torch --mega --seed=10
```
![Avocado Armchair](examples/avocado_armchair.png)


```
python image_from_text.py --text='court sketch of godzilla on trial' --mega --seed=100
```

![Godzilla Trial](examples/godzilla_trial.png)
