# Indus-GPT: A Hybrid Neural Architecture for the Probabilistic Decipherment of the Indus Valley Script

### Introduction: The Last Great Undeciphered Script of the Ancient World

The Indus Valley Civilization (IVC), one of the world's oldest urban societies, flourished from approximately 2600 to 1900 BCE across a vast expanse of modern-day Pakistan and northwestern India.¹ Its cities, distinguished by sophisticated urban planning and advanced water management systems, stand as a testament to a highly organized culture.¹ Yet, over a century after the civilization's rediscovery by Sir John Marshall in 1924, its people remain silent.² The single greatest barrier to understanding their societal structure, economy, religion, and daily life is the undeciphered nature of their writing system, the Indus script.² This script, found on thousands of artifacts, represents the earliest known form of writing from the Indian subcontinent, but its meaning is a profound and enduring mystery.⁴

The central challenge in deciphering the Indus script is the complete absence of a bilingual or multilingual inscription, a "Rosetta Stone" that could provide a direct key for translation.² The successful decipherment of Egyptian hieroglyphs was contingent on the Rosetta Stone's parallel texts in Hieroglyphic, Demotic, and Ancient Greek.⁷ Without such a comparative artifact, any approach to the Indus script must rely on the analysis of its internal structure, a task complicated by the extreme brevity of the available texts and the unknown nature of the underlying language.²

This report posits that in the absence of a physical key, a new analytical key must be forged from computational methods. It introduces the concept of *Indus-GPT* (Inductive Grammar & Probabilistic-symbol Transformer), a novel, hybrid neural architecture designed specifically to address the unique constellation of challenges presented by the Indus script. This algorithm is not conceived as an automated oracle that will produce a definitive, absolute translation. Rather, it is designed to function as a powerful scientific instrument for two primary purposes: first, to probabilistically model the script's internal grammar with a sophistication that exceeds prior statistical attempts; and second, to rigorously and quantitatively evaluate the competing linguistic hypotheses about the script's underlying language family. By transforming qualitative linguistic debates into testable computational models, *Indus-GPT* aims to provide a data-driven pathway toward finally understanding the language of this great ancient civilization.

The subsequent sections of this report will deconstruct the Indus enigma into its fundamental computational components, present the detailed architectural blueprint of the proposed algorithm, outline a rigorous protocol for its implementation and evaluation, and discuss the anticipated results and their role in a new, human-in-the-loop paradigm of decipherment.

***

## I. The Indus Enigma: A Computational Deconstruction

To design an effective computational solution, it is imperative to first deconstruct the problem of the Indus script into its constituent parts. This involves a precise characterization of the script's known properties, a clear-eyed assessment of the corpus's limitations, and a formalization of the linguistic hypotheses that the model must test. These elements define the constraints and requirements that shape the architecture of *Indus-GPT*.

### 1.1 The Anatomy of the Script: Known Parameters

Decades of archaeological and epigraphic research have established several key parameters of the Indus script, which serve as foundational inputs for any computational model.

* **Sign Inventory**: The script comprises a finite set of distinct symbols or graphemes. Scholarly estimates of the total number of unique signs vary, ranging from approximately 400 to as high as 700.¹ Within this large inventory, a much smaller core group of signs appears with high frequency. Studies have identified that only about 31 signs occur over 100 times, while the vast majority are used rarely.⁹ This heavily skewed frequency distribution suggests a system with a core functional set of signs, supplemented by a large "long tail" of signs that may be logograms for specific names, places, or commodities, or simply rare stylistic variants.
* **Writing System Type**: There is a broad consensus among scholars that the Indus script is likely **logo-syllabic**.³ This means it is a mixed system that combines logograms (signs representing entire words or concepts) with syllabograms (signs representing phonetic syllables). This dual nature is a critical feature that must be explicitly modeled, as a purely phonetic or purely logographic assumption would likely fail.
* **Writing Direction**: The script is predominantly written from **right-to-left**. This has been determined by observing features like the cramping of signs on the left side of inscriptions, indicating the scribe was running out of space. A key characteristic, however, is the use of the **boustrophedon** style in some multi-line texts, where the direction of writing alternates with each line—for instance, right-to-left in the first line and left-to-right in the second.² For computational analysis, all text sequences must be preprocessed to normalize them into a single, consistent logical direction (e.g., logical right-to-left) before being fed into a model.
* **Visual and Structural Complexity**: The signs themselves are a mix of pictographic (resembling objects like fish, jars, or people) and abstract geometric shapes.⁴ A significant feature is the use of **ligaturing**, where basic signs are combined or modified with diacritics to form new, composite signs.¹ Detailed analysis of these composite signs suggests that these modifications are not merely for saving space but serve to alter the meaning or add grammatical value to the basic signs.¹ Furthermore, the script does not appear in isolation; it is frequently paired with iconographic motifs, most famously the animal figures on seals (bulls, elephants, rhinoceroses, and the mythical "unicorn").² This accompanying imagery may provide crucial contextual information, possibly identifying the owner of the seal or the origin of goods, and must be considered part of the overall symbolic system.⁴
* **Numerical System**: A small but significant breakthrough has been the identification of a rudimentary decimal-based numerical system. Single downward vertical strokes represent units (up to nine), and semicircles are used for units of ten.² This provides a solid, albeit small, anchor of known meaning within the vast sea of undeciphered signs and confirms a structured approach to administrative and commercial tracking.⁴

