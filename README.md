# BeCAPTCHA-Mouse Benchmark 
BeCAPTCHA-Mouse Benchmark for development of bot detection technologyes based on mouse dynamics.

## INSTRUCTIONS FOR DOWNLOADING BeCAPTCHA-Mouse Benchmark
1) [Download license agreement](http://atvs.ii.uam.es/atvs/licenses/BeCAPTCHA_Mouse_Benchmark.pdf), send by email one signed and scanned copy to **atvs@uam.es** according to the instructions given in point 2.
 
 
2) Send an email to **atvs@uam.es**, as follows:

   *Subject:* **[DATABASE benchmark: BeCAPTCHA_Mouse_Benchmark]**

   Body: Your name, e-mail, telephone number, organization, postal mail, purpose for which you will use the database, time and date at which you sent the email with the signed license agreement.
 

3) Once the email copy of the license agreement has been received at ATVS, you will receive an email with a username, a password, and a time slot to download the database.
 

4) [Download the benchmark](http://atvs.ii.uam.es/atvs/intranet/BeCAPTCHA_Mouse_Benchmark), for which you will need to provide the authentication information given in step 4. After you finish the download, please notify by email to **atvs@uam.es** that you have successfully completed the transaction.
 

5) For more information, please contact: **atvs@uam.es**


## DESCRIPTION OF BeCAPTCHA-Mouse BENCHMARK
BeCAPTCHA-Mouse benchmark contains more than 10K synthetic mouse trayectories generated with two methods: 

**Method 1: Function-based Mouse Trajectory Synthesis**  
With this approach the mouse trajectories are generated according to three different trajectory shapes (linear, quadratic, and exponential) and three different velocity profiles (constant, logarithmic, and Gaussian). 
To generate a synthetic trajectory **{x̂, ŷ}** with *M* points, first we define the initial point [*x̂<sub>1</sub>, ŷ<sub>1</sub>*] and ending point [*x̂<sub>M</sub>, ŷ<sub>M</sub>*]. Second, we select one of three velocity profiles: *i)* constant velocity, where the distance between adjacent points is constant; *ii)* logarithmic velocity, where the distances are gradually increasing (acceleration); and *iii)* Gaussian velocity, in which the distances first increase and then decrease when they get close to the end of the trajectory (acceleration and deceleration). Third, we generate a sequence **x̂** between *x̂<sub>1</sub>* and *x̂<sub>M</sub>* spaced according to the selected velocity profile. The **ŷ** sequence is then generated according to the shape function. For example, for a shape defined by the quadratic function *ŷ = ax̂<sup>2</sup> + bx̂ + c*, we fit *b* and *c* for *a* fixed value of *a* by using the initial and ending points. We repeat the process fixing either *b* or *c*. The range of the parameters {*a, b, c*} explored is determined by analyzing real
mouse movements fitted to quadratic functions. Linear and exponential shapes are generated similarly.
Fig. 1 (trajectories D, E, and F) shows some examples of these mouse trajectories synthesized. That figure also shows the 3 diferent velocity profiles considered: the 3 trajectories in *E* have constant velocity, *F* shows acceleration (the distance between adjacent samples increases gradually), and *D* has initial acceleration and final deceleration. We can generate infinite mouse trajectories
with this approach by varying the parameters of each function.

