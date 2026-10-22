# Deep Learning — 1-mark MCQ bank

Three units from the class list, written from the lecture decks (CNN, BPTT, LSTM, GRU, Transformers to BERT, Autoencoders).

**How to sit this:** cover the answer pages. Choose the **best** option. Then read the one-line reason. A 1-mark paper rewards the reason, not a memorised definition. If you can say the reason aloud, a reworded question still falls the same way.

There is **no negative marking** assumed. One question, one mark.

Topics that are on the unit list but were not their own deck (transfer learning, recursive nets, deep belief networks, deep Boltzmann machines, GANs, semi-supervised learning) are included at the same depth, and tied to the stacked-autoencoder and BERT ideas you already have.

---

# Unit A — Convolutional neural networks

Architecture, pooling, convolution and its variants, transfer learning, object recognition and computer vision.

### A1
A CNN is used in this course mainly for data that

a) is a time-ordered sequence of variable length  
b) lives on a grid, such as an image, where nearby values belong together  
c) is an unordered bag of words  
d) has one label per sequence and no spatial layout

### A2
Sliding the **same** filter over the whole image gives

a) a separate set of weights at every pixel, like a fully connected layer  
b) shared weights, fewer parameters, and the same local pattern can fire anywhere in the image  
c) a guarantee that the network will not overfit  
d) one output number for the entire image, before any other layer runs

### A3
Match the layer with the job given in class.

a) Convolution reduces dimensions; pooling extracts features; dropout increases capacity  
b) Convolution extracts features; pooling reduces the spatial size; dropout reduces overfitting; the fully connected layer joins every unit to every unit in the next layer  
c) Pooling extracts edges; convolution is only used for classification; dropout is used at test time  
d) The fully connected layer shares one filter across the image; convolution does not share weights

### A4
An image is \(n \times n\), the kernel is \(f \times f\), the stride is \(S\), and the padding is \(P\). The output spatial size is

a) \(n \times f \times S + P\)  
b) \(\dfrac{n + 2P - f}{S} + 1\)  
c) \(n - f - 2P + S\)  
d) \(f \times S + P\)

### A5
A \(5 \times 5\) image, a \(3 \times 3\) kernel, stride 1, no padding. The feature map is

a) \(5 \times 5\)  
b) \(3 \times 3\)  
c) \(2 \times 2\)  
d) \(4 \times 4\)

### A6
Zero-padding is used so that

a) the kernel can see the border pixels and, with the right \(P\), the spatial size can be kept  
b) the number of filters doubles  
c) dropout can be removed  
d) the image becomes grayscale

### A7
Raising the stride from 1 to 2, with the kernel unchanged,

a) increases the number of learned weights in that filter  
b) makes the feature map spatially smaller, because the filter jumps ahead  
c) is the same operation as a sigmoid  
d) converts a CNN into an RNN

### A8
Class kernels are an odd size (\(3 \times 3\), \(5 \times 5\)) so that

a) the output is always \(1 \times 1\)  
b) the kernel has a centre pixel  
c) padding becomes illegal  
d) max pooling is unnecessary

### A9
On an RGB image, **one** filter

a) produces three feature maps, one per colour, which are never combined  
b) has a kernel slice per channel, and those channel responses are **added** into one feature map  
c) ignores two of the three channels  
d) must be \(1 \times 1\), otherwise colour cannot be used

### A10
“Weight sharing” in a CNN means

a) every filter in the layer is forced to be a copy of the first filter  
b) the weights of a filter are reused at every spatial position  
c) the fully connected layers share their matrix with the first convolution  
d) bias terms are set to zero

### A11
Max pooling with a \(2 \times 2\) window and stride 2

a) learns a \(2 \times 2\) kernel by gradient descent  
b) replaces each window by its largest value, so a small shift of a strong response inside the window need not change the pooled output  
c) always increases the number of channels  
d) is applied only at test time

### A12
Global average pooling

a) averages each entire feature map down to one number  
b) is another name for a \(3 \times 3\) convolution  
c) removes the need for any convolution  
d) is the same as dropout with \(p = 0.5\)

### A13
Which description matches **LeNet** as given in class?

a) RGB \(227 \times 227\), about 60 million parameters, ReLU, max pooling, 1000 classes  
b) Grayscale \(32 \times 32\) digits, about 60,000 parameters, tanh in the middle, softmax at the end, average pooling, 10 classes  
c) \(224 \times 224\) input, only \(3 \times 3\) kernels, about 138 million parameters  
d) Skip connections and about 11 million parameters

### A14
Which description matches **AlexNet** as given in class?

a) Average pooling, tanh, about 60,000 parameters, 10 digit classes  
b) ReLU in the hidden layers, softmax at the end, max pooling, dropout, local response normalisation, RGB \(227 \times 227\), 1000 classes, about 60 million parameters  
c) Only identity skip connections, no pooling  
d) A single fully connected layer on raw pixels

### A15
In the AlexNet layout from class, dropout sits

a) in place of every convolution  
b) between the last pooling layer and the first fully connected layer, to generalise better  
c) only on the input pixels, before any filter  
d) after the final softmax, during testing

### A16
Dropout, as used in this unit,

a) drops units at **training** time, often about 20% to 50% of them, so co-adapted detectors cannot be relied on  
b) drops units only at test time, to average several models  
c) is a pooling method  
d) increases the parameter count on purpose

### A17
Local response normalisation in this lecture is

a) a trainable convolution  
b) a non-trainable competition: a locally strong response suppresses its surroundings (lateral inhibition), which matters because ReLU, \(\max(0, x)\), does not bound large positive values  
c) another name for batch normalisation  
d) applied to the loss, not to activations

### A18
Inter-channel LRN and intra-channel LRN differ as follows.

a) Inter-channel competes across nearby **feature maps** at one pixel; intra-channel competes across a **spatial neighbourhood** of the same map  
b) Both are learned \(3 \times 3\) filters  
c) Inter-channel is max pooling; intra-channel is average pooling  
d) Intra-channel is used only in LeNet

### A19
ZFNet, as presented in class, is

a) an AlexNet-style CNN with the parameters adjusted  
b) a residual network with 152 layers  
c) an autoencoder  
d) a bidirectional RNN

### A20
VGG replaces a large kernel by a stack of \(3 \times 3\) kernels because

a) a \(3 \times 3\) kernel sees more of the image than a \(5 \times 5\) kernel in one layer  
b) two stride-1 \(3 \times 3\) layers have the receptive field of one \(5 \times 5\), use fewer weights (\(18\) vs \(25\) per input channel), and insert two nonlinearities  
c) \(3 \times 3\) kernels remove the need for pooling and fully connected layers  
d) VGG has fewer than 60,000 parameters

### A21
The VGG network in the slides takes

a) \(32 \times 32\) grayscale images and about 60,000 parameters  
b) \(224 \times 224 \times 3\) images, many \(3 \times 3\) convolutions, and on the order of 138 million parameters  
c) a sequence of words and one hidden state  
d) only \(1 \times 1\) filters

### A22
The Inception (GoogLeNet) idea in class is

a) only to stack more layers, never to widen a layer  
b) to apply more than one filter size at the **same** level (\(1 \times 1\), \(3 \times 3\), \(5 \times 5\)): smaller kernels see local structure, larger kernels see a wider pattern, and the module uses batch normalisation and RMSprop  
c) to remove all convolutions and keep only fully connected layers  
d) to use a single \(11 \times 11\) filter and no parallel branches

### A23
A plain very deep CNN can get **worse** as depth grows, even on the training set. ResNet’s answer is

a) to delete pooling  
b) a skip (shortcut) so the block can learn a residual \(F(x)\), with output \(F(x) + x\), giving the gradient a path that does not have to travel through every weight  
c) to replace ReLU by a linear activation in every layer  
d) to use a larger dropout rate only

