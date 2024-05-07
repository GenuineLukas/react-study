# Python for Data Science-Pandas

- Pandas is an open source library built on top of NumPy
- it allows for fast analysis and data cleaning and preparation
- it excels in performance and productivity
- it also has built-in visualization features
- it can work with data from a wide variety of sources

- series
    - series is very similar to NumPy array, in fact, it’s built on the NumPy Array, but what’s different is that **it can be indexed by label**.
    - in series, you can specify what you want the index to be. For example, you can set the index to be the labels.
    - Panda series is very flexible that it can hold almost every data type and its data, it can even hold the built-in functions as its data.
    - Remember that when you’re performing operations with a Pandas series, your integers are going to be converted into floats. That’s so you don’t accidentally lose information based off of some weird division and that ‘s the same for NumPy.
    
    ```python
    import numpy as np
    import pandas as pd
    
    labels = [ 'a', 'b', 'c']
    my_data = [10, 20, 30]
    arr = np.array(my_data)
    d = {'a':10, 'b':20, 'c':30}
    
    pd.Series(data = my_data, index = labels)
    pd.Series(arr, labels) # works the same as above
    pd.Series(d)# you can directly put dictionry so it works the same as above
    
    # HOW TO GRAB INFO FROM THE SERIES   
    ser1 = pd.Series([1, 2, 3, 4], ['USA', 'Germany', 'USSR', 'Japan'])
    ser2 = pd.Series([1, 2, 5, 4], ['USA', 'Germany', 'Italy', 'Japan'])
    # you can index with the index
    ser1['USA']
    ser2['Germany']
    
    print(ser1 + ser2)
    '''
    Germany    4.0
    Italy      NaN
    Japan      8.0
    USA        2.0
    USSR       NaN
    dtype: float64
    '''
    #what happened was that for the index that both series don't share, 
    #the corresponding value became none, and the values after the
    #operation became floats.
    ```
    
