# The Power of Plots

## Background
Comparing the performance of Pymaceutics Inc.'s target drug, Capomulin, with other potential treatments for squamous cell carcinoma (SCC).<br/>

**Dataset:** <br/>
Changes in tumor volume in 249 mice with SCC tumors within 45 days after multidrug treatment.


## Targets<br/>
- Generating tables, charts and figures needed for the technical report of the study.<br/>
- creating a top-level summary of the study results.<br/>

**Tasks:**<br/>
1. Prepare the data.<br/>
2. Generate summary statistics.<br/>
3. Create bar charts and pie charts.<br/>
4. Calculate quartiles, find outliers, and create a box plot.<br/>
5. Create a line plot and a scatter plot.<br/>
6. Calculate correlation and regression. <br/>
7. Submit your final analysis. <br/>

### 1. Prepare the Data
- Merge the `mouse_metadata` and `study_results` DataFrames into a single DataFrame.<br/>
  Use `pd.merge()` to get the merged DataFrame(Combine_df), set "how" as "outer".<br/>
  These two DataFrames have difference size of data<br/>
  
- Display the number of unique mice IDs in the data. <br/>
  `Combine_df["Mouse ID"].unique()`
  
- Display the data associated with mouse ID which are duplicated on time points, and then create a new DataFrame where this data is removed. <br/>
  Use `.duplicated()` to have the rows which is duplicated on "Mouse ID" and "Timepoint"<br/>
  Use `.unique().tolist()` have the list(DuplicatedonID) of the mouse ID with duplicated timepoint.<br/>
  
- Display the updated number of unique mice IDs.<br/>
  Use `.isin()`, and export the csv file.<br/>
  [Duplicated on ID.csv](https://github.com/Ash-Tao/plots-challenge/blob/main/Pymaceuticals/output/Duplicated%20on%20ID.csv)<br/>
  
### 2. Generate Summary Statistics
- Create two summary statistics DataFrames(The mean, median, variance, standard deviation, and SEM of the tumor volume for each drug regimen):<br/>

  - Use `.groupby()`<br/>
    - Get results in five unique series objects. <br/>
      ``` python
      mean = FinalData_df.groupby(FinalData_df["Drug Regimen"])["Tumor Volume (mm3)"].mean()
      ```
      The calculation function at the end can be changed to `.median()`, `.var()`, `.std()` and `.sem()`.<br/>
    - Combine these objects into a single summary statistics DataFrames.<br/>
      Combine these objects as a dictionary and convert it into a DataFrames, and rename the columns.<br/>
  - Use `.agg()` <br/>
      ``` python
      SummaryGoupbyAgg = FinalData_df.groupby("Drug Regimen").agg({"Tumor Volume (mm3)": ["mean","median","var","std","sem"]})
      ```

### 3. Create Bar Charts and a Pie Charts

Generate two bar plots which are identical and show the total number of timepoints for all mice tested for each drug regimen.<br/>
The bar charts and the pie charts created with different methods look the same.<br/>
__Bar Chart:__<br/>
<img src="https://github.com/Ash-Tao/plots-challenge/blob/main/Pymaceuticals/output/BarChart%20-%20Timepoints%20for%20Drug%20Regimen%20-%20Pandas.png" width="450">  <img src="https://github.com/Ash-Tao/plots-challenge/blob/main/Pymaceuticals/output/BarChart%20-%20Timepoints%20for%20Drug%20Regimen%20-%20Pyplot.png" width="450"><br/>
__Pie Chart:__<br/>
<img src="https://github.com/Ash-Tao/plots-challenge/blob/main/Pymaceuticals/output/PieChart%20-%20Sex%20Distribution%20(across%20the%20full%20timepoints)%20-%20Pandas.png" width="450">  <img src="https://github.com/Ash-Tao/plots-challenge/blob/main/Pymaceuticals/output/PieChart%20-%20Sex%20Distribution%20(across%20the%20full%20timepoints)%20-%20Pyplot.png" width="450"><br/>

__The differences:__<br/>
- There is difference on the function use for generating the chart.<br/>
  __pandas:__  `DataFrame.plot()`<br/>
  __pyplot:__  `plt.bar()` or `plt.pie()`<br/>
- There is difference on the data need to be prepared<br/>
  __pandas:__  DataFrame<br/>
  __pyplot:__  x/y axis requires explicit data series<br/>

### 4. Calculate Quartiles, Find Outliers, and Create a Box Plot 

- Calculate the final tumor volume of each mouse across four of the most promising treatment regimens: Capomulin, Ramicane, Infubinol, and Ceftamin. Then, calculate the quartiles and IQR and determine if there are any potential outliers across all four treatment regimens. Follow these substeps:<br/>
  - Create a grouped DataFrame that shows the last (greatest) time point for each mouse.<br/>
    ``` python
    # Start by getting the last (greatest) timepoint for each mouse
    MaxTimepoint = pd.DataFrame(FinalData_df.groupby(FinalData_df["Mouse ID"])["Timepoint"].max()).reset_index()
    ```
  - Merge this grouped DataFrame with the original cleaned DataFrame.<br/>
    ``` python
    # Merge this group df with the original dataframe to get the tumor volume at the last timepoint.
    # Use how="inner" to exclusive the data other than the maximum value。
    FinalTumorVolume_df = MaxTimepoint.merge(FinalData_df, how="inner", left_on=["Mouse ID", "Timepoint"], right_on=["Mouse ID", "Timepoint"])
    ```
  - Determine outliers by using the upper and lower bounds, and then print the results.<br/>
    - Prepare different data for 4 treatment regimens.
      ``` python
      CapomulinLastPoint_df = FinalTumorVolume_df.loc[(FinalTumorVolume_df["Drug Regimen"]=="Capomulin"),:]
      ```
    - Use formula to calculate。Results as follows:
      ![alt text](https://github.com/Ash-Tao/plots-challenge/blob/main/Pymaceuticals/Sample%20for%20outliers_upper%20and%20lower%20bounds.png)
- Using Matplotlib, generate a box plot of the final tumor volume for all four treatment regimens. Highlight any potential outliers in the plot by changing their color and style.<br/>
      ![alt text](https://github.com/Ash-Tao/plots-challenge/blob/main/Pymaceuticals/output/BoxPlot%20-%20Final%20Tumor%20Volume(4%20regimens).png)


### Create a Line Plot and a Scatter Plot

1. Select a mouse that was treated with Capomulin and generate a line plot of tumor volume vs. time point for that mouse.

2. Generate a scatter plot of tumor volume versus mouse weight for the Capomulin treatment regimen.

### Calculate Correlation and Regression

1. Calculate the correlation coefficient and linear regression model between mouse weight and average tumor volume for the Capomulin treatment. 

2. Plot the linear regression model on top of the previous scatter plot.