### A24
In a residual block, an **identity** shortcut is used when the tensor shapes already match. A **projection** shortcut is used when

a) the programmer wants to remove batch normalisation  
b) the number of channels or the spatial size changes, so \(x\) must be mapped (typically by a \(1 \times 1\) convolution) before it can be added to \(F(x)\)  
c) the network is LeNet  
d) the loss is mean squared error

### A25
The class figure for that ResNet is about

a) 60,000 parameters  
b) 11 million parameters, with batch normalisation and skip connections  
c) 138 million parameters and no skips  
d) 4 weight matrices inside one RNN cell

### A26
Transfer learning for a CNN means

a) training every weight from random values on the small target set  
b) reusing filters learned on a large source task (for example ImageNet), replacing the final classifier to match the new classes, and fine-tuning on the target data  
c) copying the test set into the training set  
d) sharing one RNN matrix across time

### A27
Early convolutional layers are the ones we usually **freeze** when the target set is small, because

a) they store the class names of ImageNet  
b) they have learned general patterns (edges, colour, texture) that transfer; later layers are more specific to the old classes and are fine-tuned or replaced  
c) frozen layers use more GPU memory  
d) the softmax cannot be changed if early layers stay trainable

### A28
A large learning rate on **all** layers, using only a few dozen target images, mainly

a) preserves the pretrained filters and cannot overfit  
b) overwrites useful pretrained filters and overfits the small set  
c) converts the CNN into a bag-of-words model  
d) is required for LeNet on MNIST

### A29
In these recognition nets the last decision is

a) a softmax over classes (10 for LeNet digits, 1000 for AlexNet)  
b) a reset gate  
c) a next-sentence prediction from `[CLS]`  
d) a reconstruction of the input pixels

### A30
Which task is the CNN unit’s own job, as listed in class?

a) Next-character prediction with backpropagation through time  
b) Image classification, recognition, optical character recognition, and medical image analysis  
c) Masked language modelling  
d) Sampling \(z\) from a standard normal to draw a new face

---

# Unit B — Sequence modelling

RNN, BPTT, bidirectional RNN, encoder–decoder, recursive nets, LSTM, GRU, attention, Transformers, sentiment case study, BERT, attention for speech and vision.

### B1
“Dog bites man” and “man bites dog” are different because

a) the two sentences use different vocabularies  
b) temporal or sequential data carries meaning in the **order**; swapping the order changes the meaning  
c) only images have order  
d) a softmax always reverses the sentence

### B2
A convolution is a weak model of a long sentence mainly because

a) it has no hidden state that carries earlier inputs, it looks inside a local window, and it expects a fixed-size grid  
b) it has too few parameters to run on a GPU  
c) filters cannot be shared  
d) ReLU cannot be used on text

### B3
The RNN step in class is \(h_t = \tanh(W_{xh} x_t + W_{hh} h_{t-1} + b_h)\). The important design choice is

a) a new \(W_{xh}\) and \(W_{hh}\) are learned at every time index  
b) the same weights are reused at every time step; \(h_t\) mixes the new input with the previous memory  
c) \(h_t\) is independent of \(h_{t-1}\)  
d) \(W_{hh}\) is used only at the output layer

### B4
Unrolling an RNN draws the cell many times. Those boxes are

a) different networks, each with its own weights  
b) the same cell at successive times, so a shared weight’s gradient is the **sum** of the gradients of all its copies  
c) a convolutional filter bank  
d) an autoencoder’s encoder and decoder

### B5
Image captioning (one image in, a sentence out) is

a) one-to-one, so it is only a feedforward net  
b) one-to-many  
c) many-to-one  
d) an undercomplete autoencoder

### B6
Sentiment of a full review (many words in, one label out) is

a) many-to-one  
b) one-to-many  
c) aligned many-to-many  
d) a \(1 \times 1\) convolution

### B7
Part-of-speech tagging, with one tag per word, is aligned many-to-many. Machine translation, where the lengths differ, is

a) also forced to have equal lengths  
b) many-to-many in the encoder–decoder (sequence-to-sequence) form  
c) one-to-one  
d) global average pooling

### B8
A vanilla RNN’s gradient on a long sequence tends to vanish because

a) each step multiplies the error by a small factor (a weight times the tanh slope), and a long product of numbers below 1 collapses  
b) the loss is never summed over time  
c) shared weights are updated only at the last step  
d) softmax outputs are always one-hot

### B9
In “Ravi, who grew up in Coimbatore and studied at PSG Tech …, says ___ loves filter coffee”, a plain RNN usually fails to predict “he” because

a) the vocabulary does not contain “he”  
b) the subject is many steps back, and the hidden state has been rewritten so many times that the early signal is gone  
c) RNNs cannot read proper names  
d) the sentence is an image

### B10
Backpropagation through time is

a) a new loss that replaces cross-entropy  
b) ordinary backpropagation on the unrolled graph, walking from the last time step toward the first  
c) used only for the output matrix \(W_{yh}\), never for \(W_{hh}\)  
d) the forward pass with the weights frozen

### B11
\(W_{yh}\) maps \(h_t\) to the scores at the **same** time. \(W_{hx}\) and \(W_{hh}\) sit **inside** the loop \(h_{t-1} \to h_t\). So

a) only \(W_{yh}\) needs error carried through time  
b) \(W_{hx}\) and \(W_{hh}\) need error carried through time; \(W_{yh}\) is a sum of local terms, one per step  
c) none of the three matrices is shared  
d) \(W_{hh}\) is not trained

### B12
With a one-hot input, the contribution of time \(t\) to \(\partial L / \partial W_{hx}\)

a) is added to every column  
b) is written into the column of the character that was the input at time \(t\)  
c) is always the zero matrix  
d) replaces \(W_{yh}\)

### B13
In the “hope” example, the column for **e** in \(\partial L / \partial W_{hx}\) is zero because

a) the letter e is the target at the last step, so its input column must be zero: e is never an **input** in that example  
b) tanh of any value is zero  
c) the learning rate is zero  
d) bidirectional nets delete the last column

### B14
If the backward pass uses only each step’s own output error and **does not** add \(W_{hh}^\top \delta_{t+1}\),

a) the early steps never hear the losses from later steps, so the gradient on the first inputs is wrong  
b) BPTT becomes exact  
c) the model trains faster and the gradient is unchanged  
d) vanishing gradients are solved

### B15
For softmax plus cross-entropy, the output error at a step is

a) \(\hat{y}_t - y_t\)  
b) \(\hat{y}_t / y_t\)  
c) always 1  
d) the reset gate

### B16
The derivative of \(\tanh\) at a hidden state \(h_t\) is

a) \(1 - h_t^2\)  
b) \(h_t(1 - h_t)\)  
c) a constant 1, so RNNs never vanish  
d) \(1 / (1 + e^{-h_t})\)

### B17
LSTM keeps two memories. Their roles in class are

a) both are rewritten from scratch by a single tanh, like a plain RNN  
b) the cell state \(C\) is the long memory, edited by forget and input; the hidden state \(h\) is what is shown onward, controlled by the output gate  
c) \(C\) is the learning rate and \(h\) is the batch size  
d) \(h\) is kept forever and \(C\) is random noise

### B18
The three LSTM gates use a sigmoid because

a) a sigmoid is a valve in \((0, 1)\): 0 blocks, 1 passes, and a value in between passes a fraction  
b) a sigmoid outputs a class among 1000 ImageNet labels  
c) gates must be negative to remember  
d) the cell state is not allowed to use addition

### B19
The cell update \(C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t\) helps long memory because