### 1.2 The Tyranny of Scarcity: Analyzing the Corpus

The physical evidence for the script, while numbering in the thousands of artifacts, imposes severe limitations that have thwarted traditional decipherment methods and pose a unique challenge for machine learning.

* **Corpus Size and Fragmentation**: The total known corpus consists of over 5,000 inscriptions, with new discoveries slowly adding to the total.⁸ These are primarily found on durable materials such as steatite seals (which make up the majority of the corpus), pottery, copper tablets, stoneware bangles, and tools made of bronze or ivory.² It is widely hypothesized that a significant volume of writing on perishable materials like palm leaves or birch bark, common in later Indian civilizations, has been lost to time, meaning the surviving corpus may be a functionally biased sample of the script's use (e.g., heavily weighted towards administrative and trade contexts).⁶
* **The Brevity Challenge**: The most formidable computational hurdle is the extreme brevity of the texts. The average length of an Indus inscription is a mere **five signs**.¹ The longest known text on a single line contains only 14 signs, and the longest inscription found on a single object has just 26 signs.¹

This brevity has profound implications for computational modeling. Traditional statistical methods in natural language processing, such as n-gram models, rely on observing recurring sequences of tokens (words or characters) to calculate the probability of a given sequence. For example, in English, seeing the sequence "the cat sat" allows a model to infer that "on" is a likely next word. However, with an average text length of five signs drawn from an inventory of over 400, the statistical landscape is incredibly sparse. The number of possible 2-gram or 3-gram combinations is enormous, but the frequency of any specific n-gram appearing in the corpus is vanishingly low. This makes it practically impossible to build a reliable model of the script's syntax based on local co-occurrence patterns alone. This fundamental problem of data sparsity is a key reason why early statistical analyses, while pioneering in their attempt to find structure, could not lead to a full decipherment and were met with valid skepticism regarding their ability to definitively prove the script's linguistic nature.¹² Consequently, any successful modern algorithm cannot depend primarily on local sequence statistics. It must be architected to learn a global, abstract model of the script's grammar by aggregating information across the entire corpus of fragmented examples. This necessitates an architecture with strong inductive biases capable of generalizing from very few examples, pointing directly toward models like Transformers, which can weigh the importance of all signs in a short sequence, augmented with explicit grammatical constraints.

| Parameter | Finding |
| :--- | :--- |
| **Total Inscriptions** | ~5,500 ⁸ |
| **Total Signs (Graphemes)** | ~400–700 ⁴ |
| **High-Frequency Signs (>100 occurrences)** | ~31 ⁹ |
| **Average Inscription Length** | ~5 signs ¹ |
| **Longest Inscription (single line)** | 14 signs ¹ |
| **Longest Inscription (total)** | 26 signs ² |
| **Primary Medium** | Steatite Seals ⁴ |
| **Other Media** | Pottery, copper tablets, tools, ivory, etc. ² |
| **Writing Direction** | Right-to-Left, Boustrophedon ² |
| **Hypothesized Type** | Logo-syllabic ³ |
**Table 1: Indus Script Corpus Characteristics.** This table quantifies the core computational challenges, notably the high ratio of unique signs to average text length, which necessitates a model capable of learning global structure from sparse local data.

### 1.3 Modeling the Unseen: Candidate Language Families

While the language of the IVC is unknown, decades of scholarship have produced several competing hypotheses, the most prominent of which link the script to known language families.⁴ These hypotheses are not merely historical debates; they provide concrete, testable, and computationally modelable frameworks of grammar.

* **The Dravidian Hypothesis**: This is arguably the most widely supported hypothesis among scholars.³ It is buttressed by the continued presence of the Brahui language, a member of the Dravidian family, in Balochistan near the core IVC region, and by perceived cultural and symbolic continuities between the IVC and later Dravidian cultures in South India.² Computationally, this hypothesis predicts a language with specific structural features:
    * **Morphology**: Primarily **agglutinative**, where grammatical functions are expressed by adding a series of distinct suffixes to a root stem.¹³ This predicts a grammar where a small set of signs should consistently appear in the final positions of inscriptions, functioning as case markers, pluralizers, or other morphemes.
    * **Word Order**: A strict **Subject-Object-Verb (SOV)** word order.¹³
    * **Case System**: A well-defined system of grammatical cases (e.g., nominative, accusative, dative) marked by postpositions or suffixes attached to an oblique stem of the noun.¹⁵

* **The Indo-Aryan (Sanskrit) Hypothesis**: An alternative theory proposes a link to an early form of Indo-Aryan, such as Vedic Sanskrit.¹ While this hypothesis faces chronological challenges for many scholars, as the migration of Indo-Aryan speakers into the subcontinent is often dated to after the IVC's decline, it provides a contrasting set of grammatical rules to test ³:
    * **Morphology**: Primarily **inflectional (or fusional)**, where grammatical information is encoded through changes within the word stem itself (e.g., vowel gradation) and through endings that often fuse multiple meanings (e.g., a single suffix marking case, number, and gender).¹⁸ This contrasts sharply with the one-morpheme-one-meaning tendency of agglutination.
    * **Word Order**: While predominantly SOV, the word order can be more flexible than in Dravidian languages due to the rich case system clarifying grammatical roles.²⁰
    * **Case System**: An elaborate system of eight cases with a complex set of declensions for nouns and adjectives.¹⁹

