
# Applications of Linear Algebra in Biology and Medicine

Linear algebra provides a framework for analyzing and interpreting complex biological data. Many computational methods in genomics, medical imaging, bioinformatics, and clinical research rely on linear algebra for tasks such as data transformation, dimensionality reduction, and modeling relationships ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=Data%20from%20thousands%20of%20transcription,wide%20expression%20data) ). Below, we explore several key applications of linear algebra in biology and medicine, with real-world examples and Python code demonstrations for each:

## Matrix Operations in Genomics and Gene Expression Analysis

High-throughput genomics experiments (like microarrays or RNA-seq) produce large matrices of data. Typically, **gene expression data** is organized as a matrix with genes as rows and samples (experiments or patients) as columns ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=a%20set%20of%20fold%20changes,there%20is%20an%20obvious%20construction) ). Each entry in this matrix might represent the expression level of a particular gene in a specific sample. Analyzing such data often involves basic matrix operations. For example, one can compare expression profiles by computing dot products (cosine similarity) between gene vectors – the angle between expression vectors offers a way to quantify how similar two gene expression patterns are ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=Here%20we%20present%20a%20framework,of%20a%20basis%20for%20a) ). Matrix algebra operations like addition and scalar multiplication are used for normalization (e.g. subtracting the mean expression from each value) and combining data from multiple experiments.

