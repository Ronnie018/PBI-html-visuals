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

#### 
