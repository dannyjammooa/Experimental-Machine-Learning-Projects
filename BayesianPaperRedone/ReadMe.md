# **Bayesian Analysis of the Imqmd Model**

### **Instructions**
1.	Download the two csv files

    a.	“e120_bugfix_model_new_mv.csv”
    
    b.	“e120_exp_result.csv”
    
2.	Open the notebook through the google colab link or download the file

3.	When running the notebook, the second cell will ask you to choose a file form a drop down menu from your computer.

    a.	The first upload should be  “e120_bugfix_model_new_mv.csv”
    
    b.	The second upload should be “e120_exp_result.csv”
    
4.	Run the rest of the notebook

If there are any questions, one can write a comment on each cell, through the google colab function of leaving a note.

### **Explanation of the Analysis**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The notebook contains the Bayesian analysis of data from an Imqmd model that tries to simulate data of experimental Heavy-ion 
collision of tin, compared with actual experimental data. We begin by uploading the two data set to the notebook and restructuring 
it in dataframes using Pandas. For the majority of the notebook we will be working with the imqmd data set titled 
“e120_bugfix_model_new_mv.csv”. When we look into the data set, we see that it contains mainly two things, the four inputs with 
Forty-Seven samples and a corresponding thirty-three output(features/dimensions) for each sample. 
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The process we will be using to make our fit and model of the Imqmd data for this analysis will be the gaussian process. However, the gaussian process has a hard time creating a best fit when working with a data set with such high dimensionality. Thus before working running our data through the gaussian process, we will need to reduce the dimensionality of the output data. To do so, we will be using the mathematical concept of Principal Component Analysis (PCA) for our dimensionality reduction. PCA calculates a covariance matrix of the original data set and performs eigenvalue decomposition on the covariance matrix to reduce the dimensionality. For this notebook and problem, we will be reducing the dimensionality from thirty-three to two. However, before we procced to the gaussian process, we will be preprocessing the data to any outliers from our data, which can harm the efficiency of the gaussian process. Outliers can be formed when using PCA, which comes in the form of big eigenvalues that have major implications.
	
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Once the dimensionality is reduced and the data cleaned of outliers, we can begin with creating our model using gaussian process. For the gaussian process, we will be using the kernels that best describe our data, which will be a squared expansional with some additive noise. We input our data through the model, however at this point the gaussian process will have created a poor fit of our data and model. To get a better fit, the kernels chosen for the gaussian process will need its hyperparameters adjusted for this problem/data set. To do so, we will be using the log-marginal likelihood to optimize the hyperparameters. Once optimized, we rerun the gaussian process to get a good fit and model of our data.
	
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Once our model has been constructed, we begin our Bayesian analysis. The method used for our Bayesian analysis is the Markov Chain Monte Carlo (MCMC). A position of our inputs is randomly selected and given a step size they are moved to the right or left. Then we use the metropolis-hasting algorithm to either accept or deny the move. The algorithm is a ratio of the current and proposed position posterior pdf.  To find the posterior pdf, we input the positions’ inputs into the gaussian process, which will grant us a predicted output based on our model, and the covariance matrix. Using both results, we can construct out likelihood function, which in this case is a multivariable gaussian distribution. Combining the likelihood function and the known priors of each input variables, we get our posterior pdf of each position.
	
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Once we run our MCMC for large iteration count, we get record all the accepted positions for the four input variables. Once we have the sampled data, we can begin to plot the data combined with the experimental data. One thing that might be a problem in this notebook is that the Imqmd data only contains forty-seven samples, which can lead to an overfitting problem with our gaussian process. 
