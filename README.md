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
         numero_de_chamados_por_nome[RATIO] * 2 < 20,      # logical test
         ROUND(numero_de_chamados_por_nome[RATIO] * 2, 0), # value if true
         20                                                # value if false
     )
</code>
</pre>
