# Analyzing-User-Engagement-and-Message-Patterns-for-Social-Media-using-SQL
Developed SQL queries for a social media app to analyze scraped data, calculating average messages, reshares per user, and identifying peak time frames


# Queries 

**Count by Username**
The following script counts(aggerates) the number of messages for each username and groups the total number of messages by username in descending order. The query illustrated that the username “Seedstars”  has the highest number of messages totaling, 3213

      SELECT username, COUNT(message) AS total_messages
      FROM messages
      GROUP BY username
      ORDER BY total_messages DESC;


**Average Number of Messages by a Single Username:**

This script calculates the average number of messages per username using an inner query.

      SELECT AVG(message_count) AS avg_messages
      FROM (
      SELECT COUNT(message) AS message_count
      FROM messages
      GROUP BY username
     ) AS subquery;

**Average Number of Reshares by a Single Username:**

This script calculates the average number of reshares per username.

    SELECT AVG(reshare_count) AS avg_reshares
    FROM (
    SELECT COUNT(reshares) AS reshare_count
    FROM messages
    GROUP BY username
    ) AS subquery;


**Ratio of Messages to Reshares:**

This script calculates the ratio between messages and reshares for each username.
       
       SELECT username, 
       COUNT(message) AS total_messages, 
       COUNT(reshares) AS total_reshares,
       (COUNT(message) / COUNT(reshares)) AS 
       message_reshare_ratio
       FROM messages
       GROUP BY username;

**Time Frame with the Highest Number of Original Messages:**

This script identifies the time frame with the highest number of original messages by filtering out reshares.

      SELECT date, COUNT(message) AS total_original_messages
      FROM messages
      WHERE reshares = 0
      GROUP BY date
      ORDER BY total_original_messages DESC
      LIMIT 1;