These competing linguistic theories can be translated into mathematical constraints or priors within a machine learning model. The debate between the Dravidian and Indo-Aryan hypotheses, often qualitative and contentious, can be reframed into a quantitative, testable question. An agglutinative language will produce different statistical patterns than an inflectional one; for instance, it will exhibit a higher frequency of a small set of signs appearing in terminal positions (as suffixes). An inflectional language will show more complex, less separable patterns of sign substitution or modification within sequences. Instead of asking a model to learn a grammar from scratch in a vacuum, we can ask a more powerful question: "Which model better explains the statistical structure of the Indus corpus—the one biased towards learning an agglutinative grammar, or the one biased towards learning an inflectional grammar?" This reframes the decipherment challenge from an impossible translation problem into a tractable hypothesis-testing problem.

| Grammatical Feature | Proto-Dravidian Family | Vedic Sanskrit (Old Indo-Aryan) |
| :--- | :--- | :--- |
| **Primary Morphological Type** | Agglutinative (suffixing) ¹³ | Inflectional/Fusional ¹⁸ |
| **Word Order** | SOV (Strict) ¹³ | SOV (Flexible) ²⁰ |
| **Case Marking** | Postpositions on oblique stem ¹⁵ | 8 distinct case endings ¹⁹ |
| **Verb Agreement** | Gender-Number-Person (GNP) ¹⁵ | Gender-Number-Person (GNP) ¹⁹ |
| **Gender System** | Masculine/Feminine/Neuter or Human/Non-Human ¹⁵ | Masculine/Feminine/Neuter ¹⁹ |
| **Number System** | Singular/Plural ¹⁴ | Singular/Dual/Plural ¹⁹ |
| **Pronoun System** | Inclusive/Exclusive 'we' distinction ¹³ | No inclusive/exclusive distinction ¹⁹ |
**Table 2: Comparative Grammatical Features for Hypothesis Testing.** This table formalizes the linguistic debate into a set of concrete, opposing features that can be translated into computational priors, forming the basis for the hypothesis-testing framework of *Indus-GPT*.

### 1.4 A Critique of Prior Computational Efforts

Computational methods are not new to the study of the Indus script, but past efforts have been limited by the available technology and the unique nature of the problem.

* **Early Statistical Models**: The work of computer scientist Rajesh Rao and his colleagues in the late 2000s was a landmark effort.¹² They used information-theoretic measures like conditional entropy to demonstrate that the Indus sign sequences were more ordered than non-linguistic systems (like DNA sequences) and shared a statistical structure consistent with known languages.¹² Their use of Markov models identified significant patterns, such as certain signs having a high probability of appearing at the beginning of inscriptions.¹² While groundbreaking, these methods were ultimately limited by the extreme data sparsity and could not conclusively distinguish between a true linguistic system and other complex, non-linguistic symbolic systems that might exhibit strong ordering rules (e.g., heraldic codes or astronomical sequences).¹²
* **Modern ML Approaches and Their Limitations**: In recent years, machine learning has been applied with remarkable success to other ancient languages.¹² Researchers at MIT, for instance, developed algorithms that were instrumental in advancing the understanding of Ugaritic and Linear B.⁷ However, these successes hinged on a critical piece of information that is absent for the Indus script: a known, related language. The model for Linear B was guided by its known relationship to an early form of Greek, and the Ugaritic model by its relationship to Hebrew.²⁴ This allowed for a "cognate-based decipherment," where the algorithm could learn to map words and sounds between the unknown and known languages. The Indus script has no confirmed linguistic relatives, rendering this powerful supervised or semi-supervised approach unusable. Attempts to apply general AI have so far only managed to identify recurring patterns without being able to interpret their meaning.⁵ This highlights the absolute necessity of a novel approach that is either fully unsupervised or, as proposed here, hypothesis-constrained unsupervised.

***

## II. Architectural Blueprint: The Indus-GPT Algorithm

To overcome the multifaceted challenges of data scarcity, script complexity, and linguistic uncertainty, *Indus-GPT* is conceived not as a monolithic model but as a modular, four-component hybrid architecture. This design allows each component to specialize in a specific sub-problem, moving systematically from the visual processing of individual signs to the grammatical analysis of sequences, all while being guided by testable linguistic constraints.

### 2.1 Component 1: The Variational Sign Encoder (VSE)

The first step in analyzing the script is to create a meaningful representation of its fundamental units: the signs themselves. Treating the 400-700 signs as discrete, unrelated tokens (e.g., sign_1, sign_58, sign_213) would be computationally inefficient and would discard a wealth of information embedded in their visual forms. The script is pictographic and shows clear evidence of signs being built from component parts or modified with diacritics.¹ A simple tokenization scheme cannot capture the fact that a sign with an extra stroke is related to the basic sign.

To address this, the VSE employs a Convolutional Variational Autoencoder (VAE), a type of generative neural network perfectly suited for learning compressed, meaningful representations (a "latent space") of complex image data.²⁶ The VSE will be trained on a dataset of high-resolution images of every unique sign variant documented in the corpus.

