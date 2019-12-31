### SQL Queries  
[Original Source]( https://en.wikibooks.org/wiki/Data_Management_in_Bioinformatics/SQL_Exercises) from wikibooks - I modified both the example dataset and the queries to work with Google BigQuery

---

Q1: Return the names of experiments performed by Tommy Student after Jan 1, 2004.  

Q2: Return the names of genes that were either positively expressed twofold or more with a significance of at least 1.0, in some experiment, or negatively expressed twofold or less with a significance of at least 1.0, in some experiment. List them alongside their organisms in a two-column format.  

Q3: Return the grandparent category of 'glycine binding'? 

Q4: Return the names of experiments that were performed before some Gasch experiment.  

Q5: Return the names of pine genes that were positively expressed more than 0.5-fold (with a significance of 1.0 or more) in at least two experiments.

 - 5a. Straightforward Answer: First, we must find the experiments where genes are upreglated and significant.
Next, we must determine the genes which were upregulated in at least two experiments. We do this by taking the product of the upregulated genes and selecting rows where the gene ID is the same but the experiment ID is different.
Finally, we determine which of these genes come from pine, and project their names.

 - 5b. We can alternatively do these steps all in one single query:

 - 5c. Subquery Answer: As another approach, we can make use of subqueries to find the answer. The key to this is to make a correlated subquery where the subquery depends on some property (in this case the gene ID) of the parent query. Note that we'll still need to make use of the Upregulated view created above to reduce code redundancy.

 - 5d. GROUP BY Answer: We can make use of advanced features for certain database systems such as PostgreSQL and MySQL to make these queries in slightly more convenient ways via the GROUP BY and COUNT.

Q6: Return the names of pine genes that were up-regulated 0.5-fold or more (with a significance of 1.0 or more) in at least three experiments.

 - 6a. Straightforward Answer: Similar to the answer for question 5. The caveat here is that while the equality evaluations are transitive, while inequality evaluations are not, and so every case must be covered.

- 6b. Alternatively:Subquery Answer - We need to build in another correlated subquery for our original correlated subquery to make this work.
GROUP BY Answer - Simply adjust the count evaluation.

Q7: Return the names of pine genes that were up-regulated 0.5-fold or more (with a significance of 1.0 or more) in at exactly two experiments.

- 7a. Straightforward Answer: The key here is identifying that taking the set of genes upregulated in two or more experiments and subtracting the set of genes upregulated in three or mor experiments gives the set of genes upregulated in precisely two experiments. Thus, our answer is the answer to question 5 subtracted by the answer to question 6.

- 7b. GROUP BY Answer

Q8: Return the genes that showed positive expression in every experiment recorded for it.  

Q9: Return the name of the gene that was most positively expressed in experiment exp23? Assume a minimum significance of 1.0.  

Q10: Return the name of the gene that was "second most positively expressed"? Assume again a minimum significance of 1.0. NOTE: See Q8 for hint.  

Q11: Return the gene(s) were positively expressed in ALL the experiments listed in the Experiments table? No constraints on significance level.  

Q12: Return a table of genes, their annotation, and any experiment in which they were either the highest or lowest expressed (of any significance level). Include a fourth column to say if they were the highest or lowest.