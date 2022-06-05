# Lending Club Case Study

## Table of Contents
* [General Info](#generalinformation)
* [Technologies Used](#technologiesused)
* [Conclusions](#conclusions)
* [Acknowledgements](#acknowledgements)

<!-- You can include any other section that is pertinent to your problem -->

## General Information
-  This case study is about identifying issues with the dataset, cleaning it and then analyzing it for deriving the new values, we are trying to get information like defaulters, rate of interest given to grade level, what sort of loans were given that has maximum number of defaulters, how much the bank made money(ROI) after providing the loan etc.

<!-- You don't have to answer all the questions - just the ones relevant to your project. -->

## Conclusions
  - ROI definition = Return on investment is a widely used financial metric for measuring the probability of gaining a return from an investment. It is a ratio that compares the gain or loss from an investment relative to its cost. It is as useful in evaluating the potential return from a stand alone investment as it is in comparing returns from several investments.
  ROI Formula
  ROI = (Net Return  on  Investment − / Cost Of Investment) × 100
  Panda syntax
  df['ROI'] = (df['total_pymnt'] / df['funded_amnt']) * 100
  df.head(10)

- graph =  df[df['loan_status']=='Charged Off'].groupby(['home_ownership'])['home_ownership'].count()
  plt.title('People with more defaulters as per home ownership category \n', fontdict={'fontsize':12, 'fontweight':5, 'color':'White'})
  graph.plot.pie(autopct='%.2f%%', shadow = True, startangle = 65)
  plt.show()
  We have drawn a pie chart and saw MORTGAGE and RENT category has the biggest number of defaulters.

- Now let’s check the grade that has the largest number of defaulters.
  plt.figure(figsize=[10, 5])
  sns.countplot(x='grade',  data=df[df['loan_status']=='Charged Off'], order=np.sort(df['grade'].unique()))
  plt.title('Distribution of Loan Defaulters by Grade')
  plt.xlabel("Grade")
  plt.ylabel("Number of Loan Defaulters")
  plt.show()
  Here we have plot a countplot which demonstrate the grades which has largest number of defaulters, by plotting this we came to know that Grade B, C and D has maximum number of defaulters

- Next we created a custom function and created a new column and marked it as loan_type. Here we derive how much percentage the bank has provided loan which are defaulters.
  def loan_type(status):
       if status == "Charged Off":
          return 'Defaulter Loan
      else:
         return 'Not Defaulter Loan'

  df['loan_type'] = df['loan_status'].apply(loan_type)
  plt.figure(figsize=(8,8))
  colors = ["green", "red", "orange", "blue"]
  df.loan_type.value_counts().plot.pie(explode = [0, 0.2], colors=colors, autopct='%1.2f%%', shadow = True, startangle = 65)
  plt.show()
  After plotting this we can clearly see that only 14.17% loans were defaulters.
  
- Then we plot boxplot and checked day wise which day of the month has allocated loans there we defaulters and non defaulters.
    plt.figure(figsize=(20,15))
    sns.barplot(x=df.issue_d, y=df.loan_amnt, hue=df.loan_type)
    plt.xticks(rotation=90)
    plt.show()


<!-- You don't have to answer all the questions - just the ones relevant to your project. -->


## Technologies Used
- Pandas - 1.4.2
- Numpy - 1.22.3
- MatplotLib - 3.5.1
- Seaborn - 0.11.2
- PandasSQL - LTS

<!-- As the libraries versions keep on changing, it is recommended to mention the version of library used in this project -->

## Acknowledgements
Give credit here.
- This project was inspired by Upgrad Tutorials
- This project was based on Live sessions of Upgrad


## Contact
Created by [@sudeepignition] - feel free to contact me!
