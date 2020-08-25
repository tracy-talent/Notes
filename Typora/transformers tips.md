<center><h1>Transformers Tips</h1></center>

1. tokenizer的encode和decode正好相反，encode可以通过参数add_special_tokens设置是否引入特殊的token进行编码，decode可以通过skip_special_tokens设置是否跳过特殊token，而tokenizer则根据我们的分词模型进行分词比如subword。通常用tokenizer.tokenize(tokenizer.decode(tokenizer.encode(seq)))来使分词序列与编码后的序列保持一致。