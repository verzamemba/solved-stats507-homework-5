Download Link: https://assignmentchef.com/product/solved-stats507-homework-5
<br>
<h1>1         Warmup: Around the Semicircular Law</h1>

The (comparatively) young field of random matrix theory (RMT) concerns the behavior of certain matrices with independent random entries. A landmark result in RMT concerns the behavior of the eigenvalues of a random symmetric matrix with normal entries. Under the proper scaling, the joint distribution of the eigenvalues of such a matrix follows the

<em>Wigner semicircular distribution</em>, which has density

√

( <u>4</u><sup>2</sup><u>−</u><em><sup>π</sup></em><em><u>x</u></em>2                      if − 2 ≤ <em>x </em>≤ 2                                        (1)

<em>f</em>(<em>x</em>) =

0               otherwise.

That is, a symmetric matrix with random normal entries will have eigenvalues whose histogram looks more and more like a semicircle of radius 2 as <em>n </em>increases to ∞. In particular, define a matrix-valued random variable <em>Z </em>∈ R<em><sup>n</sup></em><sup>×<em>n </em></sup>by generating <em>Z<sub>i,j </sub></em>i.i.d. normal with mean 0 and variance 1<em>/n </em>for all 1 ≤ <em>i </em>≤ <em>j </em>≤ <em>n</em>, and set <em>Z<sub>j,i </sub></em>= <em>Z<sub>i,j </sub></em>for 1 ≤ <em>j </em>≤ <em>i </em>≤ <em>n</em>. Then the matrix <em>Z </em>∈R<em><sup>n</sup></em><sup>×<em>n </em></sup>is called a <em>Wigner matrix</em>.

<ol>

 <li>Define a function wigner_density that takes a single number (integer or float) as its input and returns a float as its output, given by the value of the semicircular density evaluated at the input. That is, for a number x, wigner_density(x) should return <em>f</em>(<em>x</em>), where <em>f </em>is defined above in Equation (1). You do not need to perform any error checking in this function, but note that your function should operate equally well on Python ints/floats and on numpy ints/floats, and you should be able to accomplish this without checking the type of the input. Use the sqrt function for the square root, <em>not </em>the Python math.sqrt function.</li>

 <li>Define a function generate_wigner that takes a single positive integer n as its argument and returns a random <em>n</em>-by-<em>n </em>Wigner matrix. Your function should raise an appropriate error in the event that the input is not an integer or if it is not positive. The output of your function may be either a numpy matrix or simply a numpy I would slightly recommend the former, for ease of use in the next subproblem. You can cast a 2-dimensional numpy array a to a matrix by writing np.matrix(a). <strong>Hint: </strong>depending on the solution you choose, you may find the numpy.triu and numpy.tril functions to be useful. A different solution makes use of the scipy.spatial.distance.squareform function.</li>

 <li>The RMT result referenced above states that the joint distribution of the eigenvalues of a random Wigner matrix converges to the semicircular law. Write a function get_spectrum that takes a numpy matrix or 2-dimensional numpy array and returns a numpy array of its eigenvalues in non-decreasing order. You do not need to perform any error checking for this function. You fill find the following documentation useful: <a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.linalg.eigh.html#numpy.linalg.eigh">https://docs.scipy.org/doc/numpy/reference/generated/numpy. </a><a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.linalg.eigh.html#numpy.linalg.eigh">eigh.html#numpy.linalg.eigh</a><a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.linalg.eigh.html#numpy.linalg.eigh">.</a></li>

 <li>Create a plot with four subplots, arranged vertically, each showing a (normalized) histogram, in blue, of the eigenvalues of a random <em>n</em>-by-<em>n </em>Wigner matrix for <em>n </em>= 100<em>,</em>200<em>,</em>500 and 1000. In each subplot, overlay a red curve indicating the density of the semicircular law, as defined in (1). <strong>Hint: </strong>depending on how you implemented wigner_density above, you may find the vectorize function helpful.</li>

</ol>

How big does <em>n </em>have to be before the semicircular law appears to be a good fit? Of course, in practice, we would answer this question more rigorously with, for example, a Kolmogorov-Smirnov test, which you can find in the scipy.stats module, but that is entirely optional. <strong>Note: </strong>this experiment involves some matrix eigenvalue computations, which are comparatively expensive. If you set <em>n </em>larger than about 5000, be prepared to wait a few minutes for your answer, especially if you are running on a laptop.

<h1>2         Plotting a Mixture of Normals</h1>

The whole reason that we use plotting software is to visualize the data that we are working with, so let’s do that. The zip file located at <a href="http://www-personal.umich.edu/~klevin/teaching/Winter2019/STATS507/hw5_files.zip">www-personal.umich.edu/</a><a href="http://www-personal.umich.edu/~klevin/teaching/Winter2019/STATS507/hw5_files.zip">~</a><a href="http://www-personal.umich.edu/~klevin/teaching/Winter2019/STATS507/hw5_files.zip">klevin/ </a><a href="http://www-personal.umich.edu/~klevin/teaching/Winter2019/STATS507/hw5_files.zip">teaching/Winter2019/STATS507/hw5_files.zip</a> contains two files, storing data from an experiment in my own research. The file points.dlm is a tab-delimited file (.dlm stands for “delimited”). Such a format is common when writing reasonably small files, and is useful if you expect to use a data set across different programs or platforms. See the documentation for the command numpy.loadtxt to see how to read this file. The file labels.npy is a numpy binary file, representing a numpy object. The .npy file format is specific to numpy. Many languages (e.g., R and MATLAB) have their own such languagespecific file formats for saving variables, workspaces, etc. These formats tend to be more space-efficient, typically at the cost of program-dependence. It is best to avoid such files if you expect to deal with the same data set in several different environments (e.g., you run experiments in MATLAB and do your statistical analysis in R). .npy files are opened using numpy.load.

The observations in my experiment were generated from a distribution that is <em>approximately </em>normal, but not precisely so. Let’s explore how well the normal approximation holds.

<ol>

 <li>Download the .zip file, extract it, and read the two files into numpy. Please include both npy and points.dlm in your final submission. The former of these should yield a numpy array of 0s and 1s, and the latter should yield a 100-by-2 numpy array, in which each row corresponds to a 2-dimensional point. The <em>i</em>-th entry of the array in labels.npy corresponds to the cluster membership label of the <em>i</em>-th row of the matrix stored in points.dlm.</li>

 <li>Generate a scatter plot of the data. Each data point should appear as an x (often called a <em>cross </em>in data visualization packages), colored according to its cluster membership as given by npy. The points with cluster label 0 should be colored blue, and those with cluster label 1 should be colored red. Set the x and y axes to both range from 0 to 1. Adjust the size of the point markers to what you believe to be reasonable (i.e., aesthetically pleasing, visible, etc).</li>

 <li>Theoretically, the data should approximate a mixture of normals with means andcovariance matrices given by</li>

</ol>

<em>.</em>

For each of these two normal distributions, add two contour lines corresponding to 1 and 2 “standard deviations” of the distribution. We will take the 1-standard deviation contour to be the level set (which is an ellipse) of the normal distribution that encloses probability mass 0.68 of the distribution, and the 2-standard deviation contour to be the level set that encloses probability mass 0.95 of the distribution. The contour lines for cluster 0 should be colored blue, and the lines for cluster 1 should be colored red. The contour lines will go off the edge of the 1-by-1 square that we have plotted. Do not worry about that. <strong>Hint: </strong>these ellipses are really just confidence regions given by

<em>,</em>

where <em>p </em>is a probability and <em>χ</em><sup>2</sup><em><sub>d </sub></em>is the quantile function for the <em>χ</em><sup>2 </sup>distribution with <em>d </em>degrees of freedom. <strong>Hint: </strong>use the optional argument levels for the pyplot.contour function.

<ol start="4">

 <li>Do the data appear normal? There should be at least one obvious outlier. Add an annotation to your figure indicating one or more such outlier(s).</li>

</ol>

<h1>3         Conway’s Game of Life</h1>

Conway’s Game of Life (<a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life">https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life</a><a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life">) </a>is a classic example of a <em>cellular automaton </em>devised by mathematician John Conway. The game is a classic example of how simple rules can give rise to complex behavior. The game is played on an <em>m</em>-by-<em>n </em>board, which we will represent as an <em>m</em>-by-<em>n </em>matrix. The game proceeds in steps. At any given time, each cell of the board (i.e., entry of our matrix), is either alive (which we will represent as a 1) or dead (which we will represent as a 0). At each step, the board evolves according to a few simple rules:

<ul>

 <li>A live cell with fewer than two live neighbors becomes a dead cell.</li>

 <li>A live cell with more than three live neighbors becomes a dead cell.</li>

 <li>A live cell with two or three live neighbors remains alive.</li>

 <li>A dead cell with <em>exactly </em>three live neighbors becomes alive.</li>

 <li>All other dead cells remain dead.</li>

</ul>

The neighbors of a cell are the 8 cells adjacent to it, i.e., left, right, above, below, upperleft, lower-left, upper-right and lower-right. We will follow the convention that the board is <em>toroidal</em>, so that using matrix-like notation (i.e., the cell (0<em>,</em>0) is in the upper-left of the board and the first coordinate specifies a row), the upper neighbor of the cell (0<em>,</em>0) is (<em>m </em>− 1<em>,</em>0), the right neighbor of the cell (<em>m </em>− 1<em>,n </em>− 1) is (<em>m </em>− 1<em>,</em>0), etc. That is, the board “wraps around”. <strong>Note: </strong>you are not required to use this matrix-like indexing. It’s just what I chose to use to explain the toroidal property.

<ol>

 <li>Write a function is_valid_board that takes an <em>m</em>-by-<em>n </em>numpy array (i.e., an ndarray) as its only argument and returns a Python Boolean that is True if and only if the argument is a valid representation of a Game of Life board. A valid board is any two-dimensional numpy ndarray with all entries either 0.0 and 1.0.</li>

 <li>Write a function called gol_step that takes an <em>m</em>-by-<em>n </em>numpy array as its argument and returns another numpy array of the same size (i.e., also <em>m</em>-by-<em>n</em>), corresponding to the board at the next step of the game. Your function should perform error checking to ensure that the provided argument is a valid Game of Life board.</li>

 <li>Write a function called draw_gol_board that takes an <em>m</em>-by-<em>n </em>numpy array (i.e., an ndarray) as its only argument and draws the board as an <em>m</em>-by-<em>n </em>set of tiles, colored black or white correspond to whether the corresponding cell is alive or dead, respectively. Your plot should <em>not </em>have any grid lines, nor should it have any axis labels or axis ticks. <strong>Hint: </strong>see the functions xticks() and plt.yticks() for changing axis ticks. <strong>Hint: </strong>you may find the function plt.get_cmap to be useful for working with the matplotlibColormap objects.</li>

 <li>Create a 20-by-20 numpy array corresponding to a Game of Life board in which allcells are dead, with the exception that the top-left 5-by-5 section of the board looks like this:</li>

</ol>

Plot this 20-by-20 board using draw_gol_board.

<ol start="5">

 <li>Generate a plot with 5 subplots, arranged in a 5-by-1 grid, showing the first fivesteps of the Game of Life when started with the board you just created, with the steps ordered from top to bottom, The figure in the 5-by-5 sub-board above is called a <em>glider</em>, and it is interesting in that, as you can see from your plot, it seems to move along the board as you run the game.</li>

</ol>

<strong>Optional additional exercise: </strong>create a function that takes two arguments, a Game of Life board and a number of steps, and generates an animation of the game as it runs for the given number of steps.