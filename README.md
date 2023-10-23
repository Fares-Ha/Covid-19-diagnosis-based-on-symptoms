# Covid-19-diagnosis-based-on-symptoms

## Introduction

The use of artificial intelligence (AI) in healthcare has become increasingly popular in recent years.
One area where AI has the potential to significantly impact patient outcomes is in the classification and diagnosis of diseases.
By analyzing personal information such as medical history, symptoms, and test results,
AI algorithms can help healthcare professionals accurately classify the type of disease a patient may have. However,
the time aspect of the data is a crucial factor that must be considered to achieve the most accurate results. In this context,
treating personal information as time series data can provide valuable insights into the progression of a patient's condition, leading to more accurate disease classification.
Time series data refers to data points that are collected over time, where each data point is associated with a specific time stamp.
In the context of disease classification, time series data can capture the dynamic changes in the disease over time.
For example, changes in symptoms or test results that refers to the disease over time can provide important insights into the progression of a disease or its response to treatment.
By treating personal information as time series data,
AI algorithms can better capture the characteristics  of a disease over time  , leading to more accurate disease classification and better treatment outcomes.
In addition, time series data can help healthcare professionals identify patterns and trends that may be indicative of disease onset or progression.
This can enable earlier intervention and treatment, leading to better patient outcomes.
Moreover, time series data can help healthcare professionals tailor treatments to individual patients based on their unique medical history and disease progression.
This personalized approach to medicine is becoming increasingly important, as it can lead to better treatment outcomes and improve patient satisfaction.


## Data analysis

The first data is gathered from the Government portal to disseminate data and information related to the Coronavirus (COVID-19) in the State of Espírito Santo.,  , it is in portuguese and  I translated it to english. 

it has more than 4800000 rows and 45 columns collected from 2020-01-23 to 2023-07-7 , the columns and their meaning are provided in Table -1- 


Table -1- The attributes naming in the data and its english meaning  based on google translation 

| Portuguese        | English           |
| ------------- |:-------------:| 
|Bairro                     |    Neighborhood of the citizen |	
|Classificacao              |   Case classification: Suspect, Confirmed, Discarded |
|Comorbidade Cardio         |    Comorbidity: Cardiovascular disease |
|Comorbidade Diabetes       |    Comorbidity: Diabetes	|
|Comorbidade Obesidade      |    Comorbidity: Obesity	|
|Comorbidade Pulmao         |    Comorbidity: Lung disease |
|Comorbidade Renal          |    Comorbidity: Kidney disease |
|Comorbidade Tabagismo      |    Comorbidity: Smoking	|
|Criterio Confirmacao       |    Criteria used to confirm the case |
|Data Cadastro              |    Date of registration in the system |
|Data Notificacao           |    Date of notification of the disease |
|Data Coleta RT PCR         |    Date of the collection of the sample	RT PCR |
|Data ColetaSoro logia      |    Date of the collection of the sample for serology test |
|Data ColetaSoro logia IGG  |    Date of the collection of the sample for IgG serology test |	
|Data Coleta Teste Rapido   |    Date of the collection of the sample for rapid test |
|Data Diagnostico           |    Date of diagnosis	|
|Data Encerramento          |    Date of closure |
|Data Obito                 |    Date of death |
|Evolucao                   |    Case evolution	|
|Idade Na Data Notificacao  |    Age of the citizen on the date of notification |
|FicouInternado	          | Indicates if the citizen was hospitalized |
|Municipio                |      City of the citizen |
|Escolaridade             |      Profile of the citizen: education level |
|Faixa Etaria             |      Age Range |
|Raca Cor                 |      Race / Color |
|Profissional Saude       |      Health Professional |
|Morador De Rua           |      Homeless |
|Possui Deficiencia       |      Disability	|
|Sexo                     |      Gender |
|Viagem lnternaciona      |      International Travel |
|Viagem Brasil            |      Domestic Travel	|
|Cefaleia                 |      Headache	:Symptom: |
|Coriza                   |      Runny Nose	:Symptom: |
|Diarreia                 |      Diarrhea	:Symptom: |
|Dificuldade Resp iratoria|      Difficulty Breathing	:Symptom:|
|Dor Garganta	           |Sore Throat	:Symptom: |
|Febre                   |       Fever	:Symptom: |
|Tosse                   |       Cough	:Symptom: |
|Status Notificacao	     |      Notification Status: Open, Closed |
|Resultado RT PCR Test:  |       Identifies the result of the RT PCR test |
|Resultado SorologiaTest:|       Identifies the result of the Serology test |
|Resultado Sorologia IGGTest: |  Identifies the result of the Serology IGG test |	
|Resultado Teste RapidoTest:  |  Identifies the result of the Rapid Test |
|TipoTesteRapido              |  The type of rapid test |


## Data Imputation using MICE algorithm

Multiple Imputation by Chained Equations (MICE) is a statistical technique used to impute missing data in a dataset.

MICE is a flexible and powerful method that can handle missing data in both continuous and categorical variables.