* **Architecture**: The VSE consists of two parts. A convolutional encoder processes the pixel data of a sign image and maps it not to a single point, but to a probability distribution within a continuous, high-dimensional latent space.²⁷ A decoder then attempts to reconstruct the original sign image from a point sampled from this latent distribution.²⁸
* **Function**: The VAE framework forces the latent space to be well-structured and continuous.²⁹ This means that visually similar signs—for example, a basic "jar" sign and a ligatured "jar with two strokes" sign—will be mapped to nearby points in this learned space. This elegantly handles the problems of sign variation, ligaturing, and damage, as the model learns the underlying "visual grammar" of the script's construction.
* **Output**: The trained VSE provides a dense, low-dimensional vector embedding for each sign in the inventory. These embeddings are not arbitrary IDs but are mathematically grounded in the visual structure of the signs. This process transforms the problem from analyzing sequences of arbitrary symbols to analyzing sequences of meaningfully related primitives, providing the subsequent grammar model with a much richer and more informative input signal, which is critical in a low-data regime.

### 2.2 Component 2: The Unsupervised Grammar Induction Core

With robust sign embeddings in hand, the next challenge is to infer the grammatical rules that govern how these signs are sequenced. Given the short, fragmented nature of the texts and the absence of any pre-parsed "gold standard" sentences for training, this task requires a powerful unsupervised approach.

The core of *Indus-GPT* will be a Transformer-based architecture specifically adapted for unsupervised grammar induction. This model will take sequences of the VSE-generated sign embeddings as its input. Its design will be inspired by recent advances in the field of unsupervised syntactic parsing and structured language models, such as Generative Pretrained Structured Transformers (GPST).³⁰

* **Mechanism**: These advanced models learn to perform two tasks simultaneously: generating a sequence of tokens (in this case, Indus signs) and inducing its underlying syntactic structure (e.g., a constituency tree showing how signs group into phrases, or a dependency tree showing head-modifier relationships).³²
* **Process**: The model operates by predicting a sequence of actions. For instance, it might use a stack-based mechanism to decide between GENERATE_SIGN(x) (which adds a new sign to the sequence) and COMBINE_CONSTITUENTS (which groups the last two elements on the stack into a new syntactic phrase).³² The self-attention mechanism of the Transformer is ideal for this, as it can dynamically weigh the importance of all previous signs and actions in the short sequence to make the most probable next decision.³⁴
* **Output**: The output of this core component is a "language-agnostic" grammar. This is a set of probabilistic rules (e.g., production rules like `S→NP VP` or dependency arcs) that best describe the structural patterns observed across the entire corpus of inscriptions, learned purely from the data itself without any prior linguistic assumptions.

### 2.3 Component 3: The Linguistic Hypothesis-Constraint Module

A purely unsupervised grammar, while structurally informative, cannot connect its findings to known linguistic phenomena or help adjudicate between the Dravidian and Indo-Aryan hypotheses. This is the function of the third, and most innovative, component of *Indus-GPT*. This module transforms the model from a pattern-finder into a hypothesis-testing engine.

The grammar induction core will not be trained in a complete vacuum. Instead, its learning process will be constrained by probabilistic priors derived from linguistic typology, as formalized in Table 2.

* **Modeling the Dravidian Hypothesis**: To test for a Dravidian-like structure, a variant of the model, *Indus-GPT-Dravidian*, will be trained. Its loss function will be modified with a regularization term that rewards the induction of grammars characteristic of agglutinative languages. For example, it will be penalized less for discovering grammars with predominantly right-branching structures where a small, recurring set of signs (potential suffixes) attach to a wide variety of stems. This biases the model to "discover" an agglutinative syntax if the evidence in the data supports it.
* **Modeling the Indo-Aryan Hypothesis**: To test for a Sanskrit-like structure, a separate variant, *Indus-GPT-Sanskrit*, will be trained. Its constraints will favor the discovery of inflectional patterns. For example, the model might be rewarded for learning substitution-based rules, where replacing one sign with another in a similar context changes the grammatical function, or for identifying more complex, non-separable relationships between signs within a sequence, reflecting fusional morphology.
* **Implementation**: These linguistic constraints can be implemented in several ways, such as adding custom regularization terms to the model's overall loss function or by directly modifying the probability distribution over the generative actions (GENERATE, COMBINE) in the Transformer core, making certain grammatical structures more or less likely to be proposed during training.
* **Output**: The result of this stage is not one model, but two (or more) separately trained, specialized models. Each model represents the best possible grammar for the Indus script under the explicit assumption of a specific language family. The relative performance of these constrained models can then be compared quantitatively.

### 2.4 Component 4: The Dual Logo-Syllabic Decoder

The final component addresses the hypothesized logo-syllabic nature of the script.³ A standard decoder that simply predicts the next "token" cannot capture the dual possibility that a sign could represent either a concept (logogram) or a sound (syllabogram).

To model this, the final hidden state output by the Transformer core will be fed into two parallel but interconnected decoder heads:

