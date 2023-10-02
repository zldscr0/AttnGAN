## README

Paper：https://arxiv.org/pdf/1711.10485.pdf?spm=a2c6h.12873639.article-detail.8.1d38523bRW84ah&file=1711.10485.pdf

Code：

Python2.7：https://github.com/taoxugit/AttnGAN

Python3.6+：https://github.com/davidstap/AttnGAN?spm=a2c6h.12873639.article-detail.11.1d38523bRW84ah（推荐）

### Dependencies

python3.9

```bash
pip install -r ./requirments.txt
```

**Data**

1. Download our preprocessed metadata for [birds](https://drive.google.com/open?id=1O_LtUP9sch09QH3s_EBAgLEctBQ5JBSJ) [coco](https://drive.google.com/open?id=1rSnbIGNDGZeHlsUlLdahj0RJ9oo6lgH9) and save them to `data/`
2. Download the [birds](http://www.vision.caltech.edu/visipedia/CUB-200-2011.html) image data. Extract them to `data/birds/`
3. Download [coco](http://cocodataset.org/#download) dataset and extract the images to `data/coco/`

若链接失效，可通过https://drive.google.com/drive/folders/1cnQHqa8BkVx90-6-UojHnbMB0WhksSRc下载birds数据集

![1](blob:https://github.com/11ab28e5-d03f-408d-91e4-8269bb725207)

##### File Structure



**Training**

`AttnGAN/code`下运行：

- Pre-train DAMSM models:
  - For bird dataset: `python pretrain_DAMSM.py --cfg cfg/DAMSM/bird.yml --gpu 0`
  - For coco dataset: `python pretrain_DAMSM.py --cfg cfg/DAMSM/coco.yml --gpu 1`
- Train AttnGAN models:
  - For bird dataset: `python main.py --cfg cfg/bird_attn2.yml --gpu 2`
  - For coco dataset: `python main.py --cfg cfg/coco_attn2.yml --gpu 3`
- `*.yml` files are example configuration files for training/evaluation our models.

训练过程截图：

![2](https://github.com/zldscr0/AttnGAN/tree/main/images/2.png)

**Pretrained Model**

由于训练时间较长，可以直接下载训练好的模型使用：

- [DAMSM for bird](https://drive.google.com/open?id=1GNUKjVeyWYBJ8hEU-yrfYQpDOkxEyP3V). Download and save it to `DAMSMencoders/`
- [DAMSM for coco](https://drive.google.com/open?id=1zIrXCE9F6yfbEJIbNP5-YrEe2pZcPSGJ). Download and save it to `DAMSMencoders/`
- [AttnGAN for bird](https://drive.google.com/open?id=1lqNG75suOuR_8gjoEPYNp8VyT_ufPPig). Download and save it to `models/`
- [AttnGAN for coco](https://drive.google.com/open?id=1i9Xkg9nU74RAvkcqKE-rJYhjvzKAMnCi). Download and save it to `models/`
- [AttnDCGAN for bird](https://drive.google.com/open?id=19TG0JUoXurxsmZLaJ82Yo6O0UJ6aDBpg). Download and save it to `models/`
  - This is an variant of AttnGAN which applies the propsoed attention mechanisms to DCGAN framework.

**Sampling**

- Run `python main.py --cfg cfg/eval_bird.yml --gpu 1` to generate examples from captions in files listed in "./data/birds/example_filenames.txt". Results are saved to `DAMSMencoders/`.
- Change the `eval_*.yml` files to generate images from other pre-trained models.
- Input your own sentence in "./data/birds/example_captions.txt" if you wannt to generate images from customized sentences.

**Validation**

- To generate images for all captions in the validation dataset, change B_VALIDATION to True in the eval_*.yml. and then run `python main.py --cfg cfg/eval_bird.yml --gpu 1`
- We compute inception score for models trained on birds using [StackGAN-inception-model](https://github.com/hanzhanggit/StackGAN-inception-model).
- We compute inception score for models trained on coco using [improved-gan/inception_score](https://github.com/openai/improved-gan/tree/master/inception_score).

更改`data/birds/example_captions.txt`中待生成图片的描述，运行

```bash
python main.py --cfg cfg/eval_bird.yml --gpu 1
```

生成图片在`AttnGAN/models/bird_AttnGAN2/example_captions`中：

![3](https://github.com/zldscr0/AttnGAN/tree/main/images/3.png)

### Reference

https://developer.aliyun.com/article/1000763

---

Contribution: Code completed by Zhixin Bai.

