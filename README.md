# PBI-html-visuals
CSS/HTML visuals for Power BI dashboards

## final result image:

![final result](https://raw.githubusercontent.com/Ronnie018/PBI-html-visuals/main/blobs/names.PNG?raw=true)

## database model image:

![database model](https://raw.githubusercontent.com/Ronnie018/PBI-html-visuals/main/blobs/database_model.PNG?raw=true)
 
NOME = name and CONTAGEM = count

## columns formulas

remember that this database model is gererated using another database with the folowing format

![model base](https://raw.githubusercontent.com/Ronnie018/PBI-html-visuals/main/blobs/model_base.PNG?raw=true)

### name / Count

#### method:
The base of all other calculated columns. Both are made using PowerQuery's GroupBy function passing the "name" column as comparission column and count lines as operation.

![database model](https://raw.githubusercontent.com/Ronnie018/PBI-html-visuals/main/blobs/groupby%20config.PNG?raw=true)

### RATIO
The percentage of the count in relation to the total data

#### method:
power BI calculated formula (DAX)

#### formula:
<pre>
<code>
RATIO = 
    VAR TOTAL = SUM(database_name[count])
    VAR PERC = (database_name[count] / TOTAL) * 100
    RETURN PERC
</code>
</pre>

TOTAL is a measure that simply sums all the occurrences.

### POSITION X / POSITION Y
this is a random position from 0 to 100 generated using DAX in both axis; It will be used to set to the name a random initial position at the screen.

#### method:
power BI calculated formula (DAX)

#### formula:

<pre>
<code>
    positionX = RANDBETWEEN(0,100)
</code>
</pre>

<pre>
<code>
    positionY = RANDBETWEEN(0,100)
</code>
</pre>

## INTEGER RATIO 

utility column that can be replaced by Ratio

#### method:
power BI calculated formula (DAX)

#### formula:

<pre>
<code>
    INTEGER_RATIO = ROUNDUP(numero_de_chamados_por_nome[RATIO], 0)
</code>
</pre>

In this case it's being used ROUNDUP, that rounds the number up, but there are three Round formulas available in DAX:
<ul>
 <li>ROUNDUP</li>
 <li>ROUNDDOWN</li>
 <li>ROUND</li>
</ul>

### FONT_SIZE 
Font size created to represent the name's percentage, without being too much great or small

#### method:
power BI calculated formula (DAX)

#### formula:

<pre>
<code>
    FONT_SIZE = if(
         numero_de_chamados_por_nome[RATIO] * 2 < 20,      // logical test
         ROUND(numero_de_chamados_por_nome[RATIO] * 2, 0), // value if true
         20                                                // value if false
     )
</code>
</pre>

### TEXT_WEIGHT

#### method:
power BI calculated formula (DAX)

#### formula:

<pre>
<code>
    TEXT_WEIGHT = IF(
        numero_de_chamados_por_nome[INTEGER_RATIO] * 100 > 900, // logical test
        900,                                                    // value if true
        numero_de_chamados_por_nome[INTEGER_RATIO] * 100        // value if false
    )
</code>
</pre>

### FROM X / FROM Y
selects from which side of the axle the position X and position Y will be applied

method: 
power BI calculated formula (DAX)

#### formula:

##### FROM X:
<pre>
<code>
    fromX = 
    VAR CHOICE = RANDBETWEEN(1,2)            // creates a binary random choice 
    RETURN IF (CHOICE = 1, "left", "right")  // converts the binary choice into CSS-readable values
</code>
</pre>

##### FROM Y:
<pre>
<code>
    fromX = 
    VAR CHOICE = RANDBETWEEN(1,2)           // creates a binary random choice 
    RETURN IF (CHOICE = 1, "top", "bottom") // converts the binary choice into CSS-readable values
</code>
</pre>

### COLORS 
Select the color the will be used to represent that ratio

##### method: 
power BI calculated formula (DAX) + model relationship

#### pre-requisites:
if you have a set of colors and want to test them for yourself just fill this column manually, otherwise, be sure that you have a table with columns and indexes as the folowing:

![database model](https://raw.githubusercontent.com/Ronnie018/PBI-html-visuals/main/blobs/colors_base.PNG?raw=true)

once you have it you can create a relationship beetween those indexes and a numeric columns on the database model:

![database model](https://raw.githubusercontent.com/Ronnie018/PBI-html-visuals/main/blobs/relationship.PNG?raw=true)

#### formula:

<pre>
<code>
    COLOR = LOOKUPVALUE(colors[colors], colors[Índice], [INTEGER_RATIO])
</code>
</pre>

