What’s cooking
================
Silke Johannsen
2019-03-01

## R information

All analyses were performed using R (ver. 3.5.1) \[R Core Team, 2018\].

## Load & inspect the data

The data set from the Kaggle competition, What’s cooking is stored in
JSON format. Load the train and test data with the jsonlite package and
inspect the objects.

<br>

<table class="table" style="margin-left: auto; margin-right: auto;">

<caption>

Train data frame:

</caption>

<thead>

<tr>

<th style="text-align:right;">

id

</th>

<th style="text-align:left;">

cuisine

</th>

<th style="text-align:left;">

ingredients

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:right;">

10259

</td>

<td style="text-align:left;">

greek

</td>

<td style="text-align:left;">

c(“romaine lettuce”, “black olives”, “grape tomatoes”, “garlic”,
“pepper”, “purple onion”, “seasoning”, “garbanzo beans”, “feta
cheese crumbles”)

</td>

</tr>

<tr>

<td style="text-align:right;">

25693

</td>

<td style="text-align:left;">

southern\_us

</td>

<td style="text-align:left;">

c(“plain flour”, “ground pepper”, “salt”, “tomatoes”, “ground black
pepper”, “thyme”, “eggs”, “green tomatoes”, “yellow corn meal”, “milk”,
“vegetable oil”)

</td>

</tr>

<tr>

<td style="text-align:right;">

20130

</td>

<td style="text-align:left;">

filipino

</td>

<td style="text-align:left;">

c(“eggs”, “pepper”, “salt”, “mayonaise”, “cooking oil”, “green chilies”,
“grilled chicken breasts”, “garlic powder”, “yellow onion”, “soy sauce”,
“butter”, “chicken livers”)

</td>

</tr>

<tr>

<td style="text-align:right;">

22213

</td>

<td style="text-align:left;">

indian

</td>

<td style="text-align:left;">

c(“water”, “vegetable oil”, “wheat”, “salt”)

</td>

</tr>

<tr>

<td style="text-align:right;">

13162

</td>

<td style="text-align:left;">

indian

</td>

<td style="text-align:left;">

c(“black pepper”, “shallots”, “cornflour”, “cayenne pepper”, “onions”,
“garlic paste”, “milk”, “butter”, “salt”, “lemon juice”, “water”,
“chili powder”, “passata”, “oil”, “ground cumin”, “boneless chicken
skinless thigh”, “garam masala”, “double cream”, “natural yogurt”, “bay
leaf”)

</td>

</tr>

<tr>

<td style="text-align:right;">

6602

</td>

<td style="text-align:left;">

jamaican

</td>

<td style="text-align:left;">

c(“plain flour”, “sugar”, “butter”, “eggs”, “fresh ginger root”, “salt”,
“ground cinnamon”, “milk”, “vanilla extract”, “ground ginger”, “powdered
sugar”, “baking powder”)

</td>

</tr>

</tbody>

</table>

<table class="table" style="margin-left: auto; margin-right: auto;">

<caption>

Test data frame:

</caption>

<thead>

<tr>

<th style="text-align:right;">

id

</th>

<th style="text-align:left;">

ingredients

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:right;">

18009

</td>

<td style="text-align:left;">

c(“baking powder”, “eggs”, “all-purpose flour”, “raisins”, “milk”,
“white sugar”)

</td>

</tr>

<tr>

<td style="text-align:right;">

28583

</td>

<td style="text-align:left;">

c(“sugar”, “egg yolks”, “corn starch”, “cream of tartar”, “bananas”,
“vanilla wafers”, “milk”, “vanilla extract”, “toasted pecans”, “egg
whites”, “light rum”)

</td>

</tr>

<tr>

<td style="text-align:right;">

41580

</td>

<td style="text-align:left;">

c(“sausage links”, “fennel bulb”, “fronds”, “olive oil”, “cuban
peppers”, “onions”)

</td>

</tr>

<tr>

<td style="text-align:right;">

29752

</td>

<td style="text-align:left;">

c(“meat cuts”, “file powder”, “smoked sausage”, “okra”, “shrimp”,
“andouille sausage”, “water”, “paprika”, “hot sauce”, “garlic cloves”,
“browning”, “lump crab meat”, “vegetable oil”, “all-purpose flour”,
“freshly ground pepper”, “flat leaf parsley”, “boneless chicken
skinless thigh”, “dried thyme”, “white rice”, “yellow onion”, “ham”)

