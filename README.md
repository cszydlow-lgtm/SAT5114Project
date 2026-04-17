Student’s Name: Caroline Szydlowski

Title: “From Neighbors to Probabilities: ML Models for Breast Cancer Detection”

Introduction

Breast cancer is the most common form of cancer globally, accounting for 1 in 8 new cancer diagnoses worldwide². Furthermore, it remains the second leading cause of cancer-related deaths among women, with over 600,000 deaths in 2020². Breast cancer can originate in several areas within the breast, including the glandular tissue, fibrous tissue, nipples, and the lymphatic and blood vessels⁷. There are many different types of breast cancer, which are identified based on where the cancer begins and the extent of its spread⁷.

Early detection is a proven strategy for improving breast cancer outcomes. According to the National Cancer Institute⁸, detecting cancer at an early stage allows for more effective treatment and significantly better survival rates. When breast cancer is identified at stage 1, more than 99% of women survive for at least five years, highlighting the critical, lifesaving role of early detection⁴.

The diagnosis of breast cancer typically begins with imaging tests such as diagnostic mammography, breast magnetic resonance imaging (MRI), or breast ultrasound⁷. While these diagnostic tools are beneficial for identifying lumps and abnormalities within breast tissue, no single test guarantees improved health outcomes for patients. Overall, these diagnostic tools, as well as the treatment of later-stage cancer, are costly to both patients and the healthcare system⁴.

In 2020, the total medical cost for breast cancer exceeded $29 billion in the United States⁴. Approximately $26.2 billion was spent on medical services, such as diagnostic tests and radiation, and $3.5 billion on prescription drugs⁴. The CDC divides costs into the initial care phase—the first year of treatment after diagnosis—and the end-of-life phase, which is the final year before death from cancer. The average per-patient cost of medical services during the initial care phase was $35,000, which nearly doubles to $76,100 during the end-of-life phase⁴. These figures highlight the financial impact of breast cancer and underscore the importance of early detection, as later-stage diagnoses often require more extensive and costly treatments.

Statistically, the diagnosis and treatment of breast cancer continue to place a significant burden on both patients and healthcare systems². To reduce this burden and improve long-term patient outcomes, early and accurate detection is essential².Given the variability in diagnostic accuracy associated with current breast cancer diagnostic tools, machine learning (ML) techniques offer a promising solution⁵. These technologies have the potential to analyze abnormalities detected in diagnostic images and improve diagnostic accuracy, thereby supporting clinicians in making timely and informed treatment decisions⁵. Accordingly, this study evaluates the effectiveness of machine learning models in accurately identifying malignant breast tumors based on a comprehensive set of predictive features.


Methods and Results

The Breast Cancer Wisconsin Diagnostic Dataset from the UCI Machine Learning Repository⁹ is a well-known dataset used to train and validate the machine learning models. This dataset has been verified as high-quality through rigorous validation processes and peer-reviewed research conducted by the University of Wisconsin and the University of California, Irvine⁷.
The dataset includes biopsy features for the classification of 569 breast masses as either malignant (cancerous) or benign (non-cancerous)⁹. The class distribution consists of 212 malignant cases and 357 benign cases⁴. The features were computed from digitized images of fine needle aspirate (FNA) biopsies of breast mass tissue⁹.
The dataset contains 30 numerical predictive features used to facilitate cancer diagnosis³,⁹. These features include the mean, standard error, and “worst” (largest) values for each characteristic derived from the FNA images³,⁹. The dataset is structured around nine key predictive attributes, each rated on a numerical scale from 1 to 10⁶,⁹. A tenth attribute, “class,” serves as the target variable, indicating whether the tumor is benign (2) or malignant (4)⁵,⁹.

The nine attributes are³,⁹:
1.	Clump Thickness – Measures the thickness of the cell clump; higher values indicate malignancy. 
2.	Uniformity of Cell Size – Evaluates similarity in cell size; irregularity suggests malignancy. 
3.	Uniformity of Cell Shape – Assesses variation in cell shape; greater variation indicates malignancy. 
4.	Marginal Adhesion – Reflects how well cells adhere; lower adhesion suggests malignancy. 
5.	Single Epithelial Cell Size – Larger epithelial cells are associated with malignancy. 
6.	Bare Nuclei – Counts cells with missing nuclei; higher counts indicate malignancy (16 of 699 original records contained missing values and were removed). 
7.	Bland Chromatin – Describes chromatin texture; irregularity suggests malignancy. 
8.	Normal Nucleoli – Larger nucleoli may indicate malignancy. 
9.	Mitoses – Measures cell division rate; higher rates suggest malignancy. 

During model training, Logistic Regression and K-Nearest Neighbors (KNN) algorithms identify patterns in these features to classify tumors⁶.
The dataset contains a mild class imbalance (~63% benign, 37% malignant). Therefore, the F1-score was selected as the primary evaluation metric rather than accuracy alone, as it accounts for both precision and recall. Oversampling techniques such as SMOTE were not applied because the imbalance was not severe.

The dataset was split into training (80%, 455 instances) and testing (20%, 114 instances) sets³,⁶. A fixed random state of 42 ensures reproducibility³,⁶. Feature scaling was performed using StandardScaler on both training and testing data to prevent data leakage³,⁶. This step is especially important for KNN, which relies on distance calculations, and for preventing features with larger values from dominating the model.

