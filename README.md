First of all we have to create tables in the database(Mysql) which is useful for storing data like restaurant data and user data and 
orders data are etc here mysql is used for storing data, fetching data and Inserting data .In this project I have used this following tables


1 User Table

  CREATE TABLE foodapp.user (
  userId INT NOT NULL AUTO_INCREMENT,
  userName VARCHAR(45) NULL,
  email VARCHAR(45) NOT NULL,
  phoneNumber VARCHAR(45) NULL,
  password VARCHAR(45) NOT NULL,
  address VARCHAR(45) NULL,
  createdDate DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  lastLogin DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (userId));

2 Restaurant Table

CREATE TABLE foodapp.restaurant (
  restaurantId INT NOT NULL AUTO_INCREMENT,
  restaurantName VARCHAR(45) NOT NULL,
  deliveryTime DATETIME NOT NULL,
  cuisineType VARCHAR(45) NOT NULL,
  address VARCHAR(45) NOT NULL,
  ratings FLOAT NULL,
  isActive VARCHAR(45) NOT NULL,
  adminId INT NULL,
  imgPath VARCHAR(45) NULL,
  PRIMARY KEY (restaurantId));

3  Menu Table

CREATE TABLE foodapp.menu (
  menuId INT NOT NULL AUTO_INCREMENT,
  restaurantId INT NOT NULL,
  menuName VARCHAR(45) NOT NULL,
  price FLOAT NOT NULL,
  description VARCHAR(205) NOT NULL,
  isAvailable VARCHAR(45) NOT NULL,
  imgPath VARCHAR(45) NULL,
  PRIMARY KEY (menuId),
  INDEX fk1_idx (restaurantId ASC) VISIBLE,
  CONSTRAINT fk1
    FOREIGN KEY (restaurantId)
    REFERENCES foodapp.restaurant (restaurantId)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);

4 Order Table

CREATE TABLE foodapp.ordertable (
  orderId INT NOT NULL AUTO_INCREMENT,
  restaurantId INT NOT NULL,
  userId INT NOT NULL,
  orderDate DATE NOT NULL,
  totalAmount FLOAT NOT NULL,
  status VARCHAR(45) NOT NULL,
  paymentMode VARCHAR(45) NOT NULL,
  PRIMARY KEY (orderId),
  INDEX fk2_idx (userId ASC) VISIBLE,
  INDEX fk3_idx (restaurantId ASC) VISIBLE,
  CONSTRAINT fk2
    FOREIGN KEY (userId)
    REFERENCES foodapp.user (userId)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT fk3
    FOREIGN KEY (restaurantId)
    REFERENCES foodapp.restaurant (restaurantId)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);

5 OrderItem Table

CREATE TABLE foodapp.orderitem (
  orderItemId INT NOT NULL AUTO_INCREMENT,
  orderId INT NOT NULL,
  menuId INT NOT NULL,
  quantity INT NOT NULL,
  subTotal FLOAT NOT NULL,
  PRIMARY KEY (orderItemId),
  INDEX fk4_idx (menuId ASC) VISIBLE,
  INDEX fk5_idx (orderId ASC) VISIBLE,
  CONSTRAINT fk4
    FOREIGN KEY (menuId)
    REFERENCES foodapp.menu (menuId)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT fk5
    FOREIGN KEY (orderId)
    REFERENCES foodapp.ordertable (orderId)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);

6 OrderHistory Table

CREATE TABLE foodapp.orderhistory (
  orderHistoryId INT NOT NULL AUTO_INCREMENT,
  orderId INT NOT NULL,
  userId INT NOT NULL,
  orderDate DATETIME NOT NULL,
  totalAmount FLOAT NOT NULL,
  status VARCHAR(45) NULL,
  PRIMARY KEY (orderHistoryId),
  INDEX fk6_idx (orderId ASC) VISIBLE,
  INDEX fk7_idx (userId ASC) VISIBLE,
  CONSTRAINT fk6
    FOREIGN KEY (orderId)
    REFERENCES foodapp.ordertable (orderId)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT fk7
    FOREIGN KEY (userId)
    REFERENCES foodapp.user (userId)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION);
    
 Home page is looks like this 
![image](https://github.com/user-attachments/assets/1fc7c4eb-8246-47b2-b974-2c45d1e81d5b)
![image](https://github.com/user-attachments/assets/dc846792-2c42-4937-8491-5f420a85f637)
 Menu looks like this  
![image](https://github.com/user-attachments/assets/2ddbc77e-65fd-4d9e-a967-1faaddd5b977)
