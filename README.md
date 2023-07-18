# Baichuan13B.cpp /百川13B的llama-cpp实现


## Description

This repo is cloned from llama.cpp. I make the following change(s):

- replace the RoPE position encoding in llama with the Alibi position encoding.
  
The main goal of `Baichuan13B.cpp` is to run the Baichuan13B model using 4-bit integer quantization on consumer device without GPU.

- Plain C/C++ implementation without dependencies
- Mixed F16 / F32 precision
- 4-bit, 5-bit and 8-bit integer quantization support


**Supported platforms:**

- [X] Mac OS (maybe)
- [X] Linux (yes)
- [X] Windows (via CMake)


**Supported models:**

- [X] Baichuan13B 

---

## Usage

### Prerequisite
- intall gcc, g++ 
- install cmake
  
### Get the Code

```bash
git clone https://github.com/ouwei2013/baichuan13b.cpp.git
cd baichuan13b.cpp
```

### Get the model:
- git clone https://huggingface.co/baichuan-inc/Baichuan-13B-Chat.git
- move the entire repo into the 'models' folder of baichuan13b.cpp

### Build

- Using `CMake`:

    ```bash
    mkdir build
    cd build
    cmake ..
    cmake --build . --config Release
    ```

### Prepare Data & Run

```bash
# install Python dependencies

python3 -m pip install -r requirements.txt

# convert the model to ggml FP16 format
# if you are in the build folder
python3 ../convert.py ../models/Baichuan-13B-Chat/

# quantize the model to 4-bits (using q4_0 method)
./bin/quantize ./models/Baichuan-13B-Chat/ggml-model-f16.bin ./models/Baichuan-13B-Chat/ggml-model-q4_0.bin q4_0

# ok let's run the model in its interactive model
./bin/main -m ../../models/Baichuan-13B-Chat/ggml-model-q4_0.bin -p "User:" -i -r 'User:' -c 1024

```

### Memory/Disk Requirements

| Model | Original size | Quantized size (4-bit) |
|------:|--------------:|-----------------------:|
| BC 13B|         27 GB |                 10.2 GB|


### Ackledgement
- A inf positive number of thanks to the Baichuan team
- A inf positive number of thansk to ggerganov for his amazing llama.cpp and ggml 
- This repo is adapted from llama.cpp by replacing RoPE embedding with Alibi position mask. 



**TODO List**

- [ ] Append the 'user_token_id' and 'assistant_token_id' from the original model to the begining of user/ai inputs. 
- [ ] Python binding
- [ ] Web demo 


### About me 
- PhD in ML,long years of engineering and research experience in NLP and general ML. 
- I am also in the market for a job related to NLP/ML.
- If you are interested, please contact via:studyouwei@gmail.com