//To create table
hive> create table baby_products(
shop_id int, price float, product string)
row format delimited
fields terminated by ',';

//To load data.csv into table baby_products
hive> load data local inpath 'Desktop/data.csv' into table baby_products; 

Problem 1: program data.csv teddy_bear baby_powder

hive> select shop_id , sum(price) from baby_products where shop_id=2  group by shop_id;


Problem 3: program data.csv scissor bath_towel

hive> select shop_id , sum(price) from baby_products where shop_id=6 and product='scissor' and product='baby_towel' group by shop_id;


Problem 4: program data.csv scissor powder_puff cotton_balls

hive> select shop_id , sum(price) from baby_products where shop_id=6 and product='scissor' and product='powder_puff' and product = 'cotton_balls' group by shop_id;