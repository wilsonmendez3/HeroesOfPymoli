

```python
import pandas as pd
import numpy as np
import csv 
```


```python
file = "Resources/purchase_data.csv" 

pymoli_df = pd.read_csv(file)
pymoli_df.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>




```python
totalplayer = pymoli_df['SN'].value_counts()
totalplayercount = totalplayer.count()

totalplayer_df = pd.DataFrame({"Total Players" : [totalplayercount]})
totalplayer_df




```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>




```python
items = pymoli_df['Item ID'].value_counts()
no_items = len(items)
#print("Number of unique items : " + str(no_items))

avg_price = pymoli_df['Price'].mean()
#print("Average Price : " + str(avg_price))

total_purchases = pymoli_df['Price'].count()
#print("Total Purchases : " + str(total_purchases))

revenue = pymoli_df['Price'].sum()
#print("Revenue : " + str(revenue))

new_df = pd.DataFrame({"Unique Items" : [no_items],
                        "Average Purchase Price" : [avg_price],
                        "Total Purchases" : [total_purchases],
                        "Revenue" : [revenue]})


new_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unique Items</th>
      <th>Average Purchase Price</th>
      <th>Total Purchases</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>3.050987</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
pymoli_cleandf = pymoli_df.drop_duplicates(subset=["SN", "Gender"], keep="first")

gender = pymoli_cleandf['Gender'].value_counts()
gender_d = dict(gender)
gendercount = pymoli_cleandf['Gender'].count()

malecount_cl = gender_d['Male']
maleperc = (malecount_cl / gendercount)
maleperc = maleperc * 100
maleperc = round(maleperc, 2)

femalecount_cl = gender_d['Female']
femaleperc = (femalecount_cl / gendercount) * 100
femaleperc = round(femaleperc, 2)

nonbincount_cl = gender_d['Other / Non-Disclosed']
nonbinperc = nonbincount_cl / gendercount
nonbinperc = nonbinperc * 100 
nonbinperc = round(nonbinperc, 2)


genderlist = [ (str(malecount_cl), str(maleperc)),
             (str(femalecount_cl), str(femaleperc)) ,
             (str(nonbincount_cl), str(nonbinperc) )]


dfGender = pd.DataFrame(genderlist, columns = ['Total Count' , 'Total Percentage',], index=['Male', 'Female', 'Nonbinary'])
dfGender

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count</th>
      <th>Total Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>84.03</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>14.06</td>
    </tr>
    <tr>
      <th>Nonbinary</th>
      <td>11</td>
      <td>1.91</td>
    </tr>
  </tbody>
</table>
</div>




```python
#PURCHASE COUNT BY GENDER
purchasecount = pymoli_df['Gender'].value_counts()
purchasecount_d = dict(purchasecount)
#purchasecount = pymoli_df['Price'].count()

malecount = purchasecount_d['Male']
femalecount= purchasecount_d['Female']
nonbincount = purchasecount_d['Other / Non-Disclosed']

#PURCHASE
sumofgender = pymoli_df.groupby('Gender')['Price'].sum()
sumofgender_d = dict(sumofgender)

malesum = sumofgender_d['Male']
malesum = round(malesum, 2)           
femalesum = sumofgender_d['Female']
femalesum = round(femalesum, 2)
nonbinsum = sumofgender_d['Other / Non-Disclosed']
nonbinsum = round(nonbinsum, 2)

avg_pricemale = round((malesum / malecount), 2)
avg_pricefemale = round((femalesum / femalecount), 2)
avg_pricenon = round((nonbinsum / nonbincount), 2)

#print(purchase)
print(avg_pricemale)
print(malesum)
```

    3.02
    1967.64



```python
# totalplayer = pymoli_df.groupby(['Gender'])['SN'].value_counts()
# totalplayer_d = dict(totalplayer)
# #totalplayercount = totalplayer.groupby['Gender')
# #print(totalplayer_d['Female'])
# # print(totalplayer_d[('Female', 'Chamjask73')])

# totalplayer_dval = totalplayer_d.values()
# #print(totalplayer_dval)
```


```python
# sumpppg = pymoli_df.groupby('Gender')['Price'].sum()
# sumpppg_d = dict(sumpppg)
# #totalplayercount = totalplayer.groupby['Gender')
# #print(sumpppg_d[('Female', 'Chamjask73')])

# #sumpppg_dval = sumpppg_d.values()
# print(sumpppg_d)
```


