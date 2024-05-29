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

hive> SELECT shop_id, SUM(price) AS total_price
FROM baby_products
WHERE product IN ('teddy_bear', 'baby_powder')
GROUP BY shop_id
ORDER BY total_price ASC
LIMIT 1;


Problem 3: program data.csv scissor bath_towel

hive> SELECT shop_id, SUM(price) AS total_price
FROM baby_products
WHERE product IN ('scissor', 'bath_towel')
GROUP BY shop_id
ORDER BY total_price ASC
LIMIT 1;


Problem 4: program data.csv scissor powder_puff cotton_balls

hive> SELECT shop_id, SUM(price) AS total_price
FROM baby_products
WHERE product IN ('scissor', 'powder_puff', 'cotton_balls')
GROUP BY shop_id
ORDER BY total_price ASC
LIMIT 1;