* **Logographic Head**: This head is a classifier that attempts to map the model's representation of a sign to a node in a predefined semantic ontology. This ontology would be constructed by domain experts and could include categories like "human," "animal," "deity," "trade good," "vessel," etc. This part of the model tries to guess the meaning of the sign.
* **Syllabic Head**: This head is a separate classifier that attempts to map the sign's representation to a phonetic value from a hypothesized phonemic inventory. The inventory used would depend on the linguistic constraint being tested (e.g., a Proto-Dravidian phonemic inventory for *Indus-GPT-Dravidian*, a Vedic Sanskrit inventory for *Indus-GPT-Sanskrit*). This part of the model tries to guess the sound of the sign.
* **Joint Training**: These two heads can be trained jointly, allowing them to share information. For example, if the model hypothesizes that a pictographic "fish" sign is a logogram for the concept "fish," it can simultaneously learn that the phonetic value of that sign might be related to the word for "fish" in the candidate language. This provides a computational mechanism for testing the famous "rebus principle" that has been proposed for the script.³
* **Output**: For each sign, the model produces a probabilistic mapping, indicating its likelihood of being a logogram with a certain meaning or a syllabogram with a certain sound, all conditioned on the overarching linguistic hypothesis being tested.

| Component | Model Type | Input | Output | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **Variational Sign Encoder (VSE)** | Convolutional Variational Autoencoder (VAE) | High-resolution images of individual Indus signs | A dense vector embedding for each unique sign, forming a continuous latent space | To create robust, visually-grounded representations of signs, handling variation and ligaturing. |
| **Unsupervised Grammar Induction Core** | Structured Transformer (GPST-inspired) | Sequences of sign embeddings from the VSE | A latent syntactic tree (constituency or dependency) for each inscription | To infer the underlying grammatical structure of the script without supervision. |
| **Linguistic Hypothesis-Constraint Module**| Probabilistic Priors / Regularization Layer | Typological rules from candidate languages (e.g., Agglutinative vs. Inflectional) | A modified loss function or action probability distribution that guides the Grammar Core | To transform the model into a hypothesis-testing engine. |
| **Dual Logo-Syllabic Decoder** | Two parallel feed-forward heads | Final hidden states from the Grammar Core | Probabilistic mappings to (1) a semantic lexicon and (2) a phonetic inventory | To explicitly model the hypothesized logo-syllabic nature of the script. |
**Table 3: Indus-GPT Architecture Summary.** This table provides an at-a-glance overview of the four-part system, clarifying the flow of data and logic from raw sign images to probabilistic linguistic interpretation.

***

## III. Implementation Protocol and Hypothesis Evaluation

Moving from architectural theory to practical application requires a detailed and rigorous implementation plan. This protocol outlines the steps for data preparation, model training, and, most critically, the framework for evaluating the competing linguistic hypotheses in the absence of a ground-truth translation.

### 3.1 Corpus Digitization and Preparation

The foundation of any machine learning project is a high-quality, well-structured dataset. The *Indus-GPT* project will leverage the decades of meticulous epigraphic work that have produced comprehensive digital corpora of the script.

* **Data Source**: The primary data source will be a complete digital aggregation of all known inscriptions. This will be built upon the monumental photographic and textual work of the multi-volume Corpus of Indus Seals and Inscriptions (CISI) series, as well as the continuously updated interactive databases maintained by scholars such as Andreas Fuls and the late Asko Parpola.⁸ These resources provide access to the full corpus of over 5,500 texts, complete with metadata about find spots, artifact types, and sign variations.⁸
* **Preprocessing Pipeline**: A multi-step pipeline will be developed to prepare this raw data for the model:
    1.  **Image Extraction and Normalization**: High-resolution images of each unique sign and its documented variants will be extracted from the corpus photographs. These images will be normalized for size, rotation, and contrast to create a clean training set for the Variational Sign Encoder (VSE).
    2.  **Sequence Transcription and Normalization**: All inscriptions will be transcribed into sequences of standardized sign identifiers. The boustrophedon writing direction will be algorithmically resolved and normalized to a single, consistent logical direction (e.g., right-to-left) to ensure uniform input for the Transformer core.
    3.  **Handling Damaged and Indistinct Signs**: The epigraphic corpora meticulously note signs that are broken, eroded, or otherwise indistinct.³⁵ These will be handled in one of two ways: either by marking them with a special *[UNKNOWN]* token that the model learns to accommodate, or, more sophisticatedly, by feeding the damaged image to the pre-trained VSE and using the embedding of the most likely "complete" sign from the latent space.
    4.  **Metadata Integration**: Associated iconography, such as the animal motifs on seals, will be encoded as a categorical feature accompanying each inscription sequence.² This metadata can be used as an additional conditioning input to the dual decoder, allowing the model to investigate whether the text's structure or content varies systematically with the accompanying image (e.g., do inscriptions on "unicorn" seals have a different grammatical structure from those on "bull" seals?).

### 3.2 A Phased Training Strategy

To manage the complexity of the hybrid architecture and ensure both stability and interpretability, the model will be trained end-to-end but in a logically phased sequence.

* **Phase 1: VSE Pre-training**: The Convolutional VAE is trained first and separately on the entire dataset of unique sign images. This crucial initial step populates the sign embedding lookup table that the rest of the model will depend on. The goal is to create a fixed, high-quality visual representation for every sign before attempting to learn grammar.
* **Phase 2: Language-Agnostic Grammar Induction**: The full *Indus-GPT* architecture (the pre-trained VSE, the Transformer Core, and the Dual Decoder) is trained on the inscription sequences without any linguistic hypothesis constraints. This establishes a baseline model. The grammar induced by this model represents the purest statistical patterns present in the data, free from any linguistic bias. This baseline is essential for measuring the effect of the constraints applied in the next phase.
* **Phase 3: Hypothesis-Constrained Fine-Tuning**: Two copies of the converged baseline model from Phase 2 are taken. One copy is then fine-tuned with the Dravidian-hypothesis constraints active, creating the final *Indus-GPT-Dravidian* model. The other copy is fine-tuned with the Indo-Aryan constraints active, creating *Indus-GPT-Sanskrit*. This process of differential fine-tuning, starting from an identical baseline, is what allows for a direct and fair comparison of the hypotheses. Any difference in final performance can be attributed directly to how well the linguistic constraints fit the underlying data.

