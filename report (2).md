# Homework 5: Analyzing Data Using Distribution Charts

**Mohan Krishna Sunkara** 
<br/> Deadline: Tuesday, March 22 by 11:59pm
<br /> UIN: 01206224

The goal of this assignment is gain experience creating distribution charts (histogram, eCDF, boxplot) and using them to help guide further analysis of the underlying data.

## Part 1: Create Distribution Charts

I chose to work with the US Census Bureau State Population dataset.

### Dataset description
- RBIRTH2019 - 2019 birth rates
- RDEATH2019 - 2019 death rates
- RNETMIG2019 - 2019 migration rates

### Question 1: for the boxplot, show the distributions for the 2019 birth rates (RBIRTH2019 column), death rates (RDEATH2019 column), and migration rates (RNETMIG2019 column) for all the states in the US (should result in 3 separate boxplot glyphs in a single chart)

### Chart: 
![](boxplot.png)<!-- -->

### Data manipulations:
- Import specific columns which are birth dates (RBIRTH2019 column, death rates (RDEATH2019 column), and migration rates (RNETMIG2019 column in python by using below code 
```
df = pd.read_csv("nst-est2019-alldata.csv", usecols = ['NAME','RBIRTH2019','RDEATH2019','RNETMIG2019'])
```
- Drop the first 5 rows using below code
```
df = df.iloc[5: , :]
```
- Use below code to draw box plot
```
sns.boxplot(x="variable", y="value", data=pd.melt(df))
plt.show()
```

### Idioms :
| Idiom:        | Boxplots                                                                                                                            |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| What: Data    | Table: many quantitative value attribute                                                                                            |
| What: Derived | Five quantitative attributes for each original attribute, representing its distribution.                                            |
| How: Encode   | One glyph/one attribute and multiple glyphs for each attribute expressing derived attribute values using vertical spatial position. |
| Why           | Find outliers, extremes, averages; identify skew.                                                                                   |

The **boxplots** uses five derived variables carefully chosen to provide information about the attribute’s distribution: the median **(50% point)**, the lower and upper quartiles **(25% and 75% points)**, and the **upper** and **lower fences** (chosen values near the extremes, beyond which points should be counted as *outliers*).
The boxplots show five numbers through the use of a glyph rather than the single number encoded by the linear mark in a bar chart.

### Observations:
- The “rate of birth” is more than the other rates.
- The "rate of death" is less than other rates.
- The median of "rate of birth" is more than 10 while other medians are less than 10.
- Number of outliers for "rate of birth" is greater than a number of outliers for "rate of death" & "rate of migration".
- The Inter Quartile Range "rate of migration" is more than the other two.

### Advantage:
- Output of different variables can be compared.
- Medians' values can be identified very easily.
- Outliers can be identified very easily.

### Disadvantages:
- The range and IQR could not be easily distinguished.
- All the statistical values using the boxplot could not be identified.

## Question 2: for the eCDF and histogram, pick one of the above columns (birth rates, death rates, or migration rates)

### eCDF Chart: 
![](birthecdf.png)<!-- -->

### Data manipulations:
- Use the code below to draw ecdf
```
import seaborn as sns
sns.ecdfplot(x = df['RDEATH2019'])
plt.show()
```
### Idiom for eCDF (Empirical Cumulative Distribution Function):

| Idiom:      | eCDF (step graph)                                 |
| ----------- | ------------------------------------------------- |
| What: Data  | Two quantitative value attributes                 |
| How: Encode | line chart with connecting marks                  |
| Why         | Shows continuous and break values                 |
| X-axis:     | Data ‘x’ in the chosen attribute (Column)         |
| Y-axis:     | Percentage (cumulative density corresponding ‘x’) |

### Advantages:
- Was able to fit the entire data in the definite axis.
- The step function provides better clarity in understanding the data distribution.

### Disadvantages:
- Could not find out the outliers
- The corresponding value of each distribution cannot be identified.
- The continuity between the range of each interval could not be identified.

### histogram chart:
![](birthehistogram.png)<!-- -->

### Data manipulations:
- Use the code below to draw ecdf
```
import seaborn as sns
sns.histplot(data = df['RDEATH2019'] )
plt.show()
```
### Idiom for Histogram:

| Idiom:      | Histogram                                                                                      |
| ----------- | ---------------------------------------------------------------------------------------------- |
| What: Data  | Table: One quantitative value attribute(item count for bin), one derived ordered key attribute |
| How: Encode | Rectilinear layout                                                                             |
| Why         | Shows frequency                                                                                |

### Observations:
- The bins, x-axis, and y-axis are as expected.
- The bins are separated into red as chosen.
- The above histogram looks normally distributed.
- The number of states with the corresponding rate of births can be identified, but much better than the histogram with binwidth =0.1.
- The y-axis has a number count from 0-15.
- The x-axis is scaled 0- 16.

### Advantages:
- Can easily compare data.
- Can differentiate range of data in each bin.
- Can easily find the approximate number of states with a corresponding range of rate of births.
- Can easily identify the median, highest, and lowest values.
- By reducing the bin size, the idiom visualization is much better.

### Disadvantages:
- Too few bins can leave out important information regarding the spread.

## Part 2: 

### Question 1 : The majority of the region's birth rate lies in which region and what are the changes of birth rate over a period of time in different regions ? 

- From the findings in part one box plot, it is clear that birth rate is highest than other two rates but to find which region has higest birth rates. 
- To change the bin size use below code
```
sns.histplot(data = df['RBIRTH2019'],binwidth = 3, bins = 50 )
```
- **But by changing bin size we can see that from the below chart that approximately 90 % percent of countries birth rate was between 10 to 13**

![](part2_hist.png)<!-- -->
### Marks and channels:
Marks: Line
<br />
Channels: x-position, y-position

- But to find how birth rate changed in various regions see below chart
![](part2_line.png)<!-- -->
### Marks and channels:
Marks: Line
<br />
Channels: x-position, y-position, color
 
- To create above line chart use below code 
```
df = pd.read_csv("nst-est2019-alldata.csv", usecols = ['NAME','RBIRTH2011','RBIRTH2012','RBIRTH2013','RBIRTH2014','RBIRTH2015','RBIRTH2016','RBIRTH2017','RBIRTH2018','RBIRTH2019'])
df = df.iloc[1:5 , :]
df = df.T
new_header = df.iloc[0] #grab the first row for the header
df = df[1:] #take the data less the header row
df.columns = new_header #set the header row as the df header
print(df)

line_chart1 = plt.plot( df['Northeast Region'])
line_chart2 = plt.plot(df['Midwest Region'])
line_chart2 = plt.plot(df['South Region'])
line_chart2 = plt.plot(df['West Region'])

plt.ylabel("Rate of birth")
plt.xlabel("Rate of birth year")
plt.title('Change in rate of birth in different regions')
plt.legend(['Northeast Region', 'Midwest Region', 'South Region', 'West Region'], loc=1)
plt.show()

```
- **From both charts, we understand that approximately 90 % percent of countries' birth rate was between 10 to 13* and we can also understand that the west region birth rate was high but high in 2011 but over a period time when it comes to 2019 South region birth rate increased.**

## Idiom for line chart:
| Idiom:      | Line chart                                                                                     |
| ----------- | ---------------------------------------------------------------------------------------------- |
| What: Data  | Table: One quantitative value attribute, oneordered key attribute                              |
| How: Encode | Show trend                                                                            |
| Scale       | Key attribute: hundreds of level                                                                                |

- To show change over period of time line chart was standard one.

## Question 2: In the entire United states how did death rate and birth rate change over period or how it is co-related?

### Data manipulations: 
- Use the code below to create a stacked line chart 
```
df_birth = pd.read_csv("nst-est2019-alldata.csv", usecols = ['NAME','RBIRTH2011','RBIRTH2012','RBIRTH2013','RBIRTH2014','RBIRTH2015','RBIRTH2016','RBIRTH2017','RBIRTH2018','RBIRTH2019'])
df_birth.rename(columns={'RBIRTH2011': '2011', 'RBIRTH2012': '2012', 'RBIRTH2012': '2013', 'RBIRTH2012': '2014', 'RBIRTH2012': '2015', 'RBIRTH2012': '2016', 'RBIRTH2012': '2017', 'RBIRTH2012': '2018', 'RBIRTH2012': '2019'}, inplace=True)
df_birth = df_birth.iloc[:1 , :]
df_birth = df_birth.T
new_header = df_birth.iloc[0] #grab the first row for the header
df_birth = df_birth[1:] #take the data less the header row
df_birth.columns = new_header #set the header row as the df header



df_death = pd.read_csv("nst-est2019-alldata.csv", usecols = ['NAME','RDEATH2011','RDEATH2012','RDEATH2013','RDEATH2014','RDEATH2015','RDEATH2016','RDEATH2017','RDEATH2018','RDEATH2019'])
df_death.rename(columns={'RDEATH2011': '2011', 'RDEATH2012': '2012', 'RDEATH2013': '2013', 'RDEATH2014': '2014', 'RDEATH2015': '2015', 'RDEATH2016': '2016', 'RDEATH2017': '2017', 'RDEATH2018': '2018', 'RDEATH2019': '2019'}, inplace=True)
df_death = df_death.iloc[:1 , :]
df_death = df_death.T
new_header = df_death.iloc[0] #grab the first row for the header
df_death = df_death[1:] #take the data less the header row
df_death.columns = new_header #set the header row as the df header

df_birth['United States'].plot(label='Tesla', color='orange')
df_death['United States'].plot(label='GM')

# line_chart3 = plt.plot(df_birth['United States'])
# line_chart4 = plt.plot(df_death['United States'])


plt.ylabel("Rate")
plt.xlabel("Year")
plt.title('Rate of birth vs rate of death')
plt.legend(['Birth rate', 'Death rate'], loc=1)
plt.show()
```
- Extract the birth and death rate columns from 2011 to 2019 from the dataset into two different data frames
- In the above code first, we renamed the columns to meaningful names then extracted the first column from it.
- Then made that column as a header.
- Plot two different data frames into one chart and name the columns as required.
  
  
### Chart : 
![](part2_bd.png)<!-- -->
### Marks and channels:
Marks: Line 
<br />
Channels: x-position, y-position, color

- From the chart, we can see that the birth rate decreases from 2011 to 2019 but the death rate increases from 2011 to 2019. 
- But the birth rate is always higher than the death rate. 
- Even though, the death rate increased from 2011 to 2019 but birth rate overcome the death rate by increasing approximately 11.5 when the death rate was 8.5. So, if we see the death rate and birth rate in 2019 birth rate has the growth and the death rate has the least number.

## Question 3: Which division has the highest net migration rate in 2019 and which state has the highest net migration rate of the following division in the same year? 

- To find which division has the highest net migration rate in 2019 we need to drawbar chart and check.
- To draw a bar chart, use the code below

## Idiom for line chart:
| Idiom:      | Bar chart                                                                                    |
| ----------- | ---------------------------------------------------------------------------------------------- |
| What: Data | Table: One quantitative value attribute, one categorical key attribute                              |
| How: Encode | Line marks, express value attribute with aligned vertical position, a separate key attribute with horizontal position             |
| why: Task | Lookup and compare values                                    |
| Scale       | Key attribute: dozens to thousand                                                                               |

```
df = pd.read_csv("nst-est2019-alldata.csv", usecols = ['DIVISION','RNETMIG2019'])
df = df.iloc[5: , :]
df.loc[df["DIVISION"] == "1", "DIVISION"] = "New England"
df.loc[df["DIVISION"] == "2", "DIVISION"] = "Middle Atlantic"
df.loc[df["DIVISION"] == "3", "DIVISION"] = "East North Central"
df.loc[df["DIVISION"] == "4", "DIVISION"] = "West North Central"
df.loc[df["DIVISION"] == "5", "DIVISION"] = "South Atlantic"
df.loc[df["DIVISION"] == "6", "DIVISION"] = "East South Central"
df.loc[df["DIVISION"] == "7", "DIVISION"] = "West South Central"
df.loc[df["DIVISION"] == "8", "DIVISION"] = "Mountain"
df.loc[df["DIVISION"] == "9", "DIVISION"] = "Pacific"
df.loc[df["DIVISION"] == "X", "DIVISION"] = "Puerto Rico"

plt.xticks(rotation = 0)
plt.bar(df['DIVISION'],df['RNETMIG2019'])
plt.title('Net migration rate vs division in 2019')
plt.xlabel('Division name')
plt.ylabel('Net migration rate')
plt.show()
```
- In the above code we first get the data and then drop the first 5 rows.
- Then we change the name of the division from a numeric number to its actual name.
- Then we plot the bar chart between division and net migration rate in 2019

![](p2q3_1.png)<!-- -->
### Marks and channels:
Marks: Lines
<br />
Channels: Vertical lengths	and	horizontal	positions

- From the above chart it's clear that the net migration rate is higher in the mountain division, south Atlantic divisions comparatively mountain has highest net migration rate around 15 percent whereas south Atlantic has 10.5 net migration rate in 2019.
- Whereas the lowest net migration rate as observed in pacific, east north central, middle Atlantic among all these divisions pacific has highest negative migration rate of -15 percent.

- From the previous chart, it is clear that the mountain division has the highest net migration rate 
- Then to check which state has the highest net migration rate in 2019 we need to drawbar chart and then compare.
- To draw a bar chart of only mountain division, use below code
```
df = pd.read_csv("nst-est2019-alldata.csv", usecols = ['NAME','RNETMIG2019','DIVISION'])
df = df.iloc[5: , :]
df = df.loc[df["DIVISION"] == "8"]
df = df.drop(["DIVISION"], axis=1)

plt.xticks(rotation = 0)
plt.bar(df['NAME'],df['RNETMIG2019'])
plt.title('Net migration rate vs state in Mountain division 2019')
plt.xlabel('States in Mountain division')
plt.ylabel('Net migration rate')
plt.show()
```
- First, we need to import data from CSV of the following columns which are "NAME", "RNETMIG2019", "DIVISION". 
- Then drop the first 5 rows. 
- Next filter only division with number 8 which corresponds to Mountain division.
- Then plot bar chart

![](p2q3_2.png)<!-- -->
### Marks and channels:
Marks: Lines
<br />
Channels: x-position, y-position

- We can observe the net migration rates of mountain division, we see Idaho has the highest net migration rate comparatively with Arizona, Nevada.
- The negative net migration rate observed in Wyoming with -1 percent.
- To summarize Idaho has the highest net migration rate and Wyoming has a negative net migration rate in mountain division in 2019.

 **To conclude mountain division has the highest net migration rate in 2019 and Idaho has the highest net migration rate in mountain division.**

## References:

* Color Codes, <https://www.w3schools.com/colors/colors_picker.asp>
* Select a subset of a data, <https://stackoverflow.com/questions/47443365/how-to-extract-certain-columns-from-a-list-of-data-frames>
* Coloring boxplot:, <http://www.sthda.com/english/wiki/ggplot2-box-plot-quick-start-guide-r-software-and-data-visualization>
* How to Make a Small Multiples Bar Chart in Excel:, <https://depictdatastudio.com/small-multiples-solution/>
* Small Multiples or Panel charts in Excel, <https://mbounthavong.com/blog/2018/5/27/communicating-data-effectively-with-data-visualizations-part-7-using-small-multiples-or-panel-charts-in-excel>
* Moving Horizontal Bar Chart Headers from Bottom to Top, <https://kb.tableau.com/articles/howto/moving-horizontal-bar-chart-headers-from-bottom-to-top>
* Formatting resizetable, <https://help.tableau.com/current/pro/desktop/en-us/formatting_resizetable.htm>
