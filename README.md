Download Link: https://assignmentchef.com/product/solved-phy224-lab2-introduction-to-fitting-methods
<br>
Introduction to fitting methods

<strong>Ohm’s law</strong>

The function curve_fit() is introduced for fitting linear data. You will perform voltage and current measurements on a resistor to find the resistance via Ohm’s law.

This lab contains explicit questions for you to answer labelled with <strong>Q</strong>. However, you still need to maintain a notebook for the lab, make plots and write Python code.

<h1>Background knowledge for exercise 2</h1>

<strong>Python </strong>arrays, numpy, pyplot, scipy, curve_fit()

<strong>Error Analysis </strong>Chi squared (<em>χ</em><sup>2</sup>), goodness of fit <strong>Physics </strong>Ohm’s law. Review this from your first year text.

<h1>1           Introduction</h1>

In this exercise, we will introduce how to <em>fit </em>experimental data to a certain function, and get <em>quantitative </em>observations from experiment.

The package “Notes on Error Analysis” can be found at <a href="http://www.physics.utoronto.ca/~phy225h/web-pages/Notes_Error.pdf">http://www.physics.utoronto.ca/</a><a href="http://www.physics.utoronto.ca/~phy225h/web-pages/Notes_Error.pdf">~</a><a href="http://www.physics.utoronto.ca/~phy225h/web-pages/Notes_Error.pdf">phy225h/ </a><a href="http://www.physics.utoronto.ca/~phy225h/web-pages/Notes_Error.pdf">web-pages/Notes_Error.pdf</a><a href="http://www.physics.utoronto.ca/~phy225h/web-pages/Notes_Error.pdf">.</a> It introduces linear and non-linear regression methods, aimed at finding the values of parameters which give the closest agreement between the data and the theoretical model. You should read the section on least-squares fitting.

Suppose our data consisted of <em>N </em>measurements (<em>y<sub>i</sub>,x<sub>i</sub></em>) with <em>i </em>= 1<em>,</em>2<em>,…,N</em>. A first step is to plot the data with error bars representing the reading error (or the standard deviation <em>σ<sub>i</sub></em>) on each point. This gives a visual check for what relation our data has.

Next, assume we know a <em>fitting function </em>which is close to the experimental data. The function depends on unknown parameters, <em>p</em><sub>1</sub><em>,p</em><sub>2</sub><em>,…</em>. We shall calculate the parameters <em>p<sub>i </sub></em>so that the function ˜<em>y</em>(<em>x<sub>i</sub></em>) would be in closest agreement with (<em>y<sub>i</sub>,x<sub>i</sub></em>). Note that ˜<em>y </em>is probably not the <em>true </em>value of the relation, but rather the <em>best </em>value we can determine from the data.

The least-squares method is a <em>maximum likelihood </em>estimation using the minimization of chi-squared,

<em> .                                                                           </em>(1)

The function <em>y</em>(<em>x<sub>i</sub></em>) that minimizes <em>χ</em><sup>2 </sup>is the curve of best fit.

In this exercise, we whall look at a <em>linear fitting method</em>, which uses the fitting function <em>y</em>(<em>x</em>) = <em>ax </em>+ <em>b</em>, where <em>a </em>and <em>b </em>are model parameters to be determined.

We shall not attempt a complete analysis of the goodness of the fit. This will be done in exercise 3.

<h1>2           Curve fitting in Python</h1>

The scipy package in Python contains functions for performing a least-squares curve fit. We will use the curve_fit() function from the scipy.optimize module.

The inputs/arguments to curve_fit() are: the model function, <em>x </em>data, <em>y </em>data, and an initial guess at the model parameters. The reading errors <em>σ<sub>i </sub></em>can also be included. In linear fitting, the model function is <em>f</em>(<em>x</em>;<em>a,b</em>) = <em>ax </em>+ <em>b</em>, which can be defined in Python as,

<table width="568">

 <tbody>

  <tr>

   <td width="568">def model_function(x, a, b):return a*x + b</td>

  </tr>

 </tbody>

</table>

Note that the dependent variable x must be the first argument.

The return values are the optimal parameter values, and the covariance matrix for those parameters. Given xdata and ydata, the full call for a linear fit to find the parameters would be,

<table width="568">

 <tbody>

  <tr>

   <td width="568">def model_function(x, a, b):return a*x + bp_opt, p_cov = curve_fit(model_function, xdata, ydata, (1, 0), sigmadata, True)</td>

  </tr>

 </tbody>

</table>

The slope of the line of best fit is p_opt[0]. Passing the value True instructs curve_fit() to use the absolute magnitudes of sigma to calculate covariance; the value p_opt is unaffected by it.

There are many keyword arguments to curve_fit(), which can be found in the <a href="https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve_fit.html">documentation</a><a href="https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve_fit.html">.</a> Commonly, you may use maxfev to control the maximum number of function calls. The default value is 200.

<h1>3           The experiment</h1>

We will be testing Ohm’s Law – the linear relation between voltage and current in electrical circuits. The voltage is our independent variable, current is the dependent variable, and resistance is the parameter we’d like to measure. There are two parts to the experiment: testing a known resistor, and testing a potentiometer.

<h2>3.1         Uncertainty from multimeters</h2>

Our later analysis requires an idea of the uncertainty in the measurements. Digital multimeters have two types of uncertainty:

<strong>Error of accuracy </strong>which depends on function (DCV, ACV, DCA, ACA and Ohm ()). This error is provided by the instrument manufacturer. This error is expressed as a percentage of the reading. Please check the link below for complete instrument specifications. The reading can be done on different scales of the same function, which changes the number of digits on display and also the error of accuracy.

