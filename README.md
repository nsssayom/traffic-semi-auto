\documentclass[runningheads]{llncs}
\usepackage{graphicx}
\usepackage{enumitem}
\usepackage{siunitx}


\setlist[description]{leftmargin=\parindent,labelindent=\parindent}
\\begin{document}
\title{Traffic Light Control Assistance for an Isolated Intersection in Dhaka City}
\author{Nazmus Shakib Sayom\orcidID{0000-0002-6339-388X}}
\authorrunning{N. S. Sayom}
\institute{American International University-Bangladesh, Dhaka, Bangladesh 
    \email{nsssayom@gmail.com}\\}
\maketitle
\begin{abstract}
Inefficient traffic light control in intersections is the main obstacle to ensure maximum utilization 
of traffic infrastructures. Ill-thought infrastructure design has ceased the possibility of an
fully-automated system to succeed in  regulating traffic flow in intersections. This paper studies 
the practicality and implementation of a real-time adaptive traffic control assistance system, 
that acquires data from Google Maps API and calculates the optimal green light time for each entry 
roads of an intersection to minimize average waiting time using an algorithm derived from network 
flow model. Responsible person will use a handheld device to get the suggestion from the server 
using RESTful Web API.

\keywords{Isolated Traffic Intersections  \and Traffic Control Assistance \and Optimal Traffic Control.}
\end{abstract}
\section{Introduction}
According to the habitants, traffic congestion is a severe , if not the
most severe problem in Dhaka's urban
life\cite{BRACInstituteofGovernanceandDevelopment2016}. RSTP, 2015 says
that average daily speed of traffic is 6.8 kmph in Dhaka which is
slightly above average walking
speed\\cite{AlmecCorporationGlobalOrientalConsultantsInternationalKatahira&Engineers2015}.
A 2017 press release by World Bank blamed the infamous traffic
congestion of killing 3.2 million working hours a
day\cite{WorldBank2017}. It also has horrendous economic consequences.
RSTP for Dhaka estimated the cost to be 11.4 Billion USD on the
2014\\cite{AlmecCorporationGlobalOrientalConsultantsInternationalKatahira&Engineers2015}.

Different methodologies can be applied to tackle the traffic congestion
problem. Bart De Schutter and B De Moor pointed out four specific
methods\cite{DeSchutter1998}:
\begin{description}
    \item [$\bullet$] Construction of new infrastructures, i.e., roads, flyovers, etc.
    \item [$\bullet$] Promoting public transports.
    \item [$\bullet$] Reducing demand by introducing taxes and tolls for using specific infrastructure.
    \item [$\bullet$] Ensuring optimized usage of existing resources.
\end{description}
The first three strategies are only useful when the fourth is present.
if the optimal usage of resources can not be ensured, adding new
resource can not assure the solution to the problem rather than creating
a bottleneck in the overall system.

The amount of car on the road is the main key factor of traffic
congestion in Dhaka city. And According to Bangladesh Road Transport
Authority (BRTA) data, until April 2018, there were 11,15,654 vehicles
in Dhaka City in total\cite{BRTA2018}. A study by Mahmudul and Haque
shows there are only 5% primary roads in Bangladesh\cite{Mahmud2008}.
So, our traffic intersections need to regulate a quite larger number of
vehicles than those were originally designed for. And thus a real-time
adaptive traffic control assistance system is required in this city.

The government tried introducing fixed-time based automated traffic
light controlling systems back in 2015 but, that caused massive traffic
congestion in the city\cite{Niloy2015}. The fixed-time control system
does not consider the present traffic situation. So, in these scenarios,
an real-time adaptive system can analyze the traffic and take
near-optimal decisions\cite{Shelby2004}. But, due to ill-thought road
design and socio-political aspects, fully automated systems will have a
lower success rate.

