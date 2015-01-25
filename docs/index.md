# Thinh-Quy

![Mou icon](http://25.io/mou/Mou_128.png)





##So do tong quat
![smaller icon](http://oi61.tinypic.com/2saxi0g.jpg)





## Cac cau lenh tao database
```
CREATE TABLE attributes
(
  id serial NOT NULL,
  name text,
  CONSTRAINT attributes_pkey PRIMARY KEY (id)
)
```
```
CREATE TABLE attributevalue
(
  id serial NOT NULL,
  attributeid integer,
  textvalue text,
  datadictionaryid integer,
  productid integer,
  CONSTRAINT attributevalue_pkey PRIMARY KEY (id)
)
```
```
CREATE TABLE category
(
  id serial NOT NULL,
  name text,
  parentcategoryid integer,
  CONSTRAINT category_pkey PRIMARY KEY (id)
)
```
```
CREATE TABLE datadictionary
(
  id serial NOT NULL,
  value text,
  CONSTRAINT datadictionary_pkey PRIMARY KEY (id)
)
```
```
CREATE TABLE distributor
(
  id serial NOT NULL,
  name text,
  CONSTRAINT distributor_pkey PRIMARY KEY (id)
)
```
```
CREATE TABLE manufacturer
(
  id serial NOT NULL,
  name text,
  CONSTRAINT manufacturer_pkey PRIMARY KEY (id)
)
```
```
CREATE TABLE product
(
  id serial NOT NULL,
  name text,
  sku text,
  description text,
  manufactorrid integer,
  date date,
  maintainduration integer,
  dateexpired date,
  originalprice integer,
  currentprice integer,
  categoryid integer,
  distributorid integer,
  CONSTRAINT product_pkey PRIMARY KEY (id)

)


```
## CAC CAU LENH TRUY VAN MAU
###Lay du lieu tu bang san pham

```
SELECT * FROM product as p
join category as c on p.categoryid = c.id
join manufacturer as m on p.manufactorrid =  m.id
join distributor as d on p.distributorid = d.id;
```
###Lay du lieu dong trong bang san pham


 ```
 select * from crosstab(
  
  '(select p.id ,p.name,a.name,d.value as value from attributes as a 
join attributevalue as  v on  a.id = v.attributeid
join datadictionary as d on d.id = v.datadictionaryid
join product as p on p.id = v.productid 
where v.textvalue is null
 order by 1,2)

UNION

select p.id ,p.name,a.name, v.textvalue as value from attributes as a 
join attributevalue as  v on  a.id = v.attributeid
join product as p on p.id = v.productid 
where v.textvalue is not null
order by 1,2' ,
'select distinct a.name from attributes as a order by 1'
) as (
  id text,
  name text,
  "bo nho trong" text,
  "chat lieu" text,
  "co man hinh" text,
  "dung tich" text,
  "kieu vay" text,
  "loai dieu hoa" text,
  "mau sac" text
  
  
  
  
) ; 

```

####Ket qua
![smaller icon](http://oi61.tinypic.com/2mpagbn.jpg)