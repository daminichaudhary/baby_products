Write a program that accepts a price file of baby products(format below) as CSV file, and a list of products that someone wants to buy, and outputs the shop they should go to, and the total price it will cost them. It is okay to purchase extra products, as long as the total cost is minimized.

price file format
shop ID, price, product 1 label (single product)
shop ID, price, product 1 label, product 2 label, ... (combo packs with multiple products)

Shop IDs are integers, all products are lower case letters and underscores, and the price is a decimal number.

Here are some samples:

Sample Data set:

Data File data.csv

1, 4.00, teddy_bear
1, 8.00, baby_powder
2, 5.00, teddy_bear
2, 6.50, baby_powder
3, 4.00, pampers_diapers
3, 8.00, johnson_wipes
4, 5.00, johnson_wipes
4, 2.50, cotton_buds
5, 4.00, bath_towel
5, 8.00, scissor
6, 5.00, scissor
6, 6.00, bath_towel, cotton_balls, powder_puff



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