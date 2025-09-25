# Data Insights Engine Tool

This tool makes it easy to get a quick look at your datasets. Whether you want summary stats, charts, outlier detection, or even basic classification insights, it handles the heavy lifting so you can focus on understanding your data and making decisions—no setup headaches required.

To build this script, I combined Python’s powerful data libraries like Pandas, scikit-learn, and TensorFlow with automation for charting, outlier detection, and classification. The process was much smoother thanks to Vibe Coding, which helped me organize the workflow and speed up development. The result is a tool that can take any CSV dataset and turn it into actionable insights in just a few steps.

**Features include:**
- Automatic installation of required Python packages if missing
- Support for any CSV dataset with numeric and categorical columns
- Automatic handling of missing values
- Generation of basic statistics for numeric features
- Creation of correlation heatmaps with strong relationships highlighted
- Detection of potential outliers using Isolation Forest
- Optional classification modeling if a target column is provided
- Confusion matrix and classification report for model evaluation
- Feature importance analysis using SHAP
- Optimized for speed using tree-based models for fast SHAP computation
- Fully automated workflow from data input to actionable insights

**What it can handle:**
- Structured tabular datasets in CSV format
- Numeric features such as age, salary, scores, or measurements
- Categorical features such as gender, city, product category, or yes/no flags
- Datasets with or without a target column for classification
- Small to medium-sized datasets (hundreds to tens of thousands of rows)

**Limitations:**
- Not designed for unstructured data like raw text, images, or audio
- Extremely large datasets may slow down SHAP feature importance calculations
- Works best when the CSV has headers and consistent formatting
- Accuracy of classification insights depends on data quality and feature relevance

# The tool in action:

Once run, it will ask you to enter the path for the CSV you want to work on. I'm going to work with the Titanic data set (remember to leave out quotation marks for the pathname).

<img width="1286" height="163" alt="image" src="https://github.com/user-attachments/assets/f4a19784-1598-4ce7-a8e4-684beb75cad9" />


You will now be presented with a menu. We're going to look into plotting some graphs so I'll select option 2.

<img width="591" height="132" alt="image" src="https://github.com/user-attachments/assets/2aaf6654-b823-4ad8-9893-cbe50f22e4e6" />


As you can see we have 4 chart types to choose from. I anticipate adding a more comprehensive list of charts further down the line.

<img width="341" height="192" alt="image" src="https://github.com/user-attachments/assets/a6fa212a-03df-4da2-a2ed-6512c7eb3b0d" /> \


## Resulting Charts

<div align="center">

### Correlation Heatmap
</div>

<img width="800" height="600" alt="Correlation" src="https://github.com/user-attachments/assets/73cfb53b-b126-43b3-a606-bfa31da63df4" />

<div align="center">

### Histogram (Age)
</div>

<img width="800" height="600" alt="Hist" src="https://github.com/user-attachments/assets/e3d067ae-91c5-44ca-8508-54a8ca0602dd" />

<div align="center">

### Bar Chart (Survived)

</div>

<img width="800" height="600" alt="Survived" src="https://github.com/user-attachments/assets/db05c827-62c2-4db8-864a-fd242d24fe83" />

<div align="center">


### Scatter Plot

</div>

<img width="800" height="600" alt="Scatter" src="https://github.com/user-attachments/assets/4e62cd3b-a9d3-44be-9943-9dacb183d1dd" />

<div align="center">
  
### Line Chart

</div>

For the Titanic dataset, the data was unordered so it resulted in a chaotic line chart, here is one from a dataset I made specifically for this purpose.
<img width="800" height="600" alt="line" src="https://github.com/user-attachments/assets/c832f1ee-8e36-476d-b63f-47190971e508" />

## Classification (Auto Model Selection)

Going back to the main menu, you might remember seeing the **Classification** option. The Classification option allows you to perform supervised machine learning on your dataset with minimal setup. Here’s how it works:

1. **Target Column Selection**  
   You choose which column in your dataset is the target (the variable you want to predict). Only numeric columns are used for features automatically, and if the target column is categorical, it is encoded so the model can process it.

2. **Dataset Splitting**  
   You specify a percentage of the data to use as the test set. The script automatically splits the dataset into training and testing sets for model training and evaluation.

3. **Automatic Model Selection**  
   The script automatically selects a suitable model based on your dataset’s characteristics:
   - **Random Forest** is used for small to medium datasets with few classes.
   - **TensorFlow Neural Network** is used for large datasets, high-dimensional data, or datasets with many classes.  
   You can override the automatic choice if you prefer a different model.

4. **Model Training and Prediction**  
   The chosen model is trained on the training set and then makes predictions on the test set.

5. **Evaluation**  
   Accuracy is calculated and displayed. A confusion matrix heatmap is also generated for visual inspection, helping you quickly see how well the model is performing across different classes.

6. **Optional Save**  
   You can save a CSV file containing the test set, actual values, and predicted values for further analysis or reporting.

This feature is designed to make classification accessible, allowing you to quickly experiment with supervised learning on numeric datasets while still providing meaningful insights into model performance.

To test this, I'll use two datasets one small for Random Forest and one large for TensorFlow

### Random Forest
**Here are the parameters I configured to run**

<img width="1162" height="230" alt="image" src="https://github.com/user-attachments/assets/17e0324d-5a1c-49b4-bbb9-47bd4893eb11" /> <br/><br/>
  

**And here is my output matrix.**

<img width="600" height="500" alt="conf1" src="https://github.com/user-attachments/assets/cc95aaf7-a9b2-47c3-b630-d16eb51b2444" />

### TensorFlow
**Given parameters:**

<img width="1600" height="183" alt="image" src="https://github.com/user-attachments/assets/f52fec6d-a51b-46c2-8b4e-52b423b1c91d" /> <br/><br/>
  

**Output:**

<img width="600" height="500" alt="conf2" src="https://github.com/user-attachments/assets/1ffaf8a8-0f64-4168-b8e8-3a81f1875f03" />

## Conclusion

So you can see it's a pretty nifty tool for some quick insights, and for when you need to generate a graph or two. More updates will be coming soon and I hope to keep building on this project.
