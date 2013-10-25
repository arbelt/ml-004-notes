<div id="table-of-contents">
<h2>
Table of Contents
</h2>
<div id="text-table-of-contents">
<ul>
<li>
<a href="#sec-1">1. Basic operations</a>
</li>
<li>
<a href="#sec-2">2. Moving data around</a>
</li>
<li>
<a href="#sec-3">3. Computing on data</a>
</li>
<li>
<a href="#sec-4">4. Plotting data</a>
</li>
<li>
<a href="#sec-5">5. Control statements and functions</a>
</li>
<li>
<a href="#sec-6">6. Vectorization</a>
</li>
</ul>
</div>
</div>
Basic operations
================

    1 == 2                                  % false
    1 ~= 2                                  % true
    1 && 0                                  % AND
    1 || 0                                  % OR

    a = 3                                   % Assignment
    a = 3;                                  % Assignment suppresses output
    a = pi;
    disp(a);
    disp(sprintf('2 decimals: %0.2f', a))   % 2 decimal places
    disp(sprintf('2 decimals: %0.6f', a))   % 6 decimal places
    format long                             % show more decimal places
    format short                            % show fewer

                                            % Matrices
    A = [1 2;
         3 4;
         5 6]

    v = [1 2 3]                             % Row vector
    v = [1;
         2;
         3]                                 % Column vector

    v = 1:0.1:2
    v = 1:6

                                            % Other ways to generate
    w = ones(2,3)                           % 2x3 matrix of ones
    w = zeros(1,3)                          % 1x3 matrix of zeros
    w = rand(1,3)                           % 1x3 matrix of uniform random variables on [0,1]
    w = randn(1,3)                          % standard normal random variables
    w = -6 + sqrt(10)*(randn(1,10000))
    hist(w)                                 % histogram of w
    hist(w, 50)                             % hist with 50 bins
    eye(4)                                  % identity matrix
    help eye                                % brings up help for function eye

Moving data around
==================

    A = [1 2;
         3 4;
         5 6]
    size(A) % returns 2-element matrix of dimensions
    size(A,1) % number rows
    v = [1 2 3 4]
    length(A) % gives longest dim, usually only vectors

    %% Loading data

    pwd % present working directory
    cd % change directory
    ls % list files in current dir

    %% Suppose we have files 'featuresX.dat' and 'priceY.dat'

    load('featuresX.dat') % single quotes for strings
    load('priceY.dat')

    who % shows variables in memory
    % contains featuresX and priceY

    whos % gives detailed view with size, bytes, class

    clear featuresX % removes variable

    v = priceY(1:10) % sets v to 1st 10 elements
    save hello.mat v; % saves v to 'hello.mat'

    clear % clears all variables

    save hello.txt v -ascii % saves as human-readable

    A(3,2) % accesses 3rd row, 2nd column
    A(2,:) % all elements in 2nd row
    A(:,2) % all elements in 2nd column

    A([1 3],:) % everything from rows 1 and 3

    A(:,2) = [10;
              11;
              12] % Assigns 2nd column of A
    A = [A, [100;
             101;
             102]] % Appends column vector

    A(:) % put all elements of A into a single vector

    A = [1 2;
         3 4;
         5 6]
    B = [11 12;
         13 14;
         15 16]

    C = [A B] % puts together horizontally
    C = [A;
         B] % stacks A and B

