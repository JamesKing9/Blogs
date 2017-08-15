# Glossary

malware ..... 恶意软件



---



# 									Reinforcement Learning

From:[this](https://d267cvn3rvuq91.cloudfront.net/s/603501/10-breakthrough-technologies-2017-reinforcement-learning/)

**By experimenting, computers are figuring out how to do things that no programmer could teach them.**

**Availability: 1 to 2 years**

*by Will Knight*

Inside a simple computer simulation, a group of self-driving cars are performing a crazy-looking maneuver on a four-lane virtual highway. Half are trying to move from the right-hand lanes just as the other half try to merge from the left. It seems like just the sort of tricky thing that might flummox a robot vehicle, but they manage it with precision.

I’m watching the driving simulation at the biggest artificial-intelligence conference of the year, held in Barcelona this past December. What’s most amazing is that the software governing the cars’ behavior wasn’t programmed in the conventional sense at all. It learned how to merge, slickly and safely, simply by practicing. During training, the control software performed the maneuver over and over, altering its instructions a little with each attempt. Most of the time the merging happened way too slowly and cars interfered with each other. But whenever the merge went smoothly, the system would learn to favor the behavior that led up to it. 

This approach, known as reinforcement learning, is largely how AlphaGo, a computer developed by a subsidiary of Alphabet called DeepMind, mastered the impossibly complex board game Go and beat one of the best human players in the world in a high-profile match last year. Now reinforcement learning may soon inject greater intelligence into much more than games. In addition to improving self-driving cars, the technology can get a robot to grasp objects it has never seen before, and it can figure out the optimal configuration for the equipment in a data center.

Reinforcement learning copies a very simple principle from nature. The psychologist Edward Thorndike documented it more than 100 years ago. Thorndike placed cats inside boxes from which they could escape only by pressing a lever. After a considerable amount of pacing around and meowing, the animals would eventually step on the lever by chance. After they learned to associate this behavior with the desired outcome, they eventually escaped with increasing speed.

​								

Some of the very earliest artificial-intelligence researchers believed that this process might be usefully reproduced in machines. In 1951, Marvin Minsky, a student at Harvard who would become one of the founding fathers of AI as a professor at MIT, built a machine that used a simple form of reinforcement learning to mimic a rat learning to navigate a maze. Minsky’s Stochastic Neural Analogy Reinforcement Computer, or SNARC, consisted of dozens of tubes, motors, and clutches that simulated the behavior of 40 neurons and synapses. As a simulated rat made its way out of a virtual maze, the strength of some synaptic connections would increase, thereby reinforcing the underlying behavior. 

There were few successes over the next few decades. In 1992, Gerald Tesauro, a researcher at IBM, demonstrated a program that used the technique to play backgammon. It became skilled enough to rival the best human players, a landmark achievement in AI. But reinforcement learning proved difficult to scale to more complex problems. “People thought it was a cool idea that didn’t really work,” says David Silver, a researcher at DeepMind in the U.K. and a leading proponent of reinforcement learning today.

That view changed dramatically in March 2016, 
however. That’s when AlphaGo, a program trained using reinforcement 
learning, destroyed one of the best Go players of all time, South 
Korea’s Lee Sedol. The feat was astonishing, because it is virtually 
impossible to build a good Go-playing program with conventional 
programming. Not only is the game extremely complex, but even 
accomplished Go players may struggle to say why certain moves are good 
or bad, so the principles of the game are difficult to write into code. 
Most AI researchers had expected that it would take a decade for a 
computer to play the game as well as an expert human.



> ##### Reinforcement Learning
>
> -   **Breakthrough**  An approach to artificial intelligence that gets computers to learn like people, without explicit instruction.		
>
> -   **Why It Matters**  Progress in self-­driving cars and other forms of automation will slow dramatically unless machines can hone skills through experience.		
>
> -   **Key Players**
>
>      \- DeepMind
>
>      \-  Mobileye
>      \- OpenAI
>      \- Google
>      \- Uber
>
> -   **Availability**  1 to 2 years		




**Jostling for position**

Silver, a mild-mannered Brit who became fascinated with artificial intelligence as an undergraduate at the University of Cambridge, explains why reinforcement learning has recently become so formidable. He says that the key is combining it with deep learning, a technique that involves using a very large simulated neural network to recognize patterns in data (see “[10 Breakthrough Technologies 2013: Deep Learning](https://www.technologyreview.com/s/513696/deep-learning/)”).

Reinforcement learning works because researchers figured out how to get a computer to calculate the value that should be assigned to, say, each right or wrong turn that a rat might make on its way out of its maze. Each value is stored in a large table, and the computer updates all these values as it learns. For large and complicated tasks, this becomes computationally impractical. In recent years, however, deep learning has proved an extremely efficient way to recognize patterns in data, whether the data refers to the turns in a maze, the positions on a Go board, or the pixels shown on screen during a computer game. 

---

# Scientists Hack a Computer Using DNA

From:[this](https://www.technologyreview.com/s/608596/scientists-hack-a-computer-using-dna/)

**Malware can be encoded into a gene and used to take over a computer program.**

*by Antonio Regalado August 10, 2017*

>   A researcher holds up a vial containing a malicious computer program stored as DNA.

<img src="http://ouqfn1c6k.bkt.clouddn.com/dna-malware.png" height="450px">

In what appears to be the first successful hack of a software program using DNA, researchers say malware they incorporated into a genetic molecule allowed them to take control of a computer used to analyze it.  

The biological malware was created by scientists at the University of Washington in Seattle, who call it the first “DNA-based exploit of a computer system.”  

To carry out the hack, researchers led by Tadayoshi Kohno (“see “[Innovators Under 35, 2007](http://www2.technologyreview.com/tr35/profile.aspx?TRID=611)”) and Luis Ceze encoded malicious software in a short stretch of DNA they purchased online. They then used it to gain “full control” over a computer that tried to process the genetic data after it was read by a DNA sequencing machine.  

The researchers warn that hackers could one day use faked blood or spit samples to gain access to university computers, steal information from police forensics labs, or infect genome files shared by scientists.  

For now, DNA malware doesn’t pose much of a security risk. The researchers admit that to pull off their intrusion, they created the “best possible” chances of success by disabling security features and even adding a vulnerability to a little-used bioinformatics program. Their paper appears [here](http://dnasec.cs.washington.edu/). 

“Their exploit is basically unrealistic,” says Yaniv Erlich, a geneticist and programmer who is chief scientific officer of MyHeritage.com, a genealogy website.  

 Previously, Kohno was among the first to show [how to hack into an automobile](https://www.technologyreview.com/s/418969/is-your-car-safe-from-hackers/) through its diagnostic port, later also [gaining access remotely](https://www.technologyreview.com/s/423292/taking-control-of-cars-from-afar/) by attacking cars though Bluetooth connections.  

The new DNA malware will be presented next week at the [Usenix Security Symposium](https://www.usenix.org/conference/usenixsecurity17) in Vancouver. “We look at emerging technologies and ask if there are upcoming security threats that might manifest, so the idea is to get ahead,” says Peter Ney, a graduate student in Kohno’s Security and Privacy Research Lab.  

To make the malware, the team translated a simple computer command into a short stretch of 176 DNA letters, denoted as A, G, C, and T. After ordering copies of the DNA from a vendor for $89, they fed the strands to a sequencing machine, which read off the gene letters, storing them as binary digits, *0*s and *1*s.  

Erlich says the attack took advantage of a spill-over effect, when data that exceeds a storage buffer can be interpreted as a computer command. In this case, the command contacted a server controlled by Kohno’s team, from which they took control of a computer in their lab they were using to analyze the DNA file.  

Companies that manufacture synthetic DNA strands and mail them to scientists are already on the alert for bioterrorists. In the future, the researchers suggest, they might also have to start checking DNA sequences for computer threats.  

The University of Washington team also cautions that hackers could use more conventional means to target people’s genetic data, precisely because it is increasingly appearing online (see “[10 Breakthrough Technologies 2015: Internet of DNA”)](https://www.technologyreview.com/s/535016/internet-of-dna/) and even being accessed through app stores (see “[10 Breakthrough Technologies 2016: DNA App Store](https://www.technologyreview.com/s/600769/10-breakthrough-technologies-2016-dna-app-store/)”).

In some cases, scientific programs used to organize and interpret DNA data aren’t actively maintained, and that could create risks, says James Bonfield, a bioinformatics expert at the Sanger Institute, in the United Kingdom. Bonfield says he authored the program that the University of Washington researchers targeted in their attack. He says the short program, “fqzcomp,” was written as an experiment for a file compression competition and probably wasn’t ever employed.

*   **Credit: **Image courtesy of Lee Organick, University of Washington.

*   **Antonio Regalado:**  Senior Editor, Biomedicine

     > I am the senior editor for biomedicine for *MIT Technology Review*. I look for stories about how technology is changing medicine and biomedical research. Before joining *MIT Technology Review* in July 2011, I lived in São Paulo, Brazil, where I wrote about science, technology, and politics in Latin America for *Science* and other publications. From 2000 to 2009, I was the science reporter at the *Wall Street Journal* and later a foreign correspondent.





