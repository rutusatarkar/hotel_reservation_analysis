SELECT * FROM hotel;
DESCRIBE hotel;


-- =================================

-- 1)total number of reserversation in dataset
SELECT COUNT(Booking_ID) AS 'total no of reservation' FROM hotel;

-- =======================================================

-- 2)which meal plan is most popular among guest
-- select count(Booking_ID) from hotel where type_of_meal_plan='Meal plan 1';
-- select count(Booking_ID) from hotel where type_of_meal_plan='Meal plan 2';
SELECT type_of_meal_plan, COUNT(Booking_ID) AS 'total_guests'
FROM hotel
WHERE type_of_meal_plan IN ('Meal plan 1', 'Meal plan 2')
GROUP BY type_of_meal_plan
ORDER BY total_guests DESC
LIMIT 1;


-- =========================================================


-- 3)what is the avg price per room for reservation involving childrens
SELECT AVG(avg_price_per_room) AS 'avg price per room involving children'FROM hotel WHERE no_of_children > 0;


-- ===========================================================


-- 4)how many reservation were made for the year 20xx(replace xx with the desired year)
SELECT COUNT(Booking_ID) AS 'total reservation' FROM hotel WHERE YEAR(arrival_date)=2018;
SELECT COUNT(Booking_ID) AS 'total reservation' FROM hotel WHERE YEAR(arrival_date)=2017;
SELECT COUNT(Booking_ID) AS 'total reservation' FROM hotel WHERE YEAR(arrival_date)=2018 OR 2017;


-- ==================================================================


-- 5) what is the most commonly booked room type?
SELECT room_type_reserved, COUNT(Booking_ID) AS 'total_booking_room_type'
FROM hotel
GROUP BY room_type_reserved
ORDER BY total_booking_room_type DESC
LIMIT 1;


-- ==================================================================


-- 6)how many reservation fall on weekend(no_of_weekend_nights>0)?
SELECT COUNT(Booking_ID) AS 'total_reservation_weekend_nights' FROM hotel WHERE no_of_weekend_nights > 0;


-- =====================================================================


-- 7)what is highest and lowest lead time for reservation?
SELECT MIN(lead_time) AS 'Min Reservation time', MAX(lead_time) AS 'Maximum Reservation time' FROM hotel;


-- ===========================================================================


-- 8) what is the most common segment time for reservation?
SELECT market_segment_type, COUNT(Booking_ID) AS 'total_reservation_type'
FROM hotel 
GROUP BY(market_segment_type)
ORDER BY(total_reservation_type) DESC
LIMIT 1;


-- =================================================================


-- 9) how many reservations have booking status of"confirmed"?
SELECT COUNT(Booking_ID) AS 'confirmed booking_status' FROM hotel WHERE booking_status="Not_Canceled"; 


-- ====================================================================


-- 10)what is the total number of adults and children across all reservation?
SELECT SUM(no_of_adults)+SUM(no_of_children) AS ' total_no_adults_&_children' FROM hotel;
select sum(no_of_adults) as Total_Adults,
sum(no_of_children) as Total_Children
from hotel;


   -- ===================================================

   
   -- 11) what is the average number of weekend nights for reservations involving children?
   SELECT AVG(no_of_weekend_nights) AS 'total weekend reservation' FROM hotel WHERE no_of_children > 0;

   
-- =======================================================


-- 12) how many reservation were made in each month of the year?
SELECT
    MONTH(arrival_date) AS 'reservation_month',
    COUNT(Booking_ID) AS 'number_of_reservation'
FROM
	hotel 
WHERE 
		YEAR(arrival_date)=2017 OR 2018
GROUP BY 
	MONTH(arrival_date)
ORDER BY
	reservation_month;

 
    -- ============================================================

    
-- 13) what is the average number of nights(both weekend and week day ) spent by guests for each room type?

SELECT
   room_type_reserved AS 'room_type',
   AVG (no_of_weekend_nights)AS 'no_of_weekend' , AVG(no_of_week_nights) AS 'number_of_week'
FROM
	hotel 
GROUP BY 
	room_type_reserved
ORDER BY
	no_of_weekend,
    number_of_week;
-- 14)for reservations involving children, what is the most common type, and what is the average price for that room type?
SELECT room_type_reserved, 
COUNT(*) AS count,
AVG(avg_price_per_room) AS'average_price'
FROM hotel
WHERE no_of_children > 0
GROUP BY room_type_reserved
ORDER BY count DESC
LIMIT 1;


-- =======================================================


-- 15) find the market segment type that generates the highest average price per room.
SELECT 
market_segment_type AS ' market_segment_type',
AVG(avg_price_per_room) AS 'avg_price'
FROM
hotel
GROUP BY
market_segment_type
ORDER BY 
avg_price DESC
LIMIT 1;


