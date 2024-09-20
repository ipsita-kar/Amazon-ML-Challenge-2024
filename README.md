# **Amazon ML Challenge: Feature Extraction from Images**

## **Problem Statement**
In this hackathon, the goal is to create a machine learning model that extracts entity values from product images. This capability is essential in fields like **healthcare, e-commerce, and content moderation**, where detailed and accurate product information is crucial. Many products lack textual descriptions, making it necessary to extract critical details such as **weight, volume, voltage, dimensions,** and more directly from images.

---

## **Data Description**
The dataset contains the following fields:

- **index**: Unique identifier (ID) for the data sample.
- **image_link**: Public URL where the product image is available for download. Example link: [Product Image](https://m.media-amazon.com/images/I/71XfHPR36-L.jpg). Use the `download_images` function from `src/utils.py` to download images. See the sample code in `src/test.ipynb`.
- **group_id**: Category code of the product.
- **entity_name**: The entity for which the value is to be extracted (e.g., "item_weight").
- **entity_value**: The value corresponding to the entity (e.g., "34 gram"). **Note**: For the test data, this column will be absent as it is the target variable.

---

## **Output Format**
The output file must contain two columns:

1. **index**: The unique identifier (ID) of the data sample (should match the test record index).
2. **prediction**: A string in the format "**x unit**", where `x` is a float and `unit` is one of the allowed units (listed in the appendix). Examples of valid predictions:
   - `"2 gram"`
   - `"12.5 centimetre"`
   - `"2.56 ounce"`
   **Invalid Examples**: `"2 gms"`, `"60 ounce/1.7 kilogram"`, `"2.2e2 kilogram"`

**Important Notes**:
- If no value is found for a test sample, return an empty string (`""`).
- Ensure your output file passes the **sanity checker** in `src/sanity.py`.

---

## **Evaluation Criteria**
The submissions are evaluated using the **F1 Score**, which is a standard measure of accuracy for classification problems.

### **Definitions**:
- **True Positives (TP)**: Both the ground truth (GT) and the output (OUT) are non-empty and match.
- **False Positives (FP)**: The output is non-empty, but the ground truth is either empty or doesn't match.
- **False Negatives (FN)**: The output is empty, but the ground truth is non-empty.
- **True Negatives (TN)**: Both the output and the ground truth are empty.

### **Formula**:
\[
F1 = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
\]
Where:
- **Precision** = TP / (TP + FP)
- **Recall** = TP / (TP + FN)

---

## **Constraints**
You are provided with a **sample output file** and a **sanity checker**. Ensure that your submission:
- Matches the format of `sample_test_out.csv`.
- Passes the `sanity.py` script check (you should receive the message: `Parsing successful for file: ...csv`).

### **Allowed Units**:
Predictions should only use the units listed in `constants.py`.