Logistic Regression was selected because the dataset is largely linearly separable based on tumor characteristics such as radius, area, and texture³. This model performs binary classification and outputs probabilities using the sigmoid function³. The sigmoid function converts a weighted sum of input features into a probability between 0 and 1, representing the likelihood of malignancy³.

Logistic Regression Performance Metrics:

Accuracy – The logistic regression model correctly classified 99.1% of malignant tumors.

Precision – The logistic regression model correctly predicted 98.6% of the tumors as malignant.

Recall – The model correctly identified 100% of the malignant tumors.

F1-Score – The score was 0.993 meaning a strong balance between precision and recall. Since there was an imbalance in the data, even though it was small, a high F1-score means the model correctly classified many of the tumor instances. 

AUC Score – The Area Under the Curve score for logistic regression was 0.998 indicating an almost perfect classification ability. 

The confusion matrix shows that all malignant tumors were correctly classified (0 false negatives), and only one benign tumor was misclassified as malignant. In a clinical context, zero false negatives indicate perfect cancer detection within the test set.

K-Nearest Neighbors (KNN) was also implemented due to the clustering tendency of features such as radius and concavity³. KNN classifies samples based on proximity to similar data points and captures non-linear relationships without assuming a data distribution³. Hyperparameter tuning was performed using GridSearchCV with 3-fold cross-validation³,⁶. The optimal model used 7 neighbors with uniform weighting, achieving an F1-score of 0.9711. Increasing the number of neighbors improved generalization, and weighting schemes had minimal impact.

KNN Performance Metrics:

Accuracy – The KNN model correctly classified 94.7% of malignant tumors.

Precision – The KNN model correctly predicted 95.7% of the tumors as malignant.

Recall – The model correctly identified 95.7% of the malignant tumors.

F1-Score – The score was 0.957 meaning a strong balance between precision and recall. Since there was an imbalance in the data, even though it was small, a high F1-score means the model correctly classified many of the tumor instances. 

AUC Score – The Area Under the Curve score for logistic regression was 0.980 indicating a high classification ability by the model.

The KNN model produced 3 false negatives and 3 false positives. In clinical settings, false negatives are particularly concerning, as they represent missed cancer diagnoses. Logistic Regression achieved a 100% detection rate, while KNN achieved 93%.
ROC curves and AUC scores were used to evaluate model performance. The ROC curve plots the true positive rate against the false positive rate at various thresholds². Logistic Regression demonstrated a curve closer to the top-left corner, indicating superior performance compared to KNN³,⁶.

Conclusion

In an article published by Mohammed Amine Naji et al. called Machine Learning Algorithms for Breast Cancer Prediction, the Breast Cancer Wisconsin dataset was used to train a Machine Learning (ML) model using similar algorithms to those used to train the ML model described in this document1. The logistic regression accuracy measure was 95.8%, the F1-score was 0.94, and the AUC score was 0.9471. For KNN, the accuracy measure was 93.7%, the F1-score was 0.91, and the AUC score was 0.9521. According to these metrics, this model outperformed the model discussed in this article.


References
1. Amine Naji M, El Filali S, Aarika K, Benlahmar EH, Abdelouhahid RA, Debauche O. Machine Learning Algorithms for Breast Cancer Prediction and Diagnosis. ScienceDirect. September 8, 2021. Accessed April 17, 2026. https://www.sciencedirect.com/science/article/pii/S1877050921014629. 
2.Arnold M, Morgan E, Rumgay H, et al. Current and future burden of breast cancer: Global statistics for 2020 and 2040. Breast. 2022;66:15-23. doi:10.1016/j.breast.2022.08.010
3. GeeksforGeeks. Breast Cancer Wisconsin (Diagnostic) Dataset. GeeksforGeeks. July 23, 2025. Accessed March 12, 2026. https://www.geeksforgeeks.org/machine-learning/breast-cancer-wisconsin-diagnostic-dataset/. 
4. Health and Economic Benefits of Breast Cancer Interventions. CDC. August 14, 2025. Accessed March 12, 2026. https://www.cdc.gov/nccdphp/priorities/breast-cancer.html. 
5. Moursi A, Aboumadi* A, Qidwai U. AI-Based Breast Cancer Detection System: Deep Learning and machine learning approaches for ultrasound image analysis. MDPI. March 30, 2025. Accessed March 12, 2026. https://www.mdpi.com/2078-2489/16/4/278. 
6. The Wisconsin Breast Cancer Dataset Explained. Biology Insights. July 22, 2025. Accessed March 12, 2026. https://biologyinsights.com/the-wisconsin-breast-cancer-dataset-explained/. 
7. What is Breast Cancer? NCI. December 2, 2025. Accessed March 12, 2026. https://www.cancer.gov/types/breast/what-is-breast-cancer. 
8. What Is a Breast Ultrasound? Breast Cancer Screening. ACS. January 14, 2022. Accessed March 12, 2026. https://www.cancer.org/cancer/types/breast-cancer/screening-tests-and-early-detection/breast-ultrasound.html. 
9. Wolberg WH, Mangasarian OL, Street N, Street W. Breast Cancer Wisconsin (Diagnostic) [dataset]. UCI Machine Learning Repository; 1993. doi:10.24432/C5DW2B.