a) it squares \(C\) at every step  
b) the path along \(C\) is multiply-by-\(f\) and add, with no tanh on that path; if the net keeps \(f\) near 1, the gradient is not forced through a long product of small tanh slopes  
c) \(f_t\) is fixed at 0.5 and cannot be learned  
d) \(C_t\) is replaced by \(h_t\) before the addition

### B20
Old cell \(0.8\), forget gate \(0.9\), input gate \(0.5\), candidate \(0.6\). The new cell state is

a) \(0.72\)  
b) \(1.02\)  
c) \(0.30\)  
d) \(0.8\)

### B21
Same numbers, but the forget gate is \(0\). The new cell state is

a) \(0.8\), the old cell is copied  
b) \(0.30\), the old cell is erased and only half of the candidate is written (\(0.5 \times 0.6\))  
c) \(1.02\)  
d) \(0\), because the input gate is also ignored

### B22
The LSTM hidden state is \(h_t = o_t \odot \tanh(C_t)\). This means

a) everything stored in \(C\) is always visible at the output  
b) the cell can keep a fact while the output gate shows only the part needed at this step  
c) \(o_t\) is a tanh, so it can be larger than 1  
d) \(h_t\) does not depend on \(C_t\)

### B23
The lecture links ResNet and LSTM by

a) both using average pooling  
b) ResNet’s skip lets the gradient pass through **depth**; the LSTM cell state lets the gradient pass through **time**  
c) both removing gates  
d) both being encoder-only Transformers

### B24
A bidirectional LSTM

a) runs one chain left to right and one right to left, then combines (concatenates) their states, so it can use future context  
b) is a feedforward net with no recurrence  
c) can be used for live next-tick prediction when the future ticks do not exist yet, with no change  
d) deletes the cell state

### B25
You would choose a bidirectional net for

a) predicting the next character before the rest of the sentence has been typed, using only the past  
b) a task where the whole sequence is already available and the future helps, such as named-entity recognition or segmenting a recorded biomedical signal  
c) replacing the softmax in LeNet  
d) training an RBM

### B26
A stacked LSTM needs `return_sequences=True` on the lower layer because

a) the next LSTM must receive a **sequence** of hidden states, not a single vector  
b) otherwise the forget gate is removed  
c) it turns the model into a CNN  
d) the embedding layer cannot be trained

### B27
The sentiment case study (a review → positive or negative) is wired as

a) many-to-one: embedding, then LSTM or GRU, then a dense unit with sigmoid and binary cross-entropy  
b) one tag per word, with a softmax over POS tags at every step  
c) an autoencoder that reconstructs the review  
d) a 1000-way ImageNet softmax

### B28
Part-of-speech tagging on the same embedding would instead be

a) many-to-one with a single sigmoid  
b) many-to-many, with an output at every time step (`return_sequences=True`) and a softmax over tags  
c) impossible for an RNN  
d) a global average pool of pixels

### B29
GRU (Cho et al., 2014), as derived in class, simplifies LSTM by

a) adding a second cell state and a fourth gate  
b) merging cell and hidden state into one \(h\), merging forget and input into one update gate \(z\), dropping the output gate, and adding a reset gate \(r\)  
c) removing all sigmoid nonlinearities  
d) using a different weight matrix at every time step

### B30
In the lecture equation \(h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t\),

a) \(z = 0.2\) keeps about 80% of the old state and writes about 20% of the new candidate; keep and write add to 100%  
b) \(z = 0.2\) deletes the state  
c) \(z\) is a tanh and can be 4  
d) \((1 - z)\) is the reset gate

### B31
Still using that lecture equation, \(z_t = 0\) and \(r_t = 0\) mean

a) \(z_t = 0\) copies \(h_{t-1}\) forward unchanged; \(r_t = 0\) builds the candidate **without** the previous state  
b) both gates delete the input \(x_t\)  
c) \(z_t = 0\) forces the candidate to replace the memory  
d) \(r_t = 0\) is the output gate of an LSTM

### B32
Some libraries write \(h_t = z_t \odot h_{t-1} + (1 - z_t) \odot \tilde{h}_t\). The lecture’s warning is

a) those libraries are not GRUs  
b) the mixer is the same idea; only the **meaning of the symbol** \(z\) is flipped, so you must see which term \(z\) multiplies  
c) reset gates do not exist in any GRU  
d) \(z\) is no longer a sigmoid

### B33
Along the GRU state, the backward factor is \((1 - z)\) in the lecture’s form. Long memory works when

a) the net learns \(z\) near 0 on the steps that should be remembered, so \((1 - z)\) stays near 1 and the state is copied forward  
b) \(z\) is fixed at 1 for every step  
c) the candidate uses a sigmoid instead of tanh and there is no gate  
d) weight sharing is turned off

### B34
Parameter count and the practical choice, as in class:

a) a GRU cell has 3 weight sets against the LSTM’s 4, so `GRU(128)` has about three-quarters the parameters of `LSTM(128)` and is the one to try first when data or compute is limited  
b) GRU always beats LSTM on very long sequences that need a separate output gate  
c) LSTM is smaller than a plain RNN  
d) GRU has no reset gate, so it cannot be bidirectional

### B35
The plain RNN encoder–decoder squeezes the whole input into

a) one context vector (the encoder’s final state) before decoding starts, which is a bottleneck for long inputs  
b) one vector per input token that the decoder can look up freely, with no attention  
c) a parse tree  
d) the softmax of a CNN

### B36
A recursive neural net differs from a recurrent one in that

a) the recursive net applies the same composition on a **tree** (a parent from its children), as in phrase-structure sentiment; the recurrent net applies it along a **chain** in time  
b) they are two names for a bidirectional LSTM  
c) a recursive net never shares weights  
d) a recursive net is an inception module

### B37
Self-attention, in the “animal … it was too tired” example, lets “it”

a) read only the previous word, like a bigram  
b) look at the other words in one step and put weight on “animal”, without pushing that fact through a chain of hidden states  
c) ignore the sentence and use a fixed word2vec vector  
d) update a cell state with a forget gate only

### B38
In scaled dot-product attention the three roles are

a) query = what I am looking for, key = what I can be matched on, value = what I pass on if I am chosen  
b) query = the loss, key = the learning rate, value = the batch size  
c) all three are the same learned vector, so separate \(W_Q, W_K, W_V\) are unnecessary  
d) values are chosen before any score is computed, and the softmax is unused

### B39
Scores are divided by \(\sqrt{d_k}\) because

a) it makes the weights sum to 2  
b) without it, large dot products drive softmax toward a one-hot vector and the gradient becomes tiny  
c) positional encoding then becomes unnecessary  
d) it replaces the residual connection

### B40
The three attention blocks in the Transformer use Q, K, V as follows.

a) Encoder self-attention: Q, K, V from the source. Masked decoder self-attention: Q, K, V from the target so far, future positions blocked. Cross-attention: Q from the decoder, K and V from the encoder output \(M\)  
b) All three blocks take Q, K, V from the encoder, and none is masked  
c) Cross-attention takes Q from the encoder and K, V from the decoder  
d) The encoder uses a causal mask and the decoder does not

### B41
The decoder mask sets future scores to \(-\infty\) before the softmax so that

a) those positions get attention weight 0, and position \(t\) cannot see tokens after \(t\)  
b) the encoder must be run again for every word  
c) the embedding dimension changes  
d) beam search is disabled

### B42
Positional encoding is **added** to the token embedding because

a) attention by itself treats the input as a set; without a position signal, “dog bites man” and “man bites dog” look the same  
b) the two vectors are concatenated, so \(d_{\text{model}}\) doubles and every later layer is resized  
c) it replaces the embedding, and the token identity is discarded  
d) positions are useful only in the CNN pooling layer

### B43
Each sublayer is wrapped as \(\mathrm{LayerNorm}(x + \mathrm{Sublayer}(x))\). The feed-forward block then

