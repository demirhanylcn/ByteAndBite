-- Retrieve payment amounts and categorize them by payment type based on specified range (Non-Equi Join)

SELECT P.AMOUNT, PT.NAME
FROM PAYMENT P, PAYMENT_TYPE PT
WHERE P.AMOUNT BETWEEN PT.LOW AND PT.HIGH;

-- Count total orders made in the year 2022 (Equi Join)

SELECT COUNT(*)
FROM PAYMENT P, VISIT V
WHERE V.ID = P.VISIT_ID
AND P.PAYMENT_DATE BETWEEN TO_DATE('2022-01-01', 'YYYY-MM-DD') AND TO_DATE('2022-12-31', 'YYYY-MM-DD');


-- Retrieve payments categorized as 'Normal' or 'Expensive' (Vertical Join)

SELECT P.AMOUNT, PT.NAME
FROM PAYMENT P, PAYMENT_TYPE PT
WHERE P.AMOUNT BETWEEN PT.LOW AND PT.HIGH
AND PT.NAME = 'Normal'

UNION

SELECT P.AMOUNT, PT.NAME
FROM PAYMENT P, PAYMENT_TYPE PT
WHERE P.AMOUNT BETWEEN PT.LOW AND PT.HIGH
AND PT.NAME = 'Expensive';

-- Display each chef with their master chef's ID, or 0 if they don't have a master chef (Outer Join with NVL)

SELECT C.ID, NVL(CF.ID,0)
FROM CHEF C, CHEF CF
WHERE C.MASTER_CHEF = CF.ID(+);


-- Find the maximum payment made in each year (Correlated Subquery)

SELECT ID, AMOUNT, P1.PAYMENT_DATE
FROM PAYMENT P1
WHERE AMOUNT = (
    SELECT MAX(AMOUNT)
    FROM PAYMENT P2
    WHERE EXTRACT(YEAR FROM P2.PAYMENT_DATE) = EXTRACT(YEAR FROM P1.PAYMENT_DATE)
);


-- Retrieve the chef who joined the restaurant the earliest (ALL Operator)


SELECT P.NAME, P.SURNAME
FROM PERSON P, CHEF C
WHERE P.ID = C.ID
AND C.HIREDATE < ALL (
SELECT HIREDATE 
FROM CHEF C1
WHERE C1.ID != C.ID);

-- Find any food item more expensive than 'Chocolate Cake' (ANY Operator)

SELECT *
FROM FOOD F
WHERE F.PRICE > ANY (
SELECT PRICE
FROM FOOD
WHERE NAME = 'Chocolate Cake');


-- Select chefs who have not cooked a specific dish ('Vegetable Stir-fry') (Correlated Subquery - NOT EXISTS)


SELECT C1.ID
FROM CHEF C1
WHERE NOT EXISTS (
SELECT C.ID
FROM COOKING C
JOIN FOOD F ON C.FOOD_ID = F.ID
WHERE NAME = 'Vegetable Stir-fry'
AND C.CHEF_ID = C1.ID)
ORDER BY C1.ID;


-- Retrieve ingredients used in the 'Chicken Alfredo' dish (Correlated Subquery - EXISTS)


SELECT *
FROM INGREDIENTS I
WHERE EXISTS (
SELECT R.INGREDIENT_ID
FROM RECIPE R
JOIN FOOD F ON R.FOOD_ID = F.ID
WHERE F.NAME = 'Chicken Alferdo'
AND R.INGREDIENT_ID = I.ID);

-- Identify chefs who are not supervising anyone


SELECT NAME, PERSON.ID
FROM CHEF,PERSON
WHERE CHEF.ID = PERSON.ID
MINUS
SELECT NAME, PERSON.ID
FROM CHEF,PERSON
WHERE PERSON.ID = CHEF.ID 
AND CHEF.ID IN ( 
SELECT MASTER_CHEF
FROM CHEF);

-- Count the number of times each food has been cooked, displaying only foods cooked more than twice (HAVING clause)

SELECT COUNT(FOOD.ID) as COOKED_TIMES, FOOD.NAME
FROM FOOD, COOKING
WHERE FOOD.ID = COOKING.FOOD_ID
GROUP BY FOOD.NAME
HAVING COUNT(FOOD.ID) > 2;

