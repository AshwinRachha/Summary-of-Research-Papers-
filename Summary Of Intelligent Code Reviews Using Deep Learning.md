# Summary Of Intelligent Code Reviews Using Deep Learning
# Intelligent Code Reviews

I just learnt about the importance of Code Reviews and some automated Static and Dynamic code analysis methods and tools which could be used to achieve the Code Review process. Lets see some intelligent code review literature in the Deep Learning world.

**https://www.kdd.org/kdd2018/files/deep-learning-day/DLDay18_paper_40.pdf**

### Summary of Above paper

- They build a deep learning based system in order to recommend a review of the common issues in the codebase. The system is called **DeepCodeReviewer (DCR)** and uses deep learning to learn review relevance to a code snippet and recommend the right review. 
- DCR has been trained from Historical Code Reviews from Microsofts Internal Repositories.
- Studies in retrospect show that reviewers tend to focus on reviews related to apparent bugs or best practices. These commonplace bugs distract reviewers from some areas of the code which are rare bugs in the program and takes a lot of developer time. DCR can alleviate this issue by recommending reviews associated with these common issues and let reviewers perform code on the important code with **high focus on essential defects**
- The researchers have generated a dataset based on previous pull requests. For any new Pull Request, they first chunked the program into small code snippets and selected a set of review candidates from the generated review repository. Finally, they used an LSTM model to predict the most relevant review of the current code snipped. 

### Their Propsed Method.

- The researchers isolated and created a dataset from their historical repositories of codes and their corresponding reviews and created a tuple of (code, review) pairs.
- They fed these pairs as input to the LSTM model which produces a score that indicates the relevance of each review and its corresponding snippet. 
- For preprocessing they removed noise from the code and review pairs and converted each into a sequence to feed to the LSTM. They used a **Lexer Tokenizer** in order to convert codes into a list of (token name, value). Alternatively they used the **Tweet Tokenizer ** from the **NLTK** package to tokenize the review comments. 
- They converted sequences were vectorized using the word2vec model.
- To generate the input data they create relevant +ve and non-relevant -ve tuples of codes and reviews. The historical PRs only contained +ve reviews so they had to synthesize -ve reviews by themselves.

- General workflow:
  1. When a new PR comes, DCR starts by splitting code files into smaller code snippets.
  2. For each code snippet, a set of candidate reviews from a repository of reviews are found. 3. Code snippets are paired with each candidate review to create tuples. 4. Preprocessing steps take place. 5. Pass tuples to the model to calculate the relevance score for each candidate. 6. Reviews that cross a certain threshold are the DCR’s recommendations for a code snippet.
- Candidate review selection: First, all parts(upper, current, lower) of the new code snippets will be feed through the LSTMs to get the encoded representation of them. Then, the cosine similarity between the new and all the code snippets in the repository (for all the three parts individually) will be calculated. Finally, the reviews from code snippets similar to new code snippets will be selected as candidates.
- Results
  - They used the TF-IDF and logistic regression method as their baseline.
  - They randomly generated 49 -ve pairs for each positive pair. Then they calculated the relevance score for all of these 50 pairs and ranked them with that score. They used this ranking to calculate their metrics.
  - They used Mean reciprocal rank measures. Mean reciprocal rank measures the ranking quality by assuming that there exists only one relevant review. Hence it penalizes all other reviews apart from the current one.

 

![img](https://soroushjavdan.github.io/images/DCR.png)

**Aftermath User Study**

- 77% of their user believed this tool could be helpful, and 66% said they would recommend it to their colleague.
