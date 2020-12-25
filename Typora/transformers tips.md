<center><h1>Transformers Tips</h1></center>

1. tokenizer的encode和decode正好相反，encode可以通过参数add_special_tokens设置是否引入特殊的token进行编码，decode可以通过skip_special_tokens设置是否跳过特殊token，而tokenizer则根据我们的分词模型进行分词比如subword。通常用tokenizer.tokenize(tokenizer.decode(tokenizer.encode(seq)))来使分词序列与编码后的序列保持一致。

2. transformers中关于AdamW如何配合学习率线性warmup和梯度裁剪使用可参考[Adamw](https://huggingface.co/transformers/migration.html)结尾处，AdamW的correct\_bias参数用于决定是否在指数加权移动平均的初期进行偏置矫正。

3. transformers的tokenizer的使用可以参考[preprocessing data](https://huggingface.co/transformers/preprocessing.html)

   ```python
   from transformers import BertTokenizer
   
   tk = BertTokenizer.from_pretrained('model name or path', model_max_length=10)
   # 如果传入的是模型名字则会下载模型到本地，可以用cahce_dir指定模型下载后的本地保存路径
   tk = BertTokenizer.from_pretrained('model name or path', model_max_length=10, cache_dir='./models')
   # model_max_length指定序列最长长度，编码时可用truncation参数决定是否对超长序列进行截断
   tk.encode(seq, truncation=True) 
   # 如果传入一个batch的seq，则直接调用tokenizer返回input_ids, token_type_ids, attention_mask
   tk(batch_seqs, padding=True, truncation=True, return_tensors='np') # return_tensors='np','pt','tf'
   # 也可以对序列对进行编码
   tk(seq1, seq2) # 要mask的位置为0，[CLS]到第一个[SEP](包含)的token_type为0，后面跟着的为1
   # 也可以对一个batch的序列对编码，假设batch_seqs1为first seq列表，batch_seqs2为second seq列表
   tk(batch_seqs1, batch_seqs2)
   ```

   