```python
# avg_purchase_total_by_gender = []
# for count_purchases in totalplayer_dval:
#     for total_purchases in sumpppg_dval:
#         avg_purchase_total_by_gender.append(total_purchases / count_purchases)
        
#print(avg_purchase_total_by_gender)


male_avgpurch = round((malesum / malecount_cl), 2)
female_avgpurch = round((femalesum / femalecount_cl), 2)
nonbin_avgpurch = round((nonbinsum / nonbincount_cl), 2)
```


```python
PurchAnal = [(str(malecount), str(avg_pricemale), str(malesum), str(male_avgpurch)) ,
             (str(femalecount), str(avg_pricefemale), str(femalesum), str(female_avgpurch)) ,
             (str(nonbincount), str(avg_pricenon), str(nonbinsum), str(nonbin_avgpurch))]

PurchAnal_df = pd.DataFrame(PurchAnal, columns = ['Purchase Count', 'Average Purchase Price','Total Purchase Value', 'Avg Total Purchase per Person',], index=['Male', 'Female', 'Nonbinary'])
PurchAnal_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>3.02</td>
      <td>1967.64</td>
      <td>4.07</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>113</td>
      <td>3.2</td>
      <td>361.94</td>
      <td>4.47</td>
    </tr>
    <tr>
      <th>Nonbinary</th>
      <td>15</td>
      <td>3.35</td>
      <td>50.19</td>
      <td>4.56</td>
    </tr>
  </tbody>
</table>
</div>




```python
pymoli_clean_age = pymoli_df.drop_duplicates(subset=["SN", "Age"], keep="first")
clean_count = pymoli_clean_age.count()

bins = [0, 9, 14, 19, 24, 29, 34, 39, 45]
names = ['<10', '10-14', '15-19', '20-24', '24-29', '30-34', '35-39', '40+']
#sn_count = []

pymoli_test = pymoli_clean_age.groupby(pd.cut(pymoli_clean_age['Age'], bins, labels=names))['SN'].count()
pymoli_test_d = dict(pymoli_test)
#print(pymoli_test_d)

sn_count = pymoli_test_d.values()
sn_count_list = list(sn_count)

sn_percount = []
for item in sn_count_list:
    perc_count = round( ((item / totalplayercount) * 100.00), 2 )
    sn_percount.append(perc_count)
#print(pymoli_test_d)

age_df = pd.DataFrame(
    {'Total Count': sn_count_list,
     'Percentage of Players': sn_percount,
    }, index=names)
age_df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.82</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79</td>
    </tr>
    <tr>
      <th>24-29</th>
      <td>77</td>
      <td>13.37</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08</td>
    </tr>
  </tbody>
</table>
</div>




```python
#PURCHASE COUNT BY AGE
pymoli_agecount = pymoli_df.groupby(pd.cut(pymoli_df['Age'], bins, labels=names))['SN'].count()
pymoli_agecount_d = dict(pymoli_agecount)
pymoli_agecount_list = list(pymoli_agecount_d.values())
#print(pymoli_agecount_list)

#Total Purchase Value 
pymoli_agepurch = pymoli_df.groupby(pd.cut(pymoli_df['Age'], bins, labels=names))['Price'].sum()
pymoli_agepurch_d = dict(pymoli_agepurch)
pymoli_agepurch_list = list(pymoli_agepurch_d.values())
#print(pymoli_agepurch_d)

# pymoli_avgpurch = []
# for sumpurch in pymoli_agepurch_list:
#     for count in pymoli_agecount_list:
#         pymoli_avgpurch.append(sumpurch/count)

avpurchage = [pymoli_agepurch_list,pymoli_agecount_list]
avpurchage_list = [(x/y) for x,y in zip(*avpurchage)]



avpurchage_pp = [pymoli_agepurch_list,sn_count_list]
avpurchage_pp_list = [(x/y) for x,y in zip(*avpurchage_pp)]
        
print(avpurchage_pp_list)
```

    [4.537058823529412, 3.7627272727272723, 3.85878504672897, 4.3180620155038785, 3.805194805194803, 4.115384615384615, 4.763548387096773, 3.186666666666667]