A practical example is the computation of a **gene signature score** used in diagnostics or prognostics. Researchers often define a risk score as a **weighted sum of expression values** for a set of genes ( [Establishment and Validation of a Gene Signature-Based Prognostic Model to Improve Survival Prediction in Adrenocortical Carcinoma Patients - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC8632466/#:~:text=the%20most%20robust%20prognostic%20markers,LASSO%20Cox%20coefficients%20as%20follows) ). In other words, a weight (coefficient) is assigned to each gene, and each patient's score is calculated by multiplying each gene's expression by its weight and summing the results. This linear combination is a simple matrix-vector multiplication: the gene expression matrix multiplied by a weight vector yields a vector of scores (one per patient). Such scores are used in cancer prognosis models where multiple gene measurements are combined into a single predictive index.

_Example:_ Suppose we have expression levels of three genes (GeneA, GeneB, GeneC) for three patients. We will represent this as a 3×3 matrix and calculate a prognostic score for each patient by multiplying the matrix with a gene-weight vector.

```python
import numpy as np
import pandas as pd

# Gene expression matrix (genes as rows, patients as columns)
df = pd.DataFrame(
    [[1.2, 3.4, 5.6],    # GeneA expression across 3 patients
     [2.1, 0.4, 1.3],    # GeneB expression
     [0.5, 1.5, 2.5]],   # GeneC expression
    index=["GeneA", "GeneB", "GeneC"],
    columns=["Patient1", "Patient2", "Patient3"]
)
print("Gene Expression Matrix (rows=genes, cols=patients):")
print(df)

# Define weights for each gene in the signature (for example, based on their importance)
weights = pd.Series([0.3, 0.5, 0.2], index=df.index)  # weights for GeneA, GeneB, GeneC
print("\nGene weights for risk score:")
print(weights)

# Calculate the risk score for each patient (matrix-vector multiplication)
score = df.T.dot(weights)  # transpose to have patients as rows, then dot with weights
print("\nRisk score per patient (weighted sum of gene expressions):")
print(score)
```

This code creates a small gene expression matrix and a weight vector. The dot product of the matrix with the weight vector yields a score for each patient. In a real study, such a score might represent a prognostic index; for instance, in oncology research, risk scores are calculated this way to stratify patients ( [Establishment and Validation of a Gene Signature-Based Prognostic Model to Improve Survival Prediction in Adrenocortical Carcinoma Patients - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC8632466/#:~:text=the%20most%20robust%20prognostic%20markers,LASSO%20Cox%20coefficients%20as%20follows) ). The linear algebra operation behind the scenes is a sum of products (matrix multiplication), illustrating how a simple matrix operation can combine information from multiple genes.

## Eigenvalues and Eigenvectors in Medical Imaging (PCA in MRI/CT Scans)

In medical imaging, data is often high-dimensional (an MRI or CT scan can contain millions of pixels or voxels). **Principal Component Analysis (PCA)**, a linear algebra technique, is widely used to reduce the dimensionality of imaging data. PCA works by finding the **eigenvectors** and **eigenvalues** of the data's covariance matrix – the eigenvectors (principal components) define directions of maximum variance, and the corresponding eigenvalues indicate the amount of variance in each direction. By projecting images onto the top principal components, one can achieve compression, noise reduction, or feature extraction. For example, PCA is used in MRI analysis to compress images while retaining essential information, making visualization and analysis easier ([Principal Component Analysis (PCA) in R Tutorial | DataCamp](https://www.datacamp.com/tutorial/pca-analysis-r#:~:text=Healthcare)). In practice, this means that a large set of MRI images can be represented by a few eigen-images (eigenvectors shaped like images) with minimal loss of detail. This technique can also assist in tasks like recognizing patterns or disease signatures in scans.

_Example:_ To illustrate PCA, let's create a synthetic dataset representing imaging data and perform PCA on it. We simulate three highly correlated features (which we can imagine as three pixel intensity readings) across many "scans," then use PCA to find the principal components.

```python
import numpy as np
from sklearn.decomposition import PCA

np.random.seed(0)
# Simulate data for 50 "scans" with 3 features (e.g., 3 pixels or measures) each
N = 50
# Create correlated features:
feature1 = np.random.normal(0, 1, size=N)
feature2 = 0.8 * feature1 + np.random.normal(0, 0.2, size=N)  # strongly correlated with feature1
feature3 = np.random.normal(0, 0.5, size=N)                   # independent noise feature
# Combine into data matrix (N samples x 3 features)
X = np.column_stack([feature1, feature2, feature3])

# Perform PCA
pca = PCA(n_components=3)
pca.fit(X)
print("Explained variance by each principal component:", pca.explained_variance_)
print("Principal components (eigenvectors):")
print(pca.components_)
```

In this code, we construct a data matrix `X` with 50 samples and 3 features. Features 1 and 2 are highly correlated, so we expect PCA to find one principal component capturing their shared variance. The output shows the **explained variance** for each principal component (these are proportional to the eigenvalues of the covariance matrix) and the principal component vectors (eigenvectors). Typically, the first principal component will have a much larger variance than the others due to the correlation between features 1 and 2. This mirrors what happens in imaging: for instance, if MRI scans have patterns common across images, PCA will capture those in the top components, effectively denoising and reducing redundancy. In fact, PCA-based compression is used to reduce MRI data for faster processing while preserving critical information ([Principal Component Analysis (PCA) in R Tutorial | DataCamp](https://www.datacamp.com/tutorial/pca-analysis-r#:~:text=Healthcare)).

## Singular Value Decomposition (SVD) in Dimensionality Reduction for High-Throughput Biological Data

Biological datasets with thousands of features (genes, proteins, etc.) often contain underlying structure and redundancy. **Singular Value Decomposition (SVD)** is a factorization of a matrix into three components (U, D, V^T) that reveals important properties and patterns in the data ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=SVD%20is%20a%20matrix%20factorization,can%20obtain%20the%20following%20factorization) ). In genomics, SVD is used for **dimensionality reduction**: it can identify a small number of composite patterns (sometimes called “eigengenes” or “eigenprofiles”) that explain most of the variation in gene expression datasets ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=vectors,SVD) ). By focusing on the largest singular values (and their corresponding singular vectors), researchers can separate signal from noise. For example, applying SVD to a genome-wide expression matrix of yeast cell cycle data revealed that the first singular vectors corresponded to a steady-state expression pattern, and subsequent vectors captured oscillatory behavior expected from cell-cycle dynamics ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=For%20microarray%20data%2C%20SVD%20can,also%20be%20used%20to%20%27de) ). This means SVD distilled thousands of gene measurements into a few patterns that described the dominant biological processes in the experiment.

