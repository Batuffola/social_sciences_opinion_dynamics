# Flexible opinion dynamics framework
Opinion dynamics are still often modeled using single contagion frameworks such as
SIR models. However, it is well established that the relationship between exposure
to a number of people holding a particular opinion and subsequent changes in an
individual’s opinion is nonlinear. This relationship is frequently expressed using
sigmoidal functions or hyperbolic tangent (tanh) functions. Numerous studies have
demonstrated that a threshold number of individuals holding a certain opinion is
necessary to induce a change in opinion. To address the complexities of real-world
opinion dynamics, several approaches incorporating different assumptions have been
developed to model complex contagion. These include:
- **Threshold Models:** These models account for the necessity of a certain pro-
portion of neighbors adopting an opinion before an individual changes their own
opinion.
- **Social Influence Models:** These include mechanisms of social reinforcement
and initial beliefs, capturing the interplay between peer influence and individual
predispositions.
- **Dynamic Networks:** Networks that evolve over time, with edges forming and
dissolving to reflect changing relationships and interactions.
- **Attraction and Distraction Forces:** Models that simulate the forces between
differing opinions, influencing the likelihood of opinion change.
- **Echo Chambers and Hubs:** Network structures that highlight the role of tightly-
knit groups (echo chambers) and highly connected individuals (hubs) in the spread
of opinions.<br>

This review aims to compare these diverse modeling approaches and integrate empirical data to enhance the understanding and predictive power of opinion dynamics models. Additionally, I intend to test out the assumptions underlying these models and explore their paradoxes, providing a critical examination of their applicability and limitations in capturing the intricacies of complex contagion in opinion dynamics.
By merging theoretical models with empirical observations, we seek to develop a more comprehensive framework for understanding and predicting opinion spread.<br>

I developed a flexible agent-based model in Python, enabling the simulation of user interactions on social graphs under varied assumptions drawn from existing opinion dynamics frameworks. The model made it possible to compare key social mechanisms—such as social influence, attraction/repulsion to differing opinions, and thresholds for contagion—within a unified framework. I tested these models on different network types involving large-scale and adaptive network structures, and visualized opinion clustering to quantitatively assess polarization. 


## Task diary: 
### implementing the model with the update function: --- done <br>


$𝑥_𝑖(t+1) = 𝑥_𝑖 + \dfrac{𝛽_𝑖}{∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}}  ∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}   𝑥_{𝑖𝑗} ∙ tanh⁡(−𝛼_𝑖 (|𝑥_{𝑖𝑗} | − 𝜌_𝑖))$<br>

