Name: Pavan Kusampudi
700#: 700762366

## Q1 – Character-Level RNN Language Model
In this question, I built a small character-level RNN that learns to predict the next character in a text. First, I created a tiny toy dataset with simple words like “hello” and “help”, and then added a slightly larger text file to make the model learn more patterns. I converted all characters into numbers using a vocabulary mapping, so the model can work with them.

Then I built batches of training data where the input is a sequence of characters and the target is the same sequence shifted by one character. The RNN tries to guess the next character at every step.

Model-wise, I used an Embedding layer (to turn characters into vectors), an RNN/GRU/LSTM layer (to learn sequential patterns), and a final Linear layer to predict the probability of each possible next character.

During training, the model sees the true previous character at each step (teacher forcing), and I optimized it using cross-entropy loss. After training, I wrote a sampling function where I provide a starting letter and the model generates the next characters. I also used different temperatures to control how random the predictions are — low temperature gives predictable output, high temperature gives more creative but messy output.

### Q2 – Toy Self-Attention + Heatmap

In this question, I created a simple demonstration of how self-attention works. I wrote a few small sentences, tokenized them by splitting on spaces, and built a vocabulary of all the unique words. Since sentences are different lengths, I padded them so everything fits nicely in a batch.

Next, I passed each token through an embedding layer and then computed the Query, Key, and Value vectors needed for attention. Using these, I applied the scaled dot-product attention formula to calculate how much each word should focus on every other word in the same sentence.

The interesting part was visualizing the attention weights. I picked one sentence and one attention head, extracted the attention matrix, and plotted it as a heatmap. This heatmap basically shows which words the model pays attention to when processing each word. Darker colors mean low attention; brighter colors mean high.


## Q3 – Scaled Dot-Product Attention

Here, I implemented scaled dot-product attention completely from scratch, just to clearly understand the math behind it. I started by creating random Q (query), K (key), and V (value) matrices. Then I followed the exact attention formula:

Multiply Q with Kᵀ to get raw attention scores.

Divide by √dₖ — this step is important because without scaling, the scores become too large and the softmax becomes unstable.

Apply softmax to turn the scores into probabilities.

Multiply those probabilities with V to get the final output vectors.

To make the behavior clear, I printed the raw scores before scaling, after scaling, the attention weights, and the final output. This made it easy to see how scaling smooths the values and prevents extreme spikes in softmax.