a) mixes tokens with each other, which is attention’s job  
b) transforms **each** position by itself (expand, ReLU, compress, same weights at every position), while attention is what mixes positions  
c) removes the need for \(W_O\)  
d) is used only in the embedding table

### B44
At inference

a) the encoder runs once per source sentence and its output \(M\) is reused; the decoder runs once per generated word until the end token  
b) both towers run once per output word, and \(M\) is recomputed every time  
c) the decoder sees future target words  
d) greedy decoding keeps every word in the vocabulary as a live hypothesis

### B45
Teacher forcing in this lecture means

a) the decoder is fed the correct target, shifted one step right, and every next-token loss is computed in parallel  
b) the model must sample its own previous prediction during training, with no gold target  
c) labels are removed and the network reconstructs pixels  
d) the learning rate is set to 1

### B46
Greedy decoding and beam search differ in that

a) greedy appends the single best next word; beam search keeps several partial sentences and continues them  
b) beam search ignores the probabilities  
c) greedy decoding runs the encoder once per word and beam search does not use \(M\)  
d) they are identical if the vocabulary is larger than 10

### B47
Which family is which?

a) BERT is decoder-only and causal; GPT reads both directions in every layer  
b) BERT is an encoder stack with **no** causal mask (both directions, every layer); GPT is decoder-only and causal; the original Transformer, T5, and BART keep an encoder and a decoder  
c) ELMo is a deep self-attention mask; BERT is two LSTMs joined only at the end  
d) ViT is an RNN with a forget gate

### B48
ELMo’s two directions and BERT’s two directions differ because

a) ELMo runs a left-to-right LSTM and a right-to-left LSTM separately and joins them late; BERT lets every token see every other token inside each layer  
b) BERT cannot see the token on its right  
c) ELMo uses `[MASK]` and BERT does not  
d) they produce the same vectors as word2vec

### B49
word2vec gives “apple” one vector. BERT’s **output** gives “apple” different vectors in “ate an apple” and “Apple released a phone” because

a) the embedding table stores two rows for every word  
b) the table lookup is still static; the contextual vector appears only after the attention layers mix the sentence  
c) a sigmoid gate copies the word  
d) positional encodings are removed

### B50
BERT’s input vector at each token is the sum of

a) token embedding + segment embedding + position embedding  
b) query, key, and value  
c) forget, input, and output gates  
d) a sinusoidal position only, with no segment embedding, as in the original Transformer

### B51
BERT’s positions differ from the original Transformer’s positions because

a) BERT learns a position vector, up to 512 tokens; the original Transformer uses fixed sine and cosine  
b) BERT concatenates the position and doubles the hidden size  
c) BERT has no position signal at all  
d) BERT uses the LSTM cell state as the position

### B52
`[CLS]` and `[SEP]` are used so that

a) `[CLS]` is ignored and `[SEP]` is the only token that enters attention  
b) the output at `[CLS]` (called \(C\)) summarises the sequence for sentence-level tasks; `[SEP]` marks the boundary between sentence A and sentence B  
c) both tokens are the answer span in every SQuAD example  
d) `[CLS]` stores the reset gate

### B53
BERT-base, as specified in class, is

a) 6 layers, \(d_{\text{model}} = 512\), 8 heads  
b) 12 layers, hidden size 768, 12 heads, feed-forward width 3072, about 110 million parameters  
c) 24 layers, hidden size 1024, about 11 million parameters  
d) one RBM

### B54
The original Transformer feed-forward uses ReLU. BERT’s feed-forward uses

a) GELU  
b) a hard forget gate  
c) average pooling  
d) no nonlinearity

### B55
Masked language modelling chooses 15% of the tokens. Of **those** chosen tokens

a) 100% become `[MASK]`  
b) 80% become `[MASK]`, 10% are replaced by a random token, and 10% are left unchanged; the loss is only on these chosen positions  
c) 80% of the whole sentence is masked, and the loss is on every token  
d) the mask is the decoder’s causal mask

### B56
The 10% “leave it unchanged” case exists because

a) `[MASK]` appears constantly at fine-tuning time, so the pretraining token and the fine-tuning token already match  
b) `[MASK]` is common in pretraining and absent in fine-tuning; the model must still build a useful vector for a token it actually sees  
c) it trains the reset gate  
d) it removes the need for next-sentence prediction

### B57
Next-sentence prediction

a) is decided from the `[CLS]` vector \(C\), with the true next sentence and a random sentence each about half the time, and its loss is added to the masked-LM loss  
b) asks every token to predict the next character with a causal mask  
c) is the only BERT objective; masked LM was removed in the original paper  
d) reconstructs the input pixels

### B58
Fine-tuning BERT is transfer learning because

a) the expensive pretraining is done once on unlabeled text, and a new task adds a small head and trains on a modest labeled set  
b) all 110 million weights are thrown away and drawn again for each task  
c) the WordPiece vocabulary must be reinvented for every dataset  
d) fine-tuning uses no labels

### B59
BERT question answering, as in the SQuAD setup from class, is

a) free generation of an answer sentence from a decoder  
b) extractive: two new vectors \(S\) and \(E\) score each passage token as a start and an end, and the chosen span maximises start score plus end score with end not before start  
c) a many-to-one sentiment sigmoid  
d) a GAN discriminator

### B60
On SQuAD 2.0 an unanswerable question is handled by

a) always returning the first passage token  
b) treating “no answer” as the span at `[CLS]`, and returning an answer only when the best span beats that null score by a margin  
c) switching BERT into a decoder-only GPT  
d) deleting the passage

### B61
A full QA system still needs a retriever in front of BERT because

a) BERT reads at most 512 tokens, so something else (BM25 or a dense search) must cut a large collection down to a few passages  
b) BERT cannot output a start index  
c) the retriever replaces the attention layers  
d) WordPiece cannot split rare words

### B62
Attention is applied to speech and to images in this lecture by

a) turning audio frames, or image patches, into tokens, then using the same attention machinery (Whisper-style audio, ViT-style patches)  
b) running max pooling on the waveform and stopping  
c) requiring a separate cell state per pixel with no tokens  
d) using LeNet’s average pooling as the attention weight

### B63
A captioning system that looks at relevant parts of an image while writing each word combines

a) a visual encoder (CNN features or image patches) with a decoder that attends, and the output shape is one-to-many  
b) only a many-to-one sentiment head  
c) a deep Boltzmann machine with no decoder  
d) global average pooling straight into a GAN

### B64
Which limitation is true of BERT, as stated in class?

a) It is a decoder and is the right tool for writing long new paragraphs  
b) It is an encoder: it classifies, tags, and points at spans; attention cost grows with the square of the length; the context window is 512 tokens  
c) It has no `[CLS]` token  
d) It uses a causal mask in every layer, like GPT

---

# Unit C — Unsupervised models

Autoencoders and their types, deep belief networks, deep Boltzmann machines, greedy learning, speech with a DBN, GANs, semi-supervised learning.

### C1
An autoencoder is trained to

a) map \(x\) to a human label \(y\)  
b) reproduce its own input, so the input is the target and no class labels are required  
c) fool a discriminator  
d) predict the next sentence from `[CLS]`

### C2
The useful object is the code \(z\) in the middle. For an undercomplete autoencoder

a) the code is shorter than the input, so the net must keep the informative part and throw the rest away  
b) the code is at least as wide as the input, and a copy of \(x\) is the intended solution  
c) the decoder is deleted before training  
d) the loss compares \(z\) with a class label

### C3
An overcomplete autoencoder (code at least as wide as the input) will happily learn to copy \(x\) unless we add

a) a wider softmax  
b) a constraint such as sparsity, input noise, or a penalty on how sensitive the code is  
c) more fully connected layers and no loss  
d) ImageNet labels on every sample