### 3.3 A Framework for Evaluating Linguistic Plausibility

The greatest challenge in this field is the impossibility of calculating a simple "accuracy" score, as there is no ground truth to compare against. Any claim of decipherment is met with skepticism because it cannot be objectively verified.⁵ Therefore, the evaluation of *Indus-GPT* must be based on internal consistency, statistical likelihood, and explanatory power. This requires a suite of metrics designed to compare the performance of the constrained models against each other. The goal is not to ask, "Is the translation correct?" but rather, "Which linguistic theory provides a more probable and coherent explanation for the observed data?"

| Metric | Description | Interpretation |
| :--- | :--- | :--- |
| **Perplexity / Evidence Lower Bound (ELBO)** | Measures the model's ability to predict a held-out test set of inscriptions. A lower score indicates a better statistical fit of the model to the data. | A significantly lower perplexity for the Dravidian-constrained model over the Sanskrit-constrained model would provide strong quantitative evidence in favor of the Dravidian hypothesis. |
| **Grammatical Coherence & Complexity** | Analysis of the size and structure of the grammar induced by the model (e.g., number of production rules, average parse tree depth). | A model that induces a compact, elegant grammar (high explanatory power with low complexity) is more likely to have captured the true underlying structure than one that relies on rote memorization. |
| **Generative Plausibility** | Qualitative evaluation by human experts (linguists, archaeologists) of novel, synthetic inscriptions generated by the trained models. | Assesses the model's ability to generalize beyond the training data and produce structurally sound texts, a hallmark of true language understanding. |
| **Linguistic Feature Alignment** | Checks if the grammatical roles assigned to signs by the model (e.g., suffix, verb) align with the expected patterns of the constraint language family (e.g., suffixes are consistently word-final; verbs appear in final position). | Verifies that the model's internal logic is consistent with the linguistic theory it is supposed to be testing, providing a crucial sanity check on the results. |
**Table 4: Proposed Evaluation Metrics for Linguistic Hypotheses.** This framework provides a rigorous, multi-faceted approach to evaluation that does not depend on a ground-truth translation, shifting the focus to the scientific standard of comparing the explanatory power of competing theories.

***

## IV. Anticipated Results and Pathways to Human-Interpretable Decipherment

The *Indus-GPT* project is not designed to be a black box that outputs a final, definitive translation. Its purpose is to serve as a sophisticated analytical tool that generates probabilistic evidence and augments the capabilities of human experts. The anticipated results must be understood within this collaborative framework.

### 4.1 From Probability to Plausibility: The Nature of the Output

The primary outputs of the *Indus-GPT* system will be multi-layered and probabilistic, designed for interpretation by scholars rather than for direct public consumption.

* **Primary Output: A Ranked Linguistic Hypothesis**: The most significant result will be a quantitative comparison of the linguistic hypotheses, based on the evaluation metrics outlined in Section III. The outcome would be a statement such as: "The Indus script's structure, as represented in the known corpus, is X times more likely to be explained by a model constrained with an agglutinative grammar (akin to Proto-Dravidian) than by one constrained with an inflectional grammar (akin to Vedic Sanskrit), as measured by the perplexity on a held-out test set." This provides a data-driven, falsifiable ranking of the major theories.
* **Secondary Output: An Induced Grammar**: For the most plausible language family, the system will output the grammar it has induced. This would take the form of a set of probabilistic production rules (for a constituency grammar) or a lexicon of dependency relations (for a dependency grammar). This formal grammar, the first of its kind derived from the entire corpus using advanced neural methods, could be studied by linguists to understand the deep syntactic structures of the language.
* **Tertiary Output: A Probabilistic Lexicon**: The dual decoder will produce a partial, probabilistic lexicon of sign functions. This would not be a simple dictionary but a set of hypotheses, for example: "Under the Dravidian-constrained model, Sign #48 has a 75% probability of functioning as a dative case marker and a 10% probability of being a logogram for 'water vessel'." This provides concrete, testable assignments for individual signs that can guide further research.

### 4.2 The Human-in-the-Loop Paradigm: Augmenting Expertise

The most successful applications of artificial intelligence in complex scientific and humanistic domains are not those that attempt to replace human experts, but those that function as powerful tools to augment their abilities.¹² A machine learning model can process data at a scale and speed unimaginable for a human scholar, identifying subtle statistical patterns across thousands of fragmented texts.²² However, it lacks the cultural, historical, and contextual knowledge that is the hallmark of human expertise.²²

*Indus-GPT* is explicitly designed to operate within this collaborative, human-in-the-loop paradigm. It functions as a "computational research assistant." The model's role is to perform a massive, unbiased analysis of the entire corpus and generate a ranked list of high-probability hypotheses. For example, it might propose that "Sign #72 consistently appears in a grammatical position consistent with a plural marker in the Dravidian-constrained model."