𝑥_𝑖 (𝑡),𝑥_𝑗 (𝑡) ∈ [0,1] --> Opinions of individuum 𝑥_𝑖 and its neighbors<br>
𝑥_{𝑖𝑗} (𝑡) = 𝑥_𝑗 (𝑡) - 𝑥_𝑖 (𝑡)  ∈ [-1,1] --> difference of opinion<br>
𝑤_𝑖𝑗 ∈ [0,1] --> social influence parameter (edge weights, allows unsymmetrical influence)<br>
𝛼_𝑖 ∈ [0,+…] --> controversy  of the topic (nonlinearity parameter,)<br>
𝜌_𝑖 ∈ [0,1]--> max opinion difference before repulsion<br>
𝛽_𝑖 --> coupling strength (stubborn agents)<br>



 find issues that fix opinions only growing in value-- fixed <br>
 colorbar is not stable between 0 and 1 --- fixed <br>

 NOTE: function is able to go out of bounds of [0,1], i cut it so that alsthough in theory 2 opinions can push each other to the extreme it can not go over 1 or below 0
 
 ### trying to find a paremeter for polarization/radicalization/consent --- done <br>
 find parameter for steady state.. done <br>
 memory of old opinion list compared to new? if true stop?<br>
 doesnt work... because of it being asymptotic <br>
 function for average changes over time.. once change is smaller than a theshold stop <br>

 
 
 
 

 polarization/radicalization/consent over mean and varianz of opinion list:<br>

 

 polarization:? mostly no steady state <br> 
 varianz opinion list > 𝜌_𝑖 ?<br>
 radicalization:?<br>
 mean opinion list not > 0.5 or <0.5<br>
 varianz opinion list << 𝜌_𝑖<br>
 consent:<br>
 mean opinion list around 0.5 <br>
 varianz opinion list << 𝜌_𝑖 ?<br>

 added a bar chart

 tried different metrics for polarisation.. most of them didnt work because of too strong parameter deoendencies.. 

 bimodalität works! <br>
 $Bipolarity = \dfrac{𝑐𝑜𝑢𝑛𝑡(|𝑥_i−0|<𝑒)+𝑐𝑜𝑢𝑛𝑡(|𝑥_i−1"|<𝑒)} {N}$ <br>
 with<br>
 $ e --> small treshold$<br>

 ### testing out model for different parameters-->  done
 𝑥_𝑖 (𝑡),𝑥_𝑗 (𝑡) ∈ [0,1] --> how heterogen?<br>
𝑤_𝑖𝑗 ∈ [0,1] --> first homogen later how heterogen/asymmetrical (social influence parameter if heterogen)<br>

𝛼_𝑖 ∈ [0,+…] --> homogene, heterogen (controversity)<br>
𝜌_𝑖 ∈ [0,1]--> homogene, heterogen(threshood before repulsion)<br>
𝛽_𝑖 --> homogene, heterogen (coupling strength)<br>

different network struktures:<br>
random net,all to all, grid<br>


 writing down table of what has been calculated with results:<br>

 ### adding update function without repulsion: --done
 ## adding different network struktures: -- done
 random 
 scalefree
 community /stoch. block model

 ### adding different update function: --done
  step at random 10 agents after each other or one

 ### remaking all graphs: --done

 ### adding dynamical networks: --done

 ### finding out what system size is normal: --done
 500 nodes often for model
 1,000–100,000 nodes for models more close to real world
 larger for comparism with data  (but often still just 20.000)

 finally network takes into consideration avg_degree for different scales
 
  redoing all graphics with that

 ### adding a modified update function for complex contagion: kind of added but not tested enough
  $𝑥_𝑖(t+1) = 𝑥_𝑖 + \dfrac{𝛽_𝑖}{∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}}  ∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}   𝑥_{𝑖𝑗} ∙ tanh⁡(−𝛼_𝑖 (|𝑥_{𝑖𝑗} | − 𝜌_𝑖))$<br>
 shifting the tanhyp before the sum
 $<𝑥_{𝑗n}>  = \dfrac{1}{∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}}  ∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}   𝑥_{𝑗} ∙ tanh⁡(−𝛼_𝑖 (|𝑥_{𝑖𝑗} | − 𝜌_𝑖))$<br>
  ### --> $𝑥_𝑖(t+1) = 𝑥_𝑖 +   tanh( 𝛽_𝑖 (\dfrac{1}{∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}}  ∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}   𝑥_{𝑗} -  𝑥_𝑖 ∙ tanh⁡(−𝛼_𝑖 (|𝑥_{𝑖𝑗} | − 𝜌_𝑖))$<br>

 oder?<br>
   $𝑥_𝑖(t+1) = 𝑥_𝑖 + 𝛽_𝑖 ∙tanh⁡(\dfrac{𝛽_𝑖}{∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}}  ∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}   𝑥_{𝑖𝑗} ∙ (−𝛼_𝑖 (|𝑥_{𝑖𝑗} | − 𝜌_𝑖)))$<br>

 ### Questions:-- answered and implemented
  + how many nodes in a network: 200 because results are super stable trueout different network sizes <br>
  + stochastic block model creates issues: not compatible with leaving the avg degree the same as in other networktypes: too sparse..<br>
                                           how to make it comparable? stochastic block models need a higher degree size to be feasable -->                                                   testing other network types with this same avg degree  <br>
                                           what should i do about weigts.. they are set to random.. but now inter and intra weights? <br>
  - complex contagion: this function:? <br>
    $𝑥_𝑖(t+1) = 𝑥_𝑖 +   tanh( 𝛽_𝑖 (\dfrac{1}{∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}}  ∑_{𝑗≠𝑖} 𝑤_{𝑖𝑗}   𝑥_{𝑗} -  𝑥_𝑖 ∙ tanh⁡(−𝛼_𝑖 (|𝑥_{𝑖𝑗} | − 𝜌_𝑖))$<br>

  - how many combinations should i allow:<br>
                                         does complex and rewiring even make sense? or complex repulsion?  yes,but not a priority <br>
                                         (according to me only makes sense again in pairwise interactions) <br>

  ### code needs clean up baaaaadly --- missing





 
 ## later combination of single and complex to have beyond pairwise possibilities: 
 ensamble opinion of clusters as complex contagion additional to single contagion pairwise