### C4
A linear autoencoder trained with mean squared error

a) spans the same subspace as PCA  
b) learns a curved manifold that PCA cannot represent  
c) is a GAN  
d) requires a sigmoid on a binary image and cannot be linear

### C5
Nonlinear hidden layers matter because

a) they let the code follow a curved manifold, not only a flat subspace  
b) they make the autoencoder identical to JPEG  
c) they remove the need for a decoder  
d) they force the code to be one-dimensional

### C6
Three properties from class: an autoencoder is

a) data-specific, lossy, and learned from examples rather than from a hand-written rule like JPEG  
b) lossless, and equally good on faces and on trees after training only on faces  
c) useful only when every sample has a class label  
d) a recurrent net with a forget gate

### C7
Mean squared error is the natural reconstruction loss for real-valued inputs. Binary cross-entropy is the natural one when

a) the inputs lie in \([0, 1]\), such as pixel intensities, and the decoder ends in a sigmoid  
b) the code is a standard normal  
c) the task is 1000-way classification  
d) the weights are tied

### C8
Tied weights set the decoder matrix to the transpose of the encoder matrix in order to

a) double the number of free parameters  
b) cut the number of free parameters and regularise  
c) remove the reconstruction loss  
d) implement max pooling

### C9
A denoising autoencoder sees a corrupted input \(\tilde{x}\) but the loss compares the output with

a) the corrupted \(\tilde{x}\), so copying the noise gives zero loss  
b) the clean \(x\), which stops the net from succeeding by copying and makes it learn the structure  
c) a class label  
d) a random vector from \(N(0, I)\)

### C10
Noise in a denoising autoencoder is

a) added in training; at test time the real (possibly noisy) input is fed and the reconstruction is read out  
b) added only at test time  
c) a substitute for the decoder  
d) illegal for ECG or speech

### C11
A convolutional autoencoder is preferred for images because

a) flattening a \(28 \times 28\) image into 784 numbers throws away neighbourhood structure; convolutions keep it, and transposed convolution (or upsampling) restores the spatial size  
b) convolution cannot implement an encoder  
c) images have no spatial structure  
d) it is required to use a sigmoid gate from an LSTM

### C12
A sparse autoencoder can have **more** hidden units than inputs. It still does not copy \(x\) because

a) an L1 or KL penalty pushes most hidden activations toward zero (a small target such as \(0.05\))  
b) the decoder is linear and the encoder is removed  
c) sparsity is a penalty on the weights only, and activations are unconstrained  
d) the code dimension \(k\) must be 1

### C13
Raising the weight \(\beta\) on the sparsity penalty

a) makes the code sparser and, past a point, makes reconstruction worse  
b) has no effect on either term  
c) removes the need for a bottleneck in every autoencoder  
d) turns the model into PCA exactly

### C14
A contractive autoencoder adds a penalty on

a) the Frobenius norm of the encoder Jacobian \(\partial h / \partial x\), so a tiny input change makes only a tiny code change  
b) the number of classes  
c) the beam width  
d) the forget gate

### C15
Denoising and contractive autoencoders both want robust features. The difference in class is

a) denoising gets robustness by training on corrupted inputs; the contractive model asks for it directly through the derivative  
b) they are the same loss  
c) only the contractive model can use images  
d) denoising requires labels

### C16
A sequence (LSTM) autoencoder stores the whole series in

a) the final encoder hidden state, and the decoder unrolls that one vector to rebuild the steps  
b) a separate parameter matrix for each time step, with no sharing  
c) the softmax over 1000 classes  
d) a \(3 \times 3\) kernel

### C17
The anomaly recipe for ECG, machines, or defect-free photos is

a) train on normal data only, then flag a new input whose reconstruction error is high  
b) train on the anomalies only, because the autoencoder is not data-specific  
c) require a label for every normal window  
d) replace the decoder by a discriminator and stop measuring reconstruction

### C18
A variational autoencoder’s encoder outputs

a) one code point with no distribution  
b) a mean \(\mu\) and a spread \(\sigma\), and the sample is \(z = \mu + \sigma \odot \varepsilon\) with \(\varepsilon \sim N(0, I)\), so the sample is differentiable  
c) a forget gate and an output gate  
d) the pixels of the nearest training image

### C19
The VAE loss is a reconstruction term plus a KL term that

a) pushes each \(q(z \mid x)\) toward \(N(0, I)\), so the codes fill a continuous region and a random draw from that prior can be decoded  
b) pushes the codes into isolated points with gaps, like a plain autoencoder  
c) is the GAN value function  
d) replaces the decoder

### C20
A plain autoencoder is a poor generator of new samples because

a) its codes are scattered points; decoding a random point in a gap usually yields noise  
b) it has a KL term and a prior  
c) the decoder is absent  
d) reconstruction is always perfect, including off the data

### C21
After a VAE is trained, new data is drawn by

a) throwing the encoder away, sampling \(z\) from \(N(0, I)\), and decoding  
b) running backpropagation through time  
c) masking 15% of tokens  
d) max-pooling the training set

### C22
Stacked (greedy) autoencoder training does which of the following?

a) Draws all layers at random and backpropagates through the full depth from the start  
b) Trains one shallow autoencoder, keeps its encoder, trains the next autoencoder on those codes, stacks the encoders, then fine-tunes; the layer-wise stage uses no labels  
c) Trains the discriminator before the generator  
d) Freezes the model and never fine-tunes

### C23
Greedy layer-wise pretraining was introduced because

a) a deep net from random weights was hard to train (vanishing gradients, poor minima); each layer can be started from a sensible representation, and labels are needed only for the final fine-tune  
b) it increases the vanishing gradient on purpose  
c) modern ReLU and batch normalisation made it the only legal way to train any net  
d) it removes the decoder from a VAE

### C24
With ReLU, batch normalisation, and a decent initialisation, end-to-end training usually works. Greedy pretraining is still the right tool mainly when

a) labeled data are scarce and the unlabeled mass can still shape the features  
b) the dataset is fully labeled and small nets are illegal  
c) the task is a \(3 \times 3\) convolution on MNIST with 60,000 labels  
d) the goal is to compute a positional encoding

### C25
A restricted Boltzmann machine is

a) an undirected bipartite graph: visible units and hidden units, with **no** connections inside the visible layer or inside the hidden layer  
b) a directed residual CNN  
c) a decoder-only Transformer  
d) a supervised softmax with no energy function

### C26
A deep belief network, in the standard construction this unit examines, is

a) undirected between every pair of adjacent layers, with equal top-down and bottom-up influence at training time  
b) a stack of RBMs trained greedily: the **top** pair stays an undirected RBM, and the lower layers form a **directed** generative model; a softmax can then be fine-tuned with labels  
c) a GAN with no hidden units  
d) an LSTM encoder–decoder

### C27
A deep Boltzmann machine differs from that DBN because

a) the DBM is undirected through the whole depth, so inference uses both bottom-up and top-down interactions and is approximate (mean-field style)  
b) the DBM has no hidden layers  
c) the DBM is trained only with next-sentence prediction  
d) the DBM forbids greedy initialisation of any kind

### C28
Speech recognition with a DBN, in the form this syllabus means, works by

a) pretraining on unlabeled acoustic frames, then fine-tuning the stack to score phonetic (HMM) states, so the network replaces the old Gaussian mixture acoustic model  
b) using the DBN as a microphone  
c) translating English to German with cross-attention and no acoustic model  
d) reconstructing the waveform with a \(3 \times 3\) kernel only

### C29
A GAN trains two networks. Their jobs are

a) a generator that maps noise \(z\) to a fake sample, and a discriminator that says whether a sample is real or fake  
b) an encoder and a decoder that minimise \(\|x - \hat{x}\|^2\) only  
c) a forward RNN and a backward RNN  
d) a start vector \(S\) and an end vector \(E\)