A human linguist can then take this specific, machine-generated hypothesis and perform a targeted, traditional linguistic analysis to confirm, refute, or refine it. They can examine the contexts in which Sign #72 appears, compare it with known plural markers in Dravidian languages, and assess its plausibility based on their deep domain knowledge. The results of this human validation can then be fed back into the system as a new, stronger constraint, allowing for an iterative refinement of the model. This creates a virtuous cycle of computational discovery and human verification, where the strengths of both machine and expert are leveraged to their fullest potential. This approach frames *Indus-GPT* not as a "decipherment machine" but as a "hypothesis generator" and "computational microscope" for the next generation of Indus scholarship.

### 4.3 Visualizing Structure: New Windows into the Script

A key benefit of using deep learning models is their ability to learn rich internal representations of data, which can be visualized to provide novel insights that are not immediately apparent from the raw data.

* **Latent Space Visualization**: The continuous latent space learned by the Variational Sign Encoder (VSE) can be projected into two or three dimensions and visualized. This would create a "map" of the Indus signs, where signs that are visually and, potentially, functionally similar would cluster together. This could reveal previously unnoticed relationships between signs, such as identifying all variants of a base sign or grouping signs that share common structural motifs.
* **Parse Tree Visualization**: The grammatical structures induced by the Transformer core can be rendered graphically as parse trees for any given inscription. This would allow researchers to visually inspect the syntactic structure that the model believes underlies the texts. Seeing a sentence like "Sign A, Sign B, Sign C" rendered as a tree where [Sign B, Sign C] form a constituent that is then modified by Sign A makes the abstract grammatical rules learned by the model concrete and intuitive, facilitating deeper analysis by linguists.

***

## Conclusion: A New Rosetta Stone Forged in Silicon

This report has laid out the architectural blueprint for *Indus-GPT*, a novel computational framework conceived to address one of the last great undeciphered scripts of the ancient world. For a century, the mystery of the Indus script has been defined by what it lacks: a bilingual key, long inscriptions, and a known linguistic affiliation. *Indus-GPT* proposes to reframe this challenge by leveraging what we now possess: a substantial digital corpus of inscriptions and powerful machine learning techniques capable of inferring global structure from sparse, local evidence.

The novelty of this approach lies in its hybrid, multi-stage architecture that systematically integrates four key innovations:

1.  **Robust Visual Symbol Embedding**: Moving beyond treating signs as arbitrary tokens by using a Convolutional VAE to create visually-grounded representations that respect the script's pictographic and composite nature.
2.  **Unsupervised Grammar Induction**: Employing a Structured Transformer to learn the latent syntactic rules of the script from the entire corpus of short, fragmented texts.
3.  **A Formal Hypothesis-Testing Framework**: Transforming the model into a scientific instrument by using a Linguistic Constraint Module to quantitatively compare the plausibility of competing theories about the script's language family.
4.  **Explicit Logo-Syllabic Modeling**: Utilizing a dual-headed decoder to directly address the likely mixed nature of the writing system.

*Indus-GPT* fundamentally shifts the paradigm of decipherment. It moves away from the speculative and often unfalsifiable claims that have characterized the field and toward a rigorous, data-driven methodology. By transforming long-standing linguistic theories into testable mathematical constraints, it provides a viable path to evaluating the most plausible linguistic identity of the Harappan people. Ultimately, this approach does not seek to replace the human scholar but to empower them with a tool of unprecedented analytical power. It represents a new model for how bespoke artificial intelligence can be harnessed to resolve the great unsolved mysteries of the human past, forging a powerful and essential synergy between the computational sciences and the humanities.

***

## Works Cited

