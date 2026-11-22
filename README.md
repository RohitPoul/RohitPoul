<p align="center">
  <img src="assets/banner.svg" alt="Rohit Poul: AI/ML, computer vision, bots, open source" width="100%">
</p>

I train segmentation models, build Telegram bots, and write the tooling around both.

## Now

**[BiRefNet anime matting](https://huggingface.co/RohitPoul/BiRefNet-anime-matting)**
Fine-tuning BiRefNet-HR to cut anime characters out cleanly. Started from the ToonOut dataset (1,228 image/mask pairs), trained in three phases: frozen backbone, full fine-tune, edge refinement. bf16 AMP, EMA, `torch.compile`. Currently around 88% full-image BIoU.
<!-- update the BIoU number after the next run finishes -->

**PokeEclipse**
A Pokémon game that lives entirely inside Telegram: stats-based combat, gym battles, trading, a TCG card system. Its CAPTCHA hides Pokémon silhouettes inside ControlNet-generated illusions, so a bot has to see the image the way a person does.

**[Persona 3 Reload portfolio](https://github.com/RohitPoul/Person-3-Reload-Potfolio)**
A portfolio built to look like a JRPG menu.

## Field notes

Things the training runs taught me the hard way.

- **The A100 wasn't the bottleneck, the filesystem was.** Training crawled on the cluster's Lustre NFS. Moving the dataset and HF cache to local NVMe fixed it. Profile the I/O before blaming the model.
- **Audit your own training script.** A line-by-line pass found inverted hard-negative mining, in-place aliasing in a Lovász gradient, and gradients clipped at a threshold of 10 when the pre-clip norm sat near 19.
- **A T4 has no native bf16.** Every A100-tuned setting gets a second look before it runs on Colab. A long BIoU plateau there turned out to be tile-inference coverage bugs and a loss/metric mismatch, not the architecture.

## Stack

```text
train    PyTorch · bf16 AMP · EMA · torch.compile · channels-last
ship     Python CLIs and GUIs · Electron desktop apps
inspect  React + Chart.js dashboards for training logs
bots     Telegram via Telethon
also     C++ · JavaScript · TensorFlow · HTML/CSS
```

## Rig

```text
local    HP OMEN 16 · RTX 5070 · Ryzen 9 8940HX    inference, tooling, GUIs
hpc      AIKosh Airawat · A100 MIG 20GB            long training runs
colab    T4                                        prototypes, demos
```

## Repos

- [Telegram-Sticker-Maker-And-Auto-Uploader](https://github.com/RohitPoul/Telegram-Sticker-Maker-And-Auto-Uploader): sticker maker and auto-uploader for Telegram
- [Background-Remover-Ai](https://github.com/RohitPoul/Background-Remover-Ai): AI background removal
- [Person-3-Reload-Potfolio](https://github.com/RohitPoul/Person-3-Reload-Potfolio): the portfolio above

Weights and datasets live on [Hugging Face](https://huggingface.co/RohitPoul).

## Collaborating

I'm up for open-source work in computer vision and Telegram bots. Open an issue or reach me through [GitHub](https://github.com/RohitPoul) or [Hugging Face](https://huggingface.co/RohitPoul).

> I don't want money, I want to learn and be there, contributing to open source and making something useful for people.
