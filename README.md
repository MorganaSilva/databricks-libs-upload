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

---

## 2. Loading Python Libraries (PyPI)

If you need to install Python libraries from PyPI:

1. In Databricks, go to the **Compute** menu and select the cluster.
2. Go to the **Libraries** tab and click **Install New**.
3. Choose **PyPI** and enter the package name, for example:
   ```
   pandas==1.5.2
   ```

You can also specify multiple libraries in a `.txt` file and install them in bulk via script.

---

## 3. Uploading Custom Libraries

If you have a custom library, you can upload it in two ways:

### a) Uploading the JAR/WHL file

1. Build your library (JAR for Java/Scala or WHL for Python).

2. Upload the file directly to the **Libraries** tab of the cluster.

3. Click **Install New** > **Upload** and select the file.

### b) Using DBFS (Databricks File System)

1. Upload the library to DBFS using the command:
   ```bash
   dbutils.fs.cp("file:/path/to/library.whl", "dbfs:/FileStore/libraries/")
   ```
2. Install the library on the cluster using:
   ```bash
   %pip install /dbfs/FileStore/libraries/library.whl
   ```

---

## 4. Installing Dependencies on Notebooks

If you want to install libraries directly on a notebook:

### a) Use `%pip` for Python libraries:
   ```pyhon
      %pip install nome-da-biblioteca
   ```

### b) For Java/Scala dependencies, use an `init script` or configure the cluster.

---

## 5. Using Init Scripts

To manage complex dependencies or install libraries before the cluster starts:

1. Create an *init script* with the necessary commands (example to install packages via `apt` or `pip`).
2. Upload the script to DBFS:
   ```bash
   dbutils.fs.put("/databricks/init/myscript.sh", "conteúdo_do_script", True)
   ```
3. Configure the cluster to use the script in *Advanced Options > Init Scripts*.

---

## 6. Using Version Control Repositories

If the library is in a Git repository, such as GitHub, you can clone it directly into Databricks:

1. Configure Git in Repos.
2. Clone the repository with the command:
   ```
   %sh git clone https://github.com/user/repo.git
   ```
3. Install the library with `%pip install` or use it directly in your code.
