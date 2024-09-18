java c
SciComp   Project   2 
Week   3 


1 BackgroundAmong the great pioneers of computational physics was Walther Ritz, who (half a century before the digital com-   puter)   invented   a   computational   method   for   solving tough   dif-   ferential   equations   that   is   among   the   most   used   today:      the   Ritz-Galerkin-method.      Whether   solving   quantum   systems   in   Hilbert   space   or   simulating   whether   a   bridge   will   crash   in   a   storm,   his   method   usually   lies   underneath.We   will   not   look   at   that   until   later   in   the   course.      Instead,   we   will   study   the   problem   he   invented   it   for:    The   mysterious   harmonics   of Chladni   plates,   one   of the   first   and   most visually   striking   experiments   that   let   us   see   sound.Ernst   Chladni,   a   musician   and   physicist   from   18th    century   Wittenberg,   discovered   that   driving   a   metal   plate   at   different   frequencies with his violin bow sometimes caused dust to gather   into beautiful patterns.    At   most   frequencies, the   dust was just   shaken   about,   but   through   a   systematic   approach   with   sand   sprinkled   over   the   plate,   he   found   that   the   magic   happened   at   certain   frequencies,   which   he   carefully   drew   and   collected.Chladni’s   drawing   of   resonnance modes he discovered with iron   plate,   violin   bow,   and   sand. 
Already   at   Chladni’s   time,   it   was   well-understood   why   the figures   appeared:    The   special   frequencies   were resonnances,   harmonics   inherent   to   the   plate   ge-ometry   that   lead   to   standing   waves. In   the nodes    (the   regions   where   the   wave   is   zero)   the   sand   settles; everywhere else it is   pushed   around   until   finding   a   nodal   region   to   rest. But it   tookover   a   hundred   years   before   anyone   could   solve   the   equations   and   predict   the   patterns.
The thin plates are ruled by Kirchhoff’s dynamics (1850), time-evolved by the biharmonic operator

similar,   but   not   the   same   as   the   wave   equation.   The   resonnance   modes   are   the   eigenfunctions   of   the   biharmonic   operator,   and   the   resonnance   frequencies   correspond   to   the   eigenvalues:

under   free   boundary   conditions,   subject   only   to   the   plate   being   a   solid,   elastic   object:

where µ is an elasticity constant, a material property of the plate.
2 Data 
The full calculation is beyond the scope of this week: You will only need to calculate the resonnance eigenvectors and eigenvalues from a matrix representation K of the biharmonic operator, which you may download here: Chladni-Kmat.npy (Python) That is, you will simply be working with the eigenproblem: 
Kx =   λx                                                                                                                               (4)
The   matrix   representation K incorporates   also the   boundary   conditions,   so that   eigenvectors will   be   solutions   to   the   full   problem.
In   Python you   load the   matrix   as   Kmat    =    np.load("Chladni-Kmat.npy").
For testing your implementation, you can use the matrices given in Project2 examplematrices.py. Simply report the results for the highest-numbered matrix that works. 
Visualization
To show your solutions, download chladni show.py and the data file chladni basis.npy for Python.
Running chladni show defines the basis set, a 15 × 500 × 500 array of 15 basis functions each defined on a 500 × 500 grid, and the following three functions:
• show_waves(x,basis_set): Shows the actual wavefunction corresponding to coefficient vec-tor x
• show_nodes(x,basis_set代 写SciComp Project 2 Week 3Python
代做程序编程语言): Shows the wavefunction zeros, where the sand gathers.
• show_all_wavefunction_nodes(T,lambdas,basis_set): Shows the zeros of all the eigen- functions defined by the columns of T.
3 Questions for Week 3 
a.    (1) Implement   a function   centers,radii    =    gershgorin(A) that locates   the   eigenvalues   of   a   matrix   using   Gershgorin’s   theorem.    (2)   Localize   the   eigenvalues   of K,   and   report   the   disk centers   and   radii.
b.    (1)   Implement   a   function   lambda    =    rayleigh qt(A,x),   which   takes   a   matrix A and   ap-   proximate   eigenvector x,   and   returns   the   approximate   eigenvalue   λ   given   by   the   Rayleigh quotient.
(2)   Implement   a   function   x,      k      =      power   iterate(A,x0)   for   power   iteration,   which   takes   a   matrix A and   an   initial   vector x0      as   arguments,   and   returns   an   eigenvector x together   with   the   number   k   of   iterations   used.       Don’t   forget   to   choose    and   implement   a   suitable   convergence   criterion.
(3)   Test   it   by   finding   the   largest   eigenvalue   of   the   example   matrices.   Report   the   eigenvalue found, the   Rayleigh   residual   (the   residual   of   the   Raleigh   quotient   as   a   least-squares   system),   and   the   number   k   of iterations   used.
(4) What   is   the   largest   eigenvalue   of K?    Visualize   your   eigenfunction   using show waves(x,basis set) to see   the wave, and show nodes(x,basis set)   to   see   where   the   sand   will   gather.    The   eigenfunction   for   the   largest   eigen-   value   should   have   nodes   along   an   8   × 8   grid.

c.      (1)   Write a Rayleigh quotient iteration function x,      k      =      rayleigh   iterate(A,x0,      shift0),   which   takes   a   matrix A,   an   initial   vector x0   ,   and   an   approximate   eigenvalue   shift0 as   ar-guments   and   returns   an   eigenvector x together   with   the   number   k   of iterations   used. 
The   multiplication   by the   inverse   matrix   should   be   implemented   using   either your   own   LU-   factorization from   as x    =    lu solve(A,y) or   QR-factorization from   as   x    =    qr   solve(A,y). NB: If you did not get either to work   in   previous weeks,   you   can   use   an   in-built   linear   solver   and   make   a   small   note   that   you   do   this.
(2)   Test   it   with   the   example   matrices,   and   report   the   eigenvalues   found,   Rayleigh   residual,   and   the   number   k   of iterations   used.
d.      An   important   feature   of   inverse   iteration   and   Rayleigh-iteration   is   the   ability   to   calculate   any      eigenvalue      and   its   eigenvectors:      given   an   approximate   starting   point,    we   obtain   an eigenvector   to   the   nearest   eigenvalue.(1)   Why   can   you   not   get   all   the   eigenvalues   and   -vectors   with   pure   power--   iteration?    (2)   Use   your   Rayleigh   quotient   iteration   function   together   with   the   Gershgorin   centers to   calculate   as   many   eigenvectors   and   eigenvalues   of K as   you   can.   Are   you   able   to   get   all   of   them?   Why?   If   not, find   the   remain-   ingone(s) by   any   means   necessary.    Check   using   show nodes(x,basis set) that   the   eigenfunction   with   lowest   eigenvalue   looks   like   a   cross:(3)   Construct   the   transformation   matrix T whose   columns   are   the   eigenvectors   in   order   of   ascending   eigenvalues, and   check   that K = TΛT−1   with   diagonal Λ. (4) Visualize   your   solu-tions   using the provided   function   show all wavefunction nodes(T,lambdas,basis set).





         
加QQ：99515681  WX：codinghelp
