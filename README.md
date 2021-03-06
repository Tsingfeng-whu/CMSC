# CMSC: Collaborative Multi-Domain Sentiment Classification

A matlab implementation of the collaborative multi-domain sentiment classification algorithm.

#Introduction

This source code is designed to implement the collaborative multi-domain sentiment classification approach (CMSC) proposed in reference [1]. The aim of CMSC approach is to train domain-specific sentiment classifiers for multiple domains simultaneously in a collaborative way. The sentiment information in different domains is shared with each other to train more accurate and robust sentiment classifiers for these domains when labeled data is scarce. In CMSC approach, the sentiment classifier of each domain is decomposed into two components, a global one and a domain-specific one. The global model can capture the general sentiment knowledge and is shared by various domains. The domain-specific model can capture the specific sentiment expressions in each domain. CMSC also incorporates the domain-specific sentiment knowledge mined from both labeled and unlabeled samples in each domain to enhance the learning of domain-specific sentiment classifiers. Besides, the similarities between different domains are incorporated into CMSC approach as regularization over the domain-specific sentiment classifiers to encourage the sharing of sentiment information between similar domains.


#Usage

###1. DSSKE.m

>	function [p_m] = DSSKE(X, y, C, theta)

>+ Function Description

>>The goal of this function is to extract domain-specific sentiment knowledge, i.e., the domain-specific sentiment word distributions, from both labeled samples and the contextual similarities mined from massive unlabeled samples. This function contains two major steps. First, extract the initial sentiment word distributions from labeled samples using PMI. Second, propagate the initial sentiment word distributions along the contextual similarities to compute the final domain-specific sentiment word distributions.

>+ Input

>>**X**:   a N*D matrix, represents the feature vectors of labeled samples in a specific domain, where N is the number of labeled samples and D is the dimension of feature vector.

>>**y**:   a N*1 vector, represents the sentiment labels of these labeled samples, where +1 for positive samples and -1 for negative samples.

>>**C**:   a D*D vector, represents the contextual similarities among features mined from massive unlabeled samples.

>>**theta**:   a non-negative real value, represents the parameter to control the relative importance of contextual similarities.

>+ Output

>>**p_m**:   a D*1 vector, represents the domain-specific sentiment word distribution learned by the algorithm.


###2. computeContentBasedDomainSimilarity.m

>	function [similarity] = computeContentBasedDomainSimilarity(X_m, X_n)

>+ Function Description

>>The goal of this function is to compute the domain similarity between two domains based on their textual term distributions according to Jensen-Shannon divergence. 

>+ Input

>>**X_m**:   a N_m*D matrix, represents the feature vectors of both labeled and unlabeled samples in domain m, where N_m is the number of samples in domain m and D is the dimension of feature vector.

>>**X_n**:   a N_n*D matrix, represents the feature vectors of both labeled and unlabeled samples in domain n, where N_n is the number of samples in domain n.

>+ Output

>>**similarity**:   a real value, represents the domain similarity between domains m and n based on their textual term distributions.


###3. computeSentimentBasedDomainSimilarity.m

>	function [similarity] = computeSentimentBasedDomainSimilarity(X_m, X_n)

>+ Function Description

>>The goal of this function is to compute the domain similarity between two domains based on their domain-specific sentiment word distributions. 

>+ Input

>>**p_m**:   a D*1 vector, represents the domain-specific sentiment word distribution of domain m, where D is the dimension of feature vector.

>>**p_n**:   a D*1 vector, represents the domain-specific sentiment word distribution of domain m.

>+ Output

>>**similarity**:   a real value, represents the domain similarity between domains m and n based on their domain-specific sentiment word distributions.


###4. CMSC.m

>	function [w, W] = CMSC(X, y, domain, p, P, S, alpha1, alpha2, beta, lambda1, lambda2, loss_type) 


>+ Function Description

>>The goal of this function is to train domain-specific sentiment classifiers for multiple domains in a collaborative way by exploiting the common sentiment knowledge shared among them. Given a small number of labeled samples in multiple domains, the domain similarities between these domains, the general sentiment knowledge extracted from general-purpose sentiment lexicons, and the domain-specific sentiment knowledge of each domain extracted from both labeled and unlabeled samples, this function will learn a global sentiment model shared by all domains to capture the general sentiment knowlege and a domain-specific sentiment model for each domain to capture the domain-specific sentiment expressions. The final domain-specific sentiment classifier of each domain is the combination of the global sentiment model and their domain-specific sentiment model. 

>+ Input

>>**X**:  a N*D matrix, represents the feature vectors of labeled samples from multiple domains, where N is the number of all labeled samples and D is the dimension of the feature vector.

>>**y**:   a N*1 vector, represents the sentiment labels of these labeled samples, where +1 for positive samples and -1 for negative samples.

>>**domain**:   a N*1 vector, represents the domain index of each labeled sample.

>>**p**:	a D*1 vector, represents the prior sentiment knowledge extracted from general-purpose sentiment lexicons, where +1 for positive sentiment experessions, -1 for negative sentiment experessions, and 0 for others.

>>**P**:	a D*M vector, represents the domain-specific sentiment knowledge of multiple domains, where M is the number of domains to be analyzed. P(:,m) is the domain-specific sentiment knowledge of the m-th domain.

>>**S**:    a M*M vector, represents the domain similarities. S(m,n) represents the domain similarity between domain m and domain n.

>>**alpha1**:  a non-negative real value, controls the relative importance of the prior general sentiment knowledge extracted from general-purpose sentiment lexicons.

>>**alpha2**:  a non-negative real value, controls the relative importance of the domain-specific sentiment knowledge extracted from both labeled and unlabeled samples.

>>**beta**: a non-negative real value, controls the relative importance of domain similarity knowledge.

>>**lambda1**:  a non-negative real value, controls the model complexity.

>>**lambda2**:  a non-negative real value, controls the model sparsity.

>>**loss_type**:  a string, represents the type of loss function used in our approach.

>+ Output

>>**w**: a D*1 vector, represents the global sentiment model shared by multiple domains.

>>**W**: a N*D matrix, represents the domain-specific sentiment models of multiple domains, where W(:,m) is the domain-specific sentiment model of domain m. 


If you have any questions or suggestions on using these source codes, welcome to contact us at wfz12@mails.tsinghua.edu.cn.

#Citation

If you use this package and like it, welcome to cite our manuscript:

[1] Fangzhao Wu, Zhigang Yuan, and Yongfeng Huang. Collaboratively Training Sentiment Classifiers for Multiple Domains. IEEE Transactions on Knowledge and Data Engineering, under review.