![](https://github.com/BiDAlab/BeCAPTCHA-Mouse/blob/master/Fig5.png)
Figigure 1. Examples of mouse trajectories and their velocity profiles employed in this work: *A* is a real one extracted from a task of the database; *B* and *C* are synthetic trajectories generated with the GAN network; *D*, *E* and *F* are generated with the knowledge-based approach. Note that for each velocity profile (*D* = Gaussian, *E* = constant, *F* = logarithmic), we include the three knowledge-based trajectories (linear, quadratic, and exponential).

**Method 2: GAN-based Trajectories**  
For this approach we employ a GAN (Generative Adversarial Network),in which two neuronal networks, commonly named Generator and Discriminator, are trained one against the other (thus the \adversarial"). The architecture of the GAN is depicted in Fig. 2.

![](https://github.com/BiDAlab/BeCAPTCHA-Mouse/blob/master/Fig6.png)
Figure 2. The proposed architecture to train a GAN Generator of synthetic mouse trajectories.The Generator learns the human features of the mouse trajectories and generate human-like ones from Gaussian Noise.

The aim of the Generator is to fool the Discriminator by generating fake samples (mouse trajectories in this work) very similar to the real ones while the Discriminator has to predict whether the sample comes from the real set or is a fake created by the Generator. Once the
Generator is trained this way, then we can use it to synthesize mouse trajectories very similar to the human ones.
The topology employed in both Generator and Discriminator consist of two LSTM (Long Short-Term Memory) layers followed by a dense layer, very similar to a recurrent auto-encoder. The dense layer of the Discriminator is used as a classification layer to distinguish between fake and real mouse trajectories, while the Generator employs the dense layer to build synthetic mouse trajectories.
Fig. 1 shows two examples (trajectories B and C) of synthetic mouse trajectories generated with the GAN network and the comparison with a real one. We can observe high similarity between the two synthetic examples and the real one.
Human mouse patterns such us the initial acceleration and the final trajectory fine correction that we discussed before are automatically learned by the GAN network and reproduced in the synthetic trajectories generated.  
The human mouse trajectories employed to train the GAN network  were extracted from Chao *et al.* [1] database, which is comprised of more than 200K mouse trajectories acquired from 58 users who completed 300 repetitions of the task.In each repetition, the task was to click 8 buttons that appeared in the screen sequentially. This task was repeated twice in each session


#### BENCHMARK STRUCTURE
BeCAPTCHA-Mouse benchmark are composed by two main folders: *'DB_GAN'* which contains the synthetic GAN trayectories and *'DB_fcn'* that contains the function-based ones. Each folder has other two folders: *'raw'* folder which contains the raw data of the synthetic mouse trayectories in .txt files, and *'neuromotor'* folder that contains the sigma-Lognormal descomposition (more details in [3]) of the raw files in .ana format. Both kind of files have the same name to match them easily.

#### FILES FORMAT
+ .txt files: it just contains two columns with the **{x̂, ŷ}** mouse coordinates.
  + COLUMN 1: represents the **x̂** coordinate.

  + COLUMN 2: represents the **ŷ** coordinate.

+ .ana files: each row contains a log-normal signal extracted from the mouse trayectory, this log-normal signal is definded by 6 parameters.  

  + COLUMN 1: represents the *D* parameter.

  + COLUMN 2: represents the *t<sub>0</sub>* parameter.

  + COLUMN 3: represents the *μ* parameter.

  + COLUMN 4: represents the *σ* parameter.

  + COLUMNS 5 : represents the *θ<sub>s</sub>* parameter.
  
  + COLUMNS 6 : represents the *θ<sub>e</sub>* parameter.
  
  + COLUMNS 7, 8: are zeros.
  

#### FILES NOMENCLATURE
The nomenclature followed to name the files of the function based method is: NNNN_y=A_vp=B_task=C.txt

+ NNNN: indicates the number of the sample.

+ A: indicates the shape of the trajectory:

  + 0 = linear.
  
  + 1 = quadratic.
  
  + 2 = exponential.
  
+ B: indicates the velocity profile:

  + 0 = constant velocity.
  
  + 1 = logarithmic velocity.
  
  + 2 = Gaussian velocity.
  
  
+ C: indicates the task (1-8) of the human mouse database in which the trayectory was synthetized. This is necessary because the function-based method needs the initial [*x̂<sub>1</sub>, ŷ<sub>1</sub>*] and the [*x̂<sub>M</sub>, ŷ<sub>M</sub>*] end point of the human trayectory to synthetyse.
.
#### REFERENCES
For further information on the benchmark and on different applications where it has been used, we refer the reader to (all these articles are publicly available in the [publications](http://atvs.ii.uam.es/atvs/listpublications.do) section of the BiDA group webpage.)

+ [TIFS2020_MobileTouchDB] R. Tolosana, R. Vera-Rodriguez, J. Fierrez and J. Ortega-Garcia, “BioTouchPass2: Touchscreen Password Biometrics Using Time-Aligned Recurrent Neural Networks”, *IEEE Transactions on Information Forensics and Security*, vol. 15, pp: 2616-2628, 2020.

+ [CVPR2019_MobileTouchDB] R. Tolosana, J. Gismero-Trujillo, R. Vera-Rodriguez, J. Fierrez and J. Ortega-Garcia, "MobileTouchDB: Mobile Touch Character Database in the Wild and Biometric Benchmark", in *Proc. IEEE Conf. on Computer Vision and Pattern Recognition Workshops, CVPRw*, Long Beach, USA, 2019.

Please remember to reference articles [CVPR2019_MobileTouchDB] on any work made public, whatever the form, based directly or indirectly on any part of the MobileTouchDB database.
