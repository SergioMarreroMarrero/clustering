---


---

<p>1.<strong>Preprocess</strong></p>
<p>It is important to differentiate the <em>segmentation variables (active variables)</em>. For example, a missing value in an <em>active variable</em> must be removed, but in the other variables could be removed or not (because is not crucial for running the model or any other important computation).</p>
<p>2.1. Missing Values:</p>
<ul>
<li>Missing value have been performed only in active variables .</li>
<li>The techique used for missin value imputation is <em>Complete Case Analsys</em>. That is because a segmentation problem is very sensitive to the values of the variable. If a variable contains to many missing value, then this variable is discarded as a segmentation variable.</li>
</ul>
<p>2.2. Numeric Variables:<br>
Outliers Treatment:</p>
<ul>
<li>Quantile Outliers: Remove data under/over a quantile</li>
<li>IQR: Remove data under X times the Interquantile Range.</li>
</ul>
<p>Standarizations:</p>
<ul>
<li>The numeric variables must be standarized in order to put all in the same order.</li>
<li>At this moment is coded the z-standarization (x-avg)/sd</li>
<li>Other standarization methods more robusts to outliers  are reccomended in the literature in order to do the standarization more robust to outliers (think that avg and sd are outlier-depent)</li>
</ul>
<p>Transformation:<br>
For some variables some transformation could be reccomended (carefully)</p>
<pre><code> Mobility
 logaritmic transformation (this transformation make short the distance of customer that are in the same order (10, 100, 1000...))
</code></pre>
<p>2.3 Categorical Variables: (There is too much to do)</p>
<p>Categorical Variables are problematic for segmentation (luckly we don’t have too much).</p>
<p>Outlier Treatment:<br>
<em>Rare labels encoding:</em><br>
If there are some predominant variables, the other variables with a proportion less than X% cand be relabeld as ‘Other’.</p>
<pre><code>This rare label encoding technique is not reccomended for variables like: most_frequen_route, because all labels are low frequency. For this variable I reccomend encode the variable using a technique named frequency encoding. 
</code></pre>
<p>Categorical Encoding:<br>
Be aware that:</p>
<ul>
<li>the <em>categorical encoding</em> technique depend of the model using for segmentation</li>
<li>when perform the categorical encoding, the distances could not be too much representative and make distorsions in the algorithms (pca, kmeans, etc.)</li>
</ul>
<p>In general the model requires all the feature as numeric, in such case:</p>
<ul>
<li>
<p>If doesn’t exist any order in the labels, <strong>and the cardinality is low</strong> then encoding the variable with one hot encoding.</p>
</li>
<li>
<p>If exists an order, then label it with such numeric order. (Basic, Premium, Super Premium)-&gt; (0,1,2)</p>
</li>
<li>
<p>The frequency encoder can be used with variables with high cardinality and if It  makes sense. For example, two important routes will have high frequency, so they both will be located close to each other in the relative frequency space.</p>
</li>
</ul>
<p>If the model used for segment is <strong>k-prototypes</strong> then is not needed to encode the categorical variables. <strong>k-prototypes</strong> use k-means for numeric and k-modes for categorical variables.</p>
<p>Another techinque that could be done is a <strong>Multi Correspondece Analysis (MCA)</strong> (This is not done). This technique is equivalente to PCA and map the categorical variables to a numeric space.</p>
<ol start="2">
<li>
<p><strong>Exploratory Factor Analysis</strong>:</p>
<p>This analysis is specially util for understand the labels of the clusters on the PCA space.</p>
<ul>
<li>Eigenvalues:
<ul>
<li>Eigenvalue/variance plot (discard less than 1)</li>
<li>Percentage expleined variance</li>
</ul>
</li>
<li>Heatmaps:
<ul>
<li>Correlation Matrix</li>
<li>Load Factor Matrix</li>
<li>Cosine Squared Matrix</li>
<li>Component Explained Matrix.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong>Clustering</strong></p>
</li>
</ol>
<p>3.1 Clustering Models:</p>
<ul>
<li>Distance Based Methods:
<ul>
<li>
<p>Partitioning Methods:</p>
<ul>
<li>k-means:
<ul>
<li>It is implemented in sktlearn</li>
<li>It is very sensible to outliers</li>
</ul>
</li>
<li>k-medoids:
<ul>
<li>It is implemented in pyclustering</li>
<li>More robust to outliers than k-means</li>
<li>Instead of calculate the average, look for the customer in the center of the cluster (the medoid)</li>
</ul>
</li>
<li>k-median:
<ul>
<li>It is implemented in pyclustering</li>
<li>More robust to outliers than k-means<br>
-k-modes:</li>
<li>It is implemented in the package KMODES</li>
<li>It is used for categorical variables<br>
-k-prototypes:</li>
<li>This is a combination of KMeans + KModes</li>
<li>It is implemented in KModes</li>
</ul>
</li>
</ul>
</li>
<li>
<p>Hierarchical Methods:</p>
</li>
<li>
<p>Others:</p>
<ul>
<li>Two step clustering (To research)</li>
</ul>
</li>
</ul>
</li>
</ul>
<p>3.2 Clustering Strategies:</p>
<p>Any clustering methods can be performed combining different techniques:</p>
<ul>
<li>PCA + K-means/median/medoid</li>
</ul>
<p>3.3 Cluster Tendency Assesment:<br>
The clustering tendency assesment determines whether a given data set has a non-random structure, which may lead to meaningful clusters.</p>
<p>Two techinques have been used to perform this step. Both techinques with the package pyclustertend.</p>
<ul>
<li>Hopkins Statistc</li>
<li>Visual assesment cluster tendency (VAT)</li>
</ul>
<p>3.4 Determining the number of clusters:</p>
<p>Take into account that given that doesn’t exist any <strong>natural cluster structure</strong> in our data (which is usual in customer data) selecting the right number of clusters should be done carefully.</p>
<p>At this moment we have: (scree plot)</p>
<ul>
<li>Inertial plot (Elbow method)</li>
<li>Silhouette average (the better the maxium point)</li>
<li>GAP statistc (package OptimalK)</li>
</ul>
<p>Other techiniques are based on consistency of the segmentation in random partion of the data of LIKE-CROSS-VALIDATION process. The idea behind is: if I repeat the same process in another random set…there is a number of cluster where the results are more consistent?.</p>
<p>3.5 Cluster Quality:<br>
Given a number of clusters, we want to see the quality of the clusters:</p>
<ul>
<li>Silhouette Analysis.</li>
</ul>
<p>3.6 Cluster Visualization:<br>
The points of the data set can be projected in a PCA space.</p>
<ul>
<li>2d visualizations</li>
<li>3d visualizations</li>
<li>Matrix Plot visualizations</li>
</ul>
<p>For understand what is the meaning of the different axes is needed to see the different heatmaps of the EFA analysis.</p>
<ol start="4">
<li>Profiling Cluster:</li>
</ol>
<ul>
<li>Look at the distributions (histograms)</li>
<li>Summary by clusters and calculate statistics</li>
<li>Radar plots</li>
</ul>

