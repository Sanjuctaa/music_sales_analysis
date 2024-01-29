# music_store_sales_analysis


Q.Who is the senior most employee based on job title?

select * from employee
order by levels desc
limit 1;


Q.Which countries have the most invoices?

select billing_country ,count(*)
from invoice
group by billing_country
order by c desc;


Q.What are the top 3 values of total invoices?

select * from invoice
order by total desc
limit 3;


Q.Write a query that returns one city that has the highest sum of invoice totals. Return the city name and sum of all invoices?

select billing_city,sum(total)
from invoice
group by billing_city
order by 2 desc limit 1 ;


Q.Write a query that returns the person who has sent the most money?

select c.customer_id, c.first_name, c.last_name, sum(i.total) as total
from customer c
join invoice i
on c.customer_id = i.customer_id
group by 1
order by 3 desc
limit 1;


Q.Write a query that returns the email, first name , last name and the genre of all rock music listeners. Return the list ordered alphabeticallyby email.

select distinct c.first_name, c.last_name, c.email from customer c
join invoice i on c.customer_id= i.customer_id
join invoice_line il on i.invoice_id = il.invoice_id
where track_id in (select track_id
from track t
join genre g on t.genre_id= g.genre_id
where g.name='Rock')
order by email;


Q.Write a query that returns the artist name and total track count of the top 10 rock bands?

select artist.artist_id, artist.name , count(artist.artist_id) as song_count
from track
join album on album.album_id = track.album_id
join artist on artist.artist_id = album.artist_id
join genre on genre.genre_id = track.genre_id
where genre.name like 'Rock'
group by artist.artist_id
order by song_count desc
limit 10;


Q.Return all the track names that have the song length longer than the average song length . Returns the name and milliseconds foreach track. Order by the song length.

select name, milliseconds from track
where milliseconds> (select avg(milliseconds) from track)
order by milliseconds desc;
