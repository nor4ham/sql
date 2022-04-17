# sql
create database store;
use store;
CREATE TABLE countries (
    code int NOT NULL,
    name varchar(20) unique ,
    continent_name varchar(20)  NOT NULL,
    PRIMARY KEY (code)
);
<br/>
use store;
CREATE TABLE users (
    id int NOT NULL,
    full_name varchar(20) ,
    email varchar(20) unique,
    gender char(1) ,
	data_of_birth varchar(15) ,
    created_at datetime DEFAULT CURRENT_TIMESTAMP,
    country_code int ,
    check(gender in ('m', 'f')),
    PRIMARY KEY (id),
    FOREIGN KEY (country_code) REFERENCES countries(code)
);

use store;
CREATE TABLE orders (
    id int NOT NULL,
    status varchar(6) ,
    created_at datetime DEFAULT CURRENT_TIMESTAMP  ,
    user_id int ,
     check(status in ('start', 'finish')),
    PRIMARY KEY (id),
    FOREIGN KEY (user_id) REFERENCES users(id)
);


use store;
CREATE TABLE products (
    id int NOT NULL,
    name varchar(10) NOT NULL ,
      price int DEFAULT 0 ,
      status varchar(10) ,
    created_at datetime DEFAULT CURRENT_TIMESTAMP,
    check(status in ('valid', 'expired')),
    PRIMARY KEY (id)
);

use store;
CREATE TABLE order_products (
    order_id int NOT NULL ,
    product_id int NOT NULL ,
    quantity int DEFAULT 0 ,
    PRIMARY KEY (order_id,product_id),
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);

use store;
INSERT INTO countries
VALUES (2,"ksa", "saudi arabia");
use store;
INSERT INTO users (id,full_name,email,gender,data_of_birth,country_code)
VALUES (2,"nourah","nourah@gmail.com","m","1-2-2022",2);
use store;
INSERT INTO orders (id,status,user_id)
VALUES (2,"start",2);
use store;
INSERT INTO products (id,name,price,status)
VALUES (2,"X",200,"valid");
use store;
INSERT INTO order_products 
VALUES (2,2,200);
use store;
UPDATE countries
SET name='X' WHERE code = 2;
use store;
DELETE FROM order_products WHERE product_id=2;
DELETE FROM products WHERE id=2;
