# EXNO-3-DS

## AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

## ALGORITHM:
STEP 1: Read the given Data.

STEP 2: Clean the Data Set using Data Cleaning Process.

STEP 3: Apply Feature Encoding for the feature in the data set.

STEP 4: Apply Feature Transformation for the feature in the data set.

STEP 5: Save the data to the file.

## FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

## Methods Used for Data Transformation:
  ### 1. FUNCTION TRANSFORMATION
• Log Transformation

• Reciprocal Transformation

• Square Root Transformation

• Square Transformation
  ### 2. POWER TRANSFORMATION
• Boxcox method

• Yeojohnson method

## CODING AND OUTPUT:
```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv('data.csv')
df
```

<img width="432" height="327" alt="image" src="https://github.com/user-attachments/assets/d4b7e541-ce2f-46e4-ba6c-812db7aa50cc" />

```
from sklearn.preprocessing import OrdinalEncoder,LabelEncoder
climate = ['Cold','Warm','Hot','Very Hot']
ele = OrdinalEncoder(categories=[climate])
ele.fit_transform(df[["Ord_1"]])
```

<img width="124" height="173" alt="image" src="https://github.com/user-attachments/assets/cce09195-c750-4e15-82fe-f4a628b39057" />

```
df['bo2'] = ele.fit_transform(df[["Ord_1"]])
df
```

<img width="469" height="325" alt="image" src="https://github.com/user-attachments/assets/f64992cc-9d04-40fb-a311-ae8a17506f02" />

```
le = LabelEncoder()
df2 = df.copy()
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```

<img width="431" height="323" alt="image" src="https://github.com/user-attachments/assets/d5d976e9-0351-4f90-9c23-d72e3b420db0" />

```
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```

<img width="430" height="325" alt="image" src="https://github.com/user-attachments/assets/a0104806-60f6-4e7c-a03e-f9f7f45594a0" />

```
from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder()
df3 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["City"]]))
df2 = pd.concat([enc,df3],axis = 1)
df2
```

<img width="779" height="326" alt="image" src="https://github.com/user-attachments/assets/6f5c22c5-2a6c-47cf-979e-1bff8c37a8ea" />

```
pd.get_dummies(df,columns=['City'])
```

<img width="770" height="404" alt="image" src="https://github.com/user-attachments/assets/dcb229c9-ecc2-442a-bf13-66f00ab250af" />

```
from category_encoders import BinaryEncoder
df = pd.read_csv('data.csv')
df
```

<img width="421" height="323" alt="image" src="https://github.com/user-attachments/assets/d9b56390-186a-4762-8cc9-2a541a89aec1" />

```
be = BinaryEncoder()
nd = be.fit_transform(df['Ord_2'])
df
```

<img width="430" height="319" alt="image" src="https://github.com/user-attachments/assets/0be5f23d-b14a-45c1-ae60-52cd068c9978" />

```
from category_encoders import TargetEncoder
te = TargetEncoder()
CC = df.copy()
new = te.fit_transform(CC["City"],y=CC["Target"])
CC = pd.concat([CC,new],axis = 1)
CC
```

<img width="497" height="316" alt="image" src="https://github.com/user-attachments/assets/beea5d78-73ed-4470-a322-13aff8db8aa2" />

```
if 'City' in CC.columns:
    CC = CC.drop('City', axis=1)
new = te.fit_transform(X = df["City"],y=df["Target"])
CC = pd.concat([CC.reset_index(drop=True),new.reset_index(drop=True)],axis = 1)
CC
```

<img width="429" height="312" alt="image" src="https://github.com/user-attachments/assets/da322723-97b1-46a3-86d1-a44ad4d0026b" />

```
df = pd.read_csv('Data_to_Transform.csv')
df
```

<img width="709" height="381" alt="image" src="https://github.com/user-attachments/assets/68c5e6fc-79fd-4a7d-95a4-896944c87c3a" />

```
df.skew()
```

<img width="247" height="180" alt="image" src="https://github.com/user-attachments/assets/ecb45adc-d050-46f0-9619-eafcab1e3560" />