- DataFrames basics
    - [np.random.seed()](https://frhyme.github.io/python-libs/np_random_get_set_state/)
    - DataFrame is just a bunch of series that share the index
    - DataFrame will be used a lot more than the series
    - you can pass-in a dictionary as the parameter of the pd.Dataframe(). Then, the key values willl be indicating each column of the dataframe.
    - **`[DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html#pandas.DataFrame)`**([data, index, columns, dtype, copy])
    - df.xs(key, axis=0, level=None, copy=None, drop_level=True)
        - Returns a cross-section (row(s) or column(s)) from the Series/DataFrame. Defaults to cross-section on the rows(axis= 0).
    - [**dropna()**](https://www.w3schools.com/python/pandas/ref_df_dropna.asp)
        - *dataframe*.dropna(axis, how, thresh, subset, inplace)
    - [**fillna()**](https://www.w3schools.com/python/pandas/ref_df_fillna.asp)
        - *dataframe*.fillna(value, method, axis, inplace, limit, downcast)
    
    ```python
    import numpy as np 
    import pandas as pd
    from  numpy.random import randn
    
    np.random.seed(101)
    df = pd.DataFrame(randn(5, 4), ['A', 'B', 'C', 'D', 'E'], ['W', 'X', 'Y','Z'])
    print(df)
    '''
              W         X         Y         Z
    A  2.706850  0.628133  0.907969  0.503826
    B  0.651118 -0.319318 -0.848077  0.605965
    C -2.018168  0.740122  0.528813 -0.589001
    D  0.188695 -0.758872 -0.933237  0.955057
    E  0.190794  1.978757  2.605967  0.683509
    '''
    
    print(df['W'])
    print(type(df['W'])) #<class 'pandas.core.series.Series'>
    #this looks like a series because it's exactly a series
    '''
    A    2.706850
    B    0.651118
    C   -2.018168
    D    0.188695
    E    0.190794
    Name: W, dtype: float64
    '''
    
    #if you want multiple series, put the list of the index of the series you want
    #in this case, you will get back the dataframe, not a series.
    print(df[['W', 'Z']])
    print(type(df[['W', 'Z']])) #<class 'pandas.core.frame.DataFrame'>
    '''
    W         Z
    A  2.706850  0.503826
    B  0.651118  0.605965
    C -2.018168 -0.589001
    D  0.188695  0.955057
    E  0.190794  0.683509
    '''
    
    #CREATING NEW COLUMN
    df["NEW"] = df['Y'] + df['Z'] #set the new column as if it already existed
    #and use any arithmatic to add it at the last column.
    print(df)
    '''
              W         X         Y         Z       NEW
    A  2.706850  0.628133  0.907969  0.503826  1.411795
    B  0.651118 -0.319318 -0.848077  0.605965 -0.242112
    C -2.018168  0.740122  0.528813 -0.589001 -0.060187
    D  0.188695 -0.758872 -0.933237  0.955057  0.021819
    E  0.190794  1.978757  2.605967  0.683509  3.289476
    '''
    
    #REMOVING COLUMNS
    #for the drop method, you should specify the axis.
    #axis = 0 is for the rows.
    #axis = 1 is for the columns.
    #for the sake of securing your data in place,
    #Pandas have you specify inplace = True/False in the drop() function.
    #if the inplace was set as True, then the changes will be made and the
    #DataFrame would be affected, unless, it wouldn't be
    df.drop("NEW", axis = 1)
    print(df)
    '''
              W         X         Y         Z       NEW
    A  2.706850  0.628133  0.907969  0.503826  1.411795
    B  0.651118 -0.319318 -0.848077  0.605965 -0.242112
    C -2.018168  0.740122  0.528813 -0.589001 -0.060187
    D  0.188695 -0.758872 -0.933237  0.955057  0.021819
    E  0.190794  1.978757  2.605967  0.683509  3.289476
    '''
    df.drop("NEW", axis = 1, inplace = True)
    print(df)
    '''
              W         X         Y         Z
    A  2.706850  0.628133  0.907969  0.503826
    B  0.651118 -0.319318 -0.848077  0.605965
    C -2.018168  0.740122  0.528813 -0.589001
    D  0.188695 -0.758872 -0.933237  0.955057
    E  0.190794  1.978757  2.605967  0.683509
    '''
    df.drop('E', axis = 0, inplace = True)
    print(df) 
    '''
              W         X         Y         Z
    A  2.706850  0.628133  0.907969  0.503826
    B  0.651118 -0.319318 -0.848077  0.605965
    C -2.018168  0.740122  0.528813 -0.589001
    D  0.188695 -0.758872 -0.933237  0.955057
    '''
    
    ##selecting rows in dataframes...
    #you basically pass in the loc() funciton the row you want.
    #you can see that not only the column of the dataframe
    #but also the row of it is series
    print(df.loc['A'])
    '''
    W    2.706850
    X    0.628133
    Y    0.907969
    Z    0.503826
    Name: A, dtype: float64
    '''
    # SECOND WAY to select row in the dataframe
    # you put the numerical index in the iloc() method although 
    # the index are labeled
    print(df.iloc[2])
    '''
    W   -2.018168
    X    0.740122
    Y    0.528813
    Z   -0.589001
    Name: C, dtype: float64
    '''
    #getting one value in the data frame
    print(df.loc['A', 'W']) #2.706849839399938
    print(df.iloc[0, 0]) #2.706849839399938
    
    #getting subsets of the dataframe
    #main point: use the list
    print(df.loc[['A', 'B'], ['W', 'Y']])
    '''
              W         Y
    A  2.706850  0.907969
    B  0.651118 -0.848077
    '''
    print(df.loc[['A', 'B', 'C'], ['W', 'Y']])
    '''
              W         Y
    A  2.706850  0.907969
    B  0.651118 -0.848077
    C -2.018168  0.528813
    '''
    ```
    
- Conditional selection in DataFrame
    
    ```python
    print(df)
    print(df > 0)
    '''
              W         X         Y         Z
    A  2.706850  0.628133  0.907969  0.503826
    B  0.651118 -0.319318 -0.848077  0.605965
    C -2.018168  0.740122  0.528813 -0.589001
    D  0.188695 -0.758872 -0.933237  0.955057
    
           W      X      Y      Z
    A   True   True   True   True
    B   True  False  False   True
    C  False   True   True  False
    D   True  False  False   True
    '''
    
    #conditions based off of the entire dataframe
    #it returns the null value
    booldf = df > 0
    print(df[booldf])
    '''
              W         X         Y         Z
    A  2.706850  0.628133  0.907969  0.503826
    B  0.651118       NaN       NaN  0.605965
    C       NaN  0.740122  0.528813       NaN
    D  0.188695       NaN       NaN  0.955057
    '''
    
    #conditions based off of the rows/columns don't return the
    #values that's false.
    booldf = df['W']>0
    print(df[booldf])
    '''
              W         X         Y         Z
    A  2.706850  0.628133  0.907969  0.503826
    B  0.651118 -0.319318 -0.848077  0.605965
    D  0.188695 -0.758872 -0.933237  0.955057
    '''
    #print the dataframe where 'W' is greater than 0 and 
    #that of a column Y
    print(df[df['W'] > 0]['Y'])
    '''
    A    0.907969
    B   -0.848077
    D   -0.933237
    Name: Y, dtype: float64
    '''
    #remember that of you want multiple columns, use lists.
    print(df[df['W'] > 0][['Y', 'X']])
    '''
              Y         X
    A  0.907969  0.628133
    B -0.848077 -0.319318
    D -0.933237 -0.758872
    '''
    
    #multiple conditions
    #when you want to execute the multiple conditions,
    #you cannot use the normal 'and' operator.
    #you should use the &(Ampersand)
    #and that's the same for |. you can't use the normal 'or'.
    #the normal 'and' operator can deal with only True/False
    #not the whole seires of boolean values
    print(df[(df['W'] > 0) & (df['Z'] > 0)]['X'])
    '''
    A    0.628133
    B   -0.319318
    D   -0.758872
    Name: X, dtype: float64
    '''
    
    #RESETTING index
    #df.reset_index(inplace = True) 
    #this also has the inplace value.
    #what happens after this is you will have the numerical
    #index values while your former index become a column named "index."
    '''
      index         W         X         Y         Z
    0     A  2.706850  0.628133  0.907969  0.503826
    1     B  0.651118 -0.319318 -0.848077  0.605965
    2     C -2.018168  0.740122  0.528813 -0.589001
    3     D  0.188695 -0.758872 -0.933237  0.955057
    '''
    
    #Setting index out of the column
    
    states = 'MA NY CA GA'.split()
    df['states'] = states
    print(df)
    '''
              W         X         Y         Z states
    A  2.706850  0.628133  0.907969  0.503826     MA
    B  0.651118 -0.319318 -0.848077  0.605965     NY
    C -2.018168  0.740122  0.528813 -0.589001     CA
    D  0.188695 -0.758872 -0.933237  0.955057     GA
    '''
    # use the set_index() method to set the index as a existing column
    # unlike reset_index() the entire column is replaced.
    df.set_index('states', inplace = True)
    print(df)
    '''
                   W         X         Y         Z
    states
    MA      2.706850  0.628133  0.907969  0.503826
    NY      0.651118 -0.319318 -0.848077  0.605965
    CA     -2.018168  0.740122  0.528813 -0.589001
    GA      0.188695 -0.758872 -0.933237  0.955057
    '''
    ```
    
- DataFrame advanced
    
    ```python
    import numpy as np
    import pandas as pd
    from  numpy.random import randn
    
    #Index Levels
    outside = ['G1', 'G1', 'G1', 'G2', 'G2', 'G2']
    inside =  [1, 2, 3, 1, 2, 3]
    hier_index = list(zip(outside, inside))
    hier_index = pd.MultiIndex.from_tuples(hier_index)
    print(hier_index)
    '''
    MultiIndex([('G1', 1),
                ('G1', 2),
                ('G1', 3),
                ('G2', 1),
                ('G2', 2),
                ('G2', 3)],
               )
    '''
    
    df = pd.DataFrame(randn(6, 2), hier_index, ['A', 'B'])
    print(df)
    '''
                 A         B
    G1 1  0.605522 -0.643799
       2  1.130307  0.140033
       3 -2.476968 -1.099418
    G2 1  0.644124 -0.630184
       2  0.071507  0.011139
       3  0.516554  1.137777
    '''
    
    ##how to call data
    print(df.loc['G1'])
    '''
              A         B
    1  0.193569 -0.603176
    2  0.091981 -0.995957
    3 -0.001067  1.607664
    '''
    print(df.loc['G1'].loc[1])
    '''
    A   -0.572921
    b    0.854279
    Name: 1, dtype: float64
    '''
    
    ##naming the index
    df.index.names = ['groups', 'num']
    print(df)
    '''
                       A         B
    groups num
    G1     1    1.841700  0.031618
           2    3.006838 -0.302056
           3    1.230571  0.197304
    G2     1   -1.289630 -0.794301
           2   -1.466819 -0.178397
           3    0.213571 -0.587756
    '''
    
    ##picking value from the table 
    print(df.loc['G2'].loc[1]['B'])
    '''
                       A         B
    groups num
    G1     1    0.711811  3.359046
           2   -0.097679  0.815648
           3   -0.760898 -0.226000
    G2     1    1.999301  1.031568
           2    0.282937 -0.079163
           3    1.887167 -1.928589
    1.0315679531401367
    '''
    
    ##cross section
    #df.xs() method enables you to cross section the two different
    #groups like you could access to the value in both G1 and G2 
    #by specipying certain index. 
    print(df.xs(2, level = "num"))
    '''
                   A         B
    groups
    G1      0.841008  1.533451
    G2      0.414457 -0.938524
    '''
    ```
    
- Missing Data
    
    a few convenient methods() to deal with missing data in pandas.
    
    when you use pandas and have missing data, what the pandas going to do is to fill up the missing space with null or NaN value.  let’s explore some methods() to drop or fill those null/NaN values
    
    - dropna()
    
    ```python
    import numpy as np
    import pandas as pd  
    
    d = {'A':[1,2,np.nan], 'B':[5, np.nan, np.nan], 'C':[1, 2, 3]}
    df = pd.DataFrame(d)
    print(df)
    '''
         A    B  C
    0  1.0  5.0  1
    1  2.0  NaN  2
    2  NaN  NaN  3
    '''
    
    ##df.dropna()
    #it drops every column or row that has one or more none/nan
    #value in it.
    copy = df.copy()
    copy.dropna(inplace=True)
    print(copy)
    '''
      A    B  C
    0  1.0  5.0  1
    '''
    ##using axis to drop the rows containing none
    copy1 = df.copy()
    copy1.dropna(axis=0, inplace=True)
    print(copy1)
    '''
      A    B  C
    0  1.0  5.0  1
    '''
    copy2 = df.copy()
    copy2.dropna(axis=1, inplace=True)
    print(copy2)
    '''
       C
    0  1
    1  2
    2  3
    '''
    ## using thresh in dropna
    #thresh drops the row/column when it has non-none values
    #less than the threshhold value specified
    copy3 = df.copy()
    copy3.dropna(axis= 1, thresh=2, inplace=True)
    print(copy3)
    '''
         A  C
    0  1.0  1
    1  2.0  2
    2  NaN  3
    '''
    ```
    
    - fillna()
    
    ```python
    import numpy as np
    import pandas as pd  
    
    d = {'A':[1,2,np.nan], 'B':[5, np.nan, np.nan], 'C':[1, 2, 3]}
    df = pd.DataFrame(d)
    print(df)
    '''
         A    B  C
    0  1.0  5.0  1
    1  2.0  NaN  2
    2  NaN  NaN  3
    '''
    
    #fillna() method that fills the none values in dataframe
    copy = df.copy()
    copy.fillna(value = "FILL VALUE", inplace=True)
    print(copy)
    '''
                A           B  C
    0           1           5  1
    1           2  FILL VALUE  2
    2  FILL VALUE  FILL VALUE  3
    '''
    
    copy1 = df.copy()
    copy1['A'].fillna(value = copy1['A'].mean(), inplace=True)
    copy1['B'].fillna(value = copy1['B'].mean(), inplace=True)
    print(copy1)
    '''
    A    B  C
    0  1.0  5.0  1
    1  2.0  5.0  2
    2  1.5  5.0  3
    '''
    ```
    
- Groupby
    
    ![Untitled](Python%20for%20Data%20Science-Pandas%209fbf14b6880b48d28252449eaa3bd72b/Untitled.png)
    
    - Groupby allows you to group together rows based off of a column and perform an aggregate function on them.
    - groupby(), sum(), std(), max(), min(), describe(), transpose()…
        
        ```python
        import numpy as np
        import pandas as pd  
        
        data = {'Company':['GOOG', 'GOOG', 'MSFT', 'MSFT', 'FB', 'FB'],
               'Person':['Sam', 'Charlie', 'Amy', 'Vanessa', 'Carl', 'Sarah'],
               'Sales':[200, 120, 340, 124, 243, 350]}
        df = pd.DataFrame(data)
        print(df)
        '''
          Company   Person  Sales
        0    GOOG      Sam    200
        1    GOOG  Charlie    120
        2    MSFT      Amy    340
        3    MSFT  Vanessa    124
        4      FB     Carl    243
        5      FB    Sarah    350
        '''
        
        #
        #you basically store a variable using groupby
        byComp = df.groupby('Company')
        #see what you get for the variable, you get an object 
        print(byComp) #<pandas.core.groupby.generic.DataFrameGroupBy object at 0x7f5fc818ab10>
        #to make a use of groupby(), you have to add any aggregate function
        print(byComp.mean())
        #when you do this, pandas automatically ignores the non-numeric column
        '''
                 Sales
        Company
        FB       296.5
        GOOG     160.0
        MSFT     232.0
        '''
        print(byComp.sum())
        '''
                 Sales
        Company
        FB         593
        GOOG       320
        MSFT       464
        '''
        print(byComp.std())
        '''
                      Sales
        Company
        FB        75.660426
        GOOG      56.568542
        MSFT     152.735065
        '''
        #you could call the aggregate function in one line
        print(df.groupby('Company').count())
        '''
                 Person  Sales
        Company
        FB            2      2
        GOOG          2      2
        MSFT          2      2
        '''
        #when you call max()/min(), if the column is in alphabet,
        #pandas process it as alphabetical order
        print(df.groupby('Company').max())
        '''
                  Person  Sales
        Company
        FB         Sarah    350
        GOOG         Sam    200
        MSFT     Vanessa    340
        '''
        print(df.groupby('Company').min())
        '''
                  Person  Sales
        Company
        FB          Carl    243
        GOOG     Charlie    120
        MSFT         Amy    124
        '''
        print(df.groupby('Company').describe())
        '''
           Sales
                count   mean         std    min     25%    50%     75%    max
        Company
        FB        2.0  296.5   75.660426  243.0  269.75  296.5  323.25  350.0
        GOOG      2.0  160.0   56.568542  120.0  140.00  160.0  180.00  200.0
        MSFT      2.0  232.0  152.735065  124.0  178.00  232.0  286.00  340.0
        '''
        print(df.groupby('Company').describe().transpose())
        '''
        Company              FB        GOOG        MSFT
        Sales count    2.000000    2.000000    2.000000
              mean   296.500000  160.000000  232.000000
              std     75.660426   56.568542  152.735065
              min    243.000000  120.000000  124.000000
              25%    269.750000  140.000000  178.000000
              50%    296.500000  160.000000  232.000000
              75%    323.250000  180.000000  286.000000
              max    350.000000  200.000000  340.abs()
        '''
        print(df.groupby('Company').describe().transpose()['FB'])
        '''
        Sales  count      2.000000
               mean     296.500000
               std       75.660426
               min      243.000000
               25%      269.750000
               50%      296.500000
               75%      323.250000
               max      350.000000
        Name: FB, dtype: float64
        '''
        ```
        
- Merging, Joining, and Concatenating
    
    *concatenate: link(things) together in a chain or series.
    
    → concatenation basically glues together the data frames.
    
    pd.concat(), pd.merge()
    
    - concatenating
        
        ```python
        import pandas as pd
        
        df1 = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
                            'B': ['B0', 'B1', 'B2', 'B3'],
                            'C': ['C0', 'C1', 'C2', 'C3'],
                            'D': ['D0', 'D1', 'D2', 'D3']}, 
                            index = [0, 1, 2, 3])
        df2 = pd.DataFrame({'A': ['A4', 'A5', 'A6', 'A7'],
                            'B': ['B4', 'B5', 'B6', 'B7'],
                            'C': ['C4', 'C5', 'C6', 'C7'],
                            'D': ['D4', 'D5', 'D6', 'D7']}, 
                            index = [4, 5, 6, 7])
        df3 = pd.DataFrame({'A': ['A8', 'A9', 'A10', 'A11'],
                            'B': ['B8', 'B9', 'B10', 'B11'],
                            'C': ['C8', 'C9', 'C10', 'C11'],
                            'D': ['D8', 'D9', 'D10', 'D11']}, 
                            index = [8, 9, 10, 11])
        
        ##Concatenation
        #in the concat method(), the parameter should be a sequence
        #
        print(pd.concat([df1, df2, df3]))
        '''
              A    B    C    D
        0    A0   B0   C0   D0
        1    A1   B1   C1   D1
        2    A2   B2   C2   D2
        3    A3   B3   C3   D3
        4    A4   B4   C4   D4
        5    A5   B5   C5   D5
        6    A6   B6   C6   D6
        7    A7   B7   C7   D7
        8    A8   B8   C8   D8
        9    A9   B9   C9   D9
        10  A10  B10  C10  D10
        11  A11  B11  C11  D11
        '''
        #joinging along the columns
        print(pd.concat([df1, df2, df3], axis = 1))
        '''
              A    B    C    D    A    B    C    D    A    B    C    D
        0    A0   B0   C0   D0  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN
        1    A1   B1   C1   D1  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN
        2    A2   B2   C2   D2  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN
        3    A3   B3   C3   D3  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN
        4   NaN  NaN  NaN  NaN   A4   B4   C4   D4  NaN  NaN  NaN  NaN
        5   NaN  NaN  NaN  NaN   A5   B5   C5   D5  NaN  NaN  NaN  NaN
        6   NaN  NaN  NaN  NaN   A6   B6   C6   D6  NaN  NaN  NaN  NaN
        7   NaN  NaN  NaN  NaN   A7   B7   C7   D7  NaN  NaN  NaN  NaN
        8   NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN   A8   B8   C8   D8
        9   NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN   A9   B9   C9   D9
        10  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  A10  B10  C10  D10
        11  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  A11  B11  C11  D11
        '''
        ```
        
    - merging
        - The [**merge()**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.merge.html) method allows you to merge DataFrames together using a similar logic as merging SQL Tables together.
        
        ```python
        ##merging example 
        left = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                            'A': ['A0', 'A1', 'A2', 'A3'],
                            'B': ['B0', 'B1', 'B2', 'B3']})
        print(left)
        '''
        key   A   B
        0  K0  A0  B0
        1  K1  A1  B1
        2  K2  A2  B2
        3  K3  A3  B3
        '''
        right = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                            'C': ['C0', 'C1', 'C2', 'C3'],
                            'D': ['D0', 'D1', 'D2', 'D3']})
        print(right)
        '''
        key   C   D
        0  K0  C0  D0
        1  K1  C1  D1
        2  K2  C2  D2
        3  K3  C3  D3
        '''
        print(pd.merge(left, right, how = 'inner', on = 'key' ))
        '''
          key   A   B   C   D
        0  K0  A0  B0  C0  D0
        1  K1  A1  B1  C1  D1
        2  K2  A2  B2  C2  D2
        3  K3  A3  B3  C3  D3
        '''
        #you could do something like
        #pd.merge(left, right, how = 'outer', on = ['key1', 'key2'])
        ```
        
    - joining
        
        this is quite similar to merge except that this one joins data frames on the index, instead of the columns.
        
        **DataFrame.join(*other*, *on=None*, *how='left'*, *lsuffix=''*, *rsuffix=''*, *sort=False*, *validate=None*)[[source]](https://github.com/pandas-dev/pandas/blob/v1.5.2/pandas/core/frame.py#L9813-L9984)**
        
        Join columns of another DataFrame.
        
        ```python
        import pandas as pd
        
        df = pd.DataFrame({'key':['K0', 'K1', 'K2', 'K3', 'K4', 'K5'],
                           'A':['A0', 'A1', 'A2', 'A3', 'A4', 'A5']})
        print(df)
        '''
          key   A
        0  K0  A0
        1  K1  A1
        2  K2  A2
        3  K3  A3
        4  K4  A4
        5  K5  A5
        '''
        other = pd.DataFrame({'key':['K0', 'K1', 'K2'], 
                              'B':['B0', 'B1', 'B2']})
        print (other)
        '''
          key   B
        0  K0  B0
        1  K1  B1
        2  K2  B2
        '''
        ##joining DataFrames
        #when the dimensions of the dataframes are different, 
        #you have to specify lsuffix and rsuffix.
        print(df.join(other, lsuffix = '_caller' , rsuffix= '_other'))
        '''
         key_caller   A key_other    B
        0         K0  A0        K0   B0
        1         K1  A1        K1   B1
        2         K2  A2        K2   B2
        3         K3  A3       NaN  NaN
        4         K4  A4       NaN  NaN
        5         K5  A5       NaN  NaN
        '''
        ```
        
    
- Useful operations
    
    useful operations in pandas
    
    ```python
    import pandas as pd
    
    df = pd.DataFrame({'col1':[1, 2, 3, 4],
                       'col2':[444, 555, 666, 444],
                       'col3':['abc', 'def', 'ghi', 'xyz']})
    print(df)
    '''
       col1  col2 col3
    0     1   444  abc
    1     2   555  def
    2     3   666  ghi
    3     4   444  xyz
    '''
    #head() method means "return the first n rows"
    print(df.head(n=3))
    '''
       col1  col2 col3
    0     1   444  abc
    1     2   555  def
    2     3   666  ghi
    '''
    #unique(), nunique(), value_counts()
    print(df['col2'].unique())#[444 555 666]
    print(df['col1'].nunique())#4
    print(df['col2'].nunique())#3
    print(df['col2'].value_counts())
    '''
    444    2
    555    1
    666    1
    Name: col2, dtype: int64
    '''
    
    ##conditional selection
    print(df[df['col1']>2])
    '''
    col1  col2 col3
    2     3   666  ghi
    3     4   444  xyz
    '''
    #what's inside the df[] is essentially a serie of boolean values
    print(df['col1']>2)
    '''
    0    False
    1    False
    2     True
    3     True
    Name: col1, dtype: bool
    '''
    #you can use boolean operator when during conditional selection
    print(df[(df['col1']>2)&(df['col2']==444)])
    '''
       col1  col2 col3
    3     4   444  xyz
    '''
    
    ##apply method
    def times2(x):
        return x*2
    
    print(df)
    '''
      col1  col2 col3
    0     1   444  abc
    1     2   555  def
    2     3   666  ghi
    3     4   444  xyz
    '''
    print(df['col1'].apply(times2))
    '''
    0    2
    1    4
    2    6
    3    8
    '''
    #lambda expression
    print(df['col1'].apply(lambda x: x*2))
    '''
    0    2
    1    4
    2    6
    3    8
    '''
    print(df.columns) #Index(['col1', 'col2', 'col3'], dtype='object')
    print(df.index) #RangeIndex(start=0, stop=4, step=1)
    
    #sort_values()
    print(df.sort_values(by='col2'))
    '''
       col1  col2 col3
    0     1   444  abc
    3     4   444  xyz
    1     2   555  def
    2     3   666  ghi
    '''
    #isnull()
    print(df.isnull())
    '''
        col1   col2   col3
    0  False  False  False
    1  False  False  False
    2  False  False  False
    3  False  False  False
    '''
    
    #pivot_table()
    data = {'A':['foo', 'foo', 'foo', 'bar', 'bar', 'bar'],
            'B':['one', 'one', 'two', 'two', 'one', 'one'],
            'C':['x', 'y', 'x', 'y', 'x', 'y'],
            'D':[1, 3, 2, 5, 4, 1]}
    df = pd.DataFrame(data)
    print(df)
    '''
         A    B  C  D
    0  foo  one  x  1
    1  foo  one  y  3
    2  foo  two  x  2
    3  bar  two  y  5
    4  bar  one  x  4
    5  bar  one  y  1
    '''
    #you put values, index, columns in the pivot_table() method
    print(df.pivot_table(values = 'D', index = ['A', 'B'], columns = 'C'))
    '''
    C          x    y
    A   B
    bar one  4.0  1.0
        two  NaN  5.0
    foo one  1.0  3.0
        two  2.0  NaN
    '''
    ```
    
- Data Input and Output
    - CSV
        
        **Preparing Data** 
        
        ```python
        import pandas as pd
        
        #preparing data
        data = {
            'CHN': {'COUNTRY': 'China', 'POP': 1_398.72, 'AREA': 9_596.96,
                    'GDP': 12_234.78, 'CONT': 'Asia'},
            'IND': {'COUNTRY': 'India', 'POP': 1_351.16, 'AREA': 3_287.26,
                    'GDP': 2_575.67, 'CONT': 'Asia', 'IND_DAY': '1947-08-15'},
            'USA': {'COUNTRY': 'US', 'POP': 329.74, 'AREA': 9_833.52,
                    'GDP': 19_485.39, 'CONT': 'N.America',
                    'IND_DAY': '1776-07-04'},
            'IDN': {'COUNTRY': 'Indonesia', 'POP': 268.07, 'AREA': 1_910.93,
                    'GDP': 1_015.54, 'CONT': 'Asia', 'IND_DAY': '1945-08-17'},
            'BRA': {'COUNTRY': 'Brazil', 'POP': 210.32, 'AREA': 8_515.77,
                    'GDP': 2_055.51, 'CONT': 'S.America', 'IND_DAY': '1822-09-07'},
            'PAK': {'COUNTRY': 'Pakistan', 'POP': 205.71, 'AREA': 881.91,
                    'GDP': 302.14, 'CONT': 'Asia', 'IND_DAY': '1947-08-14'},
            'NGA': {'COUNTRY': 'Nigeria', 'POP': 200.96, 'AREA': 923.77,
                    'GDP': 375.77, 'CONT': 'Africa', 'IND_DAY': '1960-10-01'},
            'BGD': {'COUNTRY': 'Bangladesh', 'POP': 167.09, 'AREA': 147.57,
                    'GDP': 245.63, 'CONT': 'Asia', 'IND_DAY': '1971-03-26'},
            'RUS': {'COUNTRY': 'Russia', 'POP': 146.79, 'AREA': 17_098.25,
                    'GDP': 1_530.75, 'IND_DAY': '1992-06-12'},
            'MEX': {'COUNTRY': 'Mexico', 'POP': 126.58, 'AREA': 1_964.38,
                    'GDP': 1_158.23, 'CONT': 'N.America', 'IND_DAY': '1810-09-16'},
            'JPN': {'COUNTRY': 'Japan', 'POP': 126.22, 'AREA': 377.97,
                    'GDP': 4_872.42, 'CONT': 'Asia'},
            'DEU': {'COUNTRY': 'Germany', 'POP': 83.02, 'AREA': 357.11,
                    'GDP': 3_693.20, 'CONT': 'Europe'},
            'FRA': {'COUNTRY': 'France', 'POP': 67.02, 'AREA': 640.68,
                    'GDP': 2_582.49, 'CONT': 'Europe', 'IND_DAY': '1789-07-14'},
            'GBR': {'COUNTRY': 'UK', 'POP': 66.44, 'AREA': 242.50,
                    'GDP': 2_631.23, 'CONT': 'Europe'},
            'ITA': {'COUNTRY': 'Italy', 'POP': 60.36, 'AREA': 301.34,
                    'GDP': 1_943.84, 'CONT': 'Europe'},
            'ARG': {'COUNTRY': 'Argentina', 'POP': 44.94, 'AREA': 2_780.40,
                    'GDP': 637.49, 'CONT': 'S.America', 'IND_DAY': '1816-07-09'},
            'DZA': {'COUNTRY': 'Algeria', 'POP': 43.38, 'AREA': 2_381.74,
                    'GDP': 167.56, 'CONT': 'Africa', 'IND_DAY': '1962-07-05'},
            'CAN': {'COUNTRY': 'Canada', 'POP': 37.59, 'AREA': 9_984.67,
                    'GDP': 1_647.12, 'CONT': 'N.America', 'IND_DAY': '1867-07-01'},
            'AUS': {'COUNTRY': 'Australia', 'POP': 25.47, 'AREA': 7_692.02,
                    'GDP': 1_408.68, 'CONT': 'Oceania'},
            'KAZ': {'COUNTRY': 'Kazakhstan', 'POP': 18.53, 'AREA': 2_724.90,
                    'GDP': 159.41, 'CONT': 'Asia', 'IND_DAY': '1991-12-16'}
        }
        
        '''
         CHN         IND         USA         IDN         BRA         PAK         NGA         BGD         RUS  ...      DEU         FRA      GBR      ITA         ARG         DZA         CAN        AUS         KAZ
        COUNTRY    China       India          US   Indonesia      Brazil    Pakistan     Nigeria  Bangladesh      Russia  ...  Germany      France       UK    Italy   Argentina     Algeria      Canada  Australia  Kazakhstan
        POP      1398.72     1351.16      329.74      268.07      210.32      205.71      200.96      167.09      146.79  ...    83.02       67.02    66.44    60.36       44.94       43.38       37.59      25.47       18.53
        AREA     9596.96     3287.26     9833.52     1910.93     8515.77      881.91      923.77      147.57     17098.2  ...   357.11      640.68    242.5   301.34      2780.4     2381.74     9984.67    7692.02      2724.9
        GDP      12234.8     2575.67     19485.4     1015.54     2055.51      302.14      375.77      245.63     1530.75  ...   3693.2     2582.49  2631.23  1943.84      637.49      167.56     1647.12    1408.68      159.41
        CONT        Asia        Asia   N.America        Asia   S.America        Asia      Africa        Asia         NaN  ...   Europe      Europe   Europe   Europe   S.America      Africa   N.America    Oceania        Asia
        IND_DAY      NaN  1947-08-15  1776-07-04  1945-08-17  1822-09-07  1947-08-14  1960-10-01  1971-03-26  1992-06-12  ...      NaN  1789-07-14      NaN      NaN  1816-07-09  1962-07-05  1867-07-01        NaN  1991-12-16
        '''
        
        df = pd.DataFrame(data).transpose()
        print(df)
        '''
        PAK    Pakistan   205.71   881.91   302.14       Asia  1947-08-14
        NGA     Nigeria   200.96   923.77   375.77     Africa  1960-10-01
        BGD  Bangladesh   167.09   147.57   245.63       Asia  1971-03-26
        RUS      Russia   146.79  17098.2  1530.75        NaN  1992-06-12
        MEX      Mexico   126.58  1964.38  1158.23  N.America  1810-09-16
        JPN       Japan   126.22   377.97  4872.42       Asia         NaN
        DEU     Germany    83.02   357.11   3693.2     Europe         NaN
        FRA      France    67.02   640.68  2582.49     Europe  1789-07-14
        GBR          UK    66.44    242.5  2631.23     Europe         NaN
        ITA       Italy    60.36   301.34  1943.84     Europe         NaN
        ARG   Argentina    44.94   2780.4   637.49  S.America  1816-07-09
        DZA     Algeria    43.38  2381.74   167.56     Africa  1962-07-05
        CAN      Canada    37.59  9984.67  1647.12  N.America  1867-07-01
        AUS   Australia    25.47  7692.02  1408.68    Oceania         NaN
        KAZ  Kazakhstan    18.53   2724.9   159.41       Asia  1991-12-16
        '''
        ```
        
        - A [comma-separated values (CSV)](https://en.wikipedia.org/wiki/Comma-separated_values)
        file is a plaintext file with a `.csv`
        extension that holds tabular data. This is one of the most popular file formats for storing large amounts of data. Each row of the CSV file represents a single table row. The values in the same row are by default separated with commas, but you could change the separator to a semicolon, tab, space, or some other character.
            
            ```python
            #write a cvs file
            #You can save your Pandas DataFrame as a CSV file with .to_csv():
            df.to_csv('data.cvs')
            ```
            
            - see how your cvs file got stored in your working directory as ‘data.cvs’ file.
                
                ```python
                ,COUNTRY,POP,AREA,GDP,CONT,IND_DAY
                CHN,China,1398.72,9596.96,12234.78,Asia,
                IND,India,1351.16,3287.26,2575.67,Asia,1947-08-15
                USA,US,329.74,9833.52,19485.39,N.America,1776-07-04
                IDN,Indonesia,268.07,1910.93,1015.54,Asia,1945-08-17
                BRA,Brazil,210.32,8515.77,2055.51,S.America,1822-09-07
                PAK,Pakistan,205.71,881.91,302.14,Asia,1947-08-14
                NGA,Nigeria,200.96,923.77,375.77,Africa,1960-10-01
                BGD,Bangladesh,167.09,147.57,245.63,Asia,1971-03-26
                RUS,Russia,146.79,17098.25,1530.75,,1992-06-12
                MEX,Mexico,126.58,1964.38,1158.23,N.America,1810-09-16
                JPN,Japan,126.22,377.97,4872.42,Asia,
                DEU,Germany,83.02,357.11,3693.2,Europe,
                FRA,France,67.02,640.68,2582.49,Europe,1789-07-14
                GBR,UK,66.44,242.5,2631.23,Europe,
                ITA,Italy,60.36,301.34,1943.84,Europe,
                ARG,Argentina,44.94,2780.4,637.49,S.America,1816-07-09
                DZA,Algeria,43.38,2381.74,167.56,Africa,1962-07-05
                CAN,Canada,37.59,9984.67,1647.12,N.America,1867-07-01
                AUS,Australia,25.47,7692.02,1408.68,Oceania,
                KAZ,Kazakhstan,18.53,2724.9,159.41,Asia,1991-12-16
                
                ```
                
                ![Untitled](Python%20for%20Data%20Science-Pandas%209fbf14b6880b48d28252449eaa3bd72b/Untitled%201.png)
                
                ![Untitled](Python%20for%20Data%20Science-Pandas%209fbf14b6880b48d28252449eaa3bd72b/Untitled%202.png)
                
                This text file contains the data separated with **commas**
                . The first column contains the row labels. In some cases, you’ll find them irrelevant. If you don’t want to keep them, then you can pass the argument `index=False`
                 to `.to_csv().`
                
                ```python
                df.to_cvs('data.cvs', index = False)
                ```
                
                ![Untitled](Python%20for%20Data%20Science-Pandas%209fbf14b6880b48d28252449eaa3bd72b/Untitled%203.png)
                
            
            The parameter `index_col`
            specifies the column from the CSV file that contains the row labels. You assign a zero-based column index to this parameter. You should determine the value of `index_col` when the CSV file contains the row labels to avoid loading them as data.
            
            ```python
            #read a cvs file
            #Once your data is saved in a CSV file, you’ll likely want to load and use it from time to time. You can do that with the Pandas read_csv() function:
            df = pd.read_csv('data.csv', index_col=0)
            print(df)
            '''
                            POP      AREA       GDP       CONT     IND_DAY
            COUNTRY
            China       1398.72   9596.96  12234.78       Asia         NaN
            India       1351.16   3287.26   2575.67       Asia  1947-08-15
            US           329.74   9833.52  19485.39  N.America  1776-07-04
            Indonesia    268.07   1910.93   1015.54       Asia  1945-08-17
            Brazil       210.32   8515.77   2055.51  S.America  1822-09-07
            Pakistan     205.71    881.91    302.14       Asia  1947-08-14
            Nigeria      200.96    923.77    375.77     Africa  1960-10-01
            Bangladesh   167.09    147.57    245.63       Asia  1971-03-26
            Russia       146.79  17098.25   1530.75        NaN  1992-06-12
            Mexico       126.58   1964.38   1158.23  N.America  1810-09-16
            Japan        126.22    377.97   4872.42       Asia         NaN
            Germany       83.02    357.11   3693.20     Europe         NaN
            France        67.02    640.68   2582.49     Europe  1789-07-14
            UK            66.44    242.50   2631.23     Europe         NaN
            Italy         60.36    301.34   1943.84     Europe         NaN
            Argentina     44.94   2780.40    637.49  S.America  1816-07-09
            Algeria       43.38   2381.74    167.56     Africa  1962-07-05
            Canada        37.59   9984.67   1647.12  N.America  1867-07-01
            Australia     25.47   7692.02   1408.68    Oceania         NaN
            Kazakhstan    18.53   2724.90    159.41       Asia  1991-12-16
            '''
            #without the index_col value determination
            df = pd.read_csv('data.csv')
            print(df)
            '''
                   COUNTRY      POP      AREA       GDP       CONT     IND_DAY
            0        China  1398.72   9596.96  12234.78       Asia         NaN
            1        India  1351.16   3287.26   2575.67       Asia  1947-08-15
            2           US   329.74   9833.52  19485.39  N.America  1776-07-04
            3    Indonesia   268.07   1910.93   1015.54       Asia  1945-08-17
            4       Brazil   210.32   8515.77   2055.51  S.America  1822-09-07
            5     Pakistan   205.71    881.91    302.14       Asia  1947-08-14
            6      Nigeria   200.96    923.77    375.77     Africa  1960-10-01
            7   Bangladesh   167.09    147.57    245.63       Asia  1971-03-26
            8       Russia   146.79  17098.25   1530.75        NaN  1992-06-12
            9       Mexico   126.58   1964.38   1158.23  N.America  1810-09-16
            10       Japan   126.22    377.97   4872.42       Asia         NaN
            11     Germany    83.02    357.11   3693.20     Europe         NaN
            12      France    67.02    640.68   2582.49     Europe  1789-07-14
            13          UK    66.44    242.50   2631.23     Europe         NaN
            14       Italy    60.36    301.34   1943.84     Europe         NaN
            15   Argentina    44.94   2780.40    637.49  S.America  1816-07-09
            16     Algeria    43.38   2381.74    167.56     Africa  1962-07-05
            17      Canada    37.59   9984.67   1647.12  N.America  1867-07-01
            18   Australia    25.47   7692.02   1408.68    Oceania         NaN
            19  Kazakhstan    18.53   2724.90    159.41       Asia  1991-12-16
            '''
            ```
            
    - Excel
        
        ## **Using Pandas to Write and Read Excel Files**
        
        [Microsoft Excel](https://products.office.com/en/excel) is probably the most widely-used spreadsheet software. While older versions used binary `[.xls](https://en.wikipedia.org/wiki/Microsoft_Excel#File_formats)` files, Excel 2007 introduced the new XML-based `[.xlsx](https://en.wikipedia.org/wiki/Microsoft_Office_XML_formats)` file. You can read and write Excel files in Pandas, similar to CSV files. However, you’ll need to install the following Python packages first:
        
        - [xlwt](https://xlwt.readthedocs.io/en/latest/) to write to `.xls` files
        - [openpyxl](https://openpyxl.readthedocs.io/en/stable/) or [XlsxWriter](https://xlsxwriter.readthedocs.io/) to write to `.xlsx` files
        - [xlrd](https://xlrd.readthedocs.io/en/latest/) to read Excel files
        
        You can install them using [pip](https://realpython.com/what-is-pip/) with a single command:
        
        `$ pip install xlwt openpyxl xlsxwriter xlrd`
        
        You can also use Conda:
        
        `$ conda install xlwt openpyxl xlsxwriter xlrd`
        
        ### **Write an Excel File**
        
        Once you have those packages installed, you can save your `DataFrame` in an Excel file with `[.to_excel()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_excel.html)`:
        
        >>>
        
        `>>> df.to_excel('data.xlsx')`
        
        The argument `'data.xlsx'` represents the target file and, optionally, its path. The above statement should create the file `data.xlsx` in your current working directory. That file should look like this:
        
        ![https://files.realpython.com/media/excel.ca33ad30becb.png](https://files.realpython.com/media/excel.ca33ad30becb.png)
        
        The first column of the file contains the labels of the rows, while the other columns store data.
        
        ### **Read an Excel File**
        
        You can load data from Excel files with `[read_excel()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html)`:
        
        ```python
        >>>
        
        >>> df = pd.read_excel('data.xlsx', index_col=0)
        >>> df
                COUNTRY      POP      AREA       GDP       CONT     IND_DAY
        CHN       China  1398.72   9596.96  12234.78       Asia         NaN
        IND       India  1351.16   3287.26   2575.67       Asia  1947-08-15
        USA          US   329.74   9833.52  19485.39  N.America  1776-07-04
        IDN   Indonesia   268.07   1910.93   1015.54       Asia  1945-08-17
        BRA      Brazil   210.32   8515.77   2055.51  S.America  1822-09-07
        PAK    Pakistan   205.71    881.91    302.14       Asia  1947-08-14
        NGA     Nigeria   200.96    923.77    375.77     Africa  1960-10-01
        BGD  Bangladesh   167.09    147.57    245.63       Asia  1971-03-26
        RUS      Russia   146.79  17098.25   1530.75        NaN  1992-06-12
        MEX      Mexico   126.58   1964.38   1158.23  N.America  1810-09-16
        JPN       Japan   126.22    377.97   4872.42       Asia         NaN
        DEU     Germany    83.02    357.11   3693.20     Europe         NaN
        FRA      France    67.02    640.68   2582.49     Europe  1789-07-14
        GBR          UK    66.44    242.50   2631.23     Europe         NaN
        ITA       Italy    60.36    301.34   1943.84     Europe         NaN
        ARG   Argentina    44.94   2780.40    637.49  S.America  1816-07-09
        DZA     Algeria    43.38   2381.74    167.56     Africa  1962-07-05
        CAN      Canada    37.59   9984.67   1647.12  N.America  1867-07-01
        AUS   Australia    25.47   7692.02   1408.68    Oceania         NaN
        KAZ  Kazakhstan    18.53   2724.90    159.41       Asia  1991-12-16
        ```
        
        `read_excel()` returns a new `DataFrame` that contains the values from `data.xlsx`. You can also use `read_excel()` with [OpenDocument spreadsheets](http://www.opendocumentformat.org/aboutODF/), or `.ods` files.
        
        You’ll learn more about working with Excel files [later on in this tutorial](https://realpython.com/pandas-read-write-files/#excel-files). You can also check out [Using Pandas to Read Large Excel Files in Python](https://realpython.com/working-with-large-excel-files-in-pandas/).
        
    - HTML
        
        you need to install *lxml* to do this.
        
        **read html file**
        
        ```python
        import pandas as pd
        
        data_html = pd.read_html("https://www.fdic.gov/resources/resolutions/bank-failures/failed-bank-list/index.html")
        ```
        
        if you do type(data_html), python will return list. 
        
        so what the pandas essentially trying to do is to find every possible table elements in the html page, make a list of them, and convert each item into a data frame. what you want to do is to cycle through the list until you get what you are looking for.
        
        ```python
        data[0] #this will return the very first table element converted into a data frame.
        ```
        
    - SQL
    - [instructions on reading and writing different type of files](https://realpython.com/pandas-read-write-files/#write-a-csv-file)