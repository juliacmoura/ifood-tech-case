
# iFood Tech Case — A/B Test Analysis

This project analyzes the performance of a promotional coupon campaign using A/B testing. The dataset includes user activity, order history, restaurant data, and A/B test assignments.

---

## 📦 Data Sources

The following files are provided for this case:

```python
order_url = "https://data-architect-test-source.s3-sa-east-1.amazonaws.com/order.json.gz"
user_url = "https://data-architect-test-source.s3-sa-east-1.amazonaws.com/consumer.csv.gz"
restaurant_url = "https://data-architect-test-source.s3-sa-east-1.amazonaws.com/restaurant.csv.gz"
ab_test_url = "https://data-architect-test-source.s3-sa-east-1.amazonaws.com/ab_test_ref.tar.gz"
```

---

## ⚠️ Download Issues

Due to **connection interruptions**, I faced issues downloading the data programmatically from the URLs. As a workaround, I manually downloaded the datasets using local commands in my terminal and uploaded them to **Databricks**:


### 📥 Step-by-Step: Data Preparation and Upload to Databricks

To successfully work with the dataset, follow the steps below:

---

#### 1. **Download the Files Manually**

Run the following commands in your terminal to download the datasets directly to your local machine:

```bash
curl -O https://data-architect-test-source.s3-sa-east-1.amazonaws.com/order.json.gz
curl -O https://data-architect-test-source.s3-sa-east-1.amazonaws.com/consumer.csv.gz
curl -O https://data-architect-test-source.s3-sa-east-1.amazonaws.com/restaurant.csv.gz
curl -O https://data-architect-test-source.s3-sa-east-1.amazonaws.com/ab_test_ref.tar.gz
```

---

#### 2. **Extract Compressed Files**

If you're on macOS or another system that struggles with `.gz` files, you may need to extract them manually:

```bash
gunzip consumer.csv.gz
```

Repeat for other `.gz` files as needed.

---

#### 3. **Upload Files to Databricks**

Navigate in the Databricks UI:

- Click **"New" → "Add or upload data"**

![Step 3 Screenshot](https://github.com/user-attachments/assets/ae04d716-8dcd-4bfa-80eb-f9fd57e29823)

---

#### 4. **Choose a Volume to Upload**

Upload your files into a volume or workspace path:

![Step 4 Screenshot](https://github.com/user-attachments/assets/91ae9136-ad5c-45d3-92b7-8da9c1c201e0)

---

#### 5. **Select Destination Directory**

Choose the destination directory for your files:

![Step 5 Screenshot](https://github.com/user-attachments/assets/189d7845-d2f4-4df3-8673-4cc4ec8cb161)

---

#### 6. **Read the Files in Your Code**

Once the files are uploaded, copy the file paths and use them in your code to load the data into Spark.

Example:

```python
df = spark.read.json("/Volumes/workspace/default/dev/order.json")
```

In this case, files were uploaded to:

```text
/Volumes/workspace/default/dev/
```

- During the initial steps, cells 4 and 12 failed due to connectivity issues and corrupted files when trying to download data directly from the provided URLs. I chose to retain these cells in the notebook as evidence of the alternative methods attempted for transparency and reproducibility.

- Additionally, I explored using [Google Colab](https://colab.research.google.com/drive/1euBJmD1Hj5kbbEaIvbGCUNfYlEJgDjpT#scrollTo=hy7bLOFMXjJi) to load the dataset. However, due to the large size of the order.json.gz file (~1.6 GB), the session exceeded Colab’s RAM limit and crashed. This confirmed the need to use a more robust environment like Databricks or a local Spark cluster for large-scale processing.


---

## 💡 Tips for Large File Handling

- The `order.json.gz` file is large (~1.6 GB) and may cause memory issues in limited environments like **Google Colab**. In my case, Colab crashed due to RAM limits when loading this file.
- For more robust data handling, it’s recommended to use **Databricks** or a local environment with sufficient memory.
- Alternatively, uploading the files to a private **S3 bucket** and mounting it on Databricks would be a scalable solution (available only on **Databricks Premium**).

---

## ✅ Next Steps

Once the data is uploaded:
1. Load the files into Spark DataFrames.
2. Run the notebook(s) for preprocessing, metric calculations, and A/B test analysis.


