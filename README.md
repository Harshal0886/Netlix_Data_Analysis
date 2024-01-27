# Netlix_Data_Analysis

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings("ignore")

df = pd.read_csv("Netflix Userbase (2).csv")
df.head()

df.info()

df["Join Date"] = df["Join Date"].astype("datetime64[ns]")

df["Join Date"].dtype

df["Last Payment Date"] = df["Last Payment Date"].astype("datetime64[ns]")

df.info()

pd.DatetimeIndex(df["Last Payment Date"]).tolist()

df["Plan Duration"].value_counts()

df.drop("Plan Duration", axis=1, inplace=True)

df.head()

%matplotlib inline
plt.title("Subscription Type")
sns.countplot(df, x="Subscription Type", hue="Subscription Type")
plt.show()

print("Total Revenue",np.sum(df["Monthly Revenue"]))

%matplotlib inline
plt.title("Join Date")
sns.histplot(df, x=("Join Date"), bins=10 , kde=True)
plt.xticks(rotation=90)
plt.show()

%matplotlib inline
plt.title("Last Payment Date")
sns.histplot(df, x=("Last Payment Date"), bins=10 , kde=True)
plt.xticks(rotation=90)
plt.show()

%matplotlib inline
plt.title("Country")
sns.countplot(df, x=("Country"), hue="Country", legend=False)
plt.xticks(rotation=90)
plt.show()

%matplotlib inline
plt.title("Age")
sns.histplot(df, x=("Age"),bins=20, kde=True)
plt.xticks(rotation=90)
plt.show()

plt.title("Gender")
sns.countplot(df,x="Gender", hue="Subscription Type")
plt.show()

%matplotlib inline
plt.title("Device")
sns.countplot(df, x=("Device"), hue="Device")
plt.xticks(rotation=90)
plt.show()

count_sub_type = df["Subscription Type"].value_counts()
count_device = df["Device"].value_counts()
count_country = df["Country"].value_counts()
count_age = df["Age"].value_counts()
count_gender = df["Gender"].value_counts()

count_country

count_age

pd.crosstab(index=df["Subscription Type"], columns = df["Country"])

pd.crosstab(index=df["Gender"], columns = df["Subscription Type"])

df["Age Group"] = pd.cut(df["Age"], bins=5, labels=["26-30", "31-35", "36-40", "41-45", "45-More"])

pd.crosstab(index=df["Age Group"], columns = df["Subscription Type"])

sns.heatmap(pd.crosstab(index=df["Age Group"], columns = df["Subscription Type"]), annot=True, fmt="d")
plt.show()


* By using this we can clearly see that the basic subscription is more often subscribed by 26-30 age group

* in 41-45 age group the subscription is less compared to other and that is premimum types 
