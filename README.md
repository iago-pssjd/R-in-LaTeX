# R-in-LaTeX
**Template for printing R code in LaTeX**

Multiple packages allow formatting programming/markup languages code in `LaTeX`. Among them, one of the most widespread is [listings](https://ctan.org/pkg/listings). Unfortunately, it does not properly format the `R` code, what has generated many questions about how to deal with it and explanations about these problems:
* [lstlisting R keywords](https://tex.stackexchange.com/a/218287/8639)
* [How to nicely display R code with the LaTeX package 'listings'?](https://r.789695.n4.nabble.com/How-to-nicely-display-R-code-with-the-LaTeX-package-listings-td4648110.html)
* [Best use of LaTeX listings package for pretty printing R code](https://stat.ethz.ch/pipermail/r-help/2006-September/113658.html)
* [Colour for R code chunk in listings package](https://stackoverflow.com/questions/21402157/colour-for-r-code-chunk-in-listings-package/21468454)

Therefore, I would not recommend using `listings` to format `R` code in `LaTeX`. Further, when there is a better alternative: using `Sweave` in combination with the `R` library `knitr`. How to do it is explained [here](https://www.r-bloggers.com/getting-started-with-sweave-knitr/). 

Next, I give a summary with the steps I currently followed:

  1. In the `LaTeX` file, include the `R` code between `<<>>=` at the beginning and `@` at the end (instead of `\begin{listings}` and `\end{listings}`), and save this file with the `Sweave` extension `.Rnw`. Right below `\begin{document}`, include `\SweaveOpts{key1=value1, key2=value2,...,keyn=valuen}`, with your desired default options for the `R` code, as for example, `echo=TRUE`, etc.
  2. In `R`, execute:
    
    ```r
    library(knitr)
    Sweave2knitr("file.Rnw")
    ```  
  applied to your file.
  
  3. In the output file `file-knitr.Rnw` ensure that right below `\begin{document}` you has
  
  ```
  <<include=FALSE, echo=FALSE>>
  opts_chunk$set(key1=value1, key2=value2,...,keyn=valuen)
  @
  ```
  Now the default options for the `R` code blocks (or chunks) can be those that the library `knitr` understands, more than those which `Sweave` allows.
  
  4. Open this file with RStudio. Open `Tools > Global Options > Sweave` and choose the option `Weave Rnw files using: knitr` (at least with `RStudio Version 1.1.463` with `Windows 10`). Then, in the main window of RStudio execute `Compile PDF`.
  5. Among the output files is the `pdf`, but also the intermediate `TeX` file, which one can customize, including `R` code colours, before applying to it `pdflatex`.

The other file in this repository is a `LaTeX` template with the essential `TeX` output of this process, with some explanatory comments added.
   
