# SZU Python Project 1: NumPy 复现 OpenCLIP ViT-B/32 图像编码器

深圳大学《Python 程序设计》Project 1 的完整实现与实验报告。

## 项目内容

在**不使用 PyTorch / OpenCLIP / GPU** 的前提下，仅用 NumPy 从零实现
OpenCLIP ViT-B-32 图像塔（image encoder）的前向计算，全部 6 组 TODO
（TODO-01 ~ TODO-06）均已完成，并与课程提供的独立 FP32 参考实现逐阶段对齐：

| 阶段 | max_abs 误差 | 结果 |
| --- | --- | --- |
| preprocess / patches | 0 | PASS |
| tokens / block0 / last_tokens | ≤ 4.8e-05 | PASS |
| output / batch | ≤ 5.5e-07 | PASS |

## 目录结构

```
├── project1-numpy-student/   # 项目代码（TODO 实现在 image_encoder.py）
│   ├── image_encoder.py      # 核心实现：patchify / MHA / TransformerBlock / 输出头
│   ├── helpers.py            # 课程提供的 LayerNorm、精确 GELU 等
│   ├── check.py              # 分阶段数值校验
│   ├── run.py                # 批量推理入口
│   └── ...
└── report/                   # 实验报告（LaTeX，XeLaTeX 编译）
    ├── main.tex
    └── figs/vit_overview.png
```

## 如何运行

由于课程权重文件（326 MB）与参考数据不入库，请先从课程附件
`project1-numpy-student` 中把以下内容复制回来：

- `weights/image_encoder.npz` → `project1-numpy-student/weights/`
- `assets/reference_outputs.npz` → `project1-numpy-student/assets/`

然后：

```bash
python -m pip install -r project1-numpy-student/requirements.txt
cd project1-numpy-student
python check.py --stage all
python run.py --output output_tokens.npz
```

## 报告编译

`report/` 使用深圳大学实验报告 LaTeX 模板，请用 **XeLaTeX** 编译
（推荐 Overleaf，中文需 Noto Serif CJK SC 字体）。