Beyond gene expression, SVD (and related methods like principal components analysis) is used in other high-throughput data scenarios – from proteomics to metabolomics – to **denoise data, reduce dimensionality, and highlight latent factors**. A well-known early application was using SVD to process DNA microarray data, showing that only a few “principal” gene expression patterns account for most of the information ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=Here%20we%20present%20a%20framework,of%20a%20basis%20for%20a) ). This helps in visualization (e.g., plotting samples in a low-dimensional space) and in machine learning tasks by mitigating the curse of dimensionality.

_Example:_ We will demonstrate SVD on a synthetic gene expression matrix. Imagine we have 100 genes (rows) measured across 50 experiments or samples (columns). We construct the data such that there are really only two underlying patterns influencing all genes (rank ~2), plus a little random noise. SVD should identify two large singular values corresponding to these patterns, with the rest of the singular values being much smaller (noise).

```python
import numpy as np

np.random.seed(42)
n_genes, n_samples = 100, 50

# Create two underlying gene expression patterns (latent factors)
gene_pattern1 = np.random.normal(size=n_genes)
gene_pattern2 = np.random.normal(size=n_genes)
# Create corresponding experiment loading patterns
sample_pattern1 = np.random.normal(size=n_samples)
sample_pattern2 = np.random.normal(size=n_samples)
# Construct the data matrix as a combination of two rank-1 matrices (plus noise)
data_matrix = np.outer(gene_pattern1, sample_pattern1) + np.outer(gene_pattern2, sample_pattern2)
data_matrix += np.random.normal(scale=0.1, size=(n_genes, n_samples))  # add small noise

# Perform SVD
U, s, Vt = np.linalg.svd(data_matrix, full_matrices=False)
print("Top 5 singular values:", s[:5])
```

After constructing the matrix with rank ~2, we perform SVD. The output shows the top singular values. We expect to see that the first two singular values are significantly larger than the rest. Indeed, the result might look like: `Top 5 singular values: [75.1, 63.4, 1.6, 1.5, 1.5, ...]` (actual values will vary due to randomness). The first two singular values dominate, reflecting the two true patterns we embedded, whereas the remaining singular values are very small (close to the noise level). In real high-throughput biological data, a rapid drop-off in singular values indicates that a few latent factors explain most of the variance ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=called%20the%20singular%20values%20of,they%20all%20are%20one) ) ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=For%20microarray%20data%2C%20SVD%20can,also%20be%20used%20to%20%27de) ). Researchers can retain those top factors for further analysis, thereby reducing dimensionality. This is the basis of PCA and other algorithms used on gene expression matrices to identify major gene expression modes or correct for batch effects.

## Linear Regression and Least Squares Methods in Clinical Research and Drug Response Modeling

**Linear regression** is a fundamental statistical tool in clinical research for modeling relationships between variables. In its simplest form, linear regression fits a straight line (or hyperplane in higher dimensions) to data points in a way that minimizes the sum of squared errors (the **least squares** criterion). This is essentially solving a linear algebra problem: finding the coefficient vector _β_ that best satisfies $Xβ \approx y$ (where _X_ is the matrix of input features and _y_ is the outcome vector) in a least-squares sense. The normal equation solution is $β = (X^T X)^{-1}X^T y$, which relies on matrix operations and inverses. In practice, linear regression is used to examine or predict outcomes based on one or more predictor variables.

In clinical and biomedical research, linear regression is widely applied. For example, researchers may use it to model how a patient's blood pressure responds to different doses of a drug, or how an outcome like cholesterol level changes with age. Some real-life scenarios include:

- **Drug dosage vs. response:** Modeling blood pressure reduction (outcome) as a function of the dose of a new antihypertensive drug (predictor).
- **Clinical measurements vs. patient attributes:** Relating cholesterol level to a patient's age, or pain relief score to the time after administering a painkiller.
- **Treatment effect modeling:** Predicting the degree of wound healing based on the initial wound size.

