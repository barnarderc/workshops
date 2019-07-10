Comparative Perspectives on Inequality (Kesler)
 
[Here](https://github.com/barnarderc/workshops/blob/master/Spring%202017/Comparative%20Perspectives%20on%20Inequality/example_chart_inequality_indicator.xlsx) is the example spreadsheet with an example chart and cleaned OECD indicator data (the example from the workshop).

Here are the steps for cleaning the data and creating the chart:

Download the indicator data from [data.oecd.org](data.oecd.org)
Delete the columns that are not required (i.e. Indicator, Subject, Measure, Frequency, Time, and Flag Codes)
Rename "Value" to the name of the indicators (e.g. "Income Inequality Gini Coefficient, Doctor Consulations, etc.)
Copy and paste all indicators into the same sheet (keep the country column with each indicator).
Sort the country and indicator (both columns at the same time, separately for each indicator) from A to Z by LOCATION (Sort button is in the Data ribbon/menu toolbar). Include the first row with the indicator and country labels (LOCATION, etc.). Make sure the "My data has headers" box is checked in the Sort dialog box.
Select only the two LOCATION columns (but do not include the cell with the word LOCATION - only the country codes should be selected). You can select non-adjacent cells by holding down the CTRL (control) button on your PC keyboard (on a Mac hold down the COMMAND key). Go to the Home ribbon/menu toolbar and click the Conditional Formatting button, then select Highlight Cells Rule, then select Duplicate Values... (then click OK in the dialog box)
Delete the country and indicator data for the UNHIGHLIGHTED cells (the cells that are not red). After these are removed, both lists should contain the same countries in the same order (alphabetical). 
Delete any blank columns in between the two sets and remove the second LOCATION column. The first column should be LOCATION, the second column should contain the income or poverty indicator, and the third column should contain the indicator you selected. Repeat twice for two additional indicators that you choose.
Click a blank/empty cell 
Go to the Insert ribbon/menu toolbar and in the charts section select the chart with dots (Scatter) and then the first option (with just dots/points). You should have a blank chart box.
Click the Select Data button in the Design ribbon/menu toolbar.
Click Add under Legend Entries (Series)
For Series Name, you can type in the name of the second indicator (e.g. Doctor Consulations)
For Series X Values, select the data (not including the first row/the indicator label) for the independent variable (the indicator that you think affects the other indicator or the indicator that you think influences the other indicator. For example, if you think income inequality influences the number of times someone visits the doctor during the year, then income inequality would be on the Series X Values).
For Series Y Values, select the data (not including the first row/the indicator label) for the dependent variable (the indicator that you think is influenced by the other indicator).
Click OK and then OK again
The chart should appear with the data plotted as individual points. Make the chart look nice by removing the gridlines, adding axis titles, changing the title to be descriptive, changing the color of the points, etc.
Add a trendline to the chart.
You're done!