# R basics course from Datacamp, finished in July 2019

* Checking for the different data types:
1. numeric (integer)
2. numeric (decimal)
3. string
4. boolean (TRUE, FALSE)

```
class(my_var)
```

returns the type of variable my_var

* Vectors:

```
my_num_vec <- c(1, 2, 3)
my_char_vec <- c("a", "b", "c")
my_bool_vec <- c(TRUE, FALSE, TRUE)
```
Can give name to the elements of a vector with the `names()` function.

```
some_vector <- c("John Doe", "poker player")
names(some_vector) <- c("Name", "Profession")
```

* Vector addition is element-wise

```
a <- c(1, 2, 3)
b <- c(4, 5, 6)
c <- a + b
```

* Selection of elements in a vector

Use square brackets as in `total_vec[1]`. But if you use the names function for that specific vector, you can call it like `total_vec["name"]`. Also can access more than one element by indicating a vector of indexes or names, such as `poker_vec[c(1,5)]`. Or to specify an interval: `poker_vec[2:4]`

* Logical comparisons

The (logical) comparison operators known to R are:

* `<` for less than
* `>` for greater than
* `<=` for less than or equal to
* `>=` for greater than or equal to
* `==` for equal to each other
* `!=` not equal to each other

* Matrices in R

To create a matrix in R, we use the command `matrix(...)`, as in:

```
matrix(1:9, byrow = TRUE, nrow = 3)
```

To create something like:

```
1 2 3
4 5 6
7 8 9
```

We can also give names to the rows and columns of the matrix as in:

```
rownames(my_matrix) <- row_names_vector
colnames(my_matrix) <- col_names_vector
```

To calculate the row sum:

```
rowSums(matrix)
```

For column sum use `colSums(matrix)`

* How to add a column to a matrix:

```
big_matrix <- cbind(matrix1, matrix2, vector1 ...)
```

* To add a row, function `rbind(matrix1, matrix2)`

* To select elements of a matrix, use square brackets:

```
my_matrix[1,2]
my_matrix[1,]
my_matrix[,1]
```
The last selects all the elements of column 1 and the penultimate selects all the elements of the first row.

* Matrix arithmetic:

In R, +, -, /, * are all elementwise!!!
To achieve traditional matrix multiplication, one has to do

```
matrix_prod <- matrix_1%*%matrix_2


* Factors

Use it to deal with categorical data, such as sex (male/female). Function `factor()`

```
sex_vector <- c("Male","Female","Female","Male","Male")
```

Then:

```
factor_sex_vector <- factor(sex_vector)
```

R finds all the types of possible categorical values and calls it Levels.

* Nominal categorical variable: there is no ordering implied
* Ordinal categorical variable: there is a natural ordering (e.g., *low, medium, high*)

Example of ordinal categorical variable:
```
factor_temperature_vector <- factor(temperature_vector, order = TRUE, levels = c("Low", "Medium", "High"))
```

* Change the names of the levels using `levels()` function, but whatch out for the order:

```
levels(factor_vector) <- c("name1", "name2",...)
```

* Get summary information about a factor:

```
summary(my_var)
```

* To create an ordinal factor:

```
factor(some_vector,
       ordered = TRUE,
       levels = c("lev1", "lev2" ...))
```

## Data frames

One can combine different data types (e.g., logical, numerical, character) into a single object.

Commands that are useful: `head(df)` and `tail(df)`, which will display only the first or last five observations in the dataset.

* Function `str(df)`: shows a compilation of information in the dataset, and is the fastest way to get info in a new dataset. Information provided:

1. The total number of observations
2. The total number of variables
3. A full list of the variables names
4. The data type of each variable
5. The first observations

* To create an own dataframe we need vectors of the same length (but not necessarily of the same data type) to describe the different variables.

```
# Definition of vectors
name <- c("Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune")
type <- c("Terrestrial planet", "Terrestrial planet", "Terrestrial planet",
          "Terrestrial planet", "Gas giant", "Gas giant", "Gas giant", "Gas giant")
diameter <- c(0.382, 0.949, 1, 0.532, 11.209, 9.449, 4.007, 3.883)
rotation <- c(58.64, -243.02, 1, 1.03, 0.41, 0.43, -0.72, 0.67)
rings <- c(FALSE, FALSE, FALSE, FALSE, TRUE, TRUE, TRUE, TRUE)

# Create a data frame from the vectors
planets_df <- data.frame(name, type, diameter, rotation, rings)
```

You can operate and have access to the elements of the dataframe as you did with the elements of a matrix, with the help of indexes `df[2,2:3]` for instance. But now you can also pass the column as the name of the variable instead of its index, such as `df[3, "prices"]`. If you want to show all the information in a column, one shortcut is to use the dolar sign: `df$prices`

* Subset function:

Allows you to extract information from the dataframe satisfying some condition:

```
subset(my_df, subset = some_condition)
```

* Sorting

Function `order()` gives you the ranked position of each element when it is applied on a variable, like a vector:

```
> a <- c(100, 10, 1000)
> order(a)
[1] 2 1 3
> a[order(a)]
[1]   10  100 1000
```

But can also be used to reorder elements in a dataframe:

```
# Use order() to create positions
positions <-  order(planets_df$diameter)

# Use positions to sort planets_df
planets_df[positions,]
```

## Lists

Can store any data type as its elements, even other lists

```
my_list <- list(comp1, comp2 ...)
```

Useful: store the names of the elements inside the list:

```
my_list <- list(name1 = your_comp1,
                name2 = your_comp2)
```

or

```
my_list <- list(your_comp1, your_comp2)
names(my_list) <- c("name1", "name2")
```

To select elements from a list, we can use square brackets, as to select the first element of it: `list[[1]]`. If the first component is a vector, then `list[[1]][2]` will select the second component of the first component. Similarly, if the name of the first component is *prices*, then you can access the same information with `list$prices[2]`.

* Append elements to a list:

Simply treating the list as a vector with the `c()` function:
```
ext_list <- c(my_list, my_name = my_val)
```
