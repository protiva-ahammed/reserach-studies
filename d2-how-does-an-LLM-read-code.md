Day 2: How does an LLM “read” code?

The key idea: a model can’t read text. It only works with numbers. So text goes through three steps before the model sees it:

Code text  →  Tokens  →  Token IDs  →  Embeddings (vectors)
"getUser"     get | User   1734 | 2105   [0.2, -1.3, ...] [0.8, 0.1, ...]

Step 1: Tokens. The text is cut into small pieces called tokens. These are not always full words. A long name like getUserById might be split into pieces such as get, User, By, Id. Why pieces? The model has a fixed dictionary (say 50,000 entries). It can’t store every possible variable name, but it can build any name from common pieces.

Step 2: Token IDs. Each piece has a number in the dictionary, like a lookup table. get might be 1734. Now the code is a list of numbers.

Step 3: Embeddings. Each ID is turned into a vector (a list of a few hundred numbers). You already know this idea from your medical imaging work: a CNN turns pixels into feature vectors, and similar images get similar features. Here, tokens with similar meaning get similar vectors.

The limit (context window): a model can only take a fixed number of tokens at once. CodeBERT takes 512. Anything longer gets cut off.

It’s like cropping an X-ray to 224×224 before feeding it to a CNN. If the tumor is in the part you cropped away, the model can’t possibly find it. Same with code: if a long Java method is cut at 512 tokens and the vulnerable line was near the end, the model never sees it. That’s a real weakness in published vulnerability research.

Note:A model is a mathematical function, so its input must be numbers it can compute with. Tokens become IDs, and IDs become vectors.”
