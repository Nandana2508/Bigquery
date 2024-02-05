 1.	To list the top 10 most common tree species in NYC

    ```SQL
    SELECT spc_common, COUNT(*) AS tree_count
    FROM `bigquery-public-data.new_york_trees.tree_census_*`
    GROUP BY spc_common
    ORDER BY tree_count DESC
    LIMIT 10;
    ```
    ![image](https://github.com/Nandana2508/Bigquery/assets/158820596/247fb93d-3691-4d5f-a33a-5c8d703e97e9)

 2.	Find the average diameter (tree_dbh) of trees in each borough

    ```SQL
    SELECT boroname, AVG(tree_dbh) AS avg_diameter
    FROM `bigquery-public-data.new_york_trees.tree_census_*`
    GROUP BY boroname;
    ```
    ![image](https://github.com/Nandana2508/Bigquery/assets/158820596/dc730647-c97a-4ab3-9317-7c22e74805d6)


 3.	Count the number of trees planted in each year

    ```SQL
    SELECT EXTRACT(YEAR FROM created_at) AS planting_year, COUNT(*) AS trees_planted
    FROM `bigquery-public-data.new_york_trees.tree_census_*`
    GROUP BY planting_year
    ORDER BY planting_year;
    ```
    ![image](https://github.com/Nandana2508/Bigquery/assets/158820596/86febbb7-3eb7-4d5d-817b-d252c387354c)

 4.	Compare tree health status between censuses

    ```SQL
    SELECT trees_2015.tree_id, trees_2005.status, trees_2015.health AS current_health
    FROM `bigquery-public-data.new_york_trees.tree_census_2015` AS trees_2015
    JOIN `bigquery-public-data.new_york_trees.tree_census_2005` AS trees_2005
    ON trees_2015.tree_id = trees_2005.objectid
    WHERE trees_2005.status != trees_2015.health;
    ```
    ![image](https://github.com/Nandana2508/Bigquery/assets/158820596/f9feb64c-fd9d-42b8-9e28-4f8185248301)

 5. Identify trees present in both censuses

    ```SQL
    SELECT t1.tree_id, t1.spc_common, t1.boroname, t2.boroname AS boroname_2005
    FROM `bigquery-public-data.new_york_trees.tree_census_2015` AS t1
    JOIN `bigquery-public-data.new_york_trees.tree_census_2005` AS t2
    ON t1.tree_id = t2.objectid;
    ```
    ![image](https://github.com/Nandana2508/Bigquery/assets/158820596/1eee3d47-984a-4805-9464-d9b4dbebe36d)
    
 6.	Count the number of trees for each specie

    ```SQL
    SELECT species_common_name, COUNT(*) AS tree_count
    FROM `bigquery-public-data.new_york_trees.tree_census_2015` AS t
    JOIN `bigquery-public-data.new_york_trees.tree_species` AS s
    ON species_common_name = species_common_name
    GROUP BY species_common_name
    ORDER BY tree_count DESC;
    ```
    ![image](https://github.com/Nandana2508/Bigquery/assets/158820596/99694019-30ee-4b66-ba0d-d09fc3d7953a)
   	
7.	List all trees with their species names and statuses

   ```SQL
    SELECT status, COUNT(*) AS tree_count
    FROM `bigquery-public-data.new_york_trees.tree_census_*`
    GROUP BY status;
   ```
  ![image](https://github.com/Nandana2508/Bigquery/assets/158820596/b2dea2f8-0a75-495f-9f33-46516a02c497)

 8. Find the tree with the largest diameter

    ```SQL
    SELECT 
    species_common_name,
    tree_size
    FROM `bigquery-public-data.new_york_trees.tree_species`
    ORDER BY tree_size DESC
    LIMIT 1;
    ```
   ![image](https://github.com/Nandana2508/Bigquery/assets/158820596/a4777d80-4c1a-4dbb-af2f-fac6d14d479f)

  9. List the tree id and their stump_id 

      ```SQL
      SELECT tree_id,stump_diam
      FROM `bigquery-public-data.new_york_trees.tree_census_2015`
      WHERE stump_diam = 10;
      ```
      <img width="487" alt="image" src="https://github.com/Nandana2508/Bigquery/assets/158820596/dcde13c4-8a72-4162-8248-6955c877bd2c">

  10. list the tree_id and their address
      
      ```SQL 
      SELECT tree_id, address
      FROM `bigquery-public-data.new_york_trees.tree_census_2015`
      WHERE address = "192 EAST 164 STREET";
      ```
      <img width="404" alt="image" src="https://github.com/Nandana2508/Bigquery/assets/158820596/39522f3c-6c98-479c-8382-84f6b3b31114">

      