<strong>Error of precision </strong>which is due to fluctuations at the level of the last digit. Take one digit (with position on the last digit and value 1) to be the error of precision.

<strong>The uncertainty is taken to be the largest of the two errors above.</strong>

For example, using a multimeter with an error of accuracy of 3%, you read 2.06 mA of the instrument.

Error of accuracy is 3% of reading:

2<em>.</em>06mA × 0<em>.</em>03 = 0<em>.</em>06mA

Error of precision is 0.01 (fluctuations in the last digit). Therefore, by choosing the largest of the two errors, we state that the uncertainty in reading 2.06mA is 0.06mA. The instrument specifications for the multimeter youll use can be found at <a href="http://www.upscale.utoronto.ca/specs/tegam130a.html">http://www.upscale.utoronto.ca/specs/tegam130a.html</a>

Be sure to track the uncertainty in measurements from the multimeter. Also, keep in mind that there are other sources of uncertainty that are harder to measure, like the quality of electrical connections.

<h2>3.2         The experiment</h2>

You will be provided with two multimeters, a board with electrical components (see Figure 1), and enough wires to connect everything. Choose one resistor, and one potentiometer for the experiment.

Figure 1: The electrical components board.

For the known resistor, perform the following.

<ol>

 <li>Connect the ameter, voltmeter, and power supply to the resistor (Figure 2). <em>Ask the TA if you’re in doubt</em></li>

 <li>Vary the voltage on the power supply.</li>

 <li>Record the voltage and current from the multimeters, along with uncertainty.</li>

 <li>Change the voltage, and record the new values – repeat.</li>

 <li>Save the data on a memory stick as a text file (extension .txt) with the data in two columns: the first column being the independent variable (voltage).</li>

 <li>After performing all the above measurements, disconnect the power, and switch the voltmeter to resistance. This will give you a reference value to compare against.</li>

</ol>

Repeat these measurements for the potentiometer, making sure not to move the dial between measurements.

<strong>Resistors are marked with coloured bars to indicate their nominal resistance through a code (there are many calculators for this online). As part of this exercise, you may also compare your results against the nominal resistance </strong>± <strong>the tolerance.</strong>

<h1>4           Analyzing the data</h1>

We will analyze the dependency of the current on the voltage using a linear fitting program. Ohm’s law for resistors sates

(2)

Thus, the resistance of a linear component can be determined by plotting <em>I </em>vs. <em>V </em>, and measuring the slope.

There are other electrical components that have nonlinear voltage-current relations, like diodes, transistors, and amplifiers. Using a linear model for these would result in a bad fit. In a later exercise, we will perform a nonlinear regression with a lightbulb.

<h1>5           Build a linear fitting program</h1>

Linear fitting is done via the Levenberg-Marquedt algorithm (an advanced least-squares method), as implemented in the scipy.optimize module. Today, you will use the curve_fit() function (i.e. scipy.optimize.curve_fit). Calculation of the statistics from the ouput of curve_fit() will be done in the next exercise.

Here is the outline of the Python program for Exercise 2a:

<ul>

 <li>import the necessary modules and functions (e.g. numpy and curve_fit())</li>

 <li>Read the data file into an array with the loadtxt()</li>

 <li>Extract the variables from the array columns.</li>

 <li>Define the model function <em>f</em>(<em>x</em>) = <em>ax </em>+ <em>b</em>.</li>

 <li>Call curve_fit() with the function, data, and initial guess for the parameters.</li>

 <li>Output the calculated parameters.</li>

 <li>Create relevant plots.</li>

</ul>

Write a program to perform a linear fit for the data you collected in Section 3. It should create a plot of current vs. voltage with errorbars and the line of best fit, and output the calculated value of resistance (the slope of the line of best fit). Run this program using the data for the resistor, and again using the data for the potentiometer.

<strong>Q1 </strong>In Ohm’s law, <em>V </em>= <em>IR</em>, the line should pass through <em>I </em>= <em>V </em>= 0. Did your linear fit pass through zero as well? If it didn’t, why do you think that happened?

<strong>Q2 </strong>What result do you find for resistance if you force the line to pass through zero? (i.e. try the model function <em>f</em>(<em>x,a</em>) = <em>ax</em>)

<strong>Q3 </strong>How does your resistance from using curve_fit() compare to the value measured with the multimeter?

<h1>6           Goodness of fit – reduced chi-squared</h1>

Recall that the <em>χ</em><sup>2 </sup>distribution gives a measure of how unlikely a measurement is. The more a model deviates from the measurements, the higher the value of <em>χ</em><sup>2</sup>. But if <em>χ</em><sup>2 </sup>is too small, it’s also an indication of a problem: usually that there weren’t enough samples.

This best (most likely) value of <em>χ</em><sup>2 </sup>depends on the number of degrees of freedom of the data, <em>ν </em>= <em>N </em>−<em>n</em>, where <em>N </em>is the number of observations and <em>n </em>is the number of parameters. This dependence is removed with the <em>reduced chi-squared </em>distribution,

<em> ,                                                                        </em>(3)

where <em>y<sub>i </sub></em>is the <em>dependent </em>data you measured, <em>x<sub>i </sub></em>is the <em>independent </em>data, <em>σ<sub>i </sub></em>is the measurement error in the <em>dependent </em>data.

For <em>χ</em><sup>2</sup><sub>red</sub>, the best value is 1:

indicates that the model is a poor fit;

indicates an incomplete fit or underestimated error variance;  indicates an over-fit model (not enough data, or the model somehow is fitting the noise).

<strong>Q4 </strong>Add a function to your program to calculate . What values were computed? How would you interpret your results?