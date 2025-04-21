# Exno:1
Name : Joshua Clement D

Register Number : 212224040143

Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
df = pd.read_csv("/content/SAMPLEIDS (1).csv")
df
```
![image](https://github.com/user-attachments/assets/51339704-03d2-46c4-951e-5da234e027e6)
```
df.info()
```
![image](https://github.com/user-attachments/assets/c6a5bc5f-3f78-4f23-b792-3aec96c70a36)
```
df.describe()
```
![image](https://github.com/user-attachments/assets/cf0f86a5-a436-47c4-8bc1-f97e4b7d6ddc)
```
df.shape
```
![image](https://github.com/user-attachments/assets/98305c9b-8d62-4334-92e7-f0d90bec14af)
```
df.isnull()
```
![image](https://github.com/user-attachments/assets/771380fd-b9eb-4333-a10b-a1977056c261)
```
df.notnull()
```
![image](https://github.com/user-attachments/assets/4f5bd51a-31de-45d6-944f-8e3f415e9cfc)
```
df.dropna(axis=0)
```
![image](https://github.com/user-attachments/assets/73234c41-415a-4ba6-b910-cf0f0ff06478)
```
df.dropna(axis=1)
```
![image](https://github.com/user-attachments/assets/3fcb4f87-0a75-4188-a130-a112ef15b812)
```
dfs=df[df["TOTAL"]>270]
dfs
```
![image](https://github.com/user-attachments/assets/a945a282-b5b2-42e0-9e38-19b4d17ecff2)
```
dfs=df[df["NAME"].str.startswith(("A","C"))&(df["TOTAL"]>250)]
dfs
```
![image](https://github.com/user-attachments/assets/a1e055c2-84d8-4839-afe5-cc56d6262598)
```
df.iloc[:4]
```
![image](https://github.com/user-attachments/assets/99db946d-2dd1-4992-9645-8aedc8976f61)
```
df.iloc[0:4,1:4]
```
![image](https://github.com/user-attachments/assets/f095507c-7951-4455-be66-9b4014069e21)
```
df.iloc[[1,3,5],[1,3]]
```
![image](https://github.com/user-attachments/assets/5dfccb61-af66-47f6-8d66-60a416671a62)
```
dfs=df.fillna(0)
dfs
```
![image](https://github.com/user-attachments/assets/c34470ea-48b9-4afb-9483-5ec3ae19eaa3)
```
dfs=df.fillna(method="ffill")
dfs
```
![image](https://github.com/user-attachments/assets/9df2e0d0-79a4-4e03-a118-05664649a193)
```
df["TOTAL"].fillna(value=df["TOTAL"].mean())
```
![image](https://github.com/user-attachments/assets/26abdece-becb-4292-905a-ead79de309cf)
```
df["TOTAL"].fillna(value=df["TOTAL"].mean(), inplace=True)
df
```
![image](https://github.com/user-attachments/assets/2b561a0e-17ac-4d37-8938-d182acc21485)
```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/0053c352-60f1-4976-b7f0-c764262c90a3)
```
df.dropna(how="any")
```
![image](https://github.com/user-attachments/assets/9b1f7e70-c7c0-49b0-aa98-95fa6204865c)
```
df.dropna(how="all")
```
![image](https://github.com/user-attachments/assets/4ba1ab9d-b29f-446f-8c88-50df31a28dfe)
```
m=df.TOTAL.mean()
m
```
![image](https://github.com/user-attachments/assets/ce3bc547-4125-4d7f-a46b-292872706dd5)
```
df.TOTAL.fillna(m,inplace=True)
df
```
![image](https://github.com/user-attachments/assets/4224f155-7c1c-4abe-9b30-a804634eabce)
```
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![image](https://github.com/user-attachments/assets/9cb9944d-703b-4173-af01-23a666903d90)

```
df.dropna(inplace=True)
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![image](https://github.com/user-attachments/assets/08c82150-0518-4fbc-a766-479038f1cc49)
```
# Outlier Detection
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/7be44148-a45d-48b4-9578-336b423912ed)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/e4e5ae3c-0930-46b0-954b-27f373226c99)
```
q1=np.percentile(af,25)
q2=np.percentile(af,50)
q3=np.percentile(af,75)
iqr=q3-q1
iqr,q1,q2,q3
```
![image](https://github.com/user-attachments/assets/cd53b544-76d5-45ca-b6fa-eb3a8cd11842)
```
lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr
lower_bound,upper_bound
```
![image](https://github.com/user-attachments/assets/e866bfd8-629a-44f9-8cc6-c9ed430adb84)
```
af=af[((af>=lower_bound) & (af<=upper_bound))]
af
```
![image](https://github.com/user-attachments/assets/eff00459-0333-4017-97cb-f9dc1a97a690)
```
af.dropna()
```
![image](https://github.com/user-attachments/assets/f97448e5-5e27-4805-81e8-a8df63f2a018)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/f36bb5c7-fe54-4c82-898f-10d5d6cb88ac)
```
data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print(mean,std)
```
![image](https://github.com/user-attachments/assets/e79818d0-5af2-4d70-8fdd-9d62cb8ff5a8)
```
threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z>threshold:
    outlier.append(i)
print(outlier)
```
![image](https://github.com/user-attachments/assets/261091ea-9deb-4f24-8c2b-7085efc014a3)
```
data={"weight":[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
df=pd.DataFrame(data)
df
```
![image](https://github.com/user-attachments/assets/c81cf10c-ad91-4ded-8fe5-a0f7b9ee528e)
```
z=np.abs(stats.zscore(df)) 
print(df[z['weight*]>3])
```
![image](https://github.com/user-attachments/assets/67e64dc7-b570-4fe8-8cd5-3dad8a50502c)
```
out=[] 
def d_o(val): 
ts=3 
m=np.mean(val) 
sd=np.std(val) 
for i in val: 
  z=(i-m)/sd 
  if np.abs(z)>ts:
    out.append(i) 
return out
op=d_o(val)
op
```
![image](https://github.com/user-attachments/assets/e01c3bad-8979-4090-a528-a1cf41a6eb2f)


# Result
      Thus we have carried out data cleansing and removed the outliers by detection using IQR and Z Score method.
