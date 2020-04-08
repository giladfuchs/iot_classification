IoT Device Recognition
Gilad Fuchs Matan Maabari
Advisor: Ph.D. Amit Dvir
September 2019
1 Abstract
The Internet of Things (IoT), also called the Internet of Everything or the
Industrial Internet, is a new technology paradigm envisioned as a global network
of machines and devices capable of interacting with each other. The IoT is
recognized as one of the most important areas of future technology and is gaining
vast attention from a wide range of industries. In addition, the rapid rise in
encrypted traffic is changing the threat landscape. As more businesses become
digital, a significant number of services and applications are using encryption
as the primary method of securing information. Encryption technology has
enabled much greater privacy and security for enterprises that use the Internet to
communicate and transact business online. Mobile, cloud and web applications
rely on well-implemented encryption mechanisms, using keys and certificates
to ensure security and trust. This project proposes the use of network traffic
analytics to characterize IoT devices, including their typical behaviour mode.
Our goal is to develop a classification method that can not only distinguish IoT
from non-IoT traffic, but also identify specific IoT devices such as types of the
companies that produce these devices, types of network stack and by classify
number of devices into certain groups. Furthermore, we will attempt to detect
attacks/problems inside the network and not inside each device, however due
to the fact that the network is encrypted we must analyze the network’s traffic
and create a machine learning system that will execute this automatically.
1
Contents
1 Abstract 1
2 Introduction 3
3 Related Work 3
4 Data-Set 4
5 Experiments 5
5.1 First experiment . . . . . . . . . . . . . . . . . . . . . . . . . . . 5
5.2 Second experiment . . . . . . . . . . . . . . . . . . . . . . . . . . 8
5.3 Third experiment . . . . . . . . . . . . . . . . . . . . . . . . . . . 10
5.4 Fourth experiment . . . . . . . . . . . . . . . . . . . . . . . . . . 13
6 SVM algorithm 13
7 Website 13
8 Conclusion 13
2
2 Introduction
There is an increasing presence of IoT devices. According to [4], in 2016, there
were more than 4.7 billion things connected to the internet. Fast-forward to
2021, the market will increase to nearly 11.6 billion IoT devices. Managing the
security of users’ IoT devices in the presence of vulnerable devices is challenging.
To accomplish this, one would need the ability to identify vulnerable devices
in order to protect other devices from potential security attacks utilizing the
vulnerable devices. Therefore, device recognition is very important. In 2016,
the world was introduced to the first “Internet of Things” malware - a strain
of malicious software that can infect connected devices such as DVRs, security
cameras, and more. Later on the malware turned the affected devices into a
botnet to facilitate a Distributed Denial of Service (DDoS) attack, which aims
to overwhelm websites with internet traffic. The attack ended up flooding one of
the largest website hosting companies in the world, bringing a variety of major,
well-known websites and services to a halt for hours. In this context, knowing
the type of device connected to the network will help to enforce security.
Device type recognition also raises privacy concerns. Once a device has been
identified, certain techniques can be used to further determine the current state
of the device. For example, if an attacker identifies a smart vacuum cleaner, he
can infer if there are people inside a house. IoT devices’ network traffic follows
a stable pattern due to the fact that they perform very specific tasks, contrary
to computers and smartphones which perform a variety of tasks. As a result,
they are well suited for Machine-Learning models.
In this project we developed a classification method that can not only distinguish IoT from non-IoT traffic, but also identify specific IoT devices, by
analyzing network traffic. We used Machine learning algorithms in order to
predict what device has generated the network traffic between 3 devices.
3 Related Work
[1] explains how data analysis techniques can be leveraged to find out specific
patterns that can help to recognize device types. Because IoT devices perform
very specific tasks, their networking behavior is very predictable. They present
a machine learning based approach in order to recognize the type of IoT devices
connected to the network by analyzing streams of packets sent and received.
Moreover, they built an experimental smart home network to generate network
traffic data and designed a model to describe IoT device network behaviors. The
data describing the network behaviors is then used to train six different machine
learning classifiers to predict the IoT devices that generated the network traffic.
Another paper [2] talks about how to analyze network traces from a testbed
of common IoT devices, and describe general methods for fingerprinting their
behavior. Then they use the information and insights derived from this data
to assess where privacy and security risks manifest themselves, as well as how
device behavior affects bandwidth. Moreover, they demonstrate simple mea3
surement that circumvent attempts at securing devices and protecting privacy.
Another paper [3] applies machine learning algorithms on network traffic
data for accurate identification of IoT devices connected to the network.In order to train and evaluate the classifier, they collected and labeled network traffic
data from nine distinct IoT devices, PCs and smartphones. Using supervised
learning, they trained a multi-stage meta classifier. In the first stage, the classifier can distinguish between traffic generated by IoT and non-IoT devices. In
the second stage, each IoT device is associated to a specific IoT device class.
The overall IoT classification accuracy of their model is 99.281%.
4 Data-Set
We created a smart home network composed of IoT devices, recorded network
traffic data and saved it into a Pcap file through Tools such as Wireshark and
Tshark. We set up a closed private network which contains a hub (which is
connected to the home Router), a computer and 3 IoT devices - a camera, a
bulb and Amazon Echo. The camera and the bulb are connected to LAN and
Amazon Echo is connected to wi-fi.
We recorded the traffic data in our private network, at different times and
with different activity for every device, and save it as a Pcap File. Then, we
filtered important data that should be analyzed, from the Pcap file to a CSV
file. We used a tool named TShark which extracted he features: (MAC source,
MAC destination, IP source, IP destination, IP length, IP protocol, time). We
generated 20 of CSV files. We used the SVM algorithm, with kernel=’sigmoid’,
and split the data for 80% train and 20% test.
After we extracted the relevant data set, we began to analyze it.
4
5 Experiments
We did 3 experiments in our project, input of every experiment was a folder
containing number of CSV files.
5.1 First experiment
We read every row of each CSV file, and append it into an array. Then we
created a dictionary (Data-structure) such that, the key was the MAC address
(from the input) and the value was a list of Objects called ’RowCsv’, that their
MAC address of the sender or receiver is the same as the key. ’RowCsv’ is an
object that simply represent the row from the CSV’s (input), containing (MAC
source, IP source, IP destination, IP length, IP protocol, time).
We created another dictionary, such that the key was the device (for instance
- Camera, Bulb or Alexa) and the value was another dictionary, such that the
key was the timestamp of period of 10 seconds that were recorded (for instance:
19:52:19 or 19:52:17 are both mapped to 19:52:10). The value was a list of
Objects called ’Sample’. A Sample contains the length of sent messages, length
of received messages, number of sent messages, number of received messages.
We calculate the average of the size of the sent and received packet. IN
addition, we count the number of sent and received packets.
S1 = PNum of packets
i=1 X(i) length of packet
S1 - Sum of the length of the Send/Receive packets.
S2 = S1/[Num of packets]
S2 - Average of the Send/Receive packets.
5
In numbers:
6
First column - Camera, Second column - Bulb, Third column - Amazon Echo :
7
5.2 Second experiment
We define N (number) and our goal is to achieve:
• The size of the first N packets sent
• The size of the first N packets received
• The N - 1 packet inter-arrival times between the first N packets sent
• The N - 1 packet inter-arrival times between the first N packets received
Our goal is to make the same experiment that we show in article [1] .
In numbers:
8
First column - Camera, Second column - Bulb, Third column - Amazon Echo :
9
We write the results into a CSV files.
5.3 Third experiment
Our goal is to combine the two previous experiments. We used the following
features: length of the N first sent packets, length of the N first received
packets, number of sent packets, number of received packets, list of distance
time for sent packets, list of distance time for received packets, last time sent
packet, last time received packet, divide length of the N first sent packets with
number of sent packets ,divide length of the N first received packets with
number of received packets. We wrote the results into a CSV file.
10
In numbers:
11
12
5.4 Fourth experiment
We did an experiment to classify if the device/component is IoT or not. After
we extracted the relevant data set, we began to analyze it, we used three
different analyst classes(the same features we had in the last three
experiments), our goal was to discover if the device/component is classified as
IoT or not by giving each set the label 0 or 1 according to it’s match.
6 SVM algorithm
A Support Vector Machine (SVM) is a universal learning machine whose
decision surface is parameterized by a set of support vectors, and by a set of
corresponding weights according to [5]. An SVM is also characterized by a
kernel function. In the SVM algorithm, we are looking to maximize the
margin between the data points and the hyperplane. In our project we
imported Pandas library to work with CSV, which will be the Data-set for the
SVM. We use ’Sigmoid’ kernel and split the data to 80% train and 20% test.
7 Website
We designed and built a new website to show our results. We used JavaScript,
HTML, CSS in order to edit, add features, and design the website. At the first
page, the user asked to enter CSV’s directory that was generated by Tshark
containing packet size, time stamp and etc. and then generate a file to the
machine according to a feature we told it, after that we send the output to
SVM algorithm and our results will contain a diagram of the precision, recall
and f1-score per IoT device.
At the second page, the user asked to enter a single CSV file and target IP
address, then does the same logic as on first page to prepare the machine for
the tests without given labels. after we send the file to the machine, and tell
which experiment to do, we receive from it the correct label.
8 Conclusion
In this work, we did three different experiments to classify IoT an non IoT
devices, and what kind of IoT device it is by analyzing network traffic data in
our network. Each experiment had different kinds of features, in order to
discover an unique pattern for a specific device, and thus to classify the
predict device with the help of ML model. We created a Website to display
our experiments results that contained a diagram of the precision, recall and
f1-score per IoT device. However, we used 3 devices, in the future we need to
perform this project with more and different devices, in order to measure our
results for different kind of devices and how they influence our ML.
13
References
[1] Zonghua Zhang Herve Debar Mustafizur R. Shahid, Gregory Blanc. Iot
devices recognition through network traffic analysis. CNRS SAMOVAR
UMR 5157, Institut Mines-Telecom, France, 2018.
[2] Yousef Amar Queen Mary University of London y.amar@qmul.ac.uk
Hamed Haddadi Imperial College London h.haddadi@imperial.ac.uk
Richard Mortier Cambridge University Computer Lab
richard.mortier@cl.cam.ac.uk Anthony Brown University of Nottingham
anthony.brown@nottingham.ac.uk James Colley University of Nottingham
james.colley@nottingham.ac.uk Andy Crabtree University of
Nottingham andy.crabtree@nottingham.ac.uk. An analysis of home iot
network traffic and behaviour. 2018.
[3] Asaf Shabtai Juan David Guarnizo Martin Ochoa2 Nils Ole Tippenhauer
Yair Meidan, Michael Bohadana and Yuval Elovici. Profiliot: A machine
learning approach for iot device identification based on network traffic
analysis. Department of Software and Information Systems Engineering,
Ben-Gurion University, Beer-Sheva, Israel, 2017.
[4] Steve Symanovich. The future of iot: 10 predictions about the internet of
things.
[5] Chris J.C. Burges. Simplified support vector decision rules. Bell
Laboratories, Lucent Technologies.
14