```python
purchanalage_df = pd.DataFrame(
    {'Purchase Count': pymoli_agecount_list,
     'Average Purchase Price': avpurchage_list,
     'Total Purchase Value': pymoli_agepurch_list,
     'Avg Total Purchase per Person': avpurchage_pp_list,
    }, index=names)
purchanalage_df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>3.353478</td>
      <td>77.13</td>
      <td>4.537059</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>2.956429</td>
      <td>82.78</td>
      <td>3.762727</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>3.035956</td>
      <td>412.89</td>
      <td>3.858785</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>3.052219</td>
      <td>1114.06</td>
      <td>4.318062</td>
    </tr>
    <tr>
      <th>24-29</th>
      <td>101</td>
      <td>2.900990</td>
      <td>293.00</td>
      <td>3.805195</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>2.931507</td>
      <td>214.00</td>
      <td>4.115385</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>3.601707</td>
      <td>147.67</td>
      <td>4.763548</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>2.941538</td>
      <td>38.24</td>
      <td>3.186667</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchSN = pymoli_df.groupby('SN')['Price'].sum()
purchSN_d = dict(purchSN)
purchSN_d_index = sorted(purchSN_d, key=purchSN_d.get, reverse=True)[:5]

purchSN_d_values = [ purchSN_d[purchSN_d_index[0]], 
                    purchSN_d[purchSN_d_index[1]], 
                    purchSN_d[purchSN_d_index[2]], 
                    purchSN_d[purchSN_d_index[3]], 
                    purchSN_d[purchSN_d_index[4]] ]

purchSN_count = pymoli_df.groupby('SN')['Price'].count()
purchSN_count_d = dict(purchSN_count)

purchSN_d_count = [ purchSN_count_d[purchSN_d_index[0]], purchSN_count_d[purchSN_d_index[1]], purchSN_count_d[purchSN_d_index[2]], purchSN_count_d[purchSN_d_index[3]], purchSN_count_d[purchSN_d_index[4]] ]
                    
#print(purchSN_d_count)


avgtop5 = [purchSN_d_values,purchSN_d_count]
avgtop5_list = [(x/y) for x,y in zip(*avgtop5)]

```


```python
top5_df = pd.DataFrame(
    {'Purchase Count': purchSN_d_count,
     'Average Purchase Price': avgtop5_list,
     'Total Purchase Value': purchSN_d_values,
    }, index=purchSN_d_index)
top5_df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lisosia93</th>
      <td>5</td>
      <td>3.792000</td>
      <td>18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>3.862500</td>
      <td>15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>4.610000</td>
      <td>13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>3.405000</td>
      <td>13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>4.366667</td>
      <td>13.10</td>
    </tr>
  </tbody>
</table>
</div>




```python
#TOP 5 PURCHASES, BY ID 

popularItem = pymoli_df['Item ID'].value_counts()
popularItem_d = dict(popularItem)
popularItem_d_index = sorted(popularItem_d, key=popularItem_d.get, reverse=True)[:5]
#TOP 5 AND PURCHASE COUNT
popularItem_d_values = [ popularItem_d[popularItem_d_index[0]], 
                        popularItem_d[popularItem_d_index[1]], 
                        popularItem_d[popularItem_d_index[2]], 
                        popularItem_d[popularItem_d_index[3]], 
                        popularItem_d[popularItem_d_index[4]] ]

#print(popularItem_d_values)

#Getting ID and Name 
popularItm = pymoli_df.groupby('Item ID')['Item Name'].value_counts()
popularItm_d = dict(popularItm)
popularItm_d_index = sorted(popularItm_d, key=popularItm_d.get, reverse=True)[:5]
popularItm_d_index_d = dict(popularItm_d_index)
popularItm_d_index_d_keys = list(popularItm_d_index_d.keys())
popularItm_d_index_d_values = list(popularItm_d_index_d.values())


#TOP 5 AND THEIR TOTAL PURCHASE SUM 
popularItem_sum = pymoli_df.groupby('Item ID')['Price'].sum()
popularItem_sum_d = dict(popularItem_sum)
popularItem_sum_d_values = list(popularItem_sum_d.values())

popularItem_sum_d_sorted = sorted(popularItem_sum_d.values(), reverse=True)[:5]
#popularItem_d_sum = [popularItem_sum_d[popularItem_sum_d_sorted[0]], 
#                      popularItem_sum_d[popularItem_sum_d_sorted[1]], 
#                      popularItem_sum_d[popularItem_sum_d_sorted[2]], 
#                      popularItem_sum_d[popularItem_sum_d_sorted[3]], 
#                      popularItem_sum_d[popularItem_sum_d_sorted[4]]]


#print(popularItem_d_sum)