```
np.log(df["Highly Positive Skew"])
```

<img width="218" height="412" alt="image" src="https://github.com/user-attachments/assets/77cc2456-bb0b-4096-bc63-3204c06bb8f3" />

```
np.reciprocal(df["Moderate Positive Skew"])
```

<img width="228" height="416" alt="image" src="https://github.com/user-attachments/assets/14fcbad9-779b-4528-a4ec-a726422ac999" />

```
np.sqrt(df["Highly Positive Skew"])
```

<img width="227" height="422" alt="image" src="https://github.com/user-attachments/assets/c89fc1ad-e098-41a2-a539-8618263a5548" />

```
np.square(df["Highly Positive Skew"])
```

<img width="224" height="421" alt="image" src="https://github.com/user-attachments/assets/e83fb325-37be-4778-8c6c-e64ae4fabf32" />

```
df["Highly Positive Skew_boxcox"], parameters = stats.boxcox(df["Highly Positive Skew"])
df
```

<img width="784" height="401" alt="image" src="https://github.com/user-attachments/assets/866ee3a3-034e-46b9-847d-31d22c5680a0" />

```
df["Moderate Negative Skew_yeojohnson"], parameters = stats.yeojohnson(df["Moderate Negative Skew"])
df
```

<img width="784" height="412" alt="image" src="https://github.com/user-attachments/assets/e4cf0db9-e610-4ac7-ba77-a640d8b74bf1" />

```
from sklearn.preprocessing import QuantileTransformer
qt = QuantileTransformer(output_distribution = 'normal')
df["Moderate Negative Skew_1"] = qt.fit_transform(df[["Moderate Negative Skew"]])
df
```

<img width="1354" height="761" alt="image" src="https://github.com/user-attachments/assets/dc6ea80b-f5cf-4cf5-8a8c-98fe9446c2d6" />

```
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df["Moderate Negative Skew"],line = '45')
plt.show()
```

<img width="553" height="414" alt="image" src="https://github.com/user-attachments/assets/94c4dc2e-7926-4e6f-8a40-0f02e2cbaad9" />

```
sm.qqplot(df["Moderate Negative Skew_1"],line = '45')
plt.show()
```

<img width="539" height="414" alt="image" src="https://github.com/user-attachments/assets/e79de3e1-bfb9-429f-8fb3-db09079c8e5a" />

```
df["Highly Negative Skew_1"] = qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line = '45')
plt.show()
```

<img width="541" height="418" alt="image" src="https://github.com/user-attachments/assets/bfcfa708-eef5-4b7f-a6bb-49aa15562e85" />

```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew_1"]),line = '45')
plt.show()
```

<img width="577" height="416" alt="image" src="https://github.com/user-attachments/assets/9982e67f-47cc-4e0e-8c83-b3ba66cfa91f" />

```
sm.qqplot(df["Highly Negative Skew_1"],line = '45')
plt.show()
```

<img width="535" height="410" alt="image" src="https://github.com/user-attachments/assets/9bab8d89-add2-44eb-b0a3-147f103b0a3d" />

```
sm.qqplot(np.abs(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```

<img width="541" height="415" alt="image" src="https://github.com/user-attachments/assets/f89e11ac-7f54-4d1b-812a-27d09167dcd2" />

```
sm.qqplot(np.log(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```
<img width="537" height="455" alt="image" src="https://github.com/user-attachments/assets/cdfb9419-b8df-40fe-81c0-4765bc2b8abb" />

```
sm.qqplot(np.sqrt(df["Moderate Negative Skew_1"]),line='45')
plt.show()
```

<img width="540" height="447" alt="image" src="https://github.com/user-attachments/assets/a2e8a3aa-b87e-42f2-b28a-2ac6664a427b" />

```
pd.concat([CC,new],axis = 1)
```

<img width="504" height="320" alt="image" src="https://github.com/user-attachments/assets/bf72a282-6a44-47d0-9672-40e5efb59156" />

## RESULT:
Thus, we have successfully performed Feature Encoding and Transformation process and saved the data to a file.
