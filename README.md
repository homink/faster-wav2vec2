# Faster Wav2Vec2 Inference with CTranslate2 
**faster-wav2vec2** is a reimplementation of Facebook AI's Wav2Vec2 model using [CTranslate2](https://github.com/OpenNMT/CTranslate2), which is a fast inference engine for Transformer models.

[Wav2Vec2EncoderLayerStableLayerNorm](https://github.com/huggingface/transformers/blob/9093b19b13f642ed63e0fa49f4091fc0283a84e3/src/transformers/models/wav2vec2/modeling_wav2vec2.py#L703) in the Wav2Vec2 model is a typical Transformer Encoder layer.
24 x Wav2Vec2EncoderLayerStableLayerNorm modules takes about 73% portion of the inference computation in [Wav2Vec2ForCTC](https://github.com/huggingface/transformers/blob/9093b19b13f642ed63e0fa49f4091fc0283a84e3/src/transformers/models/wav2vec2/modeling_wav2vec2.py#L1859).

[faster-whisper](https://github.com/guillaumekln/faster-whisper) inspired this work and the current implementation in [CTranslate2](https://github.com/OpenNMT/CTranslate2) [PR](https://github.com/OpenNMT/CTranslate2/pull/1520/files). You can check the development [repository](https://github.com/homink/CTranslate2).

An [example](https://github.com/homink/CTranslate2/blob/437086983733dec9d58f32674cec85d06bb535b3/python/tests/test_transformers.py#L948) is available for your experiment.

We have in-house fine-tuned Japanese Wav2Vec2 model and observed GPU memory usage from 3060MB to 1897MB and xRT from 0.027 to 0.016 with [CTranslate2](https://github.com/OpenNMT/CTranslate2) 'int8' quantization.

## Update 2024/09/09 
All model inference processing moved from Pytorch to CTranslate2 (https://github.com/OpenNMT/CTranslate2/pull/1758) and now available at [CTranslate2 4.41.0](https://github.com/OpenNMT/CTranslate2/releases/tag/v4.4.0), showing the speend & memory gain.