#print(popularItem_ID_d_index_d_keys)

#FINDING PRICE

popularItem_price = pymoli_df.groupby('Item ID')['Price'].value_counts()
popularItem_price_d = dict(popularItem_price)
popularItem_price_d_index = sorted(popularItem_price_d, key=popularItem_price_d.get, reverse=True)[:5]
popularItem_price_d2_index = dict(popularItem_price_d_index)
popularItem_price_d2_index_values = list(popularItem_price_d2_index.values())                          


#popularItem_price = pymoli_df('Item Name')['Price'].value_counts()
#popularItem_price_d = dict(popularItem_price)
#popularItem_price_d_values = list(popularItem_price_d.values())
#popularItem_price_d_index = sorted(popularItem_price_d, key=popularItem_price_d.get, reverse=True)[:5]


Totalpurchaseval = [] 
for i in range(0, len(popularItem_d_values)):
     Totalpurchaseval.append(popularItem_d_values[i]*popularItem_price_d2_index_values[i]) 
        
        
#print(Totalpurchaseval)
#print(popularItem_sum_d_values)
print(popularItm)
```


```python
top5items_df = pd.DataFrame(
    {'Item ID': popularItm_d_index_d_keys,
    'Name': popularItm_d_index_d_values,
     'Purchase Count': popularItem_d_values,
     'Item Price': popularItem_price_d2_index_values,
     'Total Purchase Value': Totalpurchaseval,
    },)
top5items_df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.23</td>
      <td>50.76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>9</td>
      <td>3.53</td>
      <td>31.77</td>
    </tr>
    <tr>
      <th>3</th>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.58</td>
      <td>41.22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>19</td>
      <td>Pursuit, Cudgel of Necromancy</td>
      <td>8</td>
      <td>1.02</td>
      <td>8.16</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python
profitableItem_sum = pymoli_df.groupby('Item ID')['Price'].sum()
profitableItem_sum_d = dict(profitableItem_sum)
#
profitableItem_d_index = sorted(profitableItem_sum_d, key=profitableItem_sum_d.get, reverse=True)[:5]
profitableItem_d_sum = [ profitableItem_sum_d[profitableItem_d_index[0]], 
                        profitableItem_sum_d[profitableItem_d_index[1]], 
                        profitableItem_sum_d[profitableItem_d_index[2]], 
                        profitableItem_sum_d[profitableItem_d_index[3]], 
                        profitableItem_sum_d[profitableItem_d_index[4]] ]

                   



profitableName = pymoli_df.groupby(['Item Name','Item ID'])['Price'].sum()
profitableName_d = dict(profitableName)
profitableName_d_index = sorted(profitableName_d, key=profitableName_d.get, reverse=True)[:5]
profitableName_d_index_d = dict(profitableName_d_index)
profitableName_d_index_d_keys = list(profitableName_d_index_d.keys())
profitableName_d_index_d_values = list(profitableName_d_index_d.values())

#print(profitableName_d_index_d_keys)


profitablePrice = pymoli_df.groupby(['Price','Item ID'])['Price'].sum()
profitablePrice_d = dict(profitablePrice)
profitablePrice_d_index = sorted(profitablePrice_d, key=profitablePrice_d.get, reverse=True)[:5]
profitablePrice_d_index_d = dict(profitablePrice_d_index)
profitablePrice_d_index_d_keys = list(profitablePrice_d_index_d.keys())
profitablePrice_d_index_d_values = list(profitablePrice_d_index_d.values())

#print(profitablePrice_d_index_d_keys)


profitableCount = pymoli_df.groupby('Item ID').agg({'Price': ['count','sum']}).reset_index()
profitableCount.sort_values([('Price', 'sum'), ('Price', 'count')], ascending=False)
#profitableCount.columns = profitableCount.columns.droplevel()
#profitableCount.columns = profitableCount.columns.droplevel()


#profitableCount = pd.DataFrame(pymoli_df.groupby('Item ID')['Price'].count())

profitableCount_zip = zip(profitableCount['count'], profitableCount['sum'])
#profitableCount_d = dict(profitableCount)
#profitableCount_d_index = sorted(profitableCount_d, key=profitableCount_d.get, reverse=True)[:5]

# profitableCount_count = profitableCount[[('Price', 'count')]]
# profitableCount = profitableCount.drop[['Item ID']]
# profitableCount_count_values = list(profitableCount_count_dict.values())

