# Ways to Upload Libs to Databricks

# How to Include External Libraries in Databricks

In Databricks, you can include external libraries in several ways, depending on where the library is hosted and how you want to use it. Here are the most common options:

---

## 1. Using Maven
If you need a Java/Scala library hosted in a Maven repository, follow the steps below:

1. Go to your **workspace** in Databricks.
2. Click on **Compute** and select the cluster where you want to add the library.
3. Click on the **Libraries** tab and click on **Install New**.
4. Choose the **Maven** option and provide the **artifact ID** in the format:
   ```
    groupId:artifactId:version
   ```
   Exemplo para o Spark XML:
      ```
        com.databricks:spark-xml_2.12:0.15.0
      ```