</td>

</tr>

<tr>

<td style="text-align:right;">

35687

</td>

<td style="text-align:left;">

c(“ground black pepper”, “salt”, “sausage casings”, “leeks”, “parmigiano
reggiano cheese”, “cornmeal”, “water”, “extra-virgin olive oil”)

</td>

</tr>

<tr>

<td style="text-align:right;">

38527

</td>

<td style="text-align:left;">

c(“baking powder”, “all-purpose flour”, “peach slices”, “corn starch”,
“heavy cream”, “lemon juice”, “unsalted butter”, “salt”, “white
sugar”)

</td>

</tr>

</tbody>

</table>

<br>

The train data have three columns named id, cuisine and ingredients,
with the ingredients column being a list. The variable id has no
duplicates and 39,774 unique entries. There are 20 distinct cuisine
entries.

The test data have two columns, id and ingredients. Ingredients again as
a list. The variable id has no duplicates and 9,944 unique entries. None
of the id’s in the test data set are present in the train data set.

Using unnest from the tidyr package to extract the ingredients list into
a more user friendly format.

<br>

<table class="table" style="margin-left: auto; margin-right: auto;">

<caption>

Train data frame flat:

</caption>

<thead>

<tr>

<th style="text-align:center;">

id

</th>

<th style="text-align:center;">

cuisine

</th>

<th style="text-align:center;">

ingredients

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

10259

</td>

<td style="text-align:center;">

greek

</td>

<td style="text-align:center;">

romaine lettuce

</td>

</tr>

<tr>

<td style="text-align:center;">

10259

</td>

<td style="text-align:center;">

greek

</td>

<td style="text-align:center;">

black olives

</td>

</tr>

<tr>

<td style="text-align:center;">

10259

</td>

<td style="text-align:center;">

greek

</td>

<td style="text-align:center;">

grape tomatoes

</td>

</tr>

<tr>

<td style="text-align:center;">

10259

</td>

<td style="text-align:center;">

greek

</td>

<td style="text-align:center;">

garlic

</td>

</tr>

<tr>

<td style="text-align:center;">

10259

</td>

<td style="text-align:center;">

greek

</td>

<td style="text-align:center;">

pepper

</td>

</tr>

<tr>

<td style="text-align:center;">

10259

</td>

<td style="text-align:center;">

greek

</td>

<td style="text-align:center;">

purple onion

</td>

</tr>

</tbody>

</table>

<table class="table" style="margin-left: auto; margin-right: auto;">

<caption>

Test data frame flat:

</caption>

<thead>

<tr>

<th style="text-align:center;">

id

</th>

<th style="text-align:center;">

ingredients

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

18009

</td>

<td style="text-align:center;">

baking powder

</td>

</tr>

<tr>

<td style="text-align:center;">

18009

</td>

<td style="text-align:center;">

eggs

</td>

</tr>

<tr>

<td style="text-align:center;">

18009

</td>

<td style="text-align:center;">

all-purpose flour

</td>

</tr>

<tr>

<td style="text-align:center;">

18009

</td>

<td style="text-align:center;">

raisins

</td>

</tr>

<tr>

<td style="text-align:center;">

18009

</td>

<td style="text-align:center;">

milk

</td>

</tr>

<tr>

<td style="text-align:center;">

18009

</td>

<td style="text-align:center;">

white sugar

</td>

</tr>

</tbody>

</table>

<br>

It is now easy to do some simple summary analysis on the data using the
dplyr & skimr package.

<br>

<table class="table" style="margin-left: auto; margin-right: auto;">

<caption>

Train data: Summary statistics

</caption>

<thead>

<tr>

<th style="text-align:left;">

type

</th>

<th style="text-align:left;">

variable

</th>

<th style="text-align:left;">

missing

</th>

<th style="text-align:left;">

complete

</th>

<th style="text-align:left;">

n

</th>

<th style="text-align:left;">

n\_unique

</th>

<th style="text-align:left;">

top\_counts

</th>

<th style="text-align:left;">

ordered

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

factor

</td>

<td style="text-align:left;">

cuisine

</td>

<td style="text-align:left;">

