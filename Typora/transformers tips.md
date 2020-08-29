<center><h1>Transformers Tips</h1></center>

1. tokenizer的encode和decode正好相反，encode可以通过参数add_special_tokens设置是否引入特殊的token进行编码，decode可以通过skip_special_tokens设置是否跳过特殊token，而tokenizer则根据我们的分词模型进行分词比如subword。通常用tokenizer.tokenize(tokenizer.decode(tokenizer.encode(seq)))来使分词序列与编码后的序列保持一致。
2. transformers中关于AdamW如何配合学习率线性warmup和梯度裁剪使用可参考[Adamw](https://huggingface.co/transformers/migration.html)结尾处，AdamW的correct\_bias参数用于决定是否在指数加权移动平均的初期进行偏置矫正。