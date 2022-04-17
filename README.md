# sql
create database store;<br/>
use store;<br/>
CREATE TABLE countries (<br/>
    code int NOT NULL,<br/>
    name varchar(20) unique ,<br/>
    continent_name varchar(20)  NOT NULL,<br/>
    PRIMARY KEY (code)<br/>
);
<br/><br/>
use store;<br/>
CREATE TABLE users (<br/>
    id int NOT NULL,<br/>
    full_name varchar(20) ,<br/>
    email varchar(20) unique,<br/>
    gender char(1) ,<br/>
	data_of_birth varchar(15) ,<br/>
    created_at datetime DEFAULT CURRENT_TIMESTAMP,<br/>
    country_code int ,<br/>
    check(gender in ('m', 'f')),<br/>
    PRIMARY KEY (id),<br/>
    FOREIGN KEY (country_code) REFERENCES countries(code)<br/>
);<br/><br/>

use store;<br/>
CREATE TABLE orders (<br/>
    id int NOT NULL,<br/>
    status varchar(6) ,<br/>
    created_at datetime DEFAULT CURRENT_TIMESTAMP  ,<br/>
    user_id int ,<br/>
     check(status in ('start', 'finish')),<br/>
    PRIMARY KEY (id),<br/>
    FOREIGN KEY (user_id) REFERENCES users(id)<br/>
);<br/><br/>


use store;<br/>
CREATE TABLE products (<br/>
    id int NOT NULL,<br/>
    name varchar(10) NOT NULL ,<br/>
      price int DEFAULT 0 ,<br/>
      status varchar(10) ,<br/>
    created_at datetime DEFAULT CURRENT_TIMESTAMP,<br/>
    check(status in ('valid', 'expired')),<br/>
    PRIMARY KEY (id)<br/>
);<br/><br/>

use store;<br/>
CREATE TABLE order_products (<br/>
    order_id int NOT NULL ,<br/>
    product_id int NOT NULL ,<br/>
    quantity int DEFAULT 0 ,<br/>
    PRIMARY KEY (order_id,product_id),<br/>
    FOREIGN KEY (order_id) REFERENCES orders(id),<br/>
    FOREIGN KEY (product_id) REFERENCES products(id)<br/>
);<br/><br/>

use store;<br/>
INSERT INTO countries<br/>
VALUES (2,"ksa", "saudi arabia");<br/><br/>
use store;<br/>
INSERT INTO users (id,full_name,email,gender,data_of_birth,country_code)<br/>
VALUES (2,"nourah","nourah@gmail.com","m","1-2-2022",2);<br/><br/>
use store;<br/>
INSERT INTO orders (id,status,user_id)<br/>
VALUES (2,"start",2);<br/><br/>
use store;<br/>
INSERT INTO products (id,name,price,status)<br/>
VALUES (2,"X",200,"valid");<br/><br/>
use store;<br/>
INSERT INTO order_products <br/>
VALUES (2,2,200);<br/><br/>
use store;<br/>
UPDATE countries<br/>
SET name='X' WHERE code = 2;<br/><br/>
use store;<br/>
DELETE FROM order_products WHERE product_id=2;<br/>
DELETE FROM products WHERE id=2;<br/>