The basic idea behind MICE is to fill in missing values in a dataset by using the observed values to create imputations that are plausible for the missing values.
MICE works by creating multiple imputations of the missing values,based on different plausible scenarios, and then combining the results to create a final imputed dataset.

The imputations are generated by modeling the conditional distribution of each missing variable given the other variables in the dataset, using a regression model or other appropriate method.

The "chained equations" part of MICE refers to the fact that each imputation depends on the other imputed variables in the dataset.
The imputations are generated in a sequence, with each variable being imputed one at a time, conditioned on the other variables in the dataset that have already been imputed.

This process is repeated for a number of iterations, generating a set of imputed datasets that can be combined to create a single imputed dataset.
So MICE can be a powerful tool for handling missing data, but it is important to carefully consider the  very important assumption underlying the method which is Missing at Random (MAR) Assumption, MICE assumes that the missing data are missing at random (MAR), meaning that the probability of a value being missing is related to observed variables in the dataset, but not to the missing values themselves. If the missing data are not MAR, MICE may produce biased or unreliable results.

The general steps for applying Multiple Imputation by Chained Equations (MICE) to impute missing data in a dataset:

1. __Identify the variables with missing data:__ Start by identifying the variables in your dataset that have missing values.
    It's important to understand the pattern of missingness in your data, as this can affect the choice of imputation method.

2. __Create a fully observed auxiliary dataset:__ To estimate the conditional distributions of the missing variables,
    you need to create a fully observed auxiliary dataset that includes all the variables in your original dataset,
    but with the missing values replaced by imputed values.
    You can use any appropriate imputation method to create the initial imputations.

3. __Select an imputation model:__ For each missing variable,
    select an appropriate imputation model that predicts the missing values based on the observed variables in the dataset.
    The imputation model can be any appropriate method, such as linear regression, logistic regression, or a decision tree.
    It's important to choose an appropriate model that captures the relationships between the variables in your dataset.

4. __Generate multiple imputations:__ Use the imputation model to generate multiple imputations of the missing values,
    conditioned on the observed values in the dataset. Each imputation should be generated in a separate dataset,
    and the number of imputations will depend on the amount of missingness in your dataset and the desired level of precision.

5. __Combine the imputations:__ Combine the multiple imputations into a single imputed dataset using appropriate rules for combining the imputations.
    One common method for combining the imputations is to take the average of the imputed values,
    but other methods may be appropriate depending on the nature of the data.

6. __Analyze the imputed dataset:__ Once you have generated the imputed dataset, you can analyze it using any appropriate statistical method,
    such as linear regression, logistic regression, or survival analysis.
    You should also assess the quality of the imputations using appropriate measures, such as mean squared error or root mean squared error.

7. __Repeat the process as needed:__ If the quality of the imputations is not satisfactory,
    you may need to repeat the process with different imputation models or parameters until you achieve satisfactory results.

I kept all symptoms features and droped all other features since the classification is based on the symptoms.

I considered the time factor while imputing it since the symptoms and characteristics for a disease (like covid-19)  may change over time, so I used Label encoder to encode the categorical features , then I divided this data frame also into chunks , each chunk represent 3 months.

I applied MICE for each chunk alone, used logistic regression model  and all the null values filled successfully.

## Feature selection

Feature selection is a process of selecting the most relevant features from a dataset for a machine learning model. The goal of feature selection is to improve the performance of the model by reducing the number of features and removing those that are not important.

There are a number of different feature selection techniques that can be used, including:

1. __Filter methods:__ Filter methods select features based on their statistical properties, such as their correlation with the target variable or their variance.
   for example  (Chi Squared , Mutual Information).

2. __Wrapper methods:__ Wrapper methods select features by building a model and evaluating the performance of the model on a holdout dataset.
   The features that improve the performance of the model are selected. for example (Recursive feature Elimination).
 
3. __Embedded methods:__ Embedded methods select features as part of the model training process.
   the model is trained on a subset of features, and the features that are most important for the model are selected.
   for example (Decision Tree , Random Forest).

I applied (Chi Squared , Mutual Information , Decision Tree , Random Forest Recursive feature Elimination) feature selection methods and compare the results.

## Data Balancing using SMOTE

I balanced the data using SMOTE algorithm.

## Concept Drift Detection

Concept drift refers to the phenomenon where the statistical properties of a target variable, concept, or underlying data distribution change over time in a predictive modeling or machine learning setting.

It occurs when the assumptions made during model training become invalid or less accurate, leading to a degradation in the model's performance or predictive ability.

Concept drift poses challenges to predictive models because the assumptions made during model training may no longer hold in the evolving data.

As a result, the model's performance can degrade, leading to decreased accuracy or reliability , and since we are dealing with time series data we need to check if there is a drift in the data to get better classification results.

I used DDM (Drift Detection Model) and ADWIN from scikit multi flow library in python to check the drift between each two consecutive chunks. 

## Overall results

I compared the results of all expirements in "covid Data Results" file.