0

</td>

<td style="text-align:left;">

428275

</td>

<td style="text-align:left;">

428275

</td>

<td style="text-align:left;">

20

</td>

<td style="text-align:left;">

ita: 77667, mex: 70029, sou: 41623, ind: 38156

</td>

<td style="text-align:left;">

FALSE

</td>

</tr>

<tr>

<td style="text-align:left;">

factor

</td>

<td style="text-align:left;">

id

</td>

<td style="text-align:left;">

0

</td>

<td style="text-align:left;">

428275

</td>

<td style="text-align:left;">

428275

</td>

<td style="text-align:left;">

39774

</td>

<td style="text-align:left;">

388: 65, 134: 59, 130: 52, 225: 49

</td>

<td style="text-align:left;">

FALSE

</td>

</tr>

<tr>

<td style="text-align:left;">

factor

</td>

<td style="text-align:left;">

ingredients

</td>

<td style="text-align:left;">

0

</td>

<td style="text-align:left;">

428275

</td>

<td style="text-align:left;">

428275

</td>

<td style="text-align:left;">

6714

</td>

<td style="text-align:left;">

sal: 18049, oli: 7972, oni: 7972, wat: 7457

</td>

<td style="text-align:left;">

FALSE

</td>

</tr>

</tbody>

</table>

<table class="table" style="margin-left: auto; margin-right: auto;">

<caption>

Train data: Top 10 Ingredients

</caption>

<thead>

<tr>

<th style="text-align:left;">

ingredients

</th>

<th style="text-align:right;">

n

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

salt

</td>

<td style="text-align:right;">

18049

</td>

</tr>

<tr>

<td style="text-align:left;">

olive oil

</td>

<td style="text-align:right;">

7972

</td>

</tr>

<tr>

<td style="text-align:left;">

onions

</td>

<td style="text-align:right;">

7972

</td>

</tr>

<tr>

<td style="text-align:left;">

water

</td>

<td style="text-align:right;">

7457

</td>

</tr>

<tr>

<td style="text-align:left;">

garlic

</td>

<td style="text-align:right;">

7380

</td>

</tr>

<tr>

<td style="text-align:left;">

sugar

</td>

<td style="text-align:right;">

6434

</td>

</tr>

<tr>

<td style="text-align:left;">

garlic cloves

</td>

<td style="text-align:right;">

6237

</td>

</tr>

<tr>

<td style="text-align:left;">

butter

</td>

<td style="text-align:right;">

4848

</td>

</tr>

<tr>

<td style="text-align:left;">

ground black pepper

</td>

<td style="text-align:right;">

4785

</td>

</tr>

<tr>

<td style="text-align:left;">

all-purpose flour

</td>

<td style="text-align:right;">

4632

</td>

</tr>

</tbody>

</table>

<table class="table" style="margin-left: auto; margin-right: auto;">

<caption>

Test data: Top 10 Ingredients

</caption>

<thead>

<tr>

<th style="text-align:left;">

ingredients

</th>

<th style="text-align:right;">

n

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

salt

</td>

<td style="text-align:right;">

4485

</td>

</tr>

<tr>

<td style="text-align:left;">

onions

</td>

<td style="text-align:right;">

2036

</td>

</tr>

<tr>

<td style="text-align:left;">

olive oil

</td>

<td style="text-align:right;">

1917

</td>

</tr>

<tr>

<td style="text-align:left;">

water

</td>

<td style="text-align:right;">

1836

</td>

</tr>

<tr>

<td style="text-align:left;">

garlic

</td>

<td style="text-align:right;">

1791

</td>

</tr>

<tr>

<td style="text-align:left;">

sugar

</td>

<td style="text-align:right;">

1630

</td>

</tr>

<tr>

<td style="text-align:left;">

garlic cloves

</td>

<td style="text-align:right;">

1535

</td>

</tr>

<tr>

<td style="text-align:left;">

butter

</td>

<td style="text-align:right;">

1230

</td>

</tr>

<tr>

<td style="text-align:left;">

ground black pepper

</td>

<td style="text-align:right;">

1205

</td>

</tr>

<tr>

<td style="text-align:left;">

all-purpose flour

</td>

<td style="text-align:right;">

1184

</td>

</tr>

</tbody>

</table>