### C30
In the basic GAN game the discriminator **maximises**, and the generator **minimises**,

a) \(\mathbb{E}[\log D(x)] + \mathbb{E}[\log(1 - D(G(z)))]\)  
b) the VAE’s KL divergence alone, with no adversary  
c) the LSTM cell state  
d) the number of convolutional filters

### C31
A useful equilibrium, and the usual failure, are

a) equilibrium: the discriminator is about \(1/2\) on real and on fake samples, because the generator has matched the data distribution; failure: mode collapse, where the generator emits only a few kinds of sample  
b) equilibrium: the discriminator is perfect and the generator has a loss of zero from the first step  
c) equilibrium: reconstruction error is zero on a held-out code \(z\) drawn from a gap  
d) failure: the forget gate sticks at 1, which is called mode collapse

### C32
Place the three generators.

a) A plain autoencoder reconstructs and leaves gaps in \(z\); a VAE adds a KL pull toward a prior so \(z\) can be sampled, often with blurrier samples; a GAN never reconstructs a paired \(x\), it matches the distribution through the discriminator, often sharper and less stable  
b) All three minimise \(\|x - \hat{x}\|^2\) and share one encoder  
c) A GAN is undercomplete PCA; a VAE is AlexNet  
d) A VAE has no decoder

### C33
Semi-supervised learning means

a) every training sample has a label  
b) no sample has a label, and the target is the input itself  
c) a small labeled set is used together with a large unlabeled set  
d) the test labels are used to train

### C34
Which pipeline is the semi-supervised one?

a) A denoising autoencoder with no class labels at any stage  
b) Greedy DBN or stacked-autoencoder pretraining on unlabeled data, then a supervised fine-tune on a few labeled examples  
c) A fully labeled 1000-way softmax trained from scratch  
d) Teacher-forced translation with a gold target at every position

### C35
A plain GAN is unsupervised. It becomes a semi-supervised method when

a) the discriminator also assigns a real class on labeled images, while unlabeled real images and fake images still train the real-versus-fake decision  
b) the generator is replaced by max pooling  
c) \(z\) is removed  
d) the discriminator is deleted after the first batch

### C36
Which pairing matches the lecture’s “which type for which job”?

a) Few labels → stacked pretraining; noise removal → denoising; images and inspection → convolutional; a new sample from a prior → variational; a time-series anomaly → sequence autoencoder  
b) Few labels → a GAN equilibrium at step 0; noise removal → a residual shortcut; new samples → LeNet  
c) Images → a bidirectional GRU with no decoder; time series → a \(1 \times 1\) convolution that ignores order  
d) Anomaly detection → train only on the rare faults and ignore normal data

---

# Answers — Unit A

| Q | Answer | Why this is the best option |
|---|---|---|
| A1 | **b** | The lecture introduces CNNs for images: a filter slides on a grid. Sequences are the RNN unit. |
| A2 | **b** | Sharing is the whole point: fewer weights than a fully connected net, and a shifted object still meets the same filter. Sharing does not by itself prevent overfitting. |
| A3 | **b** | Those are the four roles on the layer slide. Dropout is a training regulariser, not a feature extractor. |
| A4 | **b** | This is the spatial-size formula used with the padding and stride slides. |
| A5 | **b** | \((5 - 3)/1 + 1 = 3\). The worked \(5 \times 5 \to 3 \times 3\) map in class is this case. |
| A6 | **a** | The padding slide surrounds the image with zeros so the border is filtered and the size can be preserved. |
| A7 | **b** | Stride is the jump. It downsamples. It does not add weights to that kernel. |
| A8 | **b** | The lecture sets the kernel to an odd size so a centre cell exists. |
| A9 | **b** | Colour slide: each channel is filtered and the maps are summed. One filter, one feature map. |
| A10 | **b** | Sharing is across **positions**. Different filters in the same layer are different detectors. |
| A11 | **b** | Max pooling has no kernel to learn. The window’s maximum is unchanged if the peak only moves inside the window. |
| A12 | **a** | “Global” means the window is the whole map, so each channel collapses to one number. |
| A13 | **b** | LeNet in class: MNIST, \(32 \times 32\), ~60,000 weights, tanh, softmax, average pooling, 10 classes. Option a is AlexNet. |
| A14 | **b** | AlexNet in class: ReLU, max pooling, dropout, LRN, \(227 \times 227 \times 3\), 1000 classes, ~60 million weights. |
| A15 | **b** | The slide places dropout between the last pool and the first fully connected layer. |
| A16 | **a** | Units are dropped while training (often 20–50%). Test uses the full net. |
| A17 | **b** | LRN is non-trainable lateral inhibition. ReLU can grow without a bound, so nearby responses are rescaled against each other. |
| A18 | **a** | Inter-channel: across filters at \((x, y)\). Intra-channel: across a spatial patch of one map. |
| A19 | **a** | The lecture treats ZFNet as AlexNet with the parameters tweaked. |
| A20 | **b** | Two \(3 \times 3\) layers see a \(5 \times 5\) field. Weights per input channel: \(9 + 9 = 18\), against \(25\), plus two ReLUs. That is the “several small kernels” point. |
| A21 | **b** | VGG in class: \(224 \times 224 \times 3\), stacks of \(3 \times 3\), about 138 million parameters. |
| A22 | **b** | Inception widens a stage: several kernel sizes in parallel, batch norm, RMSprop. Small kernels are local; large kernels see more context. |
| A23 | **b** | The lecture’s reason for the skip: deep plain nets suffer a vanishing gradient. \(F(x) + x\) gives the gradient a shortcut through depth. |
| A24 | **b** | Identity adds \(x\) unchanged. If the shape changes, a projection (a \(1 \times 1\) convolution) makes the two tensors addable. |
| A25 | **b** | The ResNet slide quotes about 11 million parameters, with batch normalisation and skips. |
| A26 | **b** | Same idea as BERT later in the course: learn features once on a large set, then adapt the head and fine-tune. |
| A27 | **b** | Early filters are generic. With little target data you freeze them so a large learning rate cannot wash them out. |
| A28 | **b** | A large learning rate on every layer, with a tiny target set, destroys the transferred features and memorises the few images. |
| A29 | **a** | Recognition ends in a softmax over the classes the architecture was built for. |
| A30 | **b** | The applications slide: classification, recognition, OCR, medical images. Next-character BPTT and masked LM belong to the sequence unit. |

---

# Answers — Unit B

