# plots challenge - The Power of Plots

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

1. Run the provided package dependency and data imports, and then merge the `mouse_metadata` and `study_results` DataFrames into a single DataFrame.

2. Display the number of unique mice IDs in the data, and then check for any mouse ID with duplicate time points. Display the data associated with that mouse ID, and then create a new DataFrame where this data is removed. Use this cleaned DataFrame for the remaining step.

3. Display the updated number of unique mice IDs.

### Generate Summary Statistics

Create two summary statistics DataFrames:

    * For the first table, use the `groupby` method to generate the mean, median, variance, standard deviation, and SEM of the tumor volume for each drug regimen. This should result in five unique series objects. Combine these objects into a single summary statistics DataFrames.

    * For the second table, use the `agg` method to produce the same summary statistics table by using a single line of code.

### Create Bar Charts and a Pie Charts

1. Generate two bar plots. Both plots should be identical and show the total number of timepoints for all mice tested for each drug regimen throughout the course of the study.

    * Create the first bar plot by using Pandas's `DataFrame.plot()` method.

    * Create the second bar plot by using Matplotlib's `pyplot` methods.

2. Generate two pie plots. Both plots should be identical and show the distribution of female or male mice in the study.

    * Create the first pie plot by using both Pandas's `DataFrame.plot()`.

    * Create the second pie plot by using Matplotlib's `pyplot` methods.

### Calculate Quartiles, Find Outliers, and Create a Box Plot 

1. Calculate the final tumor volume of each mouse across four of the most promising treatment regimens: Capomulin, Ramicane, Infubinol, and Ceftamin. Then, calculate the quartiles and IQR and determine if there are any potential outliers across all four treatment regimens. Follow these substeps:

    * Create a grouped DataFrame that shows the last (greatest) time point for each mouse. Merge this grouped DataFrame with the original cleaned DataFrame.

    * Create a list that holds the treatment names, as well as a second, empty list to hold the tumor volume data.

    * Loop through each drug in the treatment list, locating the rows in the merged DataFrame that correspond to each treatment. Append the resulting final tumor volumes for each drug to the empty list. 

    * Determine outliers by using the upper and lower bounds, and then print the results.
    
2. Using Matplotlib, generate a box plot of the final tumor volume for all four treatment regimens. Highlight any potential outliers in the plot by changing their color and style.

  **Hint**: All four box plots should be within the same figure. Use this [Matplotlib documentation page](https://matplotlib.org/gallery/pyplots/boxplot_demo_pyplot.html#sphx-glr-gallery-pyplots-boxplot-demo-pyplot-py) for help with changing the style of the outliers.

### Create a Line Plot and a Scatter Plot

1. Select a mouse that was treated with Capomulin and generate a line plot of tumor volume vs. time point for that mouse.

2. Generate a scatter plot of tumor volume versus mouse weight for the Capomulin treatment regimen.

### Calculate Correlation and Regression

1. Calculate the correlation coefficient and linear regression model between mouse weight and average tumor volume for the Capomulin treatment. 

2. Plot the linear regression model on top of the previous scatter plot.
