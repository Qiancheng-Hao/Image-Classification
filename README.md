# Image Classification Challenge #

## Project Overview ##
### Dataset ###
**Size**: 50,000 training images, doubled to 100,000 via data augmentation.  
**Categories**: 10 evenly distributed labels (0-9), with ~5,000 images per category.  
### Objective ###
Develop a robust classifier to accurately predict labels for a test set, leveraging feature extraction, data augmentation, and machine learning techniques.  
## Methodology ##
### 1. Data Augmentation ###
To enhance the dataset's diversity and improve model generalization:  
**Technique**: Horizontally flipped all 50,000 original images.  
**Result**: Doubled the training set to 100,000 images.  
**Implementation**: Flipped images saved in train_ims_rever with a reverse_ prefix, labels combined in train_combined.csv.  
### 2. Feature Extraction ###
We used the **Histogram of Oriented Gradients (HOG)** method to extract features from images:  
**Optimal Parameter**s:  
resize_size: 128x128  
pixels_per_cell: (16, 16)  
cells_per_block: (4, 4)  
orientations: 10  
**Purpose**: Captures edge and shape information efficiently.  
### 3. Classifier Exploration ###
We tested three classifiers to determine the best approach:  
**Random Forest (RF)**:   
Best Accuracy: 54%  
Parameters: pixels_per_cell=(16,16), cells_per_block=(3,3), orientations=9, n_estimators=200  
**K-Nearest Neighbors (KNN)**:  
Best Accuracy: 52%  
Parameters: pixels_per_cell=(16,16), cells_per_block=(3,3), orientations=12, k=5  
**Support Vector Machine (SVM)**:  
Best Accuracy: 66.12% (initial), improved to 75% in final solution  
Parameters: pixels_per_cell=(8,8), cells_per_block=(2,2), orientations=9, C=10, kernel=rbf  
**Conclusion**: SVM outperformed RF and KNN by over 10%, making it our chosen classifier.  
### 4. Final Solution ###  
**Data Preprocessing**  
**Split**: 85% training, 15% validation (train_test_split, test_size=0.15).  
**Standardization**: Scaled features to a mean of 0 and standard deviation of 1 using StandardScaler to improve convergence and performance.  
**PCA**: Tested but excluded due to potential information loss.  
**Model Training**  
**Classifier**: SVM with C=10, kernel=rbf, probability=True.  
**Features**: HOG-extracted features from 100,000 images (size: 100,000 x 4000).  
**Training**: Performed on scaled features with memory optimization (gc.collect()).  
**Prediction**  
Processed test images from test_ims, extracted HOG features, scaled them, and predicted labels using the trained SVM.  
Results saved to test.csv.  
## Results ##
**Final Accuracy**: 75% on the test set.  
**Key Improvements**:
Data augmentation doubled the dataset, enhancing generalization.  
Optimized HOG parameters and SVM settings boosted accuracy from 66.12% to 75%.  
## Code Structure ##
**Dependencies**  
see the requirements.txt  

# After the competition # 
We try to use CNN to retrain the data, and when to find the highest accuracy that we can reached .......
