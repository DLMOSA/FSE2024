# Deep Learning Framework Testing Method via Heuristic Guidance based on Multiple Model Measurements

This is the implementation repository of our *FSE'24* paper: **Deep Learning Framework Testing Method via Heuristic Guidance based on Multiple Model Measurements**.



## 1. Description

Deep learning frameworks are the basis for the development and deployment of deep learning applications. To guarantee the quality of deep learning frameworks, many framework testing methods regarding deep learning models as test inputs are proposed. However, there are still some limitations in the generated models, such as type variety, model scale, and structural diversity. To overcome these limitations, we propose DLMOSA, a DL framework testing method via heuristic guidance based on multiple model measurements. To achieve a balanced rate between single-branch and model-branch models, we adopt model representation suitable for both single-branch and multi-branch models. Then, we design mutation to generate models based on these representations. To avoid generating excessively large models containing too many operators, we design a novel measurement to limit the scale of the models. To generate more diversified models, we design a DAG-based measurement for the model structural diversity. Based on the proposed two measurements and considering the existing methods' measurement for bug detection ability, we design a heuristic guidance. We apply DLMOSA to test three widely used deep learning frameworks. The experimental results show that DLMOSA outperforms state-of-the-art methods in both effectiveness and efficiency. DLMOSA successfully detects 17 crashes, 1 NaN bug, and 5813 inconsistencies. Among them, all of the detected crashes are confirmed. 



You can access this repository using the following command:

```shell
git clone https://github.com/DLMOSA/FSE2024.git
```



## 2. Framework version

We use three widely-used DL frameworks (*i.e.*, ***TensorFlow***, ***PyTorch***, and ***MindSpore***). We conduct the experimental environment as follow:

| TensorFlow | PyTorch | MindSpore | Keras |
| :--------: | :-----: | :-------: | :---: |
|   2.8.0    | 1.12.0  |   2.1.0   | 2.6.0 |



## 3. Environment

**Step 0:** Please install ***anaconda***.

**Step 1:** Create a conda environment. Run the following commands.

```sh
conda create -n DLMOSA python=3.9
source activate DLMOSA
pip install tensorflow==2.8.0
pip install mindspore==2.1.0
pip install torch==1.12.0
pip install keras==2.6.0
```

## 4. File structure

This project contains five folders. The **LEMON-master** folder is the downloaded open source code for LEMON. The **Muffin-main** folder is the downloaded open source code for Muffin. The **Ramos** folder is the downloaded open source code for Ramos. The **DLMOSA** folder is the source code for our method. The **result** folder is the experimental result data. To know the execution methods of LEMON, Muffin and Ramos, please refer to the corresponding research papers. In this document, we will introduce how to run the source code for DLMOSA.

In the source code for DLMOSA, the folders named **DataStruct, Test, and Method** contain the body for the method. The program entry of the method is **main.py**. Run **main.py** to run DLMOSA after installing the experimental environment.

The folder named **result_analysis** is used in the Evaluation section, which will be explained in the following sections.

## 5. Experiments

### 5.1 Main Method

Make sure you are now in the ***conda*** visual environment!

Use the following command to run the experiment according to the configuration:

```shell
python main.py
```

The testing results will be stored in `./new_result.csv`.

### 5.2 Evaluation

#### 5.2.1 Evaluation for DLMOSA

**Step 1:** Set **file_path** and **result_csv** in **./DLMOSA_Structure.py**, **./DLMOSA_Structure_and_precision_bugs.py** and ./**DLMOSA_edit_distance.py**. Especially, set **file_path** to the location of new_result.csv(new generated). Set **result_csv** to the location of the structural analysis output.

**Step 2:** Use the following command:

```shell
python DLMOSA_Structure.py
python DLMOSA_Structure_and_precision_bugs.py
python DLMOSA_edit_distance.py
```

The structural analysis results will be exhibited in the output and stored in `./DLMOSA_graph.csv` and`./DLMOSA_graph_and_precision_bugs.csv`.

#### 5.2.2 Evaluation for LEMON, Muffin and Ramos

Generate model files using open source code of their respective methods. Then convert these models to strings similar to those in **new_result.csv**. After that, run the corresponding analysis method. The configuration is similar to 5.2.1.