Computing on data
=================

    A = [1 2;
         3 4;
         5 6]
    B = [11 12;
         13 14;
         15 16]
    C = [1 1;
         2 2]

    A*C                             % matrix mult
    A .* B                          % element-wise multiplication
    A .^ 2                          % element-wise squaring

    v = [1;
         2;
         3]

    1 ./ v                          % element-wise inverse
    log(v)                          % element-wise log
    exp(v)                          % element-wise exponentiation
    abs(x)
    -v

    v + ones(length(v), 1)          % increment all values
    v + 1                           % same thing

    A'                              % transpose of A
    (A')'                           % gives A back
    a = [1 15 2 0.5]
    max(a)                          % max of a
    [val, ind] = max(a)             % vals and indices of max
    max(A)                          % column-wise max
    a < 3                           % element-wise comparison
    A = magic(3)                    % 3x3 magic squares
    [r,c] = find(A >= 7)            % finds elements of A satisfying condition
    sum(a)                          % sum of elements of a
    prod(a)
    floor(a)                        % rounding
    ceil(a)

    max(rand(3), rand(3))           % element-wise max
    max(A,[],1)                     % column-wise max (default)
    max(A,[],2)                     % per-row max
    max(max(A))                     % largest in A
    max(A(:))                       % same

    A = magic(9)
    sum(A,1)                        % sums columns
    sum(A,2)                        % sums columns
    sum(sum(A .* eye(9)))           % sums main diag
    sum(sum(A .* flipud(eye(9))))   % sums opposite diagonal

    A = magic(3)
    temp = pinv(A)                  % pseudo-inverse A
    temp * A                        % gives back identity

Plotting data
=============

    t = [0:0.01:0.98];
    y1 = sin(2*pi*4*t);
    plot(t,y1);
    y2 = cos(2*pi*4*t);
    plot(t,y2);
    plot(t,y1);
    hold on;                                % plots new figures on old ones
    plot(t, y2, 'r');                       % add plot in red color
    xlabel('time')
    ylabel('value')
    legend('sin', 'cos')
    title('my plot')
    print -dpng 'myPlot.png'                % saves the plot
    close                                   % disappears existing figure
    figure(1);
    plot(t, y1);
    figure(2);
    plot(t, y2);                            % produces 2 figures
    subplot(1,2,1)                          % divides plot into 1x2 grid, access first element
    plot(t, y1);
    subplot(1,2,2);
    plot(t, y2);
    axis([0.5 1 -1 1])                      % sets axis limits

    clf;                                    % clears figure
    A = magic(5);
    imagesc(A);                             % shows matrix as colors
    imagesc(A), colorbar, colormap gray;    % adds colorbar and sets grays
    imagesc(magic(15)), colorbar, colormap gray;

    a=1, b=2, c=3                           % chains commands; "comma-chaining"

Control statements and functions
================================

    v = zeros(10,1)
    for i = 1:10,
      v(i) = 2^i;
    end;
    v

    indices=1:10;
    for i = indices,
      disp(i);
    end;

    i = 1;
    while i <= 5,
      v(i) = 100;
      i = 1+1;
    end;

    i = 1;
    while true,
      v(i) = 999;
      i = i+1;
      if i == 6,
        break;
      end;
    end;

    v(1) = 2;

    if v(1)==1,
      disp('The value is one');
    elseif v(1) == 2,
      disp('The value is two');
    else
      disp('The value is not one or two');
    end;

Defining functions.

Octave uses files with `.m` extension

    function y = squareThisNumber(x)
      % will return one var y, is a function of one var x

      y = x^2;

Search path

    addpath('/path/to/functions') % adds dir to search path

Multiple return values:

    function [y1, y2] = squareAndCubeThisNumber(x)
      y1 = x^2;
      y2 = x^3;

Octave function to compute cost function

    X = [1 1;
         1 2;
         1 3];
    y = [1;
         2;
         3]

    theta=[0;
           1];

    j = costFunctionJ(x,y,theta)

    function J = costFunctionJ(X, y, theta)

             % X is design matrix
             % y is class labels

      m = size(X,1); % number training examples
      predictions = X*theta; % predictions on examples given theta

      sqrErrors = (predictions-y).^2;
      J = 1/(2*m) * sum(sqrErrors);

Vectorization
=============

Do things with nice linear algebra libraries – it goes faster, and is easier.

-   Don't write loops, use functions that work on vectors

-   For instance, dot product better than looping and summing

Example in C++

    double prediction = theta.transpose() * x;

Gradient descent example

    delta = (1/m) *  X' * ( h(X) - y )
    theta = theta - alpha * delta