| Q | Answer | Why this is the best option |
|---|---|---|
| B1 | **b** | The temporal-data slide uses this pair: order is the signal. |
| B2 | **a** | A filter has no memory outside its window and wants a fixed grid. An RNN carries \(h\) and accepts variable length. |
| B3 | **b** | Temporal weight sharing: one cell, reused. The new state depends on \(x_t\) and \(h_{t-1}\). |
| B4 | **b** | Unrolling is a drawing of one cell. Shared weights add their gradients across time. That is BPTT. |
| B5 | **b** | One image, many words. The lecture’s one-to-many example. |
| B6 | **a** | Many inputs, one label. Sentiment and the ECG-style examples are many-to-one. |
| B7 | **b** | Equal length, one output per step: aligned many-to-many. Unequal length: encoder–decoder. |
| B8 | **a** | The product of many factors near \(0.5\) is about \(0.001\) after 10 steps. Early tokens stop teaching the weights. |
| B9 | **b** | The subject is far from the blank. A plain \(h\) is overwritten at every word. |
| B10 | **b** | BPTT is backpropagation on the unrolled graph, from \(t = T\) back to \(t = 1\). |
| B11 | **b** | A weight needs the through-time path only if it sits inside \(h_{t-1} \to h_t\). \(W_{yh}\) is outside that loop. Every shared matrix is still summed over time. |
| B12 | **b** | One-hot \(x_t\) picks one column. That step’s \(\delta_t\) is written there. |
| B13 | **a** | The inputs are h, o, p. The letter e is a target, never an input, so its column stays 0. |
| B14 | **a** | \(W_{hh}^\top \delta_{t+1}\) is the through-time term. Drop it and later losses never reach earlier inputs. |
| B15 | **a** | For this pair of loss and softmax, the lecture uses \(\hat{y} - y\). |
| B16 | **a** | \(\tanh'(a_t) = 1 - h_t^2\). Option b is the sigmoid derivative. |
| B17 | **b** | \(C\) is the notebook; \(h\) is the line you read out. A plain RNN has only \(h\), and it is fully rewritten. |
| B18 | **a** | Sigmoid in \((0, 1)\) is a valve. The candidate uses tanh so the new note is in \((-1, 1)\). |
| B19 | **b** | The cell path is scaled by the forget gate, which the net can hold near 1. A plain RNN cannot choose to keep its multiplier near 1. |
| B20 | **b** | \(0.9 \times 0.8 + 0.5 \times 0.6 = 0.72 + 0.30 = 1.02\). The lecture’s numerical step. |
| B21 | **b** | \(f = 0\) drops the old cell. What remains is \(i \odot \tilde{C} = 0.30\). |
| B22 | **b** | The output gate can hide part of \(C\). Memory and “what we show now” are separate. |
| B23 | **b** | The lecture says this in both the ResNet slide and the LSTM slide: a highway through depth, a highway through time. |
| B24 | **a** | Two directions, states combined. The future must already be in the sequence. |
| B25 | **b** | NER and a recorded signal have the future in hand. Live next-step prediction does not. |
| B26 | **a** | The upper LSTM reads a sequence. A lower LSTM that returns one vector cannot feed it. |
| B27 | **a** | The Keras case study: one sigmoid, binary cross-entropy, one label per review. |
| B28 | **b** | Tagging is aligned many-to-many: a distribution over tags at each position. |
| B29 | **b** | One state, one update gate doing both keep and write, no output gate, plus a reset gate. Three weight sets instead of four. |
| B30 | **a** | \(z = 0.2\) writes 20% and keeps 80%. The two fractions sum to 1, like one mixer tap. |
| B31 | **a** | \(z = 0\) copies \(h\). \(r = 0\) zeros the previous state inside the candidate, so the draft is based on the current input. |
| B32 | **b** | The lecture notes the PyTorch-style swap. Learn which term keeps the old state; do not memorise the letter \(z\) alone. |
| B33 | **a** | \((1 - z) \approx 1\) is the GRU version of a forget gate held near 1. The state, and the gradient, pass along. |
| B34 | **a** | 3/4 the matrices, so about 3/4 the weights at the same hidden size. Try GRU when you are short of data or time; try LSTM when you need the extra gate and a very long memory. Accuracy is often close. |
| B35 | **a** | Classic seq2seq compresses the sentence into one vector. That is the bottleneck attention was built to remove. |
| B36 | **a** | Recursive: a tree, parent from children, shared composition. Recurrent: a chain. Bidirectional and stacked models are still chains. |
| B37 | **b** | Each word attends to all words in one step. Nothing has to survive a chain of updates from “animal” to “it”. |
| B38 | **a** | The lecture’s three questions: what am I looking for, what can I be matched on, what do I hand over. |
| B39 | **b** | Large \(d_k\) makes dot products large, softmax saturates, gradients die. The scale keeps the scores in a usable range. |
| B40 | **a** | Encoder: source with source. Masked self-attention: target with target, future hidden. Cross-attention: decoder queries, encoder keys and values. \(M\) is the bridge. |
| B41 | **a** | \(-\infty\) under softmax becomes weight 0. This is training-time and inference-time causality. The encoder is not masked. |
| B42 | **a** | Addition keeps the shape \(d_{\text{model}}\). Concatenation would not. Without positions, attention is blind to order. |
| B43 | **b** | Attention mixes **across** positions. The feed-forward block transforms **inside** one position, with shared weights. The residual is the same skip idea as ResNet. |
| B44 | **a** | \(M\) is computed once. Each new word is appended and only the decoder repeats. Greedy keeps a single best word, not the whole vocabulary. |
| B45 | **a** | Shift the gold target right by one. The mask stops each position seeing the answer it must predict. All positions are trained together. |
| B46 | **a** | Greedy: argmax, append, repeat. Beam: several living hypotheses (the lecture illustrates a beam of 4). |
| B47 | **b** | Encoder-only, decoder-only, and encoder–decoder are the three families on the variants slide. |
| B48 | **a** | ELMo joins two directions late. BERT has no causal mask, so both directions meet in every layer. |
| B49 | **b** | The lookup table has one row per piece. Context is produced by attention. That is why the two apples separate. |
| B50 | **a** | Token + segment + position, summed. Segment embeddings are the BERT addition; the original Transformer does not have them. |
| B51 | **a** | Learned positions, length limit 512, against fixed sine/cosine of any length in the original Transformer. |
| B52 | **b** | \(C\) is the sentence vector (classification, next-sentence). `[SEP]` ends a segment. In QA, segment A is the question and segment B is the passage. |
| B53 | **b** | Base: \(L = 12\), \(H = 768\), \(A = 12\), FFN \(3072\), ~110M. Large is 24 / 1024 / 16 / ~340M. Option a is the original Transformer base. |
| B54 | **a** | BERT’s position-wise feed-forward uses GELU. The 2017 Transformer uses ReLU. |
| B55 | **b** | 15% are selected. Inside that subset the split is 80 / 10 / 10. Other positions are not in the loss, so the two directions can be used safely. |
| B56 | **b** | If every selected token were `[MASK]`, the model would only learn a symbol it will not see at fine-tuning time. |
| B57 | **a** | NSP is a two-way decision on \(C\), mixed half and half, added to the masked-LM loss. It is not causal next-token prediction. |
| B58 | **a** | Pretrain once. Fine-tune a head (and the stack) per task. The lecture calls this transfer learning. |
| B59 | **b** | The answer is a span copied from the passage. Only \(S\) and \(E\) are new. Score \(= s_i + e_j\) with \(j \ge i\). |
| B60 | **b** | The null span is `[CLS]`. A real span must beat it by a tuned margin. |
| B61 | **a** | 512 tokens is the window. The retriever chooses a handful of passages; BERT reads those. |
| B62 | **a** | The “beyond text” slide: patches, audio frames, or signal windows become the tokens. Attention itself does not change. |
| B63 | **a** | Captioning is the one-to-many pattern. Attention (or a decoder state) decides where to look while the words are written. |
| B64 | **b** | Encoder-only, quadratic attention, 512 tokens. Generation is the decoder-only family’s job. |

---

# Answers — Unit C

| Q | Answer | Why this is the best option |
|---|---|---|
| C1 | **b** | Self-supervised: the target is \(x\). No class labels. |
| C2 | **a** | \(k < d\) is what forces compression. If the code is wide enough, copying is an easy perfect solution. |
| C3 | **b** | The lecture’s three cures for the copy solution: sparsity, noise, contraction. |
| C4 | **a** | Linear encoder, linear decoder, squared error: the column space matches PCA. The nonlinear case is the next question. |
| C5 | **a** | Extra nonlinear layers are how the model leaves the flat PCA subspace. |
| C6 | **a** | Data-specific, lossy, learned. A face autoencoder is a poor compressor for trees, which is also why a bad reconstruction flags anomalies. |
| C7 | **a** | MSE matches real-valued measurements. BCE with a sigmoid matches inputs scaled to \([0, 1]\). |
| C8 | **b** | \(W' = W^\top\) is optional. It halves the free matrices and regularises. |
| C9 | **b** | The target stays the clean \(x\). Copying \(\tilde{x}\) does not drive the loss to zero. |
| C10 | **a** | Corrupt during training. At test, pass the input you actually have and read the reconstruction. |
| C11 | **a** | The conv-autoencoder slide: convolutions keep locality; a transposed convolution grows the map back. |
| C12 | **a** | The penalty is on **activations** (KL toward a small \(\rho\), or L1), so the code can be wide and still sparse. |
| C13 | **a** | A heavier penalty means fewer units fire, and the reconstruction term loses. |
| C14 | **a** | The extra term is \(\lambda \|J_f(x)\|_F^2\). |
| C15 | **a** | Noise is an implicit robustness; the Jacobian penalty is explicit. |
| C16 | **a** | The encoder reads \(x_1 \ldots x_T\); \(z\) is the final state; the decoder unrolls it. |
| C17 | **a** | Train on normal only. A large reconstruction error means “this does not look like what I was trained on”. |
| C18 | **b** | \(q(z \mid x) = N(\mu, \sigma^2)\), reparameterised so the gradient reaches \(\mu\) and \(\sigma\). |
| C19 | **a** | The KL term packs the codes around the prior. That is what makes a random \(z\) decodable. |
| C20 | **a** | No prior, so the codes do not fill the space. A point in a gap has never been trained as a code. |
| C21 | **a** | Sample the prior, decode. The encoder is not required at generation time. |
| C22 | **b** | Layer 1 on \(x\), layer 2 on \(h_1\), then stack, then fine-tune. Steps before the fine-tune have no labels. |
| C23 | **a** | Greedy initialisation was the practical answer to vanishing gradients and bad minima in early deep nets. |
| C24 | **a** | The speaker notes: with modern tricks you usually train end to end; stacking remains useful when labels are scarce. |
| C25 | **a** | “Restricted” means the missing within-layer links. Given the other side, the units in one layer are independent, which is what makes an RBM trainable. |
| C26 | **b** | DBN: greedy RBM stack, undirected at the top, directed generative model below, then optional discriminative fine-tuning. |
| C27 | **a** | DBM: undirected all the way up, so both directions interact and inference is approximate. That is the 1-mark contrast with a DBN. |
| C28 | **a** | Unlabeled frames pretrain features; fine-tuning predicts phonetic states; those scores replace the GMM inside the HMM recogniser. |
| C29 | **a** | \(G\) maps \(z\) to data space. \(D\) classifies real versus fake. There is no reconstruction pair \((x, \hat{x})\). |
| C30 | **a** | \(D\) maximises this value; \(G\) minimises it. At a solved game, \(D\) cannot tell the two sources apart. |
| C31 | **a** | \(D \approx 1/2\) is the success picture. Mode collapse is the usual way \(G\) cheats: a few samples that still fool \(D\). |
| C32 | **a** | Reconstruction with gaps; reconstruction plus a prior; adversarial matching with no paired reconstruction. VAE samples are often blurrier; GAN training is less stable. |
| C33 | **c** | Some labels, many unlabeled inputs. Option b is unsupervised or self-supervised. Option a is supervised. |
| C34 | **b** | Pretrain on everything you have, fine-tune on the labels you have. A denoising autoencoder alone never sees a class label, so it is not yet semi-supervised. |
| C35 | **a** | The extra class head is what brings the few labels in. Until then a GAN does not know your class names. |
| C36 | **a** | The applications table: stacked for few labels, denoising for noise, convolutional for images, variational for generation, sequence autoencoder for series anomalies. |

---

# Letter key

Use this for a timed run. Reasons are above.

**Unit A.** A1 b, A2 b, A3 b, A4 b, A5 b, A6 a, A7 b, A8 b, A9 b, A10 b, A11 b, A12 a, A13 b, A14 b, A15 b, A16 a, A17 b, A18 a, A19 a, A20 b, A21 b, A22 b, A23 b, A24 b, A25 b, A26 b, A27 b, A28 b, A29 a, A30 b.

**Unit B.** B1 b, B2 a, B3 b, B4 b, B5 b, B6 a, B7 b, B8 a, B9 b, B10 b, B11 b, B12 b, B13 a, B14 a, B15 a, B16 a, B17 b, B18 a, B19 b, B20 b, B21 b, B22 b, B23 b, B24 a, B25 b, B26 a, B27 a, B28 b, B29 b, B30 a, B31 a, B32 b, B33 a, B34 a, B35 a, B36 a, B37 b, B38 a, B39 b, B40 a, B41 a, B42 a, B43 b, B44 a, B45 a, B46 a, B47 b, B48 a, B49 b, B50 a, B51 a, B52 b, B53 b, B54 a, B55 b, B56 b, B57 a, B58 a, B59 b, B60 b, B61 a, B62 a, B63 a, B64 b.

**Unit C.** C1 b, C2 a, C3 b, C4 a, C5 a, C6 a, C7 a, C8 b, C9 b, C10 a, C11 a, C12 a, C13 a, C14 a, C15 a, C16 a, C17 a, C18 b, C19 a, C20 a, C21 a, C22 b, C23 a, C24 a, C25 a, C26 b, C27 a, C28 a, C29 a, C30 a, C31 a, C32 a, C33 c, C34 b, C35 a, C36 a.

**130 questions, 130 marks if you take the whole bank.** A semester paper will use a small subset. Any heading on the three-unit list has at least two questions here.

---

# If you freeze in the exam

Say the short version, then tick the option that matches it.

- **CNN:** one shared filter, slid on the image. Pooling shrinks. LeNet is small, tanh, average pool, digits. AlexNet is ReLU, max pool, dropout, LRN, 1000 classes. VGG is stacked \(3 \times 3\). Inception is several kernel sizes at one level. ResNet adds \(F(x) + x\).
- **Transfer:** keep early filters, replace the classifier, fine-tune gently. A huge learning rate on a tiny dataset wipes the filters.
- **RNN:** one cell copied through time. Sentiment is many-to-one. Translation lengths differ, so use an encoder–decoder. The plain encoder’s single vector is the bottleneck.
- **BPTT:** add the gradient of a shared weight over time. Error enters the past through \(W_{hh}\). \(W_{yh}\) does not send error backward through time.
- **LSTM:** \(C_t = f \odot C_{t-1} + i \odot \tilde{C}\), and \(h = o \odot \tanh(C)\). Forget near 1 remembers. This is a skip through time.
- **GRU lecture form:** \(h = (1 - z) \odot \text{old} + z \odot \text{new}\). \(z = 0\) copies the memory. \(r = 0\) writes the candidate without the past. If a library swaps \(z\), read which term it multiplies.
- **Bidirectional** needs the future to already be there. **Recursive** composes a tree; **recurrent** walks a chain.
- **Attention:** softmax of scaled scores mixes values. Encoder sees all source tokens. Decoder cannot see future target tokens. Cross-attention: query from the decoder, key and value from \(M\).
- **BERT:** both directions, encoder only. Input is token + segment + position. Mask 15%, then 80/10/10. `[CLS]` does sentence tasks. QA points at a start and an end. It does not write a new paragraph.
- **Autoencoder:** rebuild \(x\). Narrow code, or a penalty, or noise, otherwise it copies. Linear + MSE behaves as PCA. VAE samples \(z\) from a prior. High reconstruction error means anomaly.
- **DBN vs DBM:** DBN is a greedy RBM stack, undirected only at the top, directed below. DBM is undirected all the way up.
- **GAN:** generator from noise, discriminator real versus fake. Not a reconstruction loss. Semi-supervised means a few real labels plus a lot of unlabeled data, which is also what fine-tuning a pretrained DBN or stacked autoencoder does.
