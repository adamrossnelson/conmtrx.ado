# conmtrx.ado
Simplifies confusion matrix output for Stata.

This code is an extension of: https://ideas.repec.org/c/boc/bocode/s458127.html

Also inspired by https://artax.karlin.mff.cuni.cz/r-help/library/caret/html/confusionMatrix.html

Another related resource https://www.statalist.org/forums/forum/general-stata-discussion/general/1371221-n-by-k-contingency-table-for-two-categorical-variable-sensitivity-specificity-ppv-npv-accuracy-calculations

## Quick install.

Use the following to install from command line:

```
copy https://raw.githubusercontent.com/adamrossnelson/conmtrx/master/conmtrx.ado "`c(sysdir_plus)'"
```

## Usage

```
conmtrx rowvar(binary) colvar(binary) [rowtitle coltitle]
```
Where rowvar is generally the predicted outcome while colvar is generally the actual outcome. Optionally `conmtrx` accepts a `rowtitle` and `coltitle`. If no row or column title specified the defaults are `Predicted` and `Actual`.

Previously with `classtabi' the syntax was:
```
classtabi #a #b #c #d [, rowlabel(string) collabel(string)]
```
Where each of the four figure (`#a #b #c #d`) represente one of the four probabilities.

|     Negatives                           |     Positives                              |
|-----------------------------------------|--------------------------------------------|
| #a -- disease=0, test=0 (true negative) | #b -- disease=0, test=1 (false positive)   |
| #c -- disease=1, test=0 (false negative)| #d -- disease=1, test=1 (true positive)    |

## Also requires

Also requires `distinct` which can be installed with `ssc install distinct` and `classtabi` also available using `ssc install classtabi`.

However `conmtrx` will check for, and if not found install `distinct` and `classtabi`.

## Demonstration output
```
. conmtrx prUnd isUnd
Specified variables binary. Producing confusion matrix.

+----------------+
| Key            |
|----------------|
|   frequency    |
| row percentage |
+----------------+

 Predicted |
     Under |     Actual   Under
           |         0          1 |     Total
-----------+----------------------+----------
         0 |        36         60 |        96 
           |     37.50      62.50 |    100.00 
-----------+----------------------+----------
         1 |         2          2 |         4 
           |     50.00      50.00 |    100.00 
-----------+----------------------+----------
     Total |        38         62 |       100 
           |     38.00      62.00 |    100.00 


           |        Actual
 Predicted |         0          1 |     Total
-----------+----------------------+----------
         0 |        36         60 |        96 
         1 |         2          2 |         4 
-----------+----------------------+----------
     Total |        38         62 |       100 



-------------------------------------------------
Sensitivity                     D/(C+D)   50.00%      
Specificity                     A/(A+B)   37.50%      
Positive predictive value       D/(B+D)    3.23%      
Negative predictive value       A/(A+C)   94.74%      
-------------------------------------------------
False positive rate             B/(A+B)   62.50%      
False negative rate             C/(C+D)   50.00%      
-------------------------------------------------
Correctly classified      A+C/(A+B+C+D)   38.00%      
-------------------------------------------------
Effect strength for sensitivity          -12.50%      
-------------------------------------------------
ROC area                                  0.4375      
-------------------------------------------------
 - conmtrx - Command was a succss.

```

## Known limitation

Does not support if statements.
