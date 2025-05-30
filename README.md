
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

Due to **connection interruptions**, I faced issues downloading the data programmatically from the URLs. As a workaround, I manually downloaded the datasets using the commands below and uploaded them to **Databricks**:

```bash
curl -O https://data-architect-test-source.s3-sa-east-1.amazonaws.com/order.json.gz
curl -O https://data-architect-test-source.s3-sa-east-1.amazonaws.com/consumer.csv.gz
curl -O https://data-architect-test-source.s3-sa-east-1.amazonaws.com/restaurant.csv.gz
curl -O https://data-architect-test-source.s3-sa-east-1.amazonaws.com/ab_test_ref.tar.gz
```

These files were loaded to path `/Volumes/workspace/default/dev/` on Databricks. 

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

---

## ⚠️ Note on Failed Attempts to download data

- During the initial steps, cells 4 and 12 failed due to connectivity issues and corrupted files when trying to download data directly from the provided URLs. I chose to retain these cells in the notebook as evidence of the alternative methods attempted for transparency and reproducibility.

- Additionally, I explored using [Google Colab](https://colab.research.google.com/drive/1euBJmD1Hj5kbbEaIvbGCUNfYlEJgDjpT#scrollTo=hy7bLOFMXjJi) to load the dataset. However, due to the large size of the order.json.gz file (~1.6 GB), the session exceeded Colab’s RAM limit and crashed. This confirmed the need to use a more robust environment like Databricks or a local Spark cluster for large-scale processing.

