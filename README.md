# Sharkwork


This is a data analysis and cleaning project made as part of a Bootcamp, in April 2023.
Please be aware that it is the first attempt at something of this size, and that this is my second week here, so **PLEASE** take that into consideration when checking out the files included.

The data was obtained from the following link: https://www.kaggle.com/datasets/teajay/global-shark-attacks.

Cleanup of the data was the **main objective** of this data analysis, with "objective and conclusions" per se being second. 

This document will be updated once the cleanup has been more or less done, and proper analysis can be done towards a certain goal.

**Data cleaning process**


- First thing, all the necessary libraries were imported with

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

As well as some output style choices.

- Due to some encoding issues, the read command was presented as such: 

Sharkattacks = pd.read_csv('attacks.csv', encoding = 'ISO 8859-1')

A check of the data type for Sharkattacks show that is indeed a pandas.core.frame.DataFrame

Checking for duplicates indicates 25723 in total, so we would drop them, creting a final size of 24 columns and 6312 entries.

Out of all the columns, only 'Year' is designed as Type = float64, so we change that to object, as the rest of them.

Further inspection of the columns indicate as much as 3364 null values in the time column, and proves that the last two columns are useless, as they are essentially empty.

We then drop all the rows that contain null values, )6302 to 6309, 8702 and 25722)

After this, given that there are multiple extra spaces and irregularities in the column names, we rename them using a dictionary.

Some exploration helps us determine which rows have null values for certain columns, so we could start dealng with them and maybe draw some conclusions.

Instead of eliminating the null values, we substitute each of them for strings relevant to the column, or that have some guidance about where else in the table the missing data can be maybe be inferred.

After that, all the columns now have 0 null values, which would make it easier to work with them.

All in all, we have a Dataframe with 6302 rows and 24 columns.

We also confirm that 3 columns, Case number, Case Number.1 and Case Number.2, have essentially the same information, but **not** the same values. So in the case of one of them being empty, the information is extracted from either of the remaining ones.

Same goes for Href formula and Href. 

I tried to cross over the text in Href formula, but was unable to in the end.

An attempt at separating data by Shark species and injuries showed the variety of strings in the species column, so they were all first transformed into lowercase, but we still obtained 1536 different unique iterations, so a different category was selected. Species is by far the colum with the biggest lack of systematic.

The column Type had a much smaller amount of unique values, some of which could be merged due to typos, to obtain 7 final ones.

Same for Fatal and Sex, which were reduced to 3 each.

Any other category had simply too many variables to manage properly.

There was an attempt to include the values in the Age column in a range, but due to the different inputs, it was discarder for the current analysis.

Some columns, like Year, had a lot of uninformative elements, but they could be used to point out another column next to them to provide it.

Once some combinations were drawn, it was becoming more obvious that most of the victims were male, however, that on itself does not merit a conclusion, given how traditionally, men have been more involved with sea-faring activities than women.

Also, more and more it showed the truly difficult challenge of drawing conclusions from such incomplete data. Many combinations show over hundreds of itertions in which the value in. column is inconclusive.

Given also how many of them are just categorical values, elements like correlation become more difficult. To bypass this, the smallest 3 columns (Type, Sex and Fatal) were encoded using One-Hot Coding into boolean values that werre then converted to int.

Each of these new columns were then appended to the end of the table. With this, we were able to produce a table of correlation values between the original order, the fatality of the accidents, the type of accident and the sex of the victim.

This was chosen due to the fact that some other conclusions did not need a correlation value to be known. For example, It is clear that most incidents would happen after a certain year, snce record-keeping of this style would not be common at the time. 

It is also easy to infer that the most number of incidents would be not only countries with access to the sea, but those near where sharks tend to be located. Also countries with a higher rate of leisure activities by the water, as well as more prone to report this type of incidents. Yemen may have more shark attacks than we see here, but it is not such a common occurrence that would merit proper record-keping.

Obviously areas with a cultural tradition with the sea would have a lot of cases, such as the case of Hawaii, especially since it is also part of the USA.

Simple enough: Richer countries would have a larger chance of leisure at sea, and thus, higher chance of shark atttacks; as well as a higher chance of having a more robbst record-keeping system. Men would also have a higher chance of being the victim, due to the fact they have traditionally been more associated to sea activities.

Our initial correlation Matrix is not very surprising, not many of the elements presented show massive correlation values.
But some possible ideas could merit further study based on this. 

For example, we can see that there seems to be a very strong correlation between one of the values of Type and one of the values of Fatal. This could indicat a specific group of data that require much higher review, and trying t find out as much as possible based on other columns.

The second biggest correlation is between the "unprovoked" values and "boating". This could mean that in cases where a boat is involved, there is a higher chance of  attacks, even if they are labelled as "unprovoked". The boat itself could have been enough disturbance to nearby sharks, or some other activity could have triggered it.

Whats more, I would not consider the unprovoked value reliable at all, as data shows unrpovoked shark attacks are not the majority, while this category appears 4595 times. This indicates the presence of an unreliable narrator or a bias in the data. 

In conclusion, we need better data, both quality-wise and in regards to reliability.