# profitableCount_sum = profitableCount[[('Price', 'sum')]]
# profitableCount_sum_dict = dict(profitableCount_sum)


#rofitableCount.sort_values(by=('Price', 'sum'), ascending=False)[:5]
#print(profitableCount)
print(profitableCount_zip)

#profitableCount_d = dict(profitableCount)
#profitableCount_d_values = list(profitableCount_d.values())

#profitableItem_sum_d = dict(profitableItem_sum)
#profitableCount_d_index = sorted(profitableCount, key=profitableCount.get, reverse=True)[:5]

# profitableCount_d_values = [ profitableCount_d[profitableCount_d_index[0]], 
#                         profitableCount_d[profitableCount_d_index[1]], 
#                         profitableCount_d[profitableCount_d_index[2]], 
#                         profitableCount_d[profitableCount_d_index[3]], 
#                         profitableCount_d[profitableCount_d_index[4]] ]


#profitableCount_d_index_d = dict(profitableCount_d_index)
# profitableCount_d_index_d_keys = list(profitableCount_d_index_d.keys())
# profitableCount_d_index_d_values = list(profitableCount_d_index_d.values())


```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    ~/anaconda3/lib/python3.7/site-packages/pandas/core/indexes/base.py in get_loc(self, key, method, tolerance)
       3077             try:
    -> 3078                 return self._engine.get_loc(key)
       3079             except KeyError:


    pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()


    pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()


    pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()


    pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()


    KeyError: 'count'

    
    During handling of the above exception, another exception occurred:


    KeyError                                  Traceback (most recent call last)

    <ipython-input-165-03037122cc4c> in <module>
         41 #profitableCount = pd.DataFrame(pymoli_df.groupby('Item ID')['Price'].count())
         42 
    ---> 43 profitableCount_zip = zip(profitableCount['count'], profitableCount['sum'])
         44 #profitableCount_d = dict(profitableCount)
         45 #profitableCount_d_index = sorted(profitableCount_d, key=profitableCount_d.get, reverse=True)[:5]


    ~/anaconda3/lib/python3.7/site-packages/pandas/core/frame.py in __getitem__(self, key)
       2684             return self._getitem_frame(key)
       2685         elif is_mi_columns:
    -> 2686             return self._getitem_multilevel(key)
       2687         else:
       2688             return self._getitem_column(key)


    ~/anaconda3/lib/python3.7/site-packages/pandas/core/frame.py in _getitem_multilevel(self, key)
       2728 
       2729     def _getitem_multilevel(self, key):
    -> 2730         loc = self.columns.get_loc(key)
       2731         if isinstance(loc, (slice, Series, np.ndarray, Index)):
       2732             new_columns = self.columns[loc]


    ~/anaconda3/lib/python3.7/site-packages/pandas/core/indexes/multi.py in get_loc(self, key, method)
       2235 
       2236         if not isinstance(key, tuple):
    -> 2237             loc = self._get_level_indexer(key, level=0)
       2238 
       2239             # _get_level_indexer returns an empty slice if the key has


    ~/anaconda3/lib/python3.7/site-packages/pandas/core/indexes/multi.py in _get_level_indexer(self, key, level, indexer)
       2494         else:
       2495 
    -> 2496             loc = level_index.get_loc(key)
       2497             if isinstance(loc, slice):
       2498                 return loc


    ~/anaconda3/lib/python3.7/site-packages/pandas/core/indexes/base.py in get_loc(self, key, method, tolerance)
       3078                 return self._engine.get_loc(key)
       3079             except KeyError:
    -> 3080                 return self._engine.get_loc(self._maybe_cast_indexer(key))
       3081 
       3082         indexer = self.get_indexer([key], method=method, tolerance=tolerance)


    pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()


    pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()


    pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()


    pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()


    KeyError: 'count'



```python
top5profit_df = pd.DataFrame(
    {'Item ID': profitableItem_d_index,
    'Name': profitableName_d_index_d_keys,
     'Purchase Count': popularItem_d_values,
     'Item Price': profitablePrice_d_index_d_keys,
     'Total Purchase Value': profitableItem_d_sum,
    },)
top5profit_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.23</td>
      <td>50.76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.58</td>
      <td>41.22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>92</td>
      <td>Final Critic</td>
      <td>9</td>
      <td>4.88</td>
      <td>39.04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>103</td>
      <td>Singed Scalpel</td>
      <td>8</td>
      <td>4.35</td>
      <td>34.80</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```
