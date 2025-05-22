### cutter/quantizor for gguf

#### install it via pip/pip3
```
pip install gguf-cutter
```
#### download the cutter by (if no py command; use python/python3 instead)
```
py -m gguf_cutter
```
### how to use it
tag: q2_k, q3_k_s, q3_k_m, q3_k_l, q4_k_s, q4_k_m, q5_k_s, q5_k_m, q6_k, q5_0, q5_1, q4_0, q4_1, q8_0
```
.\quantizor.exe [input_path] [output_path] [tag]
```
#### example:
if you want to cut a `f16` gguf into `q4_k_m`, you should execute the `command` above in that way (put your f16 gguf file in the current directory with `quantizor.exe` together)
```
.\quantizor.exe your-gguf-f16.gguf output-gguf-q4_k_m.gguf q4_k_m
```
then, after completing the process, the quantized `q_4_k_m` will be saved in the current directory

#
### additional chapter: make your own executable quantizor/cutter
#### compile the .exe file for your customized machine if the .exe above doesn't work
git clone llama.cpp:
```
git clone https://github.com/ggml-org/llama.cpp
```

apply the custom patch:
```
cd llama.cpp
git checkout tags/b4387
git apply ..\quantizor.patch
```

compile the llama-quantize for your machine:
```
mkdir build
cd build
cmake ..
cmake --build . --config Debug -j10 --target llama-quantize
```

quantize your file:
```
cd bin
.\llama-quantize.exe your-gguf-f16.gguf output-gguf-q4_k_m.gguf q4_k_m
```