In all these cases, linear regression provides an equation (line) that best fits the observed data ([](https://www.unanijournal.com/articles/15/1-1-14-773.pdf#:~:text=might%20be%20useful%20in%20clinical,calculation%20of%20the%20relationship%20between)). In pharmacology and oncology, linear models are often a starting point for drug response modeling – for instance, predicting tumor shrinkage or patient survival from baseline measurements or treatment doses. While many dose-response relationships are nonlinear, linear regression and its extensions (or linear approximations) are used for simplicity or for initial analysis.

_Example:_ Suppose we want to model the relationship between drug dose and tumor size reduction in a simplistic scenario. We’ll generate some synthetic data for dose (X) and response (Y) where the true relationship is roughly linear, then use linear regression to fit a line and retrieve its parameters.

```python
import numpy as np
from sklearn.linear_model import LinearRegression

np.random.seed(0)
# Generate synthetic data: 10 patients with different drug doses (in arbitrary units)
doses = np.random.uniform(0, 50, 10)        # predictor (e.g., dose)
# Simulate responses (e.g., tumor size reduction in mm) with an underlying linear relationship plus noise
true_intercept = 5.0
true_slope = 2.0
responses = true_intercept + true_slope * doses + np.random.normal(0, 5, size=10)

# Fit a linear regression model
X = doses.reshape(-1, 1)  # reshape for sklearn (10x1 matrix)
model = LinearRegression().fit(X, responses)

print("Fitted intercept:", model.intercept_)
print("Fitted slope:", model.coef_[0])
```

Here, we created a random set of doses and generated responses using `response = 5 + 2 * dose + noise`. The linear regression model should recover coefficients close to 5 (intercept) and 2 (slope). Indeed, the output might be:

```
Fitted intercept: 6.77  (approximately 5, within noise)
Fitted slope: 2.00      (approximately 2)
```

These values indicate the best-fit line is roughly `response ≈ 6.77 + 2.00 * dose`. The fitting process used linear algebra under the hood (specifically, a least-squares solution). With this model, we could predict the response for a new dose. For instance, a dose of 30 (in the same units) would give `response ≈ 6.77 + 2*30 ≈ 66.8`. Linear regression models like this enable researchers to interpret the influence of predictors on outcomes and make predictions. In clinical research, using regression analysis in this way helps quantify associations and can guide dosing decisions or identify risk factors ([](https://www.unanijournal.com/articles/15/1-1-14-773.pdf#:~:text=might%20be%20useful%20in%20clinical,calculation%20of%20the%20relationship%20between)). More complex scenarios might involve multiple predictors (multivariable linear regression) or require logistic regression if the outcome is binary, but the underlying principle of fitting coefficients via linear algebra remains similar.

## Network Analysis and Graph Theory in Protein Interaction Networks

Biological interactions can be naturally modeled as networks (graphs). For example, a **protein-protein interaction (PPI) network** represents proteins as nodes and their physical or functional interactions as edges. Analyzing these networks often leverages linear algebra through the use of **adjacency matrices** and matrix operations. Any network can be represented by an adjacency matrix _A_, where $A_{ij}$ indicates the connection strength between node _i_ and node _j_ ([Graph theory: adjacency matrices | Network analysis of protein interaction data](https://www.ebi.ac.uk/training/online/courses/network-analysis-of-protein-interaction-data-an-introduction/introduction-to-graph-theory/graph-theory-adjacency-matrices/#:~:text=Every%20network%20can%C2%A0be%20expressed%20mathematically,see%20later%20in%20the%20course)). Once we have this matrix, we can compute various network properties using linear algebra. For instance, the degree of each node (number of interactions) can be obtained by summing rows or columns of the adjacency matrix. More advanced measures like **eigenvector centrality** are defined via linear algebra: eigenvector centrality assigns scores to nodes such that each node’s score is proportional to the sum of its neighbors’ scores – this leads to an eigenvalue problem $A x = \lambda x$. The solution (eigenvector _x_ for the largest eigenvalue) gives the centrality scores. Nodes with high eigenvector centrality are those connected to many other well-connected nodes, indicating they are influential in the network.

In protein interaction networks, these analyses identify key proteins (often called "hubs" or "essential proteins"). Highly connected proteins may be crucial for cellular processes, and their removal can be lethal, a concept known as centrality-lethality in systems biology. Network centrality measures (degree, betweenness, eigenvector, etc.) have been used to prioritize important genes/proteins for further study ([DiffSLC: A graph centrality method to detect essential proteins of a protein-protein interaction network | PLOS One](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0187091#:~:text=Identification%20of%20central%20genes%20and,weighting%20factor%20to%20bias%20the)). For example, if a particular protein has a high eigenvector centrality, it might interact with many other important proteins, making it a potential target for drug therapy or a critical point in a signaling pathway. Graph algorithms and linear algebra thus come together to elucidate the structure of interactomes.

_Example:_ Consider a small protein interaction network of five proteins. We will create a graph, represent it as an adjacency matrix, and compute basic centrality measures using NetworkX (a network analysis library). This will illustrate how linear algebra concepts apply (implicitly) through these computations.

```python
import networkx as nx

# Define a small protein interaction network
G = nx.Graph()
proteins = ["MAPK1", "TP53", "EGFR", "AKT1", "TNF"]  # example protein nodes
G.add_nodes_from(proteins)
# Add interactions (edges) between proteins
edges = [
    ("TP53", "MAPK1"), ("TP53", "EGFR"), ("TP53", "AKT1"),  # TP53 interacts with three others
    ("MAPK1", "EGFR"), ("MAPK1", "AKT1"), ("MAPK1", "TNF"), # MAPK1 is a hub connecting to four proteins
    ("EGFR", "AKT1")  # EGFR interacts with AKT1 (in addition to TP53 and MAPK1)
]
G.add_edges_from(edges)

# Compute degree centrality and eigenvector centrality
deg_cent = nx.degree_centrality(G)
eig_cent = nx.eigenvector_centrality(G)
print("Degree Centrality:")
for node, score in deg_cent.items():
    print(f"{node}: {score:.2f}")
print("\nEigenvector Centrality:")
for node, score in eig_cent.items():
    print(f"{node}: {score:.2f}")
```

In this network:

- **MAPK1** interacts with four other proteins, so it has the highest degree (degree centrality 1.00, meaning 100% of the other nodes are connected to it).
- **TP53**, **EGFR**, and **AKT1** each interact with three others (degree centrality 0.75), and **TNF** interacts with only one (degree 0.25).
- The eigenvector centrality scores rank the nodes similarly: MAPK1 comes out on top (it scores highest at about 0.52), while TP53, EGFR, and AKT1 form the next tier (around 0.48 each), and TNF is much lower (~0.17). These values are the entries of the leading eigenvector of the adjacency matrix.

```
Degree Centrality:
MAPK1: 1.00  
TP53: 0.75  
EGFR: 0.75  
AKT1: 0.75  
TNF: 0.25  

Eigenvector Centrality:
MAPK1: 0.52  
TP53: 0.48  
EGFR: 0.48  
AKT1: 0.48  
TNF: 0.17
```

The results show that **MAPK1** is a hub in this network, which might indicate it’s a critical signaling protein. Indeed, many signaling pathways in cells (e.g., the MAPK/ERK pathway) have hub proteins like MAPK1 that interact with multiple partners. Representing the network as an adjacency matrix and calculating the eigenvector centrality is fundamentally a linear algebra exercise – it requires finding the dominant eigenvector of the matrix ([Graph theory: adjacency matrices | Network analysis of protein interaction data](https://www.ebi.ac.uk/training/online/courses/network-analysis-of-protein-interaction-data-an-introduction/introduction-to-graph-theory/graph-theory-adjacency-matrices/#:~:text=Every%20network%20can%C2%A0be%20expressed%20mathematically,see%20later%20in%20the%20course)). In larger PPI networks studied in research, centrality measures have helped identify essential proteins that could be potential drug targets or that are important for the network’s integrity ([DiffSLC: A graph centrality method to detect essential proteins of a protein-protein interaction network | PLOS One](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0187091#:~:text=Identification%20of%20central%20genes%20and,weighting%20factor%20to%20bias%20the)). This showcases how graph theory and linear algebra together enable insights into biological networks.

## Conclusion

Linear algebra serves as a unifying language across diverse areas of biology and medicine. From the **genomic scale** (where expression data are matrices and techniques like SVD and PCA extract meaningful patterns) to the **organ or organism scale** (where imaging data are decomposed using eigenvectors), and from **molecular networks** (analyzed via adjacency matrices and eigenvalues) to **clinical models** (fitted with regression equations solved by least squares), the concepts of vectors, matrices, and linear transformations are everywhere. These methods not only provide computational efficiency for handling large datasets but also offer deeper insight – revealing hidden structure in data, reducing noise, and pointing to underlying biological principles. As biomedical data continue to grow in size and complexity, linear algebra will remain an indispensable tool in turning data into knowledge, guiding both research and clinical decision-making.

**Sources:**

1. Kuruvilla, F.G., et al. (2002). _Vector algebra in the analysis of genome-wide expression data_. **Genome Biology**, 3(3):research0011 ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=Data%20from%20thousands%20of%20transcription,wide%20expression%20data) ) ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=Here%20we%20present%20a%20framework,of%20a%20basis%20for%20a) )
    
2. Datacamp Tutorial. _Principal Component Analysis in R – Image Processing and Healthcare_ ([Principal Component Analysis (PCA) in R Tutorial | DataCamp](https://www.datacamp.com/tutorial/pca-analysis-r#:~:text=Healthcare))
    
3. Alter, O., et al. (2000). _Singular value decomposition for genome-wide expression data processing and modeling_. **PNAS**, 97(18):10101-10106 ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=called%20the%20singular%20values%20of,they%20all%20are%20one) ) ( [Vector algebra in the analysis of genome-wide expression data - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC88809/#:~:text=For%20microarray%20data%2C%20SVD%20can,also%20be%20used%20to%20%27de) )
    
4. Minitab Blog. _Understanding Linear Regression_ – Real-world examples of regression in clinical studies ([](https://www.unanijournal.com/articles/15/1-1-14-773.pdf#:~:text=might%20be%20useful%20in%20clinical,calculation%20of%20the%20relationship%20between))
    
5. EMBL-EBI Training. _Network analysis of protein interaction data – Adjacency matrices and centrality_ ([Graph theory: adjacency matrices | Network analysis of protein interaction data](https://www.ebi.ac.uk/training/online/courses/network-analysis-of-protein-interaction-data-an-introduction/introduction-to-graph-theory/graph-theory-adjacency-matrices/#:~:text=Every%20network%20can%C2%A0be%20expressed%20mathematically,see%20later%20in%20the%20course))
    
6. Mistry, D. et al. (2017). _DiffSLC: A graph centrality method to detect essential proteins of a protein-protein interaction network_. **PLOS One**, 12(11): e0187091 ([DiffSLC: A graph centrality method to detect essential proteins of a protein-protein interaction network | PLOS One](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0187091#:~:text=Identification%20of%20central%20genes%20and,weighting%20factor%20to%20bias%20the))
    
7. Zitterbart, K. et al. (2021). _Establishment of a Gene Signature-Based Prognostic Model in ACC_. **Cancers**, 13(21):5381 ( [Establishment and Validation of a Gene Signature-Based Prognostic Model to Improve Survival Prediction in Adrenocortical Carcinoma Patients - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC8632466/#:~:text=the%20most%20robust%20prognostic%20markers,LASSO%20Cox%20coefficients%20as%20follows) )