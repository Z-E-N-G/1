[TOC]

# §1 Basic Concepts

## Some Shortcuts

```matlab
exit,quit % quit
Ctrl-C % interruption
Ctrl-l % moving one word to the left
Ctrl-r % .......................right
Ctrl-a % moving to the beginning of the line
Ctrl-e % ..............end..................
Ctrl-k % deleting from here to the end of the line
```

## Some Tips

1. You are allowed to **define** more than one variable on the same line, provided they are separated by ';'.

2. You can input '...' at the end of the line in order to continue typing on the next line.

3. In MATLAB, The elements of the matrix are indexed by **column first and then row**.

4. Date Formats
	| Numbers | <span id="FORM">Forms</span> ([BACK](#form)) |
   | ------- | -------------------------------------------- |
   | 0       | 22-Apr-2020 02:14:00                         |
   | 1       | 22-Apr-2020                                  |
   | 2       | 04/22/20                                     |
   | 3       | Apr                                          |
   | 4       | A     (April)                                |
   | 5       | 4     (April)                                |
   | 6       | 04/22                                        |
   | 7       | 22                                           |
   | 8       | Thu     (Thursday)                           |
   | 9       | T      (Thursday)                            |
   | 10      | 2020                                         |
   | 11      | 20     (2020)                                |
   | 12      | Apr20                                        |
   | 13      | 02:14:00                                     |
   | 14      | 02:14:00 AM                                  |
   | 15      | 02:14                                        |
   | 16      | 02:14 AM                                     |
   | 17      | Q2-20     ($2_{nd}$ quarters of 1 hour-2020) |
   | 18      | Q2                                           |

5. Output Formats

   1. Normally, integer or short float with 4 decimal places

   2. Format Changes

      ```matlab
      >> format
      >> p=1/3-1
      
      p =
      
         -0.6667
      
      >> format short;p
      
      p =
      
         -0.6667
      
      >> format long;p
      
      p =
      
        -0.666666666666667
      
      >> format short e;p
      
      p =
      
        -6.6667e-01
      
      >> format long e;p
      
      p =
      
          -6.666666666666667e-01
      
      >> format hex;p
      
      p =
      
         bfe5555555555556
      
      >> format +;p
      
      p =
      
      -
      
      >> format bank;p
      
      p =
      
               -0.67
      
      >> format rat;p
      
      p =
      
            -2/3
            
      >> format compact;p
      p =
            -2/3
      ```

6. Help Commands

## Numerical Matrices

1. 2-dim Matrices

   > row: separated by ' ' or ','
   >
   > column: separated by ';' or Enter

   ```matlab
   % e.g.
   >> A=[1,2,3;4,5,6;]
   % or
   >> A=[1 2 3
   4 5 6]
   
   A =
   
        1     2     3
        4     5     6
   ```

   ```matlab
   % You can also assign to the elements of a matrix one by one.
   >> B ( 1,1 ) = 1;
   B ( 1,2 ) = 7;
   B ( 2,1 ) =-5;
   B ( 2,2 ) = 0
   
   B =
   
        1     7
       -5     0
   ```

2. Multi-dim Matrices

   ```matlab
   % e.g.1 constructed from 2 known 2-dim matrices
   >> A=[1 2 3
   4 5 6];
   >> B=[11 12 13
   14 15 16];
   >> C(:,:,1)=A;
   >> C(:,:,2)=B
   
   C(:,:,1) =
   
        1     2     3
        4     5     6
   
   
   C(:,:,2) =
   
       11    12    13
       14    15    16
   % e.g.2 change one element of the above C
   >> C(1,1,1)=100
   
   C(:,:,1) =
   
      100     2     3
        4     5     6
   
   
   C(:,:,2) =
   
       11    12    13
       14    15    16
   ```

3. Dimensions and Lengths

   1. `size(#)`

      ```matlab
      % size(Matrix_name): giving the length of every dim
      >> size(A)
      
      ans =
      
           2     3
      % size(Matrix_name,Dim_number): giving the length of the specific dim
      >> size(A,2)
      
      ans =
      
           3
      % size(Row_vector_name/Column_vector_name):returning 1 & the length of the row vector / the length of the column vector & 1
      >> X=[1 2 3 4 5]
      
      X =
      
           1     2     3     4     5
      
      >> size(X)
      
      ans =
      
           1     5
      ```

   2. `length(#)`

      ```matlab
      % length(Vector_name):giving the length of the vector
      >> length(X)
      
      ans =
      
           5
      % length(Matrix_name):giving the maximum of the length of each dimension of the matrix
      >> length(C)
      
      ans =
      
           3
      ```

   3. `ndims(#)`

      ```matlab
      % ndims(Matrix_name): giving the dimension of the matrix
      >> ndims(C)
      
      ans =
      
           3
      ```

4. Conversion between Subscripts and indexes

   1. `sub2ind`

      ```matlab
      % sub2ind(size,Sub_No): The given subscripts of elements will be converted into homologous indexes.
      >> ind=sub2ind(size(A),[1,2;1,2],[1,1;3,2])
      
      ind =
      
           1     2
           5     4
      ```

   2. `ind2sub`

      ```matlab
      % ind2sub(size,Ind_No): This is the inverse process of the mentioned above.
      >> [I,J]=ind2sub(size(A),ind)
      
      I =
      
           1     2
           1     2
      
      
      J =
      
           1     1
           3     2
      ```

## Variables

1. Some Basic Rules

   1. In MATLAB, variables are **case sensitive** and the predefined are usually **lowercase**.
   2. 'A~Z', 'a~z' and '_' can be used to name a variable, but the first char of the name must be a letter.

2. Simple Data Types

   | Types    | Explanations                                    |
   | -------- | ----------------------------------------------- |
   | `double` | Double-precision floating-point format/64-digit |
   | `char`   | 16-digit                                        |
   | `sparse` | To storage sparse matrix                        |
   | `unit8`  | 8-digit unsigned int                            |

3. Logical Functions

   | Functions      | Explanations                                 |
   | -------------- | -------------------------------------------- |
   | `iscell(x)`    | If true, return 1; Else return 0/Cell matrix |
   | `isfield(x)`   | Ditto                                        |
   | `isfinite(x)`  | Return the same vector as x                  |
   | `islogical(x)` | Same as $1_{st}$/Logical vector              |
   | `isnumeric(x)` | Ditto/Numeric vector                         |
   | `isstr(x)`     | Ditto/String                                 |
   | `isstruct(x)`  | Ditto/Structure                              |
   | `isobject(x)`  | Ditto/Object                                 |
   | `logical(x)`   | Return a logical vector that can be used     |

4. Predefined Variables

   | Variables           | Explanations                                                 |
   | ------------------- | ------------------------------------------------------------ |
   | `ans`               | assigned the value of the last expression, which doesn't have a name |
   | `eps`               | the diff between 1 and the closest representative floating-point number<br />You can set a new value, but it can't restore by the command 'clear'. |
   | `realmax` `realmin` | the biggest/smallest float-point number                      |
   | `pi`                | namely $\pi$                                                 |
   | `inf`               | defined as $\frac{1}{0}$<br />When 0 becomes the divisor, it will return 'inf' instead of interruption. |
   | `NaN`               | defined as 'Not a Number'<br />It is '%'type or $\frac{inf}{inf}$ |
   | `i` `j`             | defined as $\sqrt{-1}$<br />You can set new values for them and restore by the command 'clear'. |

5. View Variables

   | commands             | Explanations                                                 |
   | -------------------- | ------------------------------------------------------------ |
   | `who`                | return all the defined variables                             |
   | `who global`         | return all the defined global variables                      |
   | `who a*`             | return all the defined variables which start with 'a'        |
   | `whos` `whos global` | show more details than `who`/`who global`                    |
   | `exist(namestr)`     | return diff values according to the definitions of variables in 'namestr' |
   | `inmem`              | return a cell vector, which includes functions and M files in memory so far |
   | `workspace`          | open 'workspace'                                             |

6. Delete Variables

   | commands                | Explanations                                                 |
   | ----------------------- | ------------------------------------------------------------ |
   | `clear`                 | delete all the defined variables and restore all the predefined except `eps` |
   | `clear name1 name2 ...` | delete the specific variables                                |
   | `clear a*`              | delete all the defined variables which start with 'a'        |
   
   > 2 equivalent descriptions: 
   >
   > `command variable`
   >
   > `command('variable')`

## Arithmetic Expressions and Mathematical Functions

1. Arithmetic Operators

   | Priority | Operators |
   | -------- | --------- |
   | H        | ^         |
   | M        | *  /  \   |
   | L        | +  -      |

2. Mathematical Functions

   | Functions   | Explanations            |
   | ----------- | ----------------------- |
   | `abs(x)`    | absolute value          |
   | `sign(x)`   | sign function           |
   | `sqrt(x)`   | $\sqrt{x}$              |
   | `pow2(x,f)` | $x\times 2^f$           |
   | `exp(x)`    | $e^x$                   |
   | `log(x)`    | $\ln{x}$                |
   | `log10(x)`  | $\log_{10}{x}$          |
   | `sin(x)...` | trigonometric functions |

   > The x in trigonometric functions must be in radians.

3. Rounding and Relevant Commands

   | Commands              | Explanations                                                 |
   | --------------------- | ------------------------------------------------------------ |
   | `round(x)`            | return the integer closest to x                              |
   | `fix(x)`              | return the integer closest to x **towards 0**                |
   | `floor(x)` `ceil(x)`  | round down/up                                                |
   | `rem(x,y)`            | return the remainder of x/y                                  |
   | `gcd(x,y)`            | GCD                                                          |
   | `[a,b,c]=gcd(x,y)`    | $a=x\cdot b+y\cdot c$                                        |
   | `lcm(x,y)`            | LCM                                                          |
   | `[t,n]=rat(x)`        | $\frac{t}{n}\in\R$ is the approximate value of x with a relative error less than $10^{-6}\ \ \ \ \ (t,n\in\Z)$ |
   | `[t,n]=rat(x,tol)`    | ... less than 'tol'                                          |
   | `rat(x)` `rat(x,tol)` | return continued fraction form of x with a relative error    |

4. Functions on Complex Numbers

   | Functions                 | Explanations                                                 |
   | ------------------------- | ------------------------------------------------------------ |
   | `real(z)` `imag(z)`       | return the real/imaginary part of z                          |
   | `abs(z)`                  | absolute value                                               |
   | `conj(z)`                 | return the complex conjugate of z                            |
   | `angle(z)`                | return the phase angle of z      $(-\pi,\pi)$                |
   | `unwrap(v)` `unwrap(v,k)` | correct the angle to make the diff of adjacent elements smaller than $\pi$/$k\pi$ |
   | `cplxpair(v)`             | return complex conjugate pairs                               |

   ```matlab
   % e.g. cplxpair
   >> v
   
   v =
   
      1.0000 + 2.0000i   2.0000 + 3.0000i  -1.0000 - 3.0000i   1.0000 - 2.0000i  -1.0000 + 3.0000i   2.0000 - 3.0000i   2.0000 + 0.0000i
   
   >> cplxpair(v)
   
   ans =
   
     -1.0000 - 3.0000i  -1.0000 + 3.0000i   1.0000 - 2.0000i   1.0000 + 2.0000i   2.0000 - 3.0000i   2.0000 + 3.0000i   2.0000 + 0.0000i
   ```

5. Coordinate Conversions

   | Conversions                       | Explanations                                                 |
   | --------------------------------- | ------------------------------------------------------------ |
   | `[theta,r]=cart2pol(x,y)`         | convert Cartesian coordinate system into polar coordinate system |
| `[x,y]=pol2cart(theta,r)`         | convert polar coordinate system into Cartesian coordinate system |
   | `[alpha,theta,r]=cart2sph(x,y,z)` | convert Cartesian coordinate system into spherical coordinate system |
   | `[x,y,z]=sph2cart(alha,theta,r)`  | converse process of the above                                |
   
6. ~~Flops and~~ Time Management

   1. ~~`flops`~~

      1. ~~$+ \ -$~~
         1. ~~real: 1 operation~~
         2. ~~complex: 2 operations~~
      2. ~~$\times\ \div$~~
         1. ~~real: 1 operation~~
         2. ~~complex: 6 operations~~
      3. ~~Elementary Functions~~
         1. ~~real: 1 operation~~
         2. ~~complex: more than 1~~ 
      4. ~~`flops(0)`  reset to 0~~

   2. Time Management

      | Commands                  | Explanations                                      |
      | ------------------------- | ------------------------------------------------- |
      | `tic`                     | start a timer                                     |
      | `toc`                     | read the time of the timer started by `tic`       |
      | `clock`<br />`fix(clock)` | return the date and time (scientific notation)    |
      | `etime(t1,t2)`            | return the seconds between t1 and t2              |
      | `eputime`                 | return the seconds of CPU since startup of MATLAB |

      ```matlab
      % e.g.
      >> tic
      >> toc
      历时 2.159932 秒。
      >> clock
      
      ans =
      
         1.0e+03 *
      
          2.0210    0.0010    0.0230    0.0170    0.0360    0.0366
      >> fix(clock)
      
      ans =
      
              2021           1          23          17          35           9
      >> etime([2020 1 23 0 0 0],[2021 1 23 0 0 0])
      
      ans =
      
         -31622400
      >> cputime
      
      ans =
      
        111.3125
      ```

      | Commands                       | Explanations                                                 |
      | ------------------------------ | ------------------------------------------------------------ |
      | `date`                         | date-month-year                                              |
      | `calendar(yyyy,mm)`            | return the appointed calendar                                |
      | `datenum(yyyy,mm,dd)`          | $1_{st}$ day: 0000-01-01                                     |
      | `datestr(d,form)`              | return the date denoted by [form](#FORM)<span id="form"> </span> |
      | `datetick(axis,form)`          | write data on the coordinate axis in the figure              |
      | `datevec(d)`                   | return `[yyyy mm dd ho mi se]`                               |
      | `enomday(yyyy,mm)`             | the number of days                                           |
      | `now`                          | similar to `datenum`                                         |
      | `[daynr dayname]=weekday(day)` | return the day of the week (1 is Sunday)                     |


# §2 Matrix Operations

## Basic Operations

1. $+\ -$

   ```matlab
   % one tip
   >> A
   A =
        1     2
        3     4
   >> A+100
   ans =
      101   102
      103   104
   ```

2. Multiplication
   
   1. $*$
      **2-dim only**
   
   2. $\cdot$
   
      ```matlab
      % dot product
      >> x=[1 2 3 4 5];y=[1;2;3;4;5];
      >> x*y
      ans =
          55
      >> y*x
      ans =
           1     2     3     4     5
           2     4     6     8    10
           3     6     9    12    15
           4     8    12    16    20
           5    10    15    20    25
      >> dot(x,y)
      ans =
          55
      >> dot(y,x)
      ans =
          55
      >> A=[1 2 3
      4 5 6];...
      B=[1 0 0
      0 0 1];
      >> dot(A,B) % namely dot(A,B,1)
      ans =
           1     0     6
      >> dot(A,B,2)
      ans =
           1
           6
      ```
   
   3. $\times$
      similar as dot product
   
   4. Convolution
   
   5. Tensor Product
   
3. Division
   $\rightarrow$ inverse matrix: `inv(Matrix_name)`

4. Conjugate and Transpose

   1. Conjugate: `A.'` or `conj(A)`
   2. Conjugate and Transpose: `A'` 

5. Exponentiation

   ```matlab
   >> A
   A =
        1     2
        2     1
   >> 2^A
   ans =
       4.2500    3.7500
       3.7500    4.2500
   >> A^2
   ans =
        5     4
        4     5
   ```

6. Element Operations
   `+` `-` `.*` `./` `.\` `.^`

## Matrix Functions and Operators

1. Matrix Functions

   |      Functions       |
   | :------------------: |
   | `expm(Matrix_name)`  |
   | `logm(Matrix_name)`  |
   | `sqrtm(Matrix_name)` |

   **Note the difference between `expm` and `exp` etc.**

2. Relational Operators
   `<` `<=` `>` `>=` `==` `~=`
   The elements of the result matrix are 0(false) or 1(true).

3. Logical Operators
   `&` `|` `~` `xor`

   ```matlab
   % e.g.
   >> A=[1 2 0];B=[0 2 3];
   >> A & B
   ans =
     1×3 logical 数组
      0   1   0
   >> A | B
   ans =
     1×3 logical 数组
      1   1   1
   >> ~ A
   ans =
     1×3 logical 数组
      0   0   1
   >> xor(A,B)
   ans =
     1×3 logical 数组
      1   0   1
   >> C=1;
   >> A & C
   ans =
     1×3 logical 数组
      1   1   0
   ```

4. Logical Functions

   1. `find` to give the values and positions of adequate elements of the matrix or vector

      ```matlab
      % e.g.1 finding nonzero elements
      >> x=[1 2 -1 0 0 3 0 4];
      >> find(x)
      ans =
           1     2     3     6     8
      >> A=[1 2 0
      2 0 0
      4 0 3];
      >> find(A)
      ans =
           1
           2
           3
           4
           9
      >> [u,v]=find(A)
      u =
           1
           2
           3
           1
           3
      v =
           1
           1
           1
           2
           3
      >> [u,v,b]=find(A)
      u =
           1
           2
           3
           1
           3
      v =
           1
           1
           1
           2
           3
      b =
           1
           2
           4
           2
           3
      % e.g.2 used with relational operators
      >> find(x>1)
      ans =
           2     6     8
      >> x(ans)
      ans =
           2     3     4
      >> length(ans)
      ans =
           3
      ```

   2. `any` `all` return Boolean values

      ```matlab
      %
      >> x=[1;0;2];y=[1;1;2];z=[0;0;0];
      >> any([x y z])
      ans =
        1×3 logical 数组
         1   1   0
      >> all([x,y,z])
      ans =
        1×3 logical 数组
         0   1   0
      >> any(any([x y z]))
      ans =
        logical
         1
      >> all(all([x y z]))
      ans =
        logical
         0
      % with relational operators
      >> all(y>0)
      ans =
        logical
         1
      >> all(all([x y z]>0))
      ans =
        logical
         0
      % verify if it is a symmetric matrix
      >> A=[1 2 3
      2 1 4
      3 4 1]
      A =
           1     2     3
           2     1     4
           3     4     1
      >> all(all(A==A'))
      ans =
        logical
         1
      % verify if it is an upper triangular matrix
      >> B=[2 3 4
      0 3 2
      0 0 1]
      B =
           2     3     4
           0     3     2
           0     0     1
      >> any(any(tril(B,-1)))
      ans =
        logical
         0
      >> all(all(B))
      ans =
        logical
         0
      >> all(all(B==triu(B)))
      ans =
        logical
         1
      ```

   3. Some Others

      | Functions                            | Explanations        |
      | ------------------------------------ | ------------------- |
      | `isnan(Matrix_name)`                 | `NaN`: 1  others: 0 |
      | `isinf(Matrix_name)`                 | `inf`: 1 others: 0  |
      | `isempty(Matrix_name)`               | empty: 1 else: 0    |
      | `isequal(Matrix_name1,Matrix_name2)` | equal: 1 else: 0    |
      | `isreal(Matrix_name)`                | real: 1  else: 0    |
      | `isfinite(Matrix_name)`              | finite: 1 others: 0 |

## Matrix Creation

1. Basic Matrix Establishment

   1. 1-matrix, 0-matrix and Unit Matrix

      ```matlab
      % ones
      >> ones(3)
      ans =
           1     1     1
           1     1     1
           1     1     1
      >> ones(4,3,2)
      ans(:,:,1) =
           1     1     1
           1     1     1
           1     1     1
           1     1     1
      ans(:,:,2) =
           1     1     1
           1     1     1
           1     1     1
           1     1     1
      >> A=[1 2 3 4 5
      2 3 1 2 5];
      >> ones(size(A))
      ans =
           1     1     1     1     1
           1     1     1     1     1
      % zeros is similar
      % eye
      	% 2-dim only!
      >> eye(4)
      ans =
           1     0     0     0
           0     1     0     0
           0     0     1     0
           0     0     0     1
      >> eye(3,4)
      ans =
           1     0     0     0
           0     1     0     0
           0     0     1     0
      >> eye(size(A))
      ans =
           1     0     0     0     0
           0     1     0     0     0
      ```

   2. Random Matrix

      1. `rand` to generate random numbers between 0 and 1 evenly

         ```matlab
         >> rand
         ans =
             0.4024
         >> rand(4)
         ans =
             0.6589    0.1084    0.9620    0.2599
             0.9013    0.0361    0.7461    0.9620
             0.9954    0.6181    0.6625    0.5402
             0.6532    0.5671    0.5233    0.0303
         >> rand(4,3,2)
         ans(:,:,1) =
             0.6963    0.3302    0.2284
             0.5197    0.2297    0.6520
             0.0590    0.1139    0.0662
             0.8900    0.3109    0.2754
         ans(:,:,2) =
             0.2818    0.6033    0.8486
             0.8801    0.7833    0.0506
             0.4443    0.1139    0.4662
             0.7559    0.9786    0.3257
         ```

      2. `randn` similar to `rand`, normally distributed random number with unit variance and zero mean



