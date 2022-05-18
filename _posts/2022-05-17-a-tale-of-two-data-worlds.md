Contrary to what the title of this post says, I'm not going to tell a story but I want to draw your attention to the two data worlds prevalent in the tech space. I've just been into [Charles Dickens writings](https://en.wikipedia.org/wiki/A_Tale_of_Two_Cities) of late, hence the title. 

In conversations with people who want to start analytics in their business and other data professionals, I notice some are not aware of the two different data worlds - transactional data and analytical data. For those who are aware, they are often confused or struggle to see why both data worlds exist. So let's dive into this particular type of data chasm and shed some light on why these two data worlds exist.

 The database that sits behind your software application is a transactional database. On the other hand, the database where your analysts answer complex questions from and perform analysis from is an analytical database. All companies that use applications as part of their business process have the former while the later is often used by companies that want to be data-driven. This difference in these two data worlds is often reflected in the organisational structures and professions these days. They also have different architectures.

To explain the difference, let's paint a scenario in which I own a hardware store. My store has an app that the customers log in to borrow tools and the app also processes payments. The database that sits at the back end of this customer app and stores every interaction the customer makes with the app is called the transactional database (also known as application or operational database). It enables the customer use the app by storing the current state of affairs and any other business rules of the store. A table in this database might look like this:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:12px 20px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:12px 20px;word-break:normal;}
.tg .tg-266k{background-color:#9b9b9b;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
.tg .tg-c6of{background-color:#ffffff;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-fymr">Date</th>
    <th class="tg-fymr">Name</th>
    <th class="tg-fymr">City</th>
    <th class="tg-fymr">Tool</th>
    <th class="tg-fymr">Amount</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c6of">Dec. 01, 2021</td>
    <td class="tg-c6of">John Doe</td>
    <td class="tg-c6of">Toronto</td>
    <td class="tg-c6of">Chainsaw</td>
    <td class="tg-c6of">$450</td>
  </tr>
  <tr>
    <td class="tg-266k">Dec. 15, 2021</td>
    <td class="tg-266k">Jane Doe</td>
    <td class="tg-266k">Brampton</td>
    <td class="tg-266k">Chainsaw</td>
    <td class="tg-266k">$260</td>
  </tr>
  <tr>
    <td class="tg-0pky">Jan. 7, 2022</td>
    <td class="tg-0pky">Bill Smith</td>
    <td class="tg-0pky">Hamilton</td>
    <td class="tg-0pky">Hammer</td>
    <td class="tg-0pky">$300</td>
  </tr>
  <tr>
    <td class="tg-0pky">Jan. 7, 2022</td>
    <td class="tg-0pky">Chris Lock</td>
    <td class="tg-0pky">Toronto</td>
    <td class="tg-0pky">Helmet</td>
    <td class="tg-0pky">$100</td>
  </tr>
</tbody>
</table><br>


In the transactional data world, the data in this table is read from and written into by the customer app in a row-wise manner. So if Jane Doe logs in, she only sees the items pertaining to her which are highlighted in gray above. Also, the tables in this world support concurrent multiple data writes so more than 1 customer can be using the app at the same time. In the example above, let's imagine Bill Smith borrowed the hammer at the same time Chris Lock borrowed the helmet, the database should be able to store both records without any loss of data and in a timely manner without any conflicts. These types of operations on a database is known as Online Transactional Processing (OLTP). Relational Database Managment Systems (RDBMS) have been optimised over the years to handle these type of workloads[^1]. Some common examples include Postgres, MySQL and SQL Server.

So far we have talked about the operational data world. The different personas in the Software Engineering field usually operate in this world and most of the work done here is geared towards increasing usability of the business application. There is another world of data where the work done on data is not to directly improve the performance of an app or implement business rules but more of answering questions, looking back to see what has gone on in the business and predicting what might happen. This other world is the analytical data world and this is were the different data and analytics personas operate in. 

Still on the example of my hardware store, after operating for a while, I will like to know what tools people borrow the most so that I can get more stock of those tools. My gut instinct might point me towards a certain tool based on what I observe, but I want to know what the data says and take action based on that - data-driven. So I enter the analytical world where a similar table like above exists but this time, I don't access it row by row. Instead, I use the table from top-bottom as seen in the table below and I apply some arithmetic operations on the "Tool" column. 

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:12px 20px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:12px 20px;word-break:normal;}
.tg .tg-1wig{font-weight:bold;text-align:left;vertical-align:top}
.tg .tg-9fd4{background-color:#9b9b9b;font-weight:bold;text-align:left;vertical-align:top}
.tg .tg-0lax{text-align:left;vertical-align:top}
.tg .tg-m71n{background-color:#9b9b9b;color:#333333;text-align:left;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-1wig">Date</th>
    <th class="tg-1wig">Name</th>
    <th class="tg-1wig">City</th>
    <th class="tg-9fd4">Tool</th>
    <th class="tg-1wig">Amount</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">Dec. 01, 2021</td>
    <td class="tg-0lax">John Doe</td>
    <td class="tg-0lax">Toronto</td>
    <td class="tg-m71n">Chainsaw</td>
    <td class="tg-0lax">$450</td>
  </tr>
  <tr>
    <td class="tg-0lax">Dec. 15, 2021</td>
    <td class="tg-0lax">Jane Doe</td>
    <td class="tg-0lax">Brampton</td>
    <td class="tg-m71n">Chainsaw</td>
    <td class="tg-0lax">$260</td>
  </tr>
  <tr>
    <td class="tg-0lax">Jan. 7, 2022</td>
    <td class="tg-0lax">Bill Smith</td>
    <td class="tg-0lax">Hamilton</td>
    <td class="tg-m71n">Hammer</td>
    <td class="tg-0lax">$300</td>
  </tr>
  <tr>
    <td class="tg-0lax">Jan. 7, 2022</td>
    <td class="tg-0lax">Chris Lock</td>
    <td class="tg-0lax">Toronto</td>
    <td class="tg-m71n">Helmet</td>
    <td class="tg-0lax">$100</td>
  </tr>
</tbody>
</table>

<br>

Furthermore, if I want to know the total amount I made on each type of tool for each city for every month, I still need to work with the table in a column-wise manner but this time, with multiple columns. These types of operations on a database is known as Online Analytical Processing (OLAP). Column-oriented database systems have been optimised for these and some examples include Redshift, Synapse and Snowflake. 

There are lots of difference between these two data worlds and these differences can be seen in the types of problems they try to solve. In the transactional world, rapid processing in the order of milliseconds is often emphasised so that customers can have a good user experience while in the analytical world, the complexity of questions you can ask or insights you can derive drives the value. Even though SQL is a common language spoken in both worlds, they have different data storage systems. For example, in the analytical data world, you have the data warehouses, data marts, data lakes and lake houses while in the operational data world you might find some NoSQL systems. ETL processing is the bridge that links the operational world with the analytical world and most often traffic moves in one direction. There is the concept of reverse ETL which is gaining some traction these days but that's a topic for another day.

There are lots of databases that are being introduced to the market and the data world is booming with new products announced almost every day. Hopefully, when you read the next announcement of the new data tool, you will be able to tell what data world it belongs to.


[^1]: There are other types of Database Management Systems that are used in the operational data world such as Document based databases.
