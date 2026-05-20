Learning Self-Attention in Natural Language Processing

This briefing document synthesizes the core principles and mechanical processes of self-attention within neural networks, as outlined in the provided technical documentation. The primary objective of these systems is to identify and attend to the most significant features within a given input.

Core Objective and Methodology

The fundamental goal of self-attention is to enable a model to determine which parts of an input sequence are most relevant to each other. This is achieved through a structured four-step process:

1. Encode position information.
2. Extract query, key, and value vectors for search.
3. Compute attention weighting.
4. Extract features with high attention.


--------------------------------------------------------------------------------


1. Positional Encoding

In modern NLP architectures, data is fed into the system simultaneously rather than sequentially. Because the model processes all words at once, it lacks an inherent sense of word order. To resolve this, the system must encode position information to understand the sequence.

* Mechanism: Position information (p_0, p_1, p_2...) is added to the initial word embeddings.
* Result: This creates a position-aware encoding, allowing the model to distinguish between words based on their location in the sentence (e.g., "He tossed the tennis ball to serve").


--------------------------------------------------------------------------------


2. Vector Extraction: Queries, Keys, and Values

The model transforms the position-aware embeddings into three distinct representations by passing them through small, trained neural networks (linear layers).

Vector Type	Functional Analogy	Description
Query (Q)	"What I am looking for"	A representation of the current token seeking related information.
Key (K)	"What I contain"	A representation of the token used for matching against queries.
Value (V)	"The information I offer"	The actual content that will be passed on if a match is found.

The Search Analogy

The document illustrates this process using a search engine or social matching analogy:

* YouTube Example: A user types "k-means clustering" (the Query). The system looks at video titles like "Introduction to Clustering" (the Key).
* The "Pangolin" Analogy: A word ("Pangolin") acts as a Subject with an Animal component interested in Nature. It sends out a Query: "I am looking for a word interested in Nature, preferably a Verb." It finds a match with "Bloom," a Verb passionate about Nature.


--------------------------------------------------------------------------------


3. Computing Attention Weighting

The "Attention Score" measures the degree of association between word pairs by computing the pairwise similarity between each Query and Key.

Similarity Metrics

The similarity is calculated using a Scaled Scalar Product, also known as Cosine Similarity.

* Calculation: V_{KEY} \cdot V_{QUERY}
* Scaling: The result is scaled by dividing the product by the size of the vector.
* Metric Range:
  * A product of 0.99 indicates a very high correlation (vectors are nearly parallel in 2D projection).
  * A product of 0.03 indicates very low correlation (vectors are nearly perpendicular).

The Softmax Function

To make these scores usable, they are passed through a Softmax function, which represents each score as a probability between zero and one.

* Value \approx 1: The network should pay maximum attention to that token.
* Value \approx 0: The word is considered irrelevant in that context.


--------------------------------------------------------------------------------


4. Feature Extraction and Condensation

Once scores are determined, they are used to weight the Value (V) vectors.

* Weighting: The scores are multiplied by the matrix of Values. This ensures that the tokens the network "attends" to are preserved, while irrelevant information is suppressed.
* Condensation: The resulting information is condensed into a single vector for each token. This new token contains the encoding of the most relevant contextual information for that specific word in the sequence.


--------------------------------------------------------------------------------


Encoder Architecture and Multi-Head Attention

The encoding block typically consists of six identical encoders stacked together.

Structure of a Single Encoder

Each encoder contains four primary elements:

1. Attentional Block: Processes the Query, Key, and Value search.
2. Residual Connection Block: Helps maintain information flow.
3. Neural Network: Further processes the condensed features.
4. Residual Connection Block: Finalizes the encoding for that layer.

Multi-Head Attention: Capturing Complex Relations

A single attentional block is insufficient for complex language because associations occur at different levels.

* Word-Level Associations: In "I love Italian food," "love" associates with "I," and "food" associates with "Italian."
* Phrase-Level Associations: To translate "Italian food," the model may also need to pay attention to "I love."
* Solution: By using multiple attentional blocks (Multi-Head Attention), the system can simultaneously detect and encode associations between words and groups of words at varying levels of abstraction.

"A value close to one indicates that the network should pay more attention to that particular token, and a value close to 0 that the word is not very relevant."