1.  Indus Script: A Study of its Sign Design - Harappa, accessed July 8, 2025, `https://www.harappa.com/sites/default/files/pdf/Indus-sign-design.pdf`
2.  Indus Valley Script - Only IAS, accessed July 8, 2025, `https://pwonlyias.com/current-affairs/indus-valley-script/`
3.  Indus Script - PMF IAS, accessed July 8, 2025, `https://www.pmfias.com/indus-script/`
4.  Indus Script, Evolution, Features, Structure, UPSC Notes, accessed July 8, 2025, `https://vajiramandravi.com/upsc-exam/indus-script/`
5.  4,000-year-old Indus script enigma waiting to be decoded: Will AI unlock the ancient mystery? | - The Times of India, accessed July 8, 2025, `https://timesofindia.indiatimes.com/science/4000-year-old-indus-script-enigma-waiting-to-be-decoded-will-ai-unlock-the-ancient-mystery/articleshow/118124829.cms`
6.  Why couldn't anyone decipher Indus valley script? : r/AskHistorians - Reddit, accessed July 8, 2025, `https://www.reddit.com/r/AskHistorians/comments/dez98s/why_couldnt_anyone_decipher_indus_valley_script/`
7.  Cracking the Code: The Quest to Decipher the Indus Valley Script - History Guild, accessed July 8, 2025, `https://historyguild.org/cracking-the-code-the-quest-to-decipher-the-indus-valley-script/`
8.  (PDF) Corpus of Indus Inscriptions - ResearchGate, accessed July 8, 2025, `https://www.researchgate.net/publication/373522666_Corpus_of_Indus_Inscriptions`
9.  Indus Valley Script - Unacademy, accessed July 8, 2025, `https://unacademy.com/content/railway-exam/study-material/general-awareness/indus-valley-script/`
10. Indus Script - World History Encyclopedia, accessed July 8, 2025, `https://www.worldhistory.org/Indus_Script/`
11. Indus script - Wikipedia, accessed July 8, 2025, `https://en.wikipedia.org/wiki/Indus_script`
12. Machine Learning for Ancient Languages: A Survey | Computational ..., accessed July 8, 2025, `https://direct.mit.edu/coli/article/49/3/703/116160/Machine-Learning-for-Ancient-Languages-A-Survey`
13. What are the major characteristics of Dravidian languages? - Quora, accessed July 8, 2025, `https://www.quora.com/What-are-the-major-characteristics-of-Dravidian-languages`
14. Dravidian Language Family - Structure & Dialects - MustGo.com, accessed July 8, 2025, `https://www.mustgo.com/worldlanguages/dravidian-language-family/`
15. Dravidian languages - Grammar, Changes, Structure | Britannica, accessed July 8, 2025, `https://www.britannica.com/topic/Dravidian-languages/Grammatical-features-and-changes`
16. Indus Valley Script Deciphered , Opinions?! : r/Dravidiology - Reddit, accessed July 8, 2025, `https://www.reddit.com/r/Dravidiology/comments/1gc5aj7/indus_valley_script_deciphered_opinions/`
17. The Indus Script Finally Deciphered - Ancient Indians, accessed July 8, 2025, `https://ancientindians.org/the-indus-script-finally-deciphered/`
18. Middle Indo-Aryan languages - Wikipedia, accessed July 8, 2025, `https://en.wikipedia.org/wiki/Middle_Indo-Aryan_languages`
19. Vedic Sanskrit grammar - Wikipedia, accessed July 8, 2025, `https://en.wikipedia.org/wiki/Vedic_Sanskrit_grammar`
20. Characteristics of the modern Indo-Aryan languages | Britannica, accessed July 8, 2025, `https://www.britannica.com/topic/Indo-Aryan-languages/Characteristics-of-the-modern-Indo-Aryan-languages`
21. Dravidian Languages and its Fundamental Grammar - world wide journals, accessed July 8, 2025, `https://www.worldwidejournals.com/paripex/recent_issues_pdf/2014/February/February_2014_1392717996_0c336_53.pdf`
22. Is Machine Learning Capable of Decoding Ancient Languages and Scripts? | Women in Tech Network, accessed July 8, 2025, `https://www.womentech.net/how-to/machine-learning-capable-decoding-ancient-languages-and-scripts`
23. MIT Researchers use Machine Learning to Translate Dead Languages, accessed July 8, 2025, `https://community.element14.com/technologies/test-and-measurement/b/blog/posts/mit-researchers-use-machine-learning-to-translate-dead-languages`
24. Dead Languages Come to Life - Communications of the ACM, accessed July 8, 2025, `https://cacm.acm.org/news/dead-languages-come-to-life/`
25. Translating lost languages using machine learning | MIT News, accessed July 8, 2025, `https://news.mit.edu/2020/translating-lost-languages-using-machine-learning-1021`
26. A Hybrid Convolutional Variational Autoencoder for Text Generation, accessed July 8, 2025, `https://arxiv.org/abs/1702.02390`
27. [1906.02691] An Introduction to Variational Autoencoders - ar5iv, accessed July 8, 2025, `https://ar5iv.labs.arxiv.org/html/1906.02691`
28. Tutorial on Variational Autoencoders - arXiv, accessed July 8, 2025, `https://arxiv.org/pdf/1606.05908`
29. [D] What are the pros and cons of using a VAE to provide a latent space for generative modelling? (especially for images or video) - Reddit, accessed July 8, 2025, `https://www.reddit.com/r/MachineLearning/comments/1g0jpzq/d_what_are_the_pros_and_cons_of_using_a_vae_to/`
30. Leveraging Grammar Induction for Language Understanding and Generation - arXiv, accessed July 8, 2025, `https://arxiv.org/html/2410.04878`
31. [2403.08293] Generative Pretrained Structured Transformers: Unsupervised Syntactic Language Models at Scale - arXiv, accessed July 8, 2025, `https://arxiv.org/abs/2403.08293`
32. Generative Pretrained Structured Transformers: Unsupervised Syntactic Language Models at Scale - ACL Anthology, accessed July 8, 2025, `https://aclanthology.org/2024.acl-long.145.pdf`
33. Transformer Grammars: Augmenting Transformer Language Models with Syntactic Inductive Biases at Scale | Transactions of the Association for Computational Linguistics - MIT Press Direct, accessed July 8, 2025, `https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00526/114315/Transformer-Grammars-Augmenting-Transformer`
34. arXiv:2311.17633v1 [cs.CL] 29 Nov 2023, accessed July 8, 2025, `https://arxiv.org/pdf/2311.17633`
35. Corpus of Indus Inscriptions [I] | Harappa, accessed July 8, 2025, `https://www.harappa.com/content/corpus-indus-inscriptions-i`
36. Corpus of Indus seals and inscriptions - Catalog - UW-Madison Libraries, accessed July 8, 2025, `https://search.library.wisc.edu/catalog/999596733002121`
37. Corpus of Indus Seals and Inscriptions, accessed July 8, 2025, `https://archive.org/download/TheIndusScript.TextConcordanceAndTablesIravathanMahadevan/Corpus%20of%20Indus%20Seals%20and%20Inscriptions.%20Collections%20in%20India.pdf`
