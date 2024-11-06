CREATE TABLE Person (
    ID NUMBER PRIMARY KEY,
    name VARCHAR2(50),
    surname VARCHAR2(50),
    phone_number VARCHAR2(50)
);

CREATE TABLE Chef (
    ID NUMBER PRIMARY KEY,
    mail_address VARCHAR2(50),
    address VARCHAR2(50),
    hiredate DATE,
    MASTER_CHEF NUMBER DEFAULT NULL,
    FOREIGN KEY (ID) REFERENCES Person(ID),
    FOREIGN KEY (MASTER_CHEF) REFERENCES Chef(ID) ON DELETE SET NULL
);

CREATE TABLE Customer (
    ID NUMBER PRIMARY KEY,
    address VARCHAR2(50),
    FOREIGN KEY (ID) REFERENCES Person(ID)
);

CREATE TABLE Food (
    ID NUMBER PRIMARY KEY,
    name VARCHAR2(50),
    price FLOAT(15)
);

CREATE TABLE Cooking (
    ID NUMBER PRIMARY KEY,
    Food_ID NUMBER,
    Chef_ID NUMBER,
    FOREIGN KEY (Food_ID) REFERENCES Food(ID),
    FOREIGN KEY (Chef_ID) REFERENCES Chef(ID)
);

CREATE TABLE Ingredients (
    ID NUMBER PRIMARY KEY,
    name VARCHAR2(50),
    type VARCHAR2(50)
);

CREATE TABLE Recipe (
    ID NUMBER PRIMARY KEY,
    Ingredient_ID NUMBER,
    Food_ID NUMBER,
    Amount_ingredient NUMBER,
    FOREIGN KEY (Ingredient_ID) REFERENCES Ingredients(ID),
    FOREIGN KEY (Food_ID) REFERENCES Food(ID)
);

CREATE TABLE VISIT (
    ID NUMBER PRIMARY KEY,
    visit_date DATE,
    Customer_ID NUMBER,
    FOREIGN KEY (Customer_ID) REFERENCES Customer(ID)
);

CREATE TABLE Payment (
    ID NUMBER PRIMARY KEY,
    payment_date DATE,
    amount FLOAT(50),
    VISIT_ID NUMBER,
    FOREIGN KEY (VISIT_ID) REFERENCES VISIT(ID)
);

CREATE TABLE "Order" (
    ID NUMBER PRIMARY KEY,
    Food_ID NUMBER,
    Amount NUMBER,
    VISIT_ID NUMBER,
    FOREIGN KEY (Food_ID) REFERENCES Food(ID),
    FOREIGN KEY (VISIT_ID) REFERENCES VISIT(ID)
);

CREATE TABLE PAYMENT_TYPE (
    NAME VARCHAR2(50) PRIMARY KEY,
    LOW NUMBER,
    HIGH NUMBER
);