This paper proposes a system which is real-time adaptive and also will
require human involvement. The proposed system uses Google Maps traffic
data for its real-time analysis. Using an efficient and comparatively
simple implementation the near-optimal solution is obtained which is
passed on to a handheld device of the responsible person to provide a
suggestion about the optimal green light duration for each entry roads
of an intersection. This duration is calculated to minimize the average
waiting time for each vehicles using mathematical models derived by S.
Lämmer et al. \cite{Lammer2008a,Lammer2008} This system also logs its
findings in a database server for future use.

\section{Algorithm for Optimal Green Light Time}
As a non-equilibrium system, traffic intersection has been studied
extensively over time from various perspective. Originally being an
NP-hard problem, it is not possible to achieve an absolute solution. A
near-optimal solution can be obtained to a certain accuracy depending on
the algorithm. Webster in 1958 for the first time investigate the
conditions for a single traffic intersection\cite{F.V.Webster1958}.
Björck and Omstedt conducted a comparative study on the algorithms used
in traffic systems\cite{Bjorck2018}. Their study concluded that a
different algorithm is fitted for different scenarios in a traffic
intersection. S. Lämmer et al. used the network flow model to calculate
the optimal green time for each entry roads in an intersection to
minimize average waiting time\cite{Lammer2008}. In another paper by S.
Lämmer et al. derived an equation for green times of each entry roads of
an intersection\cite{Lammer2008a}:

\begin{equation}
    \hat{n}(t) \propto \hat{g}(t)q^{max}
\end{equation}

Here, \begin{math}\hat{n}(t)\end{math} represents the total number of
vehicles in a road section, \begin{math}\hat{g}(t)\end{math} is the
green time for a road section, \begin{math}\ q^{max}\end{math}
represents the capacity, i.e., the maximum number of vehicles the road
section can accommodate when saturated

from this equation green time \begin{math}\hat{g}_{i}(t)\end{math} of
any entry road \begin{math}i\end{math} can be derived:

\begin{equation}
    \hat{g}_{i}(t) = \frac{\hat{n}_{i}(t)}{\hat{q}_{i}^{max}}\alpha
\end{equation} Here, $\alpha$ is a constant and its value will vary
depending on intersection width, length, average vehicle dimension and
speed limit of the road.

\section{Implementation}
\subsection{Scenario}
For this study, SAARC Fountain intersection (N \ang{23.8191441}, E
\ang{90.4525954}) was chosen because of its homogenous and
near-saturated traffic flow. This intersection has 5 entry roads. The
road section length has been set to 500 meter.

\subsection{System Structure}
\begin{figure}
    \includegraphics[width=\textwidth]{traffic.png}
    \caption{Graphical representation of data for the proposed system.} \label{fig1}
    \end{figure}
\subsubsection{Handheld Device}
This can be any mobile device that supports a web browser, e.g.,
Android, iOS or KaiOS phones. A native or web application
chronologically sends request to server using RESTful API and receives
JSON response with near-optimal green time for each entry points of the
intersection.

\subsubsection{Application Server}
Application server hosts the RESTful API endpoints. On arrival of the
requests from the client, this server runs its
\textbf{headless browser module} that returns the screenshot of the
intersection with the traffic data layer from Google Maps JS API. The
application server has an image processing program developed with C++
and OpenCV library that scans the screenshot image and after calculating
near-optimal solution using equation (2), it returns the optimal green
time for each entry roads in JSON format.

\subsubsection{Database Server}
Application server logs all extracted data into this database server for
future usage. Advanced Artificial Intelligences could be trained to
solve this type of problems even with more accuracy and efficiency with
these data in the future.

\section{Conclusion and Further Research}
A real-time adaptive traffic control assistance system has been studied
in this paper. Google Maps traffic data has been used here as a data
source. This system can fill the void of a semi-automatic adaptive
traffic control system that is very much needed for Dhaka city to ensure
the maximized usage of its resources.

This study was conducted in a very limited time frame and resources were
not available to conduct a simulation or field run of the proposed
system to verify its theoretical superiority, which could be part of
future studies. Q-learning can be added to this system for further
optimization of the solution. This system only focuses on an isolated
intersection. So, topics for further research also include expanding
this system for multiple adjunct intersections.

\bibliographystyle{plain}
\bibliography{traffic}
\\end{document}